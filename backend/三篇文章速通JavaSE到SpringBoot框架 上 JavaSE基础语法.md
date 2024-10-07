
### 前置环境
java开发工具包
`https://www.oracle.com/cn/java/technologies/downloads/`

idea编辑器
`https://www.jetbrains.com/idea/download/?section=mac`
### 变量
变量本质上就是代表一个”可操作的存储空间”，空间位置是确定的，但是里面放置什么值不确定。我们可通过变量名来访问“对应的存储空间”，从而操纵这个“存储空间”存储的值。Java是一种强类型语言，每个变量都必须声明其数据类型。变量的数据类型决定了变量古据存储空间的大小<br/>

Java是一种强类型语言，每个变量都必须声明其数据类型Java的数据类型可分为两大类：基本数据类型(primitive data type)和引用数据类型(reference data type)
#### 基本数据类型
- 整形： byte 、short、  int、  long
- 浮点型：float 、double
- 字符型：char 
- 布尔型：boolean
```java
public class test2 {  
    public static void main(String[] args) {  
       // 基本数据类型  
//【1】整数类型  
        byte a=8 ;//数范围：-128~127    布尔型（boolean）  
        short b=2980; //表数范围：正负三万  
        int c =19883; //表数范围：正负21亿   
long d=12345678919L;//表数范国：很大很大，如果表示的数的范国超过int类型表数范国就需要加  
        // 【2】浮点类型：  
        float e =3.14f;  //如果用fLoat类型表示一个小数，后面必须加上f  
        double f=3.14;  
//【3】字符型：  
        char g ='a' ;//单引号引起来的单个字符  
        System.out.println("hello world");//后续学习的字符串是多个单个字符拼接的  
//【4】布尔类型  
        boolean f1ag = true;  //  布尔值只有两个：true、false  
    }  
}
```
#### 引用数据类型
- 类 （class）
- 接口 （interface）
- 数组 （array）
#### 标识符
- 由26个英文字母大小写，0-9 ，_或 $ 组成。
- 数字不可以开头。
- 不可以使用关键字和保留字，但能包含关键字和保留字。
- Java中严格区分大小写，长度无限制。
- 标识符不能包含空格。
####  运算符
需要注意的是，在二元运算中表达式的结果取决于类型范围最大的那个，且类型最小为int

也就是说，如果两个byte类型的数据进行运算，由于运算的类型最小为int，所以其结果不是byte类型而是int类型，所以无法赋值给byte的变量，需要进行强制类型转换

**（1）二元运算符**：+、-、*、/、%

**（2）一元运算符**：++、--

**（3）赋值运算符**：=、+=、-=、*=、/=、%=

**（4）关系运算符**：==、!=、>、>=、 <、<=

**（5）逻辑运算符**：&、|、^、!、&&、||

**（6）三元运算符**：exp1 ？ exp2 ： exp3

```java
int a1 = 10, b1 = 5;  
int sum = a + b; // 加法  
int diff = a - b; // 减法  
int product = a * b; // 乘法  
int quotient = a / b; // 除法  
int remainder = a % b; // 取模  
  
int num = 5;  
num++; // 自增，num变为6  
num--; // 自减，num变为5  
  
int x = 10; // 赋值  
x += 5; // 等价于 x = x + 5; x现在为15  
x -= 3; // 等价于 x = x - 3; x现在为12  
  
int c1 = 10, d1 = 20;  
boolean isEqual = (a == b); // false  
boolean isGreater = (a > b); // false  
  
  
boolean flag1 = true, flag2 = false;  
boolean result = flag1 && flag2; // false  
result = flag1 || flag2; // true  
  
int max = (a > b) ? a : b; // 如果a大于b，max为a，否则为b
```
### 流程控制
![[Pasted image 20240922183901.png]]
####  三种基本流程结构
- **顺序结构**：程序从上到下逐行地执行，中间没有任何判断和跳转。
- **分支结构**：根据条件，选择性地执行某段代码。  
有==if…else==和==switch-case==两种分支语句。
```java
public class IfElseExample {  
    public static void main(String[] args) {  
        int score = 85;  
        if (score >= 60) {  
            System.out.println("及格");  
        } else {  
            System.out.println("不及格");  
        }  
    int day = 3;  
	switch (day) {  
    case 1:  
        System.out.println("星期一");  
        break;  
    case 2:  
        System.out.println("星期二");  
        break;  
    case 3:  
        System.out.println("星期三");  
        break;  
    default:  
        System.out.println("未知的日子");  
}
        
    } 

}
```
- **循环结构**：根据循环条件，重复性的执行某段代码。  有==while==、==do…while==、==for==三种循环语句。 
```java
public class WhileExample {  
    public static void main(String[] args) {  
        int count = 0;  
        while (count < 5) {  
            System.out.println("Count: " + count);  
            count++;  
        }  
        int count1 = 0;  
    //   先执行一次循环体，然后判断条件。
	do {  
    System.out.println("Count: " + count1);  
    count1++;  
	} while (count1 < 5);

for (int i = 0; i < 5; i++) {  
    System.out.println("Count: " + i);  
}

    }  
    
}


```

