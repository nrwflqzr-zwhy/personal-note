# make的基础用法

## 前言

首先，Make 只是一个过渡性的工具，而 CMake 才是最终的构建工具。因此，在使用 CMake 之前，有必要对 Make 有一定的了解。这样，在使用 CMake 时，才能更加得心应手。

## 1. 准备文件

新建，项目文件夹hello，及文件main.cpp，factorial.cpp，printhello.cpp，functions.h。

hello目录的结构如下：

```
hello/
	├──main.cpp
	├──factorial.cpp
	├──printhello.cpp
	└──functions.h
```

main.cpp

```c++
#define _FUNCTIONS_H_
#include <iostream>
#include "functions.h"
using namespace std;

int main()
{
	printhello();

	cout << "This is main:" << endl;
	cout << "The factorial of 5 is:" << factorial(5) << endl;
	return 0;
}
```

printhello.cpp

```c++
#include <iostream>
#include "functions.h"
using namespace std;

void printhello()
{
	int i;
	cout << "Hello World!" << endl;
}
```

factorial.cpp

```c++
#include "functions.h"

int factorial(int n)
{
	if (n==1)
		return 1;
	else
		return n * factorial(n-1);
}
```

function.h

```c++
#ifdef _FUNCTIONS_H_
#define _FUNCTIONS_H_
void printhello();
int factorial(int n);
#endif


```

## 2. 编译

使用g++命令直接编译、运行

```shell
g++ main.cpp factorial.cpp printhello.cpp -o main
./main
```

这种方法适用于小型项目。对于大型项目来说，此法编译效率低，这时候make工具就派上用场了。

## 3. make工具

### 3.1makefile三要素

![img](https://maxwell-lx.vip/content/images/2023/04/image-1-1.png)

- 目标：规则的目标，可以是 Object File（一般称它为中间文件），也可以是可执行文件，还可以是一个标签；
- 依赖：是我们的依赖文件，要生成 targets 需要的文件或者是另一个目标。可以是多个，也可以是没有；
- 命令：make 需要执行的命令（任意的 shell 命令）。可以有多条命令，每一条命令占一行。

语法：

\[目标]:[依赖]

\[TAB] [命令]

3.2make工作原理

### 3.2 make工作原理

![img](https://maxwell-lx.vip/content/images/2023/04/pSeQGpF-4.png)

## 4. 实战

### 4.1version-1

```makefile
hello: main.cpp printhello.cpp factorial.cpp
	g++ -o hello main.cpp printhello.cpp factorial.cpp
```

### 4.2version-2

```makefile
CXX = g++
TARGET = hello 
OBJ = main.o printhello.o factorial.o

$(TARGET): $(OBJ)
	$(CXX) -o $(TARGET) $(OBJ)

main.o: main.cpp
	$(CXX) -c main.cpp

printhello.o: printhello.cpp
	$(CXX) -c printhello.cpp

factorial.o: factorial.cpp
	$(CXX) -c factorial.cpp
```

### 4.3version-3

```makefile
CXX = g++
TARGET = hello 
OBJ = main.o printhello.o factorial.o

CXXFLAGS = -c -Wall

$(TARGET): $(OBJ)
	$(CXX) -o $@ $^

%.o: %.cpp
	$(CXX) $(CXXFLAGS) $< -o $@

.PHONY: clean
clean:
	rm -f *.o $(TARGET)
```



### 4.4version-4

```makefile
CXX = g++
TARGET = hello 
SRC = $(wildcard *.cpp)
OBJ = $(patsubst %.cpp, %.o, $(SRC))

CXXFLAGS = -c -Wall

$(TARGET): $(OBJ)
	$(CXX) -o $@ $^

%.o: %.cpp
	$(CXX) $(CXXFLAGS) $< -o $@

.PHONY: clean
clean:
	rm -f *.o $(TARGET)
```

## 5. 常见的自动化变量解析符

|   变量   |                             解析                             |
| :------: | :----------------------------------------------------------: |
|    $0    |                       当前脚本的文件名                       |
| $n(n>=1) | 传递给脚本或函数的参数。n 是一个数字，表示第几个参数。例如，第一个参数是 1，第二个参数是2 |
|    $#    |                 传递给脚本或函数的参数个数。                 |
|    $*    |                 传递给脚本或函数的所有参数。                 |
|    $@    |                        表示目标文件。                        |
|    $?    |             上个命令的退出状态，或函数的返回值。             |
|    $$    | 当前 Shell 进程 ID。对于 Shell 脚本，就是这些脚本所在的进程 ID。 |
|    $^    |                      表示所有的依赖文件                      |
|    $<    |                      表示第一个依赖文件                      |

.PHONY，makefile的特殊变量，用于生成“伪目标”。make中的“目标”通常指文件，但有时功能和文件名会重叠。以clean为例，我们需要clean来清除全部的中间文件，但同时我们不需要真的生成一个名为"clean"文件，所以当目标文件夹存在一个“clean”文件时，“clean”功能就不会被执行，所以需要一个"伪目标"去执行“clean”功能。

wildcard，用于防止通配符解析失败。使变量定义时，括号里的通配符仍然生效。

patsubst，用于防止替换文件解析失效。替换文件后缀。
