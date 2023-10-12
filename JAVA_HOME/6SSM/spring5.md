# Spring 5

## 一、Spring 5 框架概述

### 1、Spring 是轻量级的开源的 JavaEE 框架

### 2、Spring 可以解决企业应用开发的复杂性

### 3、Spring 有两个核心部分：==IOC== 和 ==Aop==

- IOC：控制反转，把创建对象过程交给 Spring 进行管理
- Aop：面向切面，不修改源代码进行功能增强

### 4、Spring 特点

- 方便解耦，简化开发
- Aop 编程支持
- 方便程序测试
- 方便和其他框架进行整合
- 方便进行事务操作
- 降低 API 开发难度

### 5、入门案例

#### 5.1 下载 spring

​		[spring官网](https://spring.io)

​		[下载地址](https://repo.spring.io/release/org/springframework/spring/)

#### 5.2 打开 IDEA 工具，创建普通的 Java Project

#### 5.3 导入 spring5 相关 jar 包

​		Beans、Core、Context、Expression 是 spring 的核心，必须包含

![image-20230112185034668](spring5.images\image-20230112185034668.png)

​		添加如下 jar 包

![image-20230112185156963](spring5.images\image-20230112185156963.png)

#### 5.4 创建普通类，在这个类创建普通方法

```java
public class User {
    public void add(){
        System.out.println("add...");
    }
}
```

#### 5.5 创建Spring配置文件，在配置文件配置创建的对象

Spring 文件使用 xml 格式

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
<!--    配置User对象创建-->
    <bean id="user" class="com.atguigu.spring5.User"></bean>
</beans>
```

#### 5.6 进行测试代码编写

```java
public class TestSpring5 {
    @Test
    public void testAdd(){
        ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
        User user = context.getBean("user", User.class);

        System.out.println(user);
        user.add();
    }
}
//输出
//com.atguigu.spring5.User@27f723
//add...
```

## 二、IOC

### 1、什么是 IOC?

1. 控制反转，把对象创建和对象之间的调用过程，交给 Spring 进行管理
2. 使用 IOC 目的：为了耦合度降低
3. 入门案例就是 IOC 的简单实现

### 2、 IOC底层原理

- xml 解析、工厂模式、反射

IOC 过程：

1. xml 配置文件，配置创建的对象

   ```xml
   <bean id="dao" class="com.atguigu.UserDao"></bean>
   ```

2. 有 service 类和 dao 类，创建工厂类

   ```java
   class UserFactory{
       public static UserDao getDao(){
           String classValue = class属性值;//1 xml 解析
           Class clazz = Class.forName(classValue);// 2 通过反射创建对象
           return (UserDao)clazz.newInstance();
       }
   }
   ```

这种方式进一步降低了耦合度，当类的路径改变时，只需要修改 xml 配置文件中的类路径，代码中不需要修改。

#### 1）IOC 接口

1. IOC 思想基于 IOC 容器完成，IOC 容器底层就是对象工厂

2. Spring 提供 IOC 容器实现的两种方式（两个接口）：

   - BeanFactory：IOC 容器基本实现，是 Spring 内部的使用接口，不提供开发人员进行使用；加载配置稳健的时候不会创建对象，在获取对象（使用）才去创建对象
   - ApplicationContext：BeanFactory 接口的子接口，提供更多更强大的功能，一般由开发人员进行使用；加载配置文件时就会创建对象

3. ApplicationContext 接口的实现类

   ![image-20230113122953887](E:\Typora_files\Java_node\5Spring\spring5.images\image-20230113122953887.png)

   FileSystemXmlApplicationContext 需要文件路径时绝对路径

   ClassPathXmlApplicationContext 文件路径是相对路径（src 文件夹）

### 3、IOC 操作 Bean 管理

#### 1）什么是 Bean 管理？

Bean 管理指的是两个操作，①是指 Spring 创建对象，②是指 Spring 注入属性

#### 2）Bean 管理操作有两种方式

- 基于 XML 配置文件方式实现
- 基于注解方式实现

#### 3）基于 xml 方式

##### ①基于 xml 方式创建对象

```xml
<bean id="user" class="com.atguigu.spring5.User"></bean>
```

- 在 spring 配置文件中，使用 bean 标签，标签里面添加对应属性，就可以实现对象创建
- 在 bean 标签中有很多属性，常用的有
  - id 属性：唯一标识
  - class属性：类全路径
- 创建对象时，默认是执行==无参构造==方法完成对象创建

##### ②基于 xml 方式注入属性

**DI：**依赖注入，就是注入属性

###### 第一种注入方式：使用 set 方法进行注入

- 创建类，定义属性和对应的 set 方法

  ```java
  public class Book{
      private String bName;
      private String bAuthor;
      
      public void setBName(String bName){
          this.bName = bName;
      }
      public void setBAuthor(String bAuthor){
          this.bAuthor = bAuthor;
      }
  }
  ```

- 在 spring 配置文件配置对象创建和属性注入

  ```xml
  <bean id="book" class="com.atguigu.spring5.Book">
  	<prperty name="bName" value="易筋经"></property>
  	<property name="bAuthor" value="达摩老祖"></property>
      <!-- name 为属性名，value 为属性值-->
  </bean>
  ```

###### 第二种注入方式：使用有参构造进行注入

- 创建类，定义属性和有参构造

  ```java
  public class Orders{
      private String oname;
      private String address;
      
      public Orders(String oname, String address){
          this.oname = oname;
          this.address = address;
      }
  }
  ```

- 在 spring 配置文件中进行配置

  ```xml
  <bean id="orders" class="com.atguigu.spring5.Orders">
  	<constructor-arg name="oname" value="电脑"></constructor-arg>
  	<constructor-arg name="address" value="China"></constructor-arg>
  </bean>
  ```

###### 第三种注入方式 p 名称空间注入（本质上还是 set 方法注入，简化了写法）

- 添加 p 名称空间在配置文件中

  ![image-20230113151027043](E:\Typora_files\Java_node\5Spring\spring5.images\image-20230113151027043.png)

- 进行属性注入，在 bean 标签里面进行操作

  ```xml
  <bean id="book" class="com.atguigu.spring5.Book" p:bname="九阳神功" p:bauthor="无名氏"></bean>
  ```

##### ③xml 注入其他类型属性

###### 字面量

- null 值

  ```xml
  <property name="address">
      <null/>
  </property>
  ```

- 属性值包含特殊符号

  ```xml
  <!--
  	1.把< > 进行转义 &lt; &gt;
  	2.把带特殊符号内容写到 CDATA
  		<<钢铁是怎样炼成的>> 写入属性中才能不报错
  -->
  <property name="address">
  	<value><![CDATA[<<钢铁是怎样炼成的>>]]</value>
  </property>
  ```

###### 注入属性-外部 bean（bean 标签在 property 外部）

- 创建两个类 service 和 dao 类

- 在 service 调用 dao 里面的方法

  ```java
  public class UserService{
      private UserDao userDao;
      public void setUserDao(UserDao userDao){
          this.userDao = userDao;
      }
      public void add(){
          System.out.println("service add....");
          userDao.update();
      }
  }
  ```

- 在 spring 配置文件中进行配置

  ```xml
  <bean id="userService" class="com.atguigu.spring5.service.UserService">
  	<property name="userDao" ref="userDao"></property>
  </bean>
  <bean id="userDao" class="com.atguigu.spring5.dao.UserDaoImpl"></bean>
  ```

###### 注入属性-内部 bean（bean 标签在 property 内部）

```java
public class Dept{
    private String dname;
    public void setDname(String dname){
        this.dname = dname;
    }
}
public class Emp{
    private String ename;
    private String gender;
    private Dept dept;
    public void setDept(Dept dept){
        this.dept = dept;
    }
    public void setEname(String ename){
        this.ename = ename;
    }
    public void setGender(String gender){
        this.gender = gender;
    }
}
```

在 spring 配置文件中进行配置

```xml
<bean id="emp" class="com.atguigu.spring5.bean.Emp">
	<property name="ename" value="lucy"></property>
	<property name="gender" value="女"></property>
	<property name="dept">
        <bean id="dept" class="com.atguigu.spring5.bean.Dept">
        	<property name="dname" value="安保部"></property>
        </bean>
    </property>
</bean>
```

###### 注入属性-级联赋值

- 第一种写法（外部bean的方式）

  ```xml
  <bean id="emp" class="com.atguigu.spring5.bean.Emp">
  	<property name="ename" value="lucy"></property>
  	<property name="gender" value="女"></property>
  	<property name="dept" ref="dept"></property>
  </bean>
  <bean id="dept" class="com.atguigu.spring5.bean.Dept">
  	<property name="dname" value="财务部"></property>
  </bean>
  ```

- 第二种写法（==需要该属性的 get 方法==，因为要获取到该属性才行）

  ```xml
  <bean id="emp" class="com.atguigu.spring5.bean.Emp">
       <!--设置两个普通属性-->
       <property name="ename" value="lucy"></property>
       <property name="gender" value="女"></property>
       <!--级联赋值-->
       <property name="dept" ref="dept"></property>
       <property name="dept.dname" value="技术部"></property>
  </bean>
  
  <bean id="dept" class="com.atguigu.spring5.bean.Dept">
       <property name="dname" value="财务部"></property>
  </bean>
  ```

###### ==注入集合类型==

- 创建类，定义数组、list、map、set 类型属性，生成对应 set 方法

  ```java
  public class Stu {
       //1 数组类型属性
       private String[] courses;
       //2 list 集合类型属性
       private List<String> list;
       //3 map 集合类型属性
       private Map<String,String> maps;
       //4 set 集合类型属性
       private Set<String> sets;
       public void setSets(Set<String> sets) {
           this.sets = sets;
       }
       public void setCourses(String[] courses) {
           this.courses = courses;
       }
       public void setList(List<String> list) {
           this.list = list;
       }
       public void setMaps(Map<String, String> maps) {
           this.maps = maps;
       }
  }
  ```

- 在 spring 配置文件进行配置

  ```xml
  <!--1 集合类型属性注入-->
  <bean id="stu" class="com.atguigu.spring5.collectiontype.Stu">
       <!--数组类型属性注入-->
  	<property name="courses">
           <array>
               <value>java 课程</value>
               <value>数据库课程</value>
           </array>
  	</property>
       <!--list 类型属性注入-->
  	<property name="list">
           <list>
               <value>张三</value>
               <value>小三</value>
           </list>
  	</property>
  	<!--map 类型属性注入-->
  	<property name="maps">
  		<map>
  			<entry key="JAVA" value="java"></entry>
  			<entry key="PHP" value="php"></entry>
  		</map>
  	</property>
       <!--set 类型属性注入-->
  	<property name="sets">
  		<set>
  			<value>MySQL</value>
  			<value>Redis</value>
  		</set>
  	</property>
  </bean>
  ```

###### 在集合里面注入对象类型属性

```xml
<!--创建多个 course 对象-->
<bean id="course1" class="com.atguigu.spring5.collectiontype.Course">
 	<property name="cname" value="Spring5 框架"></property>
</bean>
<bean id="course2" class="com.atguigu.spring5.collectiontype.Course">
 	<property name="cname" value="MyBatis 框架"></property>
</bean>
<!--注入 list 集合类型，值是对象-->
<property name="courseList">
 	<list>
 		<ref bean="course1"></ref>
 		<ref bean="course2"></ref>
 	</list>
</property>
```

###### **把集合注入部分提取出来**

- 在 spring 配置文件中引入名称空间 util

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
   	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   	xmlns:p="http://www.springframework.org/schema/p"
   	xmlns:util="http://www.springframework.org/schema/util"
   	xsi:schemaLocation="http://www.springframework.org/schema/beans 
  		http://www.springframework.org/schema/beans/spring-beans.xsd
  		http://www.springframework.org/schema/util 
  		http://www.springframework.org/schema/util/spring-util.xsd">
  ```

- 使用 util 标签完成 list 集合注入提取

  ```xml
  <!--1 提取 list 集合类型属性注入-->
  <util:list id="bookList">
   	<value>易筋经</value>
   	<value>九阴真经</value>
   	<value>九阳神功</value>
  </util:list>
  <!--2 提取 list 集合类型属性注入使用-->
  <bean id="book" class="com.atguigu.spring5.collectiontype.Book">
   	<property name="list" ref="bookList"></property>
  </bean>
  ```


##### ④Factory Bean

Spring 有两种类型 bean，一种==普通 bean==，另外一种==工厂 bean（FactoryBean）==

1. 普通 bean：在配置文件中定义 bean 类型就是返回类型

2. 工厂 bean：在配置文件定义 bean 类型可以和返回类型一样

   - 第一步 创建类，实现接口 FactoryBean 作为工厂 bean

   - 第二步 实现接口里面的方法，在实现的方法中定义返回 bean 类型

     ```java
     public class MyBean implements FactoryBean<Course> {
     	//定义返回 bean
     	@Override
     	public Course getObject() throws Exception {
     		Course course = new Course();
      		course.setCname("abc");
             return course;
      	}
      	@Override
      	public Class<?> getObjectType() {
      		return null;
      	}
     	@Override
      	public boolean isSingleton() {
      		return false;
      	}
     }
     ```

     ```xml
     <bean id="myBean" class="com.atguigu.spring5.factorybean.MyBean">
     </bean>
     ```

     ```java
     @Test
     public void test3() {
      	ApplicationContext context = new ClassPathXmlApplicationContext("bean3.xml");
         //配置文件中是 MyBean 类型，但是返回的是 Course 类型
      	Course course = context.getBean("myBean", Course.class);
      	System.out.println(course);
     }
     ```

##### ⑤bean 作用域，设置 bean 是单例还是多实例

1. spring 中，默认情况下是单例的
2. spring 配置文件 bean 标签中有属性 scope 用于设置单例还是多例
   - singleton，默认值，表示是单实例对象，在 spring 加载配置文件时就会创建对象
   - prototype，表示是多实例对象，在调用 getBean() 方法的时候才会创建对象
   - request，每次 http 请求将会有各自的 bean 实例，类似于 prototype。也就是说每个 request 作用域内的请求只创建一个实例
   - session，在一个 http session 中，一个 bean 定义对应一个 bean 实例。也就是说每个 session 作用域内的请求只创建一个实例
   - global session，在一个全局的 http session 中，一个 bean 定义对应一个 bean 实例

![image-20230114140944237](E:\Typora_files\Java_node\5Spring\spring5.images\image-20230114140944237.png)

#### 4）基于注解方式

##### ①什么是注解？

- 注解是代码特殊标记，格式：@注解名称(属性名称=属性值, 属性名称=属性值..)

- 使用注解，注解作用在类上面，方法上面，属性上面

- 使用注解目的：简化 xml 配置

##### ②spring 针对 bean 管理中创建对象提供注解

- @Component
- @Service
- @Controller
- @Repository

上述四个注解的功能是一样的，都可以用来创建 bean 实例

##### ③基于注解方式实现对象创建

1. 引入依赖

   ![image-20230114182515446](E:\Typora_files\Java_node\5Spring\spring5.images\image-20230114182515446.png)

2. 开启组件扫描

   ```xml
   <!--开启组件扫描
    	1 如果扫描多个包，多个包使用逗号隔开
    	2 扫描包上层目录
   -->
   <context:component-scan base-package="com.atguigu"></context:component-scan>
   ```

3. 创建类，在类上面添加创建对象注解

   ```java
   //在注解里面 value 属性值可以省略不写，
   //默认值是类名称，首字母小写
   //UserService -- userService
   @Component(value = "userService") //<bean id="userService" class=".."/>
   public class UserService {
    	public void add() {
    		System.out.println("service add.......");
    	}
   }
   ```

##### ④开启组件扫描细节配置

```xml
<!--示例 1
 use-default-filters="false" 表示现在不使用默认 filter，自己配置 filter
 context:include-filter ，设置扫描哪些内容
-->
<context:component-scan base-package="com.atguigu" use-default-filters="false">
 	<context:include-filter type="annotation" 							
        	expression="org.springframework.stereotype.Controller"/>
</context:component-scan>
<!--示例 2
 下面配置扫描包所有内容
 context:exclude-filter： 设置哪些内容不进行扫描
-->
<context:component-scan base-package="com.atguigu">
 <context:exclude-filter type="annotation" 
 		expression="org.springframework.stereotype.Controller"/>
</context:component-scan>
```

##### ⑤基于注解方式实现属性注入

- @Autowired：根据属性类型进行自动装配

  ```java
  @Service
  public class UserService {
   	//定义 dao 类型属性
   	//不需要添加 set 方法
   	//添加注入属性注解
   	@Autowired 
   	private UserDao userDao;
   	public void add() {
   		System.out.println("service add.......");
   		userDao.add();
   	}
  }
  ```

- @Qualifier：根据名称进行注入

  这个@Qualifier 注解的使用，和上面@Autowired 一起使用

  ```java
  //定义 dao 类型属性
  //不需要添加 set 方法
  //添加注入属性注解
  @Autowired //根据类型进行注入
  @Qualifier(value = "userDaoImpl") //根据名称进行注入
  private UserDao userDao;
  ```

- @Resource：可以根据类型注入，可以根据名称注入

  @Resource 是 javax 包中的注解，不是 spring 官方提供的注解

  ```java
  //@Resource //根据类型进行注入
  @Resource(name = "userDaoImpl") //根据名称进行注入
  private UserDao userDao;
  ```

- @Value：注入普通类型属性

  ```java
  @Value(value = "abc")
  private String name;
  ```

### 4、bean 生命周期

生命周期是对象从创建到销毁的过程

1. 通过构造器创建 bean 实例（无参数构造）
2. 为 bean 的属性设置值和对其他 bean 引用（调用 set 方法）
3. 把 bean 实例传递 bean 后置处理器的方法 postProcessBeforeInitialization
4. 调用 bean 的初始化方法（需要进行初始化方法的配置）
5. 把 bean 实例传递 bean 后置处理器的方法 postProcessAfterInitialization
6. bean 可以使用了（获取到了对象）
7. 当容器关闭时，调用 bean 的销毁的方法（需要进行配置销毁的方法）

```java
public class Orders {
 //无参数构造
 	public Orders() {
 		System.out.println("第一步 执行无参数构造创建 bean 实例");
 	}
 	private String oname;
 	public void setOname(String oname) {
 		this.oname = oname;
 		System.out.println("第二步 调用 set 方法设置属性值");
 	}
 	//创建执行的初始化的方法
 	public void initMethod() {
 		System.out.println("第三步 执行初始化的方法");
 	}
 	//创建执行的销毁的方法
 	public void destroyMethod() {
 		System.out.println("第五步 执行销毁的方法");
 	}
}
```

```xml
<bean id="orders" class="com.atguigu.spring5.bean.Orders" init-method="initMethod" destroy-method="destroyMethod">
 	<property name="oname" value="手机"></property>
</bean>
```

```java
@Test
public void testBean3() {
	// ApplicationContext context =
	// new ClassPathXmlApplicationContext("bean4.xml");
 	ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("bean4.xml");
 	Orders orders = context.getBean("orders", Orders.class);
 	System.out.println("第四步 获取创建 bean 实例对象");
 	System.out.println(orders);
 	//手动让 bean 实例销毁
 	context.close();
 }
```

#### 1）添加 bean 后置处理器

创建类，实现接口 BeanPostProcessor，创建后置处理器

```java
public class MyBeanPost implements BeanPostProcessor {
 	@Override
 	public Object postProcessBeforeInitialization(Object bean, String beanName) 
throws BeansException {
 		System.out.println("在初始化之前执行的方法");
 		return bean;
 }
 	@Override
 	public Object postProcessAfterInitialization(Object bean, String beanName) 
throws BeansException {
 		System.out.println("在初始化之后执行的方法");
 		return bean;
 	}
}
```

```xml
<!--配置后置处理器-->
<bean id="myBeanPost" class="com.atguigu.spring5.bean.MyBeanPost"></bean>
```

### 5、自动装配（xml 方式）

根据指定装配规则（属性名称或者属性类型），Spring 自动将匹配的属性值进行注入

- 根据属性名称自动注入

  ```xml
  <!--实现自动装配
   	bean 标签属性 autowire，配置自动装配
   	autowire 属性常用两个值：
   	byName 根据属性名称注入 ，注入值 bean 的 id 值和类属性名称一样
   	byType 根据属性类型注入
  -->
  <bean id="emp" class="com.atguigu.spring5.autowire.Emp" autowire="byName">
   	<!--<property name="dept" ref="dept"></property>-->
  </bean>
  <bean id="dept" class="com.atguigu.spring5.autowire.Dept"></bean>
  ```

- 根据属性类型自动注入

  ```xml
  <!--实现自动装配
   	bean 标签属性 autowire，配置自动装配
   	autowire 属性常用两个值：
   	byName 根据属性名称注入 ，注入值 bean 的 id 值和类属性名称一样
   	byType 根据属性类型注入
  -->
  <bean id="emp" class="com.atguigu.spring5.autowire.Emp" autowire="byType">
   	<!--<property name="dept" ref="dept"></property>-->
  </bean>
  <bean id="dept" class="com.atguigu.spring5.autowire.Dept"></
  ```

### 6、xml 引入外部属性文件

**引入 context 名称空间**

```xml
<beans xmlns="http://www.springframework.org/schema/beans" 
 		xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
 		xmlns:p="http://www.springframework.org/schema/p" 
 		xmlns:util="http://www.springframework.org/schema/util" 
 		xmlns:context="http://www.springframework.org/schema/context" 
 		xsi:schemaLocation="http://www.springframework.org/schema/beans 
			http://www.springframework.org/schema/beans/spring-beans.xsd 
 			http://www.springframework.org/schema/util 
			http://www.springframework.org/schema/util/spring-util.xsd 
 			http://www.springframework.org/schema/context 
			http://www.springframework.org/schema/context/spring-context.xsd">
<!--引入外部属性文件-->
<context:property-placeholder location="classpath:jdbc.properties"/>
<!--配置连接池-->
<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
 	<property name="driverClassName" value="${prop.driverClass}"></property>
 	<property name="url" value="${prop.url}"></property>
 	<property name="username" value="${prop.userName}"></property>
 	<property name="password" value="${prop.password}"></property>
</bean>
```

### 7、完全注解开发

①使用 @Configuration 创建配置类，代替配置文件

```java
@Configuration //作为配置类，替代 xml 配置文件
@ComponentScan(basePackages = {"com.atguigu"})
public class SpringConfig {
}
```

②读取配置时要使用 AnnotationConfigApplicationContext() 方法

```java
@Test
public void testService2() {
 	//加载配置类
 	ApplicationContext context = new AnnotationConfigApplicationContext(SpringConfig.class);
 	UserService userService = context.getBean("userService", UserService.class);
 	System.out.println(userService);
 	userService.add();
}
```

## 三、AOP

### 1、什么是 AOP?

AOP 是面向切面编程，利用 AOP 可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的**耦合度**降低，提高程序的可重用性，同时提高了开发的效率；

通俗的讲：AOP 能够不修改源代码，在主干功能里面添加新功能

简单举例：

<img src="E:\Typora_files\Java_node\5Spring\spring5.images\image-20230115180127912.png" alt="image-20230115180127912" style="zoom:67%;" />

### 2、AOP 底层原理

AOP 底层使用 动态代理

#### 1）有接口情况，使用 JDK 动态代理

创建接口实现类代理对象，增强类的方法

![image-20230115181321192](E:\Typora_files\Java_node\5Spring\spring5.images\image-20230115181321192.png)

#### 2）没有接口情况，使用 CGLIB 动态代理

创建子类的代理对象，增强类的方法

![image-20230115181429264](E:\Typora_files\Java_node\5Spring\spring5.images\image-20230115181429264.png)