#### 方法和方法的重载
方法(method)就是一段用来完成特定功能的代码片段
##### 方法声明格式
\[修饰符1修饰符2 ...]\返回值类型  方法名(形式参数列表){
<br/>
}
##### 方法的调用方式
对象名.方法名(实参列表)<br/>
方法名(实参列表)
```java
public class MyClass {  
  
    // 方法声明  
    public int add(int a, int b) {  
        return a + b; // 方法体  
    }  
  
    public static void main(String[] args) {  
        MyClass obj = new MyClass(); // 创建对象  
        int result = obj.add(5, 3); // 方法调用  
        System.out.println("结果: " + result); // 输出结果  
    }  
}
```
### 方法的重载
`方法的载只和方法名、形参列表有关，与其它无关`
要求：方法名必须相同，形参列表必须不同（类型不同，顺序不同，个数不同）
```java
public class OverloadExample {  
  
    // 方法重载：无参数  
    public void display() {  
        System.out.println("无参数的方法");  
    }  
  
    // 方法重载：一个整数参数  
    public void display(int a) {  
        System.out.println("整数参数: " + a);  
    }  
  
    // 方法重载：两个字符串参数  
    public void display(String str1, String str2) {  
        System.out.println("字符串参数: " + str1 + ", " + str2);  
    }  
  
    public static void main(String[] args) {  
        OverloadExample obj = new OverloadExample();  
  
        // 调用不同重载的方法  
        obj.display(); // 无参数  
        obj.display(10); // 一个整数参数  
        obj.display("Hello", "World"); // 两个字符串参数  
    }  
}
```
#### 方法的重写

发生在子类和父类中，当子类对父类提供的方法不满意的时候，要对父类的方法进行重写方法的重写有严格的格式要求
`子类的方法名字和父类必须一致，参数列表（个数，类型，顺序）也要和父类一致。`
```java
class Animal {  
    // 父类方法  
    public void sound() {  
        System.out.println("动物发出声音");  
    }  
}  
  
class Dog extends Animal {  
    // 重写父类方法  
    @Override  
    public void sound() {  
        System.out.println("汪汪");  
    }  
}  
  
class Cat extends Animal {  
    // 重写父类方法  
    @Override  
    public void sound() {  
        System.out.println("喵喵");  
    }  
}  
  
public class OverrideExample {  
    public static void main(String[] args) {  
        Animal myDog = new Dog(); // 向上转型  
        Animal myCat = new Cat(); // 向上转型  
  
        myDog.sound(); // 输出: 汪汪  
        myCat.sound(); // 输出: 喵喵  
    }
```
#### 重载和重写的区别
重载：在同一个类中，当方法名相同，形参列表不同的时候，多个方法构成了重载
重写：在不同的类中，子类对父类提供的方法不满意，对父类的方法进行重写
### 数组
数组是相同类型数据的有序集合。其中，每一个数据称作一个元素，每个元素可以通过一个索引（下标）来访问它们。

