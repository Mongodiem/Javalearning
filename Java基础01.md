[TOC]

# Java基础01

# 注释

单行注释、多行注释、文档注释

```java
/**
 * Welcome类（我是文档注释）
 * @author Carpediem
 * @version1.0
 */
public class Welcome {
    //我是单行注释
    public static void main(String[] args/*我是行内注释*/){
        System.out.println("Hello world");
    }
    /*
    我是多行注释
    我是多行注释
     */
}
//Output:Hello world
```

# 标识符

字母 下划线_  美元符号$**开头**

标识符：字母、下划线、美元符、数字的任意组合

Java标识符**大小写**敏感，无长度限制

## 标识符命名规范

- 表示**类名**的标识符：每个单词的首字母大写
- 表示**方法**和**变量**的标识符：第一个单词小写，第二个单词开始大写

```java
/**
 * 测试标识符的用法
 * @author Carpediem 
 */
public class TestIdentifier {
    public static void main(String[] args) {
        int a123=1;
        int $a=3;
        int _abc=4;

        int 年龄=18;
        System.out.println("Guess");
    }

}
//output:Guess
```

# 变量的本质

- 变量的本质就是代表一个**可操作的存储空间**
- 空间位置确定，放置的值不确定
- 通过**变量名**来访问对应的**存储空间**，从而操纵存储空间**存储的值**
- 变量的**数据类型**决定了变量占据**存储空间**的大小
- 变量是程序中最基本的**存储单元**，要素**变量名**+**变量类型**+**作用域**
- 变量使用前必须先**声明**，才能为其**分配**相应长度的存储空间

```java
type varName [=value][,varName[=value]...];
//[]中的内容为可选项，即可有可无
数据类型  变量名  [=初始值] [,变量名  [=初始值]…];
```

## 变量的分类

| 类型                 | 声明位置           | 从属于      | 备注                         |
| -------------------- | ------------------ | ----------- | ---------------------------- |
| 局部变量             | 方法或语句块内部   | 方法/语句块 | 必须先初始化（赋值）才能使用 |
| 成员变量（实例变量） | 类内部，方法外部   | 对象        | 会自动初始化                 |
| 静态变量（类变量）   | 类内部，static修饰 | 类          | 会自动初始化                 |

```java
/**
 * 测试变量
 * @author Carpediem
 */
public class TestVariable {
    int a;//成员变量，从属于对象；成员变量会自动被初始化
    static int size;//静态变量，从属于类

    public static void main(String[] args) {
        {
            int age;//局部变量，从属于语句块
            age=18;

        }
        int salary=3000;//局部变量，从属于方法
        int guo=12;
        System.out.println(guo);
        int i;
//        int j=i+5;//编译出错，变量i还未被初始化
    }

}
output:12
```

# 常量

**final**关键字来定义一个常量，常量一旦初始化后不能再更改其值

```java
final type varName=value;
```

# 数据类型

java数据类型分为：**基本数据类型**和**引用数据类型**

