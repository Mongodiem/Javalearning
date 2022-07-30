[TOC]

# JAVA基础03

# 继承extends

- 如果定义一个类时，没有调用**extends**,则他的**父类**是：**java.lang.Object**
- Java中类**没有**多继承，**接口**有**多继承**
- 子类继承父类，可以得到除了**父类的构造方法**外父类的**全部属性**和**方法**
- 子类**不可以直接**访问父类的**私有的属性和方法**
- 父类也称作超类、基类、派生类等

```java
/**
 * 使用extends实现继承
 * @author Carpediem
 * @version 1.0
 */
public class Test {
    public static void main(String[] args) {
        Student s=new Student("Carpediem",168,"CS");
        s.rest();
        s.study();
    }
}
class Person{
    String name;
    int height;
    public void rest(){
        System.out.println("Rest for a while");
    }
}
class Student extends Person{
    String major;
    public void study(){
        System.out.println("In UESTC,Studying CS");
    }
    public Student(String name,int height,String major){
//        继承父类的属性
        this.name=name;
        this.height=height;
        this.major=major;
    }
}
output:
Rest for a while
In UESTC,Studying CS
```

## instanceof运算符

- 二元运算符，左边是**对象**，右边是**类**
- **对象**是**类**或**子类**创建的**对象**时，返回**true**,否则**false**

```java
/**
 * 使用instanceof运算符进行类型判断
 * @author Carpediem
 * @version 1.1
 */
public class Test {
    public static void main(String[] args) {
        Student s=new Student("Carpediem",168,"CS");
        System.out.println(s instanceof Person);
        System.out.println(s instanceof Student);

    }
}
output:
true
true
```

## 方法重写override

- 子类通过重写父类的方法，可以用自身的行为**替换**父类的行为
- 方法名、形参列表相同
- **返回值**类型和**声明异常**类型，子类小于等于父类
- 访问**权限**，子类大于等于父类
- 方法重写是实现**多态**的必要条件

```java
/**
 * 测试方法重写
 * @author Carpediem
 * @version 1.0
 */
public class TestOverride {
    public static void main(String[] args) {
        Vehicle v1=new Vehicle();
        Vehicle v2=new Bentley();
        Vehicle v3=new Plane();
        v1.run();
        v2.run();
        v3.run();
        v2.stop();
        v3.stop();
    }
}
class Vehicle{
    public void run(){
        System.out.println("Running....");
    }
    public void stop(){
        System.out.println("Stop!");
    }
}
class Bentley extends Vehicle{
    public void run(){
//        重写父类方法
        System.out.println("Running quickly");
    }
}
class Plane extends Vehicle{
    public void run(){
        System.out.println("Flying in the sky!");
    }
    public void stop(){
        System.out.println("Land and Stop flying");
    }
}
output:
Running....
Running quickly
Flying in the sky!
Stop!
Land and Stop flying
```

# Object类

- Object类是所有Java类的**根基类**，即所有的Java对象都拥有Object类的**属性**和**方法**

```java
public class Person {
    ...
}
//equal to ：
public class Person extends Object {
    ...
}
```

## toString方法

- Object类中定义有public String toString()方法，其返回值是 String 类型。

源码为:

```java
   public String toString() {
        return getClass().getName() + "@" + Integer.toHexString(hashCode());
    }
```



```java
/**
 * 测试toString()方法重写
 * @author Carpediem
 * @version 2.0
 */
class Person{
    String name;
    int age;
    @Override
    public String toString(){
        return  name+",age:"+age;
    }
}
public class TestOverride{
    public static void main(String[] args) {
        Person p=new Person();
        p.age=22;
        p.name="Lipton";
        System.out.println("info:"+p);

        TestOverride t=new TestOverride();
        System.out.println(t);

    }
}
output:
info:Lipton,age:22
TestOverride@1b6d3586
```

## equals方法和==

-  Object 的 equals 方法默认就是比较两个对象的hashcode(**对象的内存地址**)，是同一个对象的**引用**时返回 true 否则返回 false
- ==代表比较双方是否相同。如果是**基本类型**则表示**值**相等，如果是**引用类型**则表示**地址**相等即是同一个对象。
-  JDK提供的一些类，如String、Date、包装类等，重写了Object的equals方法，调用这些类的equals方法， x.equals (y) ，当x和y所引用的对象是同一类对象且属性内容相等时（并不一定是相同对象），返回 true 否则返回 false。