数组的声明   类型标识符数组名<br/>
数组的创建  new类型标识符\[数组长度]\ <br/>
数组的赋值  数组名\[下标]\=具体数值<br/>
数组的使用  通过下标访问数组元素<br/>
数组的遍历  普通for循环 增强for循环

##### 数组的特点
1.长度是确定的。数组一旦被创建，它的大小就是不可以改变的。
2.其元素的类型必须是相同类型，不允许出现混合类型。
3.数组类型可以是任何数据类型，包括基本类型和引用类型
4.数组有索引的：索引从0开始，到数组.length-1结束

### 面向对象
#### 基本概念
**类**:对对象向上抽取出像的部分、公共的部分以此形成类，类就相当于一个模版<br/>
**对象**：模版下具体的产物可以理解为具体对象，对象就是一个一个具体的实例，就相当于这个模版下具体的产品
==Java中先定义类，再创建对象==
#### 类的编写和对象的创建与使用
##### 类的编写
1.给类起一个见名知意的名字，首字母大写，驼峰命名原则<br/>
2.类的特性编写，特性即类的属性部分。<br/>

3.类的行为编写，行为即类的方法部分。
##### 对象的创建和使用
创建格式：类名对象名=new类名0<br/>
给对象的属性赋值：对象名.属性名=值<br/>
调用对象的方法：\[返回值类型名字=]对象名.方法名（参数列表）<br/>
==对于一个类来说   般有三种常见的成员：属性、方法、构造器。==
这三种成员都可以定义零个或多个。
构造方法也叫构造器，是一个创建对象时被自动调用的特殊方法，用于对象的初始化。Java通过new关键字来调用构造器，从而返回该类的实例
#### 构造器
若无参数列表，称之为无参构造器（空构造器）<br/>
若有参数列表，称之为有参构造器<br/>
如果一个类没有显式编写构造器的话，那么系统会为这个类默认分配一个空构造器调用构造器以后，对对象进行初始化操作，将对象的地址返回给实例
尽量保证空构造器的存在
##### 构造器特点
   1. 构造器的方法名必须和类名一致
   2. 构造器通过new关键字调用
   3. 构造器不能定义返回值类型，不能在构造器里使用return关键字来返回某个值。
   4. 如果我们没有定义构造器，则编译器会自动定义一个无参的构造方法。如果已定义则编译器不会自动添加！
```java
class Person {  
    private String name;  
    private int age;  
  
    // 无参构造器（空构造器）  
    public Person() {  
        this.name = "未知";  
        this.age = 0;  
    }  
  
    // 有参构造器  
    public Person(String name, int age) {  
        this.name = name;  
        this.age = age;  
    }  
  
    // 方法用于显示信息  
    public void display() {  
        System.out.println("姓名: " + name + ", 年龄: " + age);  
    }  
}  
  
public class ConstructorExample {  
    public static void main(String[] args) {  
        // 使用无参构造器创建对象  
        Person person1 = new Person();  
        person1.display(); // 输出: 姓名: 未知, 年龄: 0  
  
        // 使用有参构造器创建对象  
        Person person2 = new Person("张三", 25);  
        person2.display(); // 输出: 姓名: 张三, 年龄: 25  
    }  
}
```
#### 封装
我们程序设计追求“高内聚，低耦合”<br/>
高内聚：类的内部数据操作细节自己完成，不允许外部干涉<br/>
低耦合：仅对外暴露少量的方法用于使用。<br/>
隐藏对象内部的复杂性，只对外公开简单的接口。便于外界调用，从而提高系统的可扩展性、可维护性，提高程序的安全性。通俗的说，把该隐藏的隐藏起来，该暴露的暴露出来。这就是封装性的设计思想<br/>
##### 以属性为案例进行封装：
1. 将属性私有化，被private修饰--》加入权限修饰符
 旦加入了权限修饰符，其他人就不可以随意的获取这个属性
