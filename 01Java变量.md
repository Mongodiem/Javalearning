# Java变量

## 1、变量的本质

变量--> **可操作的存储空间**,空间位置确定，所存放的值不确定

变量名-->用于**访问**对应的存储空间，从而操纵这个存储空间存储的值

> Java是一种强类型语言，每个变量都必须声明其数据类型。变量的数据类型决定了变量占据存储空间的大小。

## 2、变量的分类

局部变量    成员变量（实例变量） 静态变量（类变量）

| 类型     | 声明位置           | 从属于      | 代码示例                                                     |
| -------- | ------------------ | ----------- | ------------------------------------------------------------ |
| 局部变量 | 方法或语句块内部   | 方法/语句块 | `public void test(){int i;i=10;int j=i+5;}`                  |
| 成员变量 | 类内部，方法外部   | 对象        | 生命周期伴随对象始终。如果不自行初始化，它会自动初始化成该类型的默认初始值。`public class Test { int i; }` |
| 静态变量 | 类内部，static修饰 | 类          | 类被加载，静态变量就有效；类被卸载，静态变量消失。           |

```java
public class TestVariable
{int a;//成员变量，从属于对象，成员变量会自动被初始化
static int size=3;//静态变量，从属于类
public static void main(String[] args){
int salary=3000;//局部变量，从属于方法
		TestVariable t=new TestVariable();
		System.out.print(t.a+" ");
		System.out.print(t.size+" ");
		System.out.print(size+" ");
		System.out.print(salary);
// 	output:0 3 3 3000
}
}
```
```java
int i;
 //  int j = i + 5; // 编译出错，变量i还未被初始化
```

## 3、常量

Java中，利用关键字**final**来定义一个常量。常量一旦被初始化不能更改。

```java
public class TestConst {
	public static void main(String [] args) {
		final double PI=3.14159;
//		PI=3.14;//编译错误，不能再被赋值
		double r=4;
		double area=PI*r*r;
		System.out.println("area="+area);
//		area=50.26544
	}
}
```

## 4、数据类型

Java的数据类型分为两大类：**基本数据类型**和**引用数据类型**。

1. 引用数据类型的大小统一为**4个字节**，记录的是其引用对象的地址
2. 基本数据类型有3类8种
   - 数值型    byte short int long float double
   - 字符型     char
   - 布尔型      boolean

![image-20220626145444653](C:\Users\Carpediem\AppData\Roaming\Typora\typora-user-images\image-20220626145444653.png)

### (1)整型变量/常量

| 类型  | 占用存储空间 | 注意事项                                                     |
| ----- | ------------ | ------------------------------------------------------------ |
| byte  | 1字节        |                                                              |
| short | 2字节        |                                                              |
| int   | 4字节        |                                                              |
| long  | 8字节        | 声明long型常量可以后加‘l 或L 。` long a = 55555555; //编译成功，在int表示的范围内(21亿内)。 long b = 55555555555;//不加L编译错误，已经超过int表示的范围。long b = 55555555555L;’` |

> Java语言整形常量的四种表示形式

- 十进制整数，如：99, -500, 0
- 八进制整数，要求以 0 开头，如：015
- 十六进制数，要求 0x 或 0X 开头，如：0x15
- 二进制数，要求0b或0B开头，如：0b01110011

### (2)浮点型变量/常量

<https://www.sxt.cn/Java_jQuery_in_action/Java_Floating_point_variables.html>

**Java浮点类型常量有两种表示形式**

- 十进制数形式，例如:3.14    314.0    0.314 
- 科学记数法形式，如314e2    314E2    314E-2 

**使用BigDecimal进行浮点数的比较**

### （3）字符型变量/常量

- 字符型在内存中占2个字节

- Java 语言中还允许使用转义字符 ‘\’ 来将其后的字符转变为其它的含义。`char c2 = '\n'; //代表换行符`

- 以后我们学的String类，其实是字符序列(char sequence)。

- ```java
  char eChar = 'a'; 
  char cChar ='中';
  ```

### (4)boolean类型变量/常量

- boolean类型有两个常量值，true和false

- boolean在内存中占一位（不是一个字节）

- 不可以使用 0 或非 0 的整数替代 true 和 false 

- boolean 类型用来判断逻辑条件，一般用于程序流程控制 

- ```java
  boolean flag;
  flag=true;
  if(flag){
      //true分支
  }else{
      //false分支
  }
  ```

## 5、运算符

<https://www.sxt.cn/Java_jQuery_in_action/Java_operator.html>

```java
//1>2的结果为false，那么整个表达式的结果即为false，将不再计算2>(3/0)
boolean c = 1>2 && 2>(3/0);
System.out.println(c);
//1>2的结果为false，那么整个表达式的结果即为false，还要计算2>(3/0)，0不能做除数，//会输出异常信息
boolean d = 1>2 & 2>(3/0);
System.out.println(d);
```

- &和|既是逻辑运算符，也是位运算符。如果两侧操作数都是boolean类型，就作为逻辑运算符。如果两侧的操作数是整数类型，就是位运算符。

- 不要把“^”当做数学运算“乘方”，是“位的异或”操作

- "+"运算符两侧的操作数中只要有一个是字符串(String)类型，系统会自动将另一个操作数转换为字符串然后再进行连接。

- ```java
  int a=12;
  System.out.println("a="+a);//输出结果: a=12
  ```

- 三目运算符

  ## 6、自动类型转换和强制类型转换

黑色的实线表示无数据丢失的自动类型转换，而虚线表示在转换时可能会有精度的损失。

![image-20220626155632314](C:\Users\Carpediem\AppData\Roaming\Typora\typora-user-images\image-20220626155632314.png)

- 自动类型转换指的是容量小的数据类型可以自动转换为容量大的数据类型。
- 可以将整型常量直接赋值给byte、 short、 char等类型变量，而不需要进行强制类型转换，只要不超出其表数范围即可。

```java
short  b = 12;  //合法
short  b = 1234567;//非法，1234567超出了short的表数范围
```

- 强制类型转换，又被称为造型，用于显式的转换一个数值的类型。在有可能丢失信息的情况下进行的转换是通过造型来完成的，但可能造成精度降低或溢出。

  ```java
  		double x  = 3.14; 
  		int nx = (int)x;   //值为3
  		char c = 'a';
  		int d = c+1;
  		System.out.println(nx);//3
  		System.out.println(d);//98
  		System.out.println((char)d);//b
  
  ```

- 不能在布尔类型和任何数值类型之间做强制类型转换
- 当将一种类型强制转换成另一种类型，而又超出了目标类型的表数范围，就会被截断成为一个完全不同的值。

```java
int x = 300;
byte bx = (byte)x;    //值为4
```