```java
/**
 * equals方法测试和自定义类重写equals方法
 * @author Carpediem
 * @version 1.0
 */
public class TestEquals {
    public static void main(String[] args) {
        Person p1 = new Person(123,"Carpediem");
        Person p2 = new Person(123,"Prajna");
        System.out.println(p1==p2);     //false，不是同一个对象
        System.out.println(p1.equals(p2));  //true，id相同则认为两个对象内容相同
        String s1 = new String("Lipton");
        String s2 = new String("Lipton");
        System.out.println(s1==s2);         //false, 两个字符串不是同一个对象
        System.out.println(s1.equals(s2));  //true,  两个字符串内容相同
        String s3 = new String("Lipton1");
        System.out.println(s1==s3);//false
        System.out.println(s1.equals(s3));//false
        String s4=new String();
        s4=s3;
        System.out.println(s4==s3);//true
        System.out.println(s3.equals(s4));//true
    }
}
class Person {
    int id;
    String name;
    public Person(int id,String name) {
        this.id=id;
        this.name=name;
    }
    public boolean equals(Object obj) {
        if(obj == null){
            return false;
        }else {
            if(obj instanceof Person) {
                Person c = (Person)obj;
                if(c.id==this.id) {
                    return true;
                }
            }
        }
        return false;
    }
}
output:
false
true
false
true
false
false
true
true
```

# super关键字

- super是直接**父亲对象的引用**
- 可以通过super来访问父类中被子类**覆盖的方法或属性**
- 使用super 调用**普通方法**，语句没有位置限制，可以在**子类**中随便调用
- 若是构造方法的第一行代码没有**显式的调用**super(...)或this(...)，Java将默认调用super()

## 继承树追溯

**构造方法调用顺序：**

   构造方法第一句总是：super(…)来调用父类对应的构造方法。所以，流程就是：先向上追溯到Object，然后再依次向下执行类的初始化块和构造方法，直到当前子类为止。

   注：静态初始化块调用顺序，与构造方法调用顺序一样，不再重复。

```java
public class TestSuper {
    public static void main(String[] args) {
        System.out.println("开始创建一个ChildClass对象......");
        new ChildClass();
    }
}
class FatherClass {
    public FatherClass() {
        System.out.println("创建FatherClass");
    }
}
class ChildClass extends FatherClass {
    public ChildClass() {
        System.out.println("创建ChildClass");
    }
}
output:
开始创建一个ChildClass对象......
创建FatherClass
创建ChildClass
```

# 封装

**访问控制符**：private、default、protected、public,说明了面向对象的**封装性**

-  private 表示私有，只有自己类能访问
- default表示没有修饰符修饰，只有同一个包的类能访问
-  protected表示可以被同一个包的类以及其他包中的子类访问
- public表示可以被该项目的所有包中的所有类访问