2. 提供public修饰的方法让别人来访问/使用
3. 即使外界可以通过方法来访问属性了，但是也不能随意访问，因为程序员可以在方法中可以加入限制条件。
```java
class Person {  
    // 私有属性  
    private String name;  
    private int age;  
  
    // 构造器  
    public Person(String name, int age) {  
        this.name = name;  
        this.age = age;  
    }  
  
    // 获取姓名  
    public String getName() {  
        return name;  
    }  
  
    // 获取年龄  
    public int getAge() {  
        return age;  
    }  
  
    // 设置年龄  
    public void setAge(int age) {  
        if (age > 0) {  
            this.age = age;  
        } else {  
            System.out.println("年龄必须大于0");  
        }  
    }  
}  
  
public class Main {  
    public static void main(String[] args) {  
        Person person = new Person("张三", 25);  
        System.out.println("姓名: " + person.getName() + ", 年龄: " + person.getAge());  
  
        person.setAge(30); // 设置新年龄  
        System.out.println("新年龄: " + person.getAge());  
    }  
}
```

#### 继承
允许一个类（子类）继承另一个类（父类）的属性和方法。通过继承，子类可以重用父类的代码，增加代码的复用性和可维护性。子类还可以扩展或重写父类的方法，以实现特定的功能。<br/>
例如，子类可以添加新的属性或方法，或重写父类的方法以改变其行为。使用 `extends` 关键字来实现继承，子类可以访问父类的公共和保护成员，但不能直接访问私有成员。<br/>
继承是对类的抽象
```java
class Animal {  
    void eat() {  
        System.out.println("动物在吃");  
    }  
}  
  
class Dog extends Animal {  
    void bark() {  
        System.out.println("狗在叫");  
    }  
}  
  
public class Main {  
    public static void main(String[] args) {  
        Dog dog = new Dog();  
        dog.eat(); // 继承自 Animal        dog.bark(); // Dog 的方法  
    }  
}
```
#### 多态
Java 多态是指同一个方法可以在不同的对象上表现出不同的行为。它主要分为两种形式：编译时多态（静态多态）和运行时多态（动态多态）。
**PS**:多态跟属性无关，多态指的是方法的多态，而不是属性的多态。
==多态的三要素：继承、重写、父类引用指向子类对象==
##### 编译时多态（方法重载）
```java
class MathUtils {  
    // 加法方法重载  
    int add(int a, int b) {  
        return a + b;  
    }  
  
    double add(double a, double b) {  
        return a + b;  
    }  
}  
  
public class Main {  
    public static void main(String[] args) {  
        MathUtils math = new MathUtils();  
        System.out.println(math.add(5, 10)); // 调用 int 加法  
        System.out.println(math.add(5.5, 10.5)); // 调用 double 加法  
    }  
}
```
##### 运行时多态（方法重写）
运行时多态是通过方法重写实现的，子类可以重写父类的方法。程序在运行时决定调用哪个方法，通常与对象的实际类型有关。
```java
class Animal {  
    void makeSound() {  
        System.out.println("动物发出声音");  
    }  
}  
  
class Dog extends Animal {  
    void makeSound() {  
        System.out.println("狗在叫");  
    }  
}  
  
class Cat extends Animal {  
    void makeSound() {  
        System.out.println("猫在叫");  
    }  
}  
  
public class Main {  
    public static void main(String[] args) {  
        Animal myDog = new Dog();  
        Animal myCat = new Cat();  
  
        myDog.makeSound(); // 输出: 狗在叫  
        myCat.makeSound(); // 输出: 猫在叫  
    }  
}
```

