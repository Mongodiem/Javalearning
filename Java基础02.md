[TOC]

# Java基础02

# 对象和类

## 对象

- 对象是一种**数据结构**，将数据和数据的行为放到了一起
- 在内存上，对象是一个**内存块**，存放了相关的**数据集合**
- 对象的本质是一种数据的组织方式

### 创建一个对象的步骤：

　　1. 分配对象空间，并将对象成员变量初始化为0或空

　　2. 执行属性值的显示初始化

　　3. 执行构造方法

　　4. 返回对象的地址给相关的变量

## 类

- **类**可以看做一个模板或者图纸，系统根据**类的定义**来创造**对象**

- 类：**class**，对象：**Object**或**Instance** *类的对象和类的实例*是一个意思

  > 每一个源文件必须有且只有一个public class，并且类名和文件名保持一致,一个Java文件可以同时定义多个class

- 类一般有三分常见的成员：**属性field**(成员变量）,**方法method**,**构造器constructor**

  

### field属性（成员变量）

- field 用于定义类或**该类对象**包含的的数据（静态特征），属性作用范围是**整个类体**
- 定义成员变量时可以对其初始化，若不，Java使用默认的值对其初始化

```java
[修饰符] 属性类型 属性名 =[默认值]
```

### 方法method

- 方法类似于面向过程中的函数，面向过程中，**函数是最基本单位**，整个程序由一个个函数调用组成，面向对象中，整个程序的基本单位是**类**，**方法是从属于类和对象的的**。

### 构造方法constructor

- 构造器是一个创建对象时被自动调用的特殊方法，目的是**对象的初始化**

- 构造器的名称与类的名称**一致**

- Java通过new关键字来调用构造器，从而返回该类的实例，是一种特殊的方法。

  ```java
  class Point{
      double x,y;
      public Point(double _x,double _y){
          x=_x;
          y=_y;
      }
      public double getDistance(Point p){
          return Math.sqrt((x-p.x)*(x-p.x)+(y-p.y)*(y-p.y));
      }
  }
  public class TestConstructor {
      public static void main(String[] args) {
          Point p=new Point(3.0,4.0);
          Point orgin=new Point(0.0,0.0);
          System.out.println(p.getDistance(orgin));
      }
  }
  output:
  5.0
  ```

  

# JVM的内存分析

- JVM的内存可分为三个区域：**栈stack**、**堆heap**、**方法区method area**

## 栈Stack

- 每个**方法**被调用都会创建一个**栈帧**（存储==局部变量==、==操作数==、==方法出口==）
- JVM为每个**线程**创建一个栈，用于存放该线程执行方法的信息（==实际参数==、==局部变量==等）
- 栈为线程私有，**不能**实现线程间的**共享**
- 栈是系统自动分配，==速度快==
- 栈是一个**连续**的内存空间，存储特性是==先进后出，后进先出==

## 堆heap

- JVM只有==一个堆==，被所有线程**共享**
- 堆用于存储**创建好**的**对象**和**数组**（*数组也是对象*）
- 堆是一个==不连续==的内存空间，分配灵活，**速度慢**

## 方法区（静态区）

- JVM只有==一个方法区==，被所有线程**共享**
- 方法区实际也是**堆**，只是用于存储==类、常量==相关的信息
- 用于存放程序中永远不变或唯一不变的内容。（==类信息【Class对象】、静态变量、字符串常量==）

# this关键字

**this**:创建好的对象的**地址**

- 构造方法调用前，对象已经创建，因此，在构造方法中也可以使用this代表**“当前对象”**

this用法：

1. 在程序中产生二义性之处，应使用this来指明**当前对象**;普通方法中，this总是指向**调用该方法的对象**。构造方法中，this总是指向正**要初始化的对象**。
2.  使用this关键字调用重载的构造方法，避免相同的初始化代码。但只能在构造方法中用，并且必须位于构造方法的第一句。
3. this**不能**用于static方法中

```java
/**
 * this代表“当前对象”实例
 * @author Carpediem 
 */
public class User {
    int id;
    String name;
    String pwd;
    public User(){

    }
    public User(int id,String name){
        System.out.println("It is initializing the object that has been create:"+this);
        this.id=id;
        this.name=name;
    }
    public void login(){
        System.out.println(this.name+" is going to login");

    }

    public static void main(String[] args) {
        User u1=new User(111,"Lipton");
        System.out.println("Print the object of Lipton: "+u1);
        u1.login();
    }
}
output:
It is initializing the object that has been create:User@1b6d3586
Print the object of Lipton: User@1b6d3586
Lipton is going to login
```

```java
/**
 * this()调用重载构造方法
 * @author Carpediem 
 */
public class TestThis {
    int a,b,c;
    TestThis(){
        System.out.println("Be about to initialize a' Hello'object");
    }
    TestThis(int a,int b){
//        Testthis()//无法调用构造方法
        this();//调用无参的构造方法，并且必须位于第一行
        a=a;
        this.a=a;
        this.b=b;
    }
    TestThis(int a, int b, int c) {
        this(a, b); // 调用带参的构造方法，并且必须位于第一行！
        this.c = c;
    }

    void sing() {
    }
    void eat() {
        this.sing(); // 调用本类中的sing();
        System.out.println("Your mom is calling you for eating！");
    }

    public static void main(String[] args) {
        TestThis hi = new TestThis(2, 3);
        hi.eat();
    }
}
output:
Be about to initialize a' Hello'object
Your mom is calling you for eating！
```

# static关键字

- 用static声明的成员变量为**静态成员变量**，也称为**类变量**

- 类变量从属于类，为该类的所有实例**共享**，在类被载入时被显示初始化

-  一般用“**类名.类属性/方法**”来调用。(也可以通过对象引用或类名(不需要实例化)访问静态成员。)

- **static修饰的成员变量和方法，从属于类。**

  **普通变量和方法从属于对象的。**

# 静态初始化块

- 构造方法用于**对象**的初始化；静态初始化块，用于**类**的初始化操作!

静态初始化块==执行顺序==：

1. 上溯到Object类，先执行Object的静态初始化块，再向下执行子类的静态初始化块，直到我们的类的静态初始化块为止。

2. 构造方法执行顺序和上面顺序一样!!

```java
/**
 * this代表“当前对象”实例
 * @author Carpediem
 */
public class User {
    int id;
    String name;
    static String college;
    String pwd;
    static {
        System.out.println("Performing initialization of the class");
        college="UESTC";
        printCollege();
    }
    public static void printCollege(){
        System.out.println(college);
    }
        public static void main(String[] args) {
        User u2=new User();
        User.college="UPenn";
        User.printCollege();
    }
}
output:
Performing initialization of the class
UESTC
UPenn
```

# 参数传值机制

> Java中，方法中所有参数都是“值传递”，也就是“传递的是值的副本”。 也就是说，我们得到的是“原参数的复印件，而不是原件”。因此，==复印件改变不会影响原件==。

1. **基本数据类型参数的传值**

　　传递的是值的副本。 副本改变不会影响原件。

2. **引用类型参数的传值**

　　传递的是值的副本。但是引用类型指的是“对象的地址”。因此，副本和原参数都**指向了同一个“地址”**，改变“副本指向地址对象的值，也意味着原参数指向对象的值也发生了改变”。

```java
/**
 * 多个变量指向同一个对象
 * @author Carpediem
 */
public class User {
    int id;
    String name;
    String pwd;

    public User(int id,String name){
        System.out.println("It is initializing the object that has been create:"+this);
        this.id=id;
        this.name=name;
    }
    public   void   testParameterTransfer01(User  u){
        u.name="Transfer01";
    }

    public   void   testParameterTransfer02(User  u){
        u  =  new  User(200,"Transfer02");
    }



    public static void main(String[] args) {

        User u1=new User(100,"Lipton");

        u1.testParameterTransfer01(u1);
        System.out.println(u1.name);

        u1.testParameterTransfer02(u1);
        System.out.println(u1.name);

    }
}
output:
It is initializing the object that has been create:User@1b6d3586
Transfer01
It is initializing the object that has been create:User@4554617c
Transfer01

```

# package

　　1. 通常是类的第一句**非注释性**语句。

　　2. 包名：**域名倒着写**即可，再**加上模块名**，便于内部管理类。

## JDK中的主要的包

| Java中的常用包 | **说明**                                                     |
| -------------- | ------------------------------------------------------------ |
| java.lang      | 包含一些Java语言的核心类，如String、Math、Integer、System和Thread，提供常用功能。 |
| java.awt       | 包含了构成抽象窗口工具集（abstract window toolkits）的多个类，这些类被用来构建和管理应用程序的图形用户界面(GUI)。 |
| java.net       | 包含执行与网络相关的操作的类。                               |
| java.io        | 包含能提供多种输入/输出功能的类。                            |
| java.util      | 包含一些实用工具类，如定义系统特性、使用与日期日历相关的函数。 |

## 导入类import

> 如果我们要使用其他包的类，需要使用import导入，从而可以在本类中直接通过类名来调用，否则就需要书写类的完整包名和类名。import后，便于编写代码，提高可维护性。

**注意要点：**

　　1. Java会默认导入java.lang包下所有的类，因此这些类我们可以直接使用。

　　2. 如果导入两个同名的类，只能用包名+类名来显示调用相关类：　

```java
java.util.Date date = new java.util.Date();
```

**【示例4-15】导入同名类的处理**　　

```java
/**
 *导入同名类的处理
 * @author Carpediem
 */
import java.sql.Date;
import java.util.*;//导入该包下所有的类。会降低编译速度，但不会降低运行速度。
public class TestImport {
    public static void main(String[] args) {
        //这里指的是java.sql.Date
        Date now;
        //java.util.Date因为和java.sql.Date类同名，需要完整路径
        java.util.Date  now2 = new java.util.Date();
        System.out.println(now2);
        //java.util包的非同名类不需要完整路径
        Scanner input = new Scanner(System.in);
    }

}

```

## 静态导入

> 静态导入(static import)是在JDK1.5新增加的功能，其作用是用于导入指定类的静态属性，这样我们可以直接使用静态属性。

```java
/**
 *静态导入的使用
 * @author Carpediem
 */
//以下两种静态导入的方式二选一即可
import static java.lang.Math.*;//导入Math类的所有静态属性
import static java.lang.Math.PI;//导入Math类的PI属性
public class TestImport {
    public static void main(String[] args) {
        System.out.println(PI);
        System.out.println(random());
    }

}
output:
3.141592653589793
0.10127090932119431
```