![图1.png](https://www.sxt.cn/360shop/Public/admin/UEditor/20170522/1495417749528447.png)

```java
class Person {
    private String name;
    private int age;
    public Person() {

    }
    public Person(String name, int age) {
        this.name = name;
        // this.age = age;//构造方法中不能直接赋值，应该调用setAge方法
        setAge(age);
    }

    public void setName(String name) {
        this.name = name;
    }
    public String getName() {
        return name;
    }
    public void setAge(int age) {
        //在赋值之前先判断年龄是否合法
        if (age > 130 || age < 0) {
            this.age = 18;//不合法赋默认值18
        } else {
            this.age = age;//合法才能赋值给属性age
        }
    }
    public int getAge() {
        return age;
    }
    @Override
    public String toString() {
        return "Person [name=" + name + ", age=" + age + "]";
    }
}

public class Test {
    public static void main(String[] args) {
        Person p1 = new Person();
        //p1.name = "hh"; //编译错误
        //p1.age = -45;  //编译错误
        p1.setName("Carpediem");
        p1.setAge(-45);
        System.out.println(p1);

        Person p2 = new Person("Lipton", 300);
        System.out.println(p2);
    }
}
output:
Person [name=Carpediem, age=18]
Person [name=Lipton, age=18]
```

# final关键字

- 修饰**变量**：被修饰的变量一旦赋值，**不能**被重新赋值
- 修饰**方法**：该方法**不可**被**子类重写**，但**可**被**重载**
- 修饰**类**：修饰的类**不**能被**继承**

# 抽象方法和抽象类

## 抽象方法

- 使用abstract修饰的**方法**，**没**有**方法体**，**只有**声明
- 定义的是一种**规范**，就是规定**子类**必须要给**抽象方法**提供**具体的实现**
- 抽象方法**必须**被**子类实现**。

## 抽象类

- 包含抽象方法的类就是抽象类，即有抽象方法的类**只能定义**成抽象类
- 通过abstract方法定义**规范**，然后要求**子类**必须定义具体**实现**
- 通过抽象类，就可以**严格限制**子类的**设计**，使子类之间更加通用
- 抽象类**不能实例化**，即不能用new来实例化抽象类。
- 抽象类**可以包含**属性、方法、构造方法。但是构造方法**不能**用来new**实例**，只能用来被子类**调用**。
- 抽象类**只能**用来**被继承**。

# 接口

- 接口就是**规范**，是比*抽象类*还**抽象**的*抽象类*，更加规范的对子类的约束
- 接口全面专业地实现了**规范和具体实现的分离**

>抽象类还提供某些具体实现，接口不提供任何实现，接口中所有方法都是抽象方法。接口是完全面向规范的，规定了一批类具有的公共方法规范。
>
> 从接口的实现者角度看，接口定义了可以向外部提供的服务。
>
>从接口的调用者角度看，接口定义了实现者能提供那些服务。
>
> 接口是两个模块之间通信的标准，==通信的规范==。如果能把你要设计的模块之间的接口定义好，就相当于完成了系统的设计大纲，剩下的就是添砖加瓦的具体实现了。大家在工作以后，做系统时往往就是使用“面向接口”的思想来设计系统。
>
>接口和实现类不是父子关系，是==实现规则的关系==。比如：我定义一个接口Runnable，Car实现它就能在地上跑，Train实现它也能在地上跑，飞机实现它也能在地上跑。就是说，如果它是交通工具，就一定能跑，但是一定要实现Runnable接口。

## 定义和使用接口

```
[访问修饰符] interface 接口名 [extends 父接口1，父接口2...]{
常量定义；
方法定义；
}
```

- 访问修饰符：只能是**public**或默认
- extends：接口可以**多继承**
- 常量：接口中的属性只能是**常量**，总是：public static final 修饰。不写也是。
- 方法：接口中的方法只能是：**public abstract**。 省略的话，也是public abstract。

```java
/**
 * 接口的使用
 * @author Carpediem
 * @version 1.0
 */
public class Test
{
    public static void main(String[] args) {
        Angel a1=new Angel();
        a1.fly();
        a1.helpOther();
        System.out.println(Volant.FLY_HIGHT);
        GoodMan g1=new GoodMan();
        g1.helpOther();

    }
}
interface Volant{
    int FLY_HIGHT=100;//总是：public static final 类型的
    void fly();//总是：public abstract void fly()

}
interface Kindness{
    void helpOther();
}

class Angel implements Volant,Kindness{
    @Override
    public void fly() {
        System.out.println("I am Angel,I am flying");
    }

    @Override
    public void helpOther() {
        System.out.println("I am helping others,I am Angel");
    }
}
class GoodMan implements Kindness{

    @Override
    public void helpOther() {
        System.out.println("I am GoodMan ,I am helping others.");
    }
}
output：
I am Angel,I am flying
I am helping others,I am Angel
100
I am GoodMan ,I am helping others.
```

1. 子类通过implements来**实现**接口中的**规范**。
2. 接口不能创建实例，但是可用于**声明引用变量类型**。
3. 一个类实现了接口，必须实现接口中**所有的方法**，并且这些方法只能是**public**的

## 接口的多继承

- 接口完全支持**多继承**
- 子接口扩展某个父接口，将会获得父接口中所定义的一切。

```java
/**
 * 接口的多继承
 * @author Carpediem
 * @version 1.0
 */
interface A{
    void testa();
}
interface B{
    void testb();
}
interface  C extends A,B{
    void testc();
}
public class Test implements C
{
    public static void main(String[] args) {
        Test t=new Test();
        t.testa();
        t.testb();
        t.testc();
    }

    @Override
    public void testa() {
        System.out.println("Test1");
    }

    @Override
    public void testb() {
        System.out.println("Test2");

    }

    @Override
    public void testc() {
        System.out.println("Test3");

    }
}
output:
Test1
Test2
Test3
```

# 内部类

- 把一个类放在另一个类的**内部定义**，称为**内部类**
- 内部类只是**编译**时的一个概念，一旦编译成功，就会称为完全不同的**两个类**，因此，内部类是**相对独立**的一种存在，其成员变量/方法名可以和外部类的相同。
- 内部类可以使用public、default、protected 、private以及static修饰。而外部顶级类(我们以前接触的类)只能使用public和default修饰。

## 内部类的作用

- 只能让**外部类**直接**访问**，**不**允许同一个包中其他类的直接访问
- 内部类可以直接访问**外部类**的属性，外部类**不能**访问内部类的**内部属性**
- 接口只是解决了多重继承的部分问题，而内部类使得多重继承的解决方案变得更加完整

>**内部类的使用场合：**
>
>1.  由于内部类提供了更好的封装特性，并且可以很方便的访问外部类的属性。所以，在==只为外部类提供服务的情况下==可以优先考虑使用内部类。
>2. 使用内部类间接实现多继承：每个内部类都能独立地继承一个类或者实现某些接口，所以无论外部类是否已经继承了某个类或者实现了某些接口，对于内部类没有任何影响。

## 内部类的分类

> 成员内部类（非静态内部类、静态内部类）、匿名内部类、局部内部类

**1. 非静态内部类**

- 非静态内部类必须寄存在一个外部类对象里，非静态内部类对象**单独属于**外部类的某个对象

- 非静态内部类中不能有**static**

- 非静态内部类可以直接访问外部类的成员，但外部类不能直接访问非静态内部类的成员（*需要通过外部类对象来创建内部类对象，从而实现访问*）

- 外部类的静态方法、静态代码块不能访问非静态内部类，包括不能使用非静态内部类定义变量、创建实例

- 成员变量的访问、内部类的访问

  ```java
  public class Test{
      private int age=10;
      class Inner{
          int age=20;
          public void show(){
              int age=30;
              System.out.println("内部类方法里的局部变量"+age);
              System.out.println("内部类的成员变量"+age);
              System.out.println("外部类的成员变量"+Test.this.age);
          }
      }
  
      public static void main(String[] args) {
          Test.Inner i1=new Test().new Inner();
          i1.show();
          Test t1=new Test();
          Test.Inner it1=t1.new Inner();
          it1.show();
      }
  }
  Output:
  内部类方法里的局部变量30
  内部类的成员变量30
  外部类的成员变量10
  内部类方法里的局部变量30
  内部类的成员变量30
  外部类的成员变量10
  ```

**2. 静态内部类**

```
public class Test{
    private int age=10;
    static class Inner{
        int age=20;
        public void show(){
            int age=30;
            System.out.println("内部类方法里的局部变量"+age);
            System.out.println("内部类的成员变量"+age);
//            System.out.println("外部类的成员变量"+Test.this.age);//Error:(9, 47) java: 无法从静态上下文中引用非静态 变量 this
        }
    }

    public static void main(String[] args) {
//        Test.Inner i1=new Test().new Inner();
        Test.Inner i1=new Test.Inner();
        i1.show();
        Test t1=new Test();
//        Test.Inner it1=t1.new Inner();//Error:(19, 24) java: 限定的新静态类
    }
}
Output:
内部类方法里的局部变量30
内部类的成员变量30
```

**3. 匿名内部类**

- 适合那种只需要使用一次的类。比如：键盘监听操作
- 匿名内部类没有访问修饰符
- 匿名内部类没有构造方法。因为它连名字都没有那又何来构造方法呢。

???

**4. 局部内部类**

内部类，它是定义在方法内部的，作用域只限于本方法，称为局部内部类

 # String

- String类又称作**不可变字符序列**
- String 位于**java.lang**包中，Java程序**默认**导入java.lang包下的所有类
- Java字符串就是Unicode字符序列
- Java**没有内置的字符串类型**，而是在标准Java类库中提供了一个**预定义的类String**，每个用双引号括起来的字符串都是String类的一个实例。

- 字符串连接+把两个字符串按给定的顺序连接在一起，并且是完全按照给定的形式

- "+"运算符两侧的操作数中只要有一个是字符串(String)类型，系统会自动将另一个操作数转换为字符串然后再进行连接。

  ```java
  public class Test{
      public static void main(String[] args) {
          String s1="Hello";
          String s2="World";
          System.out.println(s1+s2);
          int age=18;
          String str = "age is" + age;  //str赋值为"age is 18"
  //这种特性通常被用在输出语句中：
          System.out.println("age  is   " + age);
          System.out.println(str);
      }
  }
  Output：
  HelloWorld
  age  is   18
  age is18
  ```

## String类和常量池

>在Java的内存分析中，我们会经常听到关于“常量池”的描述，实际上常量池也分了以下三种：
>
>**1. 全局字符串常量池(String Pool)**
>
>   全局字符串常量池中存放的内容是在类加载完成后存到String Pool中的，在每个VM中只有一份，存放的是字符串常量的引用值(在堆中生成字符串对象实例)。
>
>**2. class文件常量池(Class Constant Pool)**
>
>   class常量池是在编译的时候每个class都有的，在编译阶段，存放的是常量(文本字符串、final常量等)和符号引用。
>
>**3. 运行时常量池(Runtime Constant Pool)**
>
>   运行时常量池是在类加载完成之后，将每个class常量池中的符号引用值转存到运行时常量池中，也就是说，每个class都有一个运行时常量池，类在解析之后，将符号引用替换成直接引用，与全局常量池中的引用值保持一致。
>
>**【示例5-28】常量池**
>
>```java
>String str1 = "abc";
>String str2 = new String("def");
>String str3 = "abc";
>String str4 = str2.intern();
>String str5 = "def";
>System.out.println(str1 == str3);// true
>System.out.println(str2 == str4);// false
>System.out.println(str4 == str5);// true
>```
>
>   示例5-28的首先经过编译之后，在该类的class常量池中存放一些符号引用，然后类加载之后，将class常量池中存放的符号引用转存到运行时常量池中，然后经过验证，准备阶段之后，在堆中生成驻留字符串的实例对象(也就是上例中str1所指向的“abc”实例对象)，然后将这个对象的引用存到全局String Pool中，也就是String Pool中，最后在解析阶段，要把运行时常量池中的符号引用替换成直接引用，那么就直接查询String Pool，保证String Pool里的引用值与运行时常量池中的引用值一致，大概整个过程就是这样了。
>
>   回到示例5-28的那个程序，现在就很容易解释整个程序的内存分配过程了，**首先，在堆中会有一个“abc”实例，全局String Pool中存放着“abc”的一个引用值，然后在运行第二句的时候会生成两个实例，一个是“def”的实例对象，并且String Pool中存储一个“def”的引用值，还有一个是new出来的一个“def”的实例对象，与上面那个是不同的实例，当在解析str3的时候查找String Pool，里面有“abc”的全局驻留字符串引用，所以str3的引用地址与之前的那个已存在的相同，str4是在运行的时候调用intern()函数，返回String Pool中“def”的引用值，如果没有就将str2的引用值添加进去，在这里，String Pool中已经有了“def”的引用值了，所以返回上面在new str2的时候添加到String Pool中的 “def”引用值，最后str5在解析的时候就也是指向存在于String Pool中的“def”的引用值，那么这样一分析之后，结果就容易理解了。**
>
>

## String类常用的方法

![图2.png](https://www.sxt.cn/360shop/Public/admin/UEditor/20170522/1495417924711064.png)

```java
public class Test{
    public static void main(String[] args) {
        String s1="Hello";
        String s2="World";
        String s3="hello";
        System.out.println(s1.charAt(3));//l
        System.out.println(s1.equals(s2));//false
        System.out.println(s1.equalsIgnoreCase(s3));//true
        System.out.println(s1.equals(s3));//false
        System.out.println(s1.indexOf("ll"));//2     
    }
}
```

## 字符串相等的判断

1. **equals**方法用来检测两个字符串内容是否相等。如果字符串s和t内容相等，则s.equals(t)返回true，否则返回false。

2. 要测试两个字符串除了大小写区别外是否是相等的，需要使用**equalsIgnoreCase**方法。

3. 判断字符串是否相等**不要使用"=="**。

![image-20220730121519202](C:\Users\Carpediem\AppData\Roaming\Typora\typora-user-images\image-20220730121519202.png)

```java
public class Test{
        public static void main(String[] args) {
            String g1 = "HelloWorld";
            String g2 = "HelloWorld";
            String g3 = new String("HelloWorld");
            System.out.println(g1 == g2); // true  指向同样的字符串常量对象
            System.out.println(g1 == g3); // false  g3是新创建的对象
            System.out.println(g1.equals(g3)); // true g1和g3里面的字符串内容一样
        }
}
```

![image-20220730122030611](C:\Users\Carpediem\AppData\Roaming\Typora\typora-user-images\image-20220730122030611.png)