### 异常处理
异常就是在程序的运行过程中所发生的不正常的事件，它会中断正在运行的程序
1. 所需文件找不到
2. 网络连接不通或中断
3.  算术运算错（被零除.）
4. 数组下标越界
5. 装载一个不存在的类或者对null对象操作
6. 类型转换异常
Java提供异常处理机制。它将异常处理代码和和业务代码分离，使程序更优雅，更好的容错性，高键壮性。
Java的异常处理是通过5个关键字来实现的：`try、catch、  finally、throw、throws`
##### try-catch执行情况
情况1：try块中代码没有出现异常
不执行catch块代码，执行catch块后边的代码<br/>
情况2：try块中代码出现异常，catch中异常类型匹配（相同或者父类）<
Java会生成相应的异常对象，Java系统寻找匹配的catch块，执行catch块代码，执行catch块后边的代码。try块中尚未执行的语句不会执行。<br/>
情况3：try块中代码出现异常，catch中异常类型不匹配
不执行catch块代码，不执行catch块后边的代码，程序会中断运行<br/>
catch块中如何处理异常
其中一种方式：自定义内容输出
```java
public class TryCatchExample {  
    public static void main(String[] args) {  
        // 情况1：try块中代码没有出现异常  
        try {  
            System.out.println("情况1：没有异常的情况。");  
            // 正常执行的代码  
        } catch (Exception e) {  
            System.out.println("捕获到异常：" + e.getMessage());  
        }  
        System.out.println("情况1后面的代码继续执行。");  
  
        // 情况2：try块中代码出现异常，catch中异常类型匹配  
        try {  
            System.out.println("情况2：即将抛出异常。");  
            int result = 10 / 0; // 抛出ArithmeticException  
        } catch (ArithmeticException e) {  
            System.out.println("捕获到ArithmeticException：" + e.getMessage());  
        }  
        System.out.println("情况2后面的代码继续执行。");  
  
        // 情况3：try块中代码出现异常，catch中异常类型不匹配  
        try {  
            System.out.println("情况3：即将抛出异常。");  
            String str = null;  
            System.out.println(str.length()); // 抛出NullPointerException  
        } catch (NumberFormatException e) {  
            // 这个catch块不会被执行  
            System.out.println("捕获到NumberFormatException：" + e.getMessage());  
        }  
        // 如果上面的try块抛出异常，程序会中断，这里不会执行  
        System.out.println("情况3后面的代码将不会执行。");  
    }  
}
```
##### throw和throws的区别：
 1. 位置不同：
throw：方法内部
throws：方法的签名处，方法的声明处
 2. 内容不同：
throw+异常对象
throws+异常的类型
 3. 作用不同：
throw：异常出现的源头，制造异常
throws：在方法的声明处，告诉方法的调用者，这个方法中可能会出现我声明的这些异常。然后调用者对这个异常进行处理：要么自己处理要么再继续向外抛出异常
```java
public class ThrowVsThrowsExample {  
  
    // 使用 throws 声明异常  
    public static void mayThrowException() throws CustomException {  
        // 这里可以根据某种条件抛出异常  
        boolean condition = true; // 修改为 false 以避免抛出异常  
        if (condition) {  
            throw new CustomException("自定义异常被抛出！");  
        }  
    }  
  
    public static void main(String[] args) {  
        try {  
            // 调用可能抛出异常的方法  
            mayThrowException();  
        } catch (CustomException e) {  
            // 捕获并处理异常  
            System.out.println("捕获到异常：" + e.getMessage());  
        }  
  
        // 下面是 throw 的示例  
        try {  
            // 直接在方法内部使用 throw            throw new IllegalArgumentException("非法参数异常被抛出！");  
        } catch (IllegalArgumentException e) {  
            System.out.println("捕获到异常：" + e.getMessage());  
        }  
    }
```
### 集合 
在 Java 中，集合（Collections）是用于存储和操作多个元素的对象。Java 提供了一组用于处理集合的类和接口，主要分为以下几种类型
##### 数组的缺点也就是集合的优点
1. 数组一旦指定了长度，那么长度就被确定了，不可以更改 
2. 删除，增加元素效率低
3. 数组中实际元素的数量是没有办法获取的，没有提供对应的方法或者属性来获取
4. 数组有序，可重复，对于无序的，不可重复的场合数组不能满足要求
![[Pasted image 20240923232050.png]]
#### ArrayList
`ArrayList` 是 Java 中最常用的集合之一，属于 `List` 接口的实现。它使用动态数组来存储元素，支持快速随机访问和动态扩展。以下是一些关键特点和基本用法：
```java
import java.util.ArrayList;  
  
public class ArrayListExample {  
    public static void main(String[] args) {  
        // 创建 ArrayList        ArrayList<String> fruits = new ArrayList<>();  
  
        // 添加元素  
        fruits.add("Apple");  
        fruits.add("Banana");  
        fruits.add("Cherry");  
  
        // 访问元素  
        System.out.println("First fruit: " + fruits.get(0)); // 输出 Apple  
        // 修改元素  
        fruits.set(1, "Blueberry"); // 将 Banana 改为 Blueberry  
        // 删除元素  
        fruits.remove("Cherry");  
  
        // 遍历 ArrayList        for (String fruit : fruits) {  
            System.out.println(fruit);  
        }  
  
        // 输出大小  
        System.out.println("Size: " + fruits.size());  
    }  
}
```
==这里不多介绍其他的集合==
### Scanner
使用Scanner类从键盘获取不同类型的变量。  
==具体实现按步骤：==  
1.   导包：import java.util.Scanner;  
2.  Scanner 的实例化：Scanner scan = new Scanner(System.in);  
3.  调用Scanner类的相关方法（next()/nextXxx()），来获取指定类型的变量  
【注意】：  
  