![img](https://www.sxt.cn/360shop/Public/admin/UEditor/20170607/1496834727293971.png)

引用数据类型的大小为**4个字节**，记录的是其**引用对象的地址*

------



## 基本数据类型

## 整型变量/常量

- 整型允许是负数
- 整型的范围与运行Java代码的机器无关-->java程序具有很强的移植能力

| **类型** | **占用存储空间** | **表数范围**                                   |
| -------- | ---------------- | ---------------------------------------------- |
| byte     | 1字节            | -2^7 ~  2^7-1（-128~127）                      |
| short    | 2字节            | -2^15 ~  2^15-1（-32768~32767）                |
| int      | 4字节            | -2^31 ~  2^31-1 (-2147483648~2147483647)约21亿 |
| long     | 8字节            | -2^63 ~  2^63-1                                |

**Java 语言整型常量的四种表示形式**

- 十进制整数，如：99, -500, 0
- 八进制整数，要求以 **0** 开头，如：015
- 十六进制数，要求**0x**或 **0X**开头，如：0x15
- 二进制数，要求**0b**或**0B**开头，如：0b01110011

Java语言的整型常数默认为int型，声明long型常量可以后加**‘ l ’或‘ L ’ **。

## 浮点型变量/常量

**浮点数使用总结**

- 默认是double类型
- 浮点数存在舍入误差，数字不能精确表示。如果需要进行不产生舍入误差的精确数字计算，需要使用**BigDecimal类。**
- 避免比较中使用浮点数，需要比较请使用BigDecimal类

| **类型**         | **占用存储空间** | **表数范围**         | 备注               |
| ---------------- | ---------------- | -------------------- | ------------------ |
| float（单精度）  | 4字节            | -3.403E38~3.403E38   |                    |
| double（双精度） | 8字节            | -1.798E308~1.798E308 | 浮点型常量默认类型 |

**Java浮点类型常量有两种表示形式**

- 十进制数形式，例如:3.14    314.0    0.314 
- 科学记数法形式，如314e2    314E2    314E-2 

```java
double f = 314e2;  //314*10^2-->31400.0
double f2 = 314e-2; //314*10^(-2)-->3.14
```

**float类型赋值时需要添加后缀F/f**

```java
float f = 3.14F;
double d1 = 3.14;
double d2 = 3.14D;
```

浮点类型float，double的数据不适合在不容许舍入误差的金融计算领域。如果需要进行不产生舍入误差的精确数字计算，需要使用**BigDecimal**类。

```java
【示例2-13】浮点数的比较一 

float f = 0.1f;
double d = 1.0/10;
System.out.println(f==d);//结果为false
【示例2-14】浮点数的比较二

float d1 = 423432423f;
float d2 = d1+1;
if(d1==d2){
   System.out.println("d1==d2");//输出结果为d1==d2
}else{
    System.out.println("d1!=d2");
}
【示例2-15】使用BigDecimal进行浮点数的比较

import java.math.BigDecimal;
public class Main {
    public static void main(String[] args) {
        BigDecimal bd = BigDecimal.valueOf(1.0);
        bd = bd.subtract(BigDecimal.valueOf(0.1));
        bd = bd.subtract(BigDecimal.valueOf(0.1));
        bd = bd.subtract(BigDecimal.valueOf(0.1));
        bd = bd.subtract(BigDecimal.valueOf(0.1));
        bd = bd.subtract(BigDecimal.valueOf(0.1));
        System.out.println(bd);//0.5
        System.out.println(1.0 - 0.1 - 0.1 - 0.1 - 0.1 - 0.1);//0.5000000000000001
    }
}
```

## 字符型变量/常量

- char类型在内存中占**2个字节**
- char类型可用来表示**Unicode**编码表中的字符
- 以后我们学的String类，其实是字符序列(char sequence)。

> Unicode具有从0到65535之间的编码，他们通常用从’\u0000’到’\uFFFF’之间的十六进制值来表示（前缀为u表示Unicode） 
>
>  Java 语言中还允许使用转义字符 ‘\’ 来将其后的字符转变为其它的含义。
>
> | **转义符** | **含义**          | **Unicode值** |
> | ---------- | ----------------- | ------------- |
> | \b         | 退格（backspace） | \u0008        |
> | \n         | 换行              | \u000a        |
> | \r         | 回车              | \u000d        |
> | \t         | 制表符（tab）     | \u0009        |
> | \“         | 双引号            | \u0022        |
> | \‘         | 单引号            | \u0027        |
> | \\         | 反斜杠            | \u005c        |
>
> ```java
> char c2 = '\n'; //代表换行符
> ```

```java
/**
 * 测试字符类型
 * @author Carpediem
 */
public class TestPrimitiveDataType {
    public static void main(String[] args) {
        char a='郭';
        char b='h';
        char c='\u0061';
        System.out.println(c);//a

        //转义字符
        System.out.println(""+'a'+'\n'+'b');
        System.out.println(""+'a'+'\t'+'b');
        System.out.println(""+'a'+'\''+'b');

        System.out.println(a+b+c);
        System.out.println('a');
        System.out.println(a);

    }
}
output:
a
a
b
a	b
a'b
37302
a
郭
```

## boolean类型变量/常量

- boolean类型有两个常量值，true和false
- 内存**1bit**
- **不可以**用0或非0整数替代true和false
- boolean类型用于判断逻辑条件，程序流程控制

```java
boolean flag;
flag=true;
if(flag){
    //true分支
}else{
    //false分支
}
```

# 运算符

| 算术运算符 | 二元运算符 | +，-，*，/，% |
| ---------- | ---------- | ------------- |
| 算术运算符 | 一元运算符 | ++，--        |

| 运算符       | 含义                             | 备注                                                         |
| ------------ | -------------------------------- | ------------------------------------------------------------ |
| 赋值运算符   | =                                | =是赋值运算符，而真正的判断两个操作数是否相等的运算符是==    |
| 扩展运算符   | +=，-=，*=，/=                   |                                                              |
| 关系运算符   | >，<，>=，<=，==，!=  instanceof | ==、!= 是所有（基本和引用）数据类型都可以使用 \> 、>=、 <、 <= 仅针对数值类型（byte/short/int/long, float/double。以及char） |
| 逻辑运算符   | &&，\|\|，!，^                   | 逻辑运算的操作数和运算结果都是boolean值。                    |
| 位运算符     | &，\|，^，~ ， >>，<<，>>>       | **1.**位运算指的是进行二进制位的运算;**2.**&和\|既是逻辑运算符，也是位运算符。如果两侧操作数都是boolean类型，就作为逻辑运算符。如果两侧的操作数是整数类型，就是位运算符。**3.**不要把“^”当做数学运算“乘方”，是“位的异或”操作。 |
| 条件运算符   | ? :                              | 其中 x 为 boolean 类型表达式，先计算 x 的值，若为true，则整个运算的结果为表达式 y 的值，否则整个运算结果为表达式 z 的值。 |
| 字符串连接符 | +                                | “+”运算符两侧的操作数中只要有一个是字符串(String)类型，系统会自动将另一个操作数**转换**为**字符串**然后再进行连接。 |



## 逻辑运算符

| 逻辑与   | &( 与)    | 两个操作数为true，结果才是true，否则是false |
| -------- | --------- | ------------------------------------------- |
| 逻辑或   | \|(或)    | 两个操作数有一个是true，结果就是true        |
| 短路与   | &&( 与)   | 只要有一个为false，则直接返回false          |
| 短路或   | \|\|(或)  | 只要有一个为true， 则直接返回true           |
| 逻辑非   | !（非）   | 取反：!false为true，!true为false            |
| 逻辑异或 | ^（异或） | 相同为false，不同为true                     |

> 短路与和短路或采用短路的方式。从左到右计算，如果只通过运算符左边的操作数就能够确定该逻辑表达式的值，则不会继续计算运算符右边的操作数，提高效率。

```java
//1>2的结果为false，那么整个表达式的结果即为false，将不再计算2>(3/0)
boolean c = 1>2 && 2>(3/0);
System.out.println(c);
//1>2的结果为false，那么整个表达式的结果即为false，还要计算2>(3/0)，0不能做除数，//会输出异常信息
boolean d = 1>2 & 2>(3/0);
System.out.println(d);
```

## 运算符优先级

- 逻辑非>逻辑与>逻辑或，如：a||b&&c的运算结果是：a||(b&&c)，而不是(a||b)&&c 

## 自动类型转换

- 自动类型转换指的是**容量小**的数据类型可以自动转换为**容量大**的数据类型。

- 可以将整型常量直接赋值给byte、 short、 char等类型变量，而不需要进行强制类型转换，只要不超出其表数范围即可。

- ```java
  short  b = 12;  //合法
  short  b = 1234567;//非法，1234567超出了short的表数范围
  ```

  

![img](https://www.sxt.cn/360shop/Public/admin/UEditor/20170516/1494906265693111.png)

> 黑色的实线表示无数据丢失的自动类型转换，而虚线表示在转换时可能会有精度的损失。

## 强制类型转换

```java
(type)var
```

- 运算符“()”中的type表示将值var想要转换成的目标数据类型。

- 当将一种类型强制转换成另一种类型，而又超出了目标类型的表数范围，就会被截断成为一个完全不同的值。

- ```java
  int x = 300;
  byte bx = (byte)x;    //值为44
  ```



# 控制语句

## switch语句

- switch语句会根据表达式的值从**相匹配的case标签处**开始执行，一直执行到**break语句处**或者是**switch语句的末尾**。如果表达式的值与任一case值不匹配，则进入**default**语句(如果存在default语句的情况)。

```java
public class TestSwitch {
    public static void main(String[] args) {
        for(int i=0;i<=10;i++){
        char c = 'a';
        int rand = (int) (26 * Math.random());
        char c2 = (char) (c + rand);
        System.out.print(i+":");
        System.out.print(c2 + ": ");
        switch (c2) {
            case 'a':
            case 'e':
            case 'i':
            case 'o':
                System.out.println("caicai");
            case 'u':
                System.out.println("元音");
//                break;
            case 'y':
            case 'w':
                System.out.println("半元音");
                break;
            default:
                System.out.println("辅音");
        }
    }}

}
output:
0:u: 元音
半元音
1:w: 半元音
2:o: caicai
元音
半元音
3:l: 辅音
4:s: 辅音
5:s: 辅音
6:g: 辅音
7:y: 半元音
8:r: 辅音
9:w: 半元音
10:w: 半元音

Process finished with exit code 0
```



## break和continue语句

- 在任何循环语句的主体部分，均可用break控制循环的流程。break用于强行退出循环，不执行循环中剩余的语句。

```java
public class TestBreak {
    public static void main(String[] args) {
        int total = 0;//定义计数器
        System.out.println("Begin");
        while (true) {
            total++;//每循环一次计数器加1
            int i = (int) Math.round(100 * Math.random());
            //当i等于88时，退出循环
            System.out.print(i+"  ");
            if (i == 88) {
                System.out.println("Exit");
                break;
            }
        }
        //输出循环的次数
        System.out.println("Game over， used " + total + " times.");
    }
}
output:Begin
50  51  18  5  34  86  60  51  17  99  74  50  21  57  47  99  59  58  51  38  84  54  16  76  27  6  85  98  73  63  69  39  23  53  41  82  22  55  74  12  73  58  59  70  40  51  13  29  58  82  55  94  95  31  45  70  83  51  24  80  12  71  66  84  34  18  31  2  21  15  64  98  64  47  3  62  26  5  81  66  87  61  59  70  80  41  45  10  96  27  27  71  92  34  28  45  12  64  47  42  94  78  40  2  37  98  59  75  42  55  71  80  81  17  16  97  47  41  38  3  64  75  79  1  34  96  0  53  32  55  78  90  93  30  52  9  25  13  62  67  70  95  95  16  91  23  44  3  98  49  64  53  39  30  32  77  81  73  51  93  64  63  14  76  74  56  51  57  96  68  4  94  21  66  27  4  54  68  0  58  49  85  62  27  5  48  94  82  24  59  60  32  58  45  32  29  23  3  90  22  46  61  31  23  75  71  5  13  81  52  88  Exit
Game over， used 211 times.

```



-  continue 语句用在循环语句体中，用于终止某次循环过程，即跳过循环体中尚未执行的语句，接着进行下一次是否执行循环的判定。

```java
【示例3-18】带标签break和continue：控制嵌套循环跳转(打印101-150之间所有的质数)

public class Test18 {
    public static void main(String args[]) {
        outer: for (int i = 101; i < 150; i++) {
            for (int j = 2; j < i / 2; j++) {
                if (i % j == 0){
                    continue outer;
                }
            }
            System.out.print(i + "  ");
        }
    }
}
```

