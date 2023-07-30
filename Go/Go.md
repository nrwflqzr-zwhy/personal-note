[TOC]

# 一、Go的两个命令

```shell
go build main.go  # 生成 .exe文件，只编译
go run main.go	# 编译并运行程序，但是中间的 .exe文件不会保留
```

# 二、变量

## 1) 变量是程序的基本组成单位

```go
package main
import "fmt"
func main(){
    // 1. 变量的定义
    var i int
    // 2. 变量的赋值
    i = 10
    // 3. 变量的使用
    fmt.Println("i = ", i)
}
```

## 2) 变量的三种使用方式

1. 指定变量类型，声明后若不赋值，使用**默认值**

	```go
	var i int
	var n1, n2, n3 int
	```

2. 根据值自行判定变量类型（类型推导）

	```go
	var num = 10.1
	```

3. 省略 var，注意:=左侧的变量不应该是已经声明过的，否则会导致编译错误

	```go
	name := "tom"
	name = "tom" //错误方式
	```

## 3) 多变量赋值

```go
var n1, n2, n3 int
var a1, a2, a3 = 100, "tom", 888
b1, b2, b3 := 100, "bob", 888
```

## 4) 全局变量

```go
var n1 = 100
var n2 = 200
var name = "jack"
//
var (
	n1 = 100
    n2 = 200
    name = "jack"
)
```

## 5) 数据类型