需要根据相应的方法。来输入指定类型的值。 <br/> 
  
如果输入的数据类型与要求的类型不匹配时，会报异常：InputMisMatchException 导致程序终止。  <br/>
```java
 import java.util.Scanner;  
  
public class ScannerExample {  
    public static void main(String[] args) {  
        Scanner scanner = new Scanner(System.in);  
  
        System.out.print("请输入一个整数: ");  
        if (scanner.hasNextInt()) {  
            int number = scanner.nextInt();  
            System.out.println("你输入的整数是: " + number);  
        } else {  
            System.out.println("输入不是一个有效的整数。");  
        }  
  
        System.out.print("请输入你的名字: ");  
        scanner.nextLine(); // 清除前一个输入的换行符  
        String name = scanner.nextLine();  
        System.out.println("你好, " + name + "!");  
  
        // 关闭 Scanner        scanner.close();  
    }  
}
```
### 根据所学语法做个综合项目
==一个简单的图书管理==
```java
// test01.java
public class test01 {  
    public static void main(String[] args){  
        ArrayList list = new ArrayList();  
        while(true) {  
            System.out.println("----图书管理----");  
            System.out.println("1.展示书籍");  
            System.out.println("2.添加书籍");  
            System.out.println("3.删除书籍");  
            System.out.println("4.退出应用");  
            Scanner sc = new Scanner(System.in);  
            System.out.println("请输入功能号码");  
            int choice = sc.nextInt();  
            if (choice == 1) {  
                System.out.println("--图书展示区域--");  
                for (int i = 0; i < list.size(); i++) {  
                    Book b = (Book)(list.get(i));  
                    System.out.println(b.getbNo() + "---" +b.getBName());  
                }  
            } else if (choice == 2) {  
                System.out.println("请输入书籍编号");  
                int bNo =sc.nextInt();  
                System.out.println("请输入书籍名字");  
                String bName = sc.next();  
                Book b = new Book();  
                b.setbNo(bNo);  
                b.setBName(bName);  
                list.add(b);  
  
            } else if (choice == 3) {  
                System.out.println("请输入删除书籍编号");  
                int delbNo = sc.nextInt();  
                for (int i = 0; i <list.size() ; i++) {  
                    Book b =  (Book)(list.get(i));  
                    if(b.getbNo() == delbNo){  
                        list.remove(b);  
                        System.out.println("删除成功");  
                        break;  
                    }  
                }  
  
            } else {  
                break;  
            }  
  
        }  
    }  
}
//Book.java
package com.zhai.test01;  
  
public class Book {  
    private int bNo;  
    private String BName;  
  
    public Book(int bNo, String BName) {  
        this.bNo = bNo;  
        this.BName = BName;  
    }  
  
    public Book() {  
    }  
  
    public int getbNo() {  
        return bNo;  
    }  
  
    public String getBName() {  
        return BName;  
    }  
  
    public void setbNo(int bNo) {  
        this.bNo = bNo;  
    }  
  
    public void setBName(String BName) {  
        this.BName = BName;  
    }  
}
```


