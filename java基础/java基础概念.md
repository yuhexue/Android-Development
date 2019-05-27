### 命名规则

- **类名**：对于所有的类来说，类名的首字母应该大写。
- **方法名**：所有的方法名都应该以小写字母开头。如果方法名含有若干单词，则后面的每个单词首字母大写。
- **源文件名**：源文件的名称应该和public类的类名保持一致。文件名的后缀为 **.java**。
- **主方法入口**：所有的 Java 程序由 **public static void main(String []args)** 方法开始执行。

### new

new 对象类型();      //括号内部参数根据构造函数定义来

### 源文件声明规则

当在一个源文件中定义多个类，并且还有import语句和package语句时，要特别注意这些规则。

- 一个源文件中只能有一个public类
- 一个源文件可以有多个非public类
- 源文件的名称应该和public类的类名保持一致。
- 如果一个类定义在某个包中，那么package语句应该在源文件的首行。
- 如果源文件包含import语句，那么应该放在package语句和类定义之间。如果没有package语句，那么import语句应该在源文件中最前面。
- import语句和package语句对源文件中定义的所有类都有效。在同一源文件中，不能给不同的类不同的包声明。

类有若干种访问级别，并且类也分不同的类型：抽象类和final类等。

除了上面提到的几种类型，Java还有一些特殊的类，如：内部类、匿名类。

### Java修饰符

像其他语言一样，Java可以使用修饰符来修饰类中方法和属性。主要有两类修饰符：

- 访问控制修饰符 : default, public , protected, private
- 非访问控制修饰符 : final, abstract, static, synchronized

### 访问控制修饰符（作用于类本身和类方法属性同效果）

Java中，可以使用访问控制符来保护对类、变量、方法和构造方法的访问。Java 支持 4 种不同的访问权限。

- **public** : 所有可见。使用对象：类、接口、变量、方法
- **default** (缺省）: 当前，同包可见。使用对象：类、接口、变量、方法
- **protected** : 当前，同包，不管在哪的子类可见。使用对象：变量、方法。 **注意：不能修饰类外部类**
- **private** : 类内可见。使用对象：变量、方法。 **注意：不能修饰外部类**

### 访问控制和继承

private方法不会被继承，其他方法的继承往大了兼容。这里的往大兼容指的是重写时不能缩小范围。

## 非访问修饰符

static 修饰符，用来修饰类方法和类变量。

final 修饰符，用来修饰类、方法和变量，final 修饰的类不能够被继承，修饰的方法不能被继承类重新定义，修饰的变量为常量，是不可修改的。

abstract 修饰符，用来创建抽象类和抽象方法。

synchronized 和 volatile 修饰符，主要用于线程的编程。

### static 修饰符

- **静态变量：**

  static 关键字用来声明独立于对象的静态变量，无论一个类实例化多少对象，它的静态变量只有一份拷贝。 静态变量也被称为类变量。局部变量不能被声明为 static 变量。

- **静态方法：**

  static 关键字用来声明独立于对象的静态方法。静态方法不能使用类的非静态变量。静态方法从参数列表得到数据，然后计算这些数据。

对类变量和方法的访问可以直接使用 **classname.variablename** 和 **classname.methodname** 的方式访问。

```java
public class InstanceCounter {    
	private static int numInstances = 0;    
	protected static int getCount() {
		return numInstances;    
    }      

	private static void addInstance() {       
		numInstances++;    
    }      

	InstanceCounter() {
		InstanceCounter.addInstance();    
	}      

	public static void main(String[] arguments) {
        System.out.println("Starting with " + InstanceCounter.getCount() + " instances");
	    for (int i = 0; i < 500; ++i){          
			new InstanceCounter();           
	    }       
        System.out.println("Created " + InstanceCounter.getCount() + " instances");    
	} 
}
```

### final 修饰符

**final 变量：**

final 表示"最后的、最终的"含义，变量一旦赋值后，不能被重新赋值。被 final 修饰的实例变量必须显式指定初始值。

final 修饰符通常和 static 修饰符一起使用来创建类常量。

## 实例

```java
public class Test{
	final int value = 10;   // 下面是声明常量的实例   
	public static final int BOXWIDTH = 6;   
	static final String TITLE = "Manager";     
	public void changeValue(){
    	value = 12; //将输出一个错误   
    } 
}
```

**final 方法**

类中的 final 方法可以被子类继承，但是不能被子类修改。

声明 final 方法的主要目的是防止该方法的内容被修改。

如下所示，使用 final 修饰符声明方法。

public class Test{     public final void changeName(){        // 方法体     } }

**final 类**

final 类不能被继承，没有类能够继承 final 类的任何特性。

## 实例

public final class Test {    // 类体 }

### abstract 修饰符

**抽象类：**

抽象类不能用来实例化对象，声明抽象类的唯一目的是为了将来对该类进行扩充。

一个类不能同时被 abstract 和 final 修饰。如果一个类包含抽象方法，那么该类一定要声明为抽象类，否则将出现编译错误。

抽象类可以包含抽象方法和非抽象方法。

## 实例

abstract class Caravan{    private double price;    private String model;    private String year;    public abstract void goFast(); //抽象方法    public abstract void changeColor(); }

**抽象方法**

抽象方法是一种没有任何实现的方法，该方法的的具体实现由子类提供。

抽象方法不能被声明成 final 和 static。

任何继承抽象类的子类必须实现父类的所有抽象方法，除非该子类也是抽象类。

如果一个类包含若干个抽象方法，那么该类必须声明为抽象类。抽象类可以不包含抽象方法。

抽象方法的声明以分号结尾，例如：**public abstract sample();**。

## 实例

public abstract class SuperClass{     abstract void m(); //抽象方法 }   class SubClass extends SuperClass{      //实现抽象方法       void m(){           .........       } }

### synchronized 修饰符

synchronized 关键字声明的方法同一时间只能被一个线程访问。synchronized 修饰符可以应用于四个访问修饰符。

## 实例

public synchronized void showDetails(){ ....... }

### transient 修饰符

序列化的对象包含被 transient 修饰的实例变量时，java 虚拟机(JVM)跳过该特定的变量。

该修饰符包含在定义变量的语句中，用来预处理类和变量的数据类型。

## 实例

public transient int limit = 55;   // 不会持久化 public int b; // 持久化

### volatile 修饰符

volatile 修饰的成员变量在每次被线程访问时，都强制从共享内存中重新读取该成员变量的值。而且，当成员变量发生变化时，会强制线程将变化值回写到共享内存。这样在任何时刻，两个不同的线程总是看到某个成员变量的同一个值。

一个 volatile 对象引用可能是 null。

## 实例

public class MyRunnable implements Runnable {     private volatile boolean active;     public void run()     {         active = true;         while (active) // 第一行         {             // 代码         }     }     public void stop()     {         active = false; // 第二行     } }

通常情况下，在一个线程调用 run() 方法（在 Runnable 开启的线程），在另一个线程调用 stop() 方法。 如果 **第一行** 中缓冲区的 active 值被使用，那么在 **第二行** 的 active 值为 false 时循环不会停止。

但是以上代码中我们使用了 volatile 修饰 active，所以该循环会停止。

### Java 变量

一个类可以包含以下类型变量：

- **局部变量**：在方法、构造方法或者语句块中定义的变量被称为局部变量。变量声明和初始化都是在方法中，方法结束后，变量就会自动销毁。
- **成员变量**：成员变量是定义在类中，方法之外的变量。这种变量在创建对象的时候实例化。成员变量可以被类中方法、构造方法和特定类的语句块访问。
- **类变量**：类变量也声明在类中，方法之外，但必须声明为static类型。

### 类变量（静态变量）

- 类变量也称为静态变量，以 static 关键字声明。
- 无论一个类创建了多少个对象，类只拥有类变量的一份拷贝。
- 静态变量除了被声明为常量外很少使用。常量是指声明为public/private，final和static类型的变量。常量初始化后不可改变。
- 静态变量储存在静态存储区。经常被声明为常量，很少单独使用static声明变量。
- 静态变量在第一次被访问时创建，在程序结束时销毁。
- 与实例变量具有相似的可见性。但为了对类的使用者可见，大多数静态变量声明为public类型。
- 默认值和实例变量相似。数值型变量默认值是0，布尔型默认值是false，引用类型默认值是null。变量的值可以在声明的时候指定，也可以在构造方法中指定。此外，静态变量还可以在静态语句块中初始化。
- 静态变量可以通过：*ClassName.VariableName*的方式访问。
- 类变量被声明为public static final类型时，类变量名称一般建议使用大写字母。如果静态变量不是public和final类型，其命名方式与实例变量以及局部变量的命名方式一致。

实例：

## Employee.java

import java.io.*;   

public class Employee {

​     //salary是静态的私有变量     

private static double salary;     

// DEPARTMENT是一个常量     

public static final String DEPARTMENT = "开发人员";     

public static void main(String[] args){ 

​    salary = 10000;         

System.out.println(DEPARTMENT+"平均工资:"+salary);     

} 

}

以上实例编译运行结果如下:

```
开发人员平均工资:10000.0
```

**注意：**如果其他类想要访问该变量，可以这样访问：**Employee.DEPARTMENT**。

本章节中我们学习了Java的变量类型，下一章节中我们将介绍Java修饰符的使用。

## 继承关键字

继承可以使用 extends 和 implements 这两个关键字来实现继承，而且所有的类都是继承于 java.lang.Object，当一个类没有继承的两个关键字，则默认继承object（这个类在 **java.lang** 包中，所以不需要 **import**）祖先类。

### extends关键字

在 Java 中，类的继承是单一继承，也就是说，一个子类只能拥有一个父类，所以 extends 只能继承一个类。

public class Penguin  extends  Animal{  }

### implements关键字

使用 implements 关键字可以变相的使java具有多继承的特性，使用范围为类继承接口的情况，可以同时继承多个接口（接口跟接口之间采用逗号分隔）。

```java
public interface A {
	public void eat();
    public void sleep(); 
}   
public interface B {
    public void show(); 
}   
public class C implements A,B { }
```

### super 与 this 关键字

super关键字：我们可以通过super关键字来实现对父类成员的访问，用来引用当前对象的父类。

this关键字：指向自己的引用。

```java
class Animal {
    void eat() {
        System.out.println("animal : eat");   
    } 
}   
class Dog extends Animal {
    void eat() {
        System.out.println("dog : eat");   
    }   
    void eatTest() {
        this.eat();   // this 调用自己的方法     
        super.eat();  // super 调用父类方法   
    } 
}   

```

### final关键字

final 关键字声明类可以把类定义为不能继承的，即最终类；或者用于修饰方法，该方法不能被子类重写：

- 声明类：

  ```
  final class 类名 {//类体}
  ```

- 声明方法：

  ```
  修饰符(public/private/default/protected) final 返回值类型 方法名(){//方法体}
  ```

**注**:实例变量也可以被定义为 final，被定义为 final 的变量不能被修改。被声明为 final 类的方法自动地声明为 final，但是实例变量并不是 final

## 构造器

子类是不继承父类的构造器（构造方法或者构造函数）的，它只是调用（隐式或显式）。

显式：如果父类的构造器带有参数，则必须在子类的构造器中显式地通过 **super** 关键字调用父类的构造器并配以参数列表。

隐式：如果父类构造器没有参数，则在子类的构造器中不需要使用 **super** 关键字调用父类构造器，系统会自动调用父类的无参构造器。

```java
class SuperClass {
  private int n;
  SuperClass(){
    System.out.println("SuperClass()");
  }
  SuperClass(int n) {
    System.out.println("SuperClass(int n)");
    this.n = n;
  }
}
// SubClass 类继承
class SubClass extends SuperClass{
  private int n;
  
  SubClass(){ // 自动调用父类的无参数构造器
    System.out.println("SubClass");
  }  
  
  public SubClass(int n){ 
    super(300);  // 调用父类中带有参数的构造器
    System.out.println("SubClass(int n):"+n);
    this.n = n;
  }
}
```

## 方法的重写规则

- 访问权限不能比父类中被重写的方法的访问权限更低。例如：如果父类的一个方法被声明为public，那么在子类中重写该方法就不能声明为protected。
- 声明为final的方法不能被重写。
- 声明为static的方法不能被重写，但是能够被再次声明。
- 构造方法不能被重写。

### 内部类和匿名类

内部类是类中类，相当于一个类进行了嵌套。

内部类当中可以调用外部类当中的属性和方法，而外部类却不能调用内部类当中的。

匿名内部类的具体名字不会在程序中编写出来，因为它已经在主方法当中被实例化了。

匿名内部类可以继承两类数据结构：一：抽象类。二：接口。

```java
//创建格式
new 父类构造器（参数列表）| 实现接口（）  
{  
	//匿名内部类的类体部分  
}
    
//举例
public abstract class Bird {
    private String name;

    public void setName(String name) {
        this.name = name;
    }
    
    public String getName() {
        return name;
	}

	public abstract int fly();
}

public class Test {
    public void test(Bird bird){
        System.out.println(bird.getName() + "能够飞 " + bird.fly() + "米");
    }

    public static void main(String[] args) {
        Test test = new Test();
        test.test(new Bird() {
            public int fly() {
                return 10000;
            }

            public String getName() {
                return "大雁";
            }
        });
}  
```

在使用匿名内部类的过程中，我们需要注意如下几点：

​      **1、**使用匿名内部类时，我们必须是继承一个类或者实现一个接口，但是两者不可兼得，同时也只能继承一个类或者实现一个接口。

​     **2、**匿名内部类中是不能定义构造函数的。

​     **3、**匿名内部类中不能存在任何的静态成员变量和静态方法。

​     **4、**匿名内部类为局部内部类，所以局部内部类的所有限制同样对匿名内部类生效。

​     **5、**匿名内部类不能是抽象的，它必须要实现继承的类或者实现的接口的所有抽象方法。

### 接口（Interface）

接口是抽象方法的集合。一个类通过继承接口的方式，从而来继承接口的抽象方法。

接口只定义派生类要用到的方法，但是方法的具体实现完全取决于派生类。接口无法被实例化。

接口并不是类，编写接口的方式和类很相似，但是它们属于不同的概念。类描述对象的属性和方法。接口则只包含类要实现的方法。

除非继承接口的类是抽象类，否则该类要定义接口中的所有方法。

### 接口与类相似点：

- 一个接口可以有多个方法。
- 接口文件保存在 .java 结尾的文件中，文件名使用接口名。
- 接口的字节码文件保存在 .class 结尾的文件中。
- 接口相应的字节码文件必须在与包名称相匹配的目录结构中。

### 接口与类的区别：

- 接口不能用于实例化对象。
- 接口没有构造方法。
- 接口中所有的方法必须是抽象方法。
- 接口不能包含成员变量，除了 static 和 final 变量。
- 接口不是被类继承了，而是要被类实现。
- 接口支持多继承。

### 接口特性

- 接口和接口中每一个方法都是是隐式抽象的，当声明一个接口和其方法时，不必使用**abstract**关键字。
- 接口中的方法都是公有的。

### 抽象类和接口的区别

- \1. 抽象类中的方法可以有方法体，就是能实现方法的具体功能，但是接口中的方法不行。
- \2. 抽象类中的成员变量可以是各种类型的，而接口中的成员变量只能是 **public static final** 类型的。
- \3. 接口中不能含有静态代码块以及静态方法(用 static 修饰的方法)，而抽象类是可以有静态代码块和静态方法。
- \4. 一个类只能继承一个抽象类，而一个类却可以实现多个接口。

### 接口的声明和实现

```java
import java.lang.*;  //引入包

//接口声明
public interface NameOfInterface
{
//任何类型 final, static 字段
//抽象方法
   public void eat();
   public void travel();
}

//接口的实现，implements
public class MammalInt implements Animal{
 
   public void eat(){
      System.out.println("Mammal eats");
   }
 
   public void travel(){
      System.out.println("Mammal travels");
   } 
 
   public static void main(String args[]){
      MammalInt m = new MammalInt();
      m.eat();
      m.travel();
   }
}
```

- 类在重写方法时要保持一致的方法名，并且应该保持相同或者相兼容的返回值类型。
- 如果实现接口的类是抽象类，那么就没必要实现该接口的方法。

在实现接口的时候，也要注意一些规则：

- 一个类只能继承一个类，但是能实现多个接口。
- 一个接口能继承另一个接口，这和类之间的继承比较相似。

## 接口的继承

一个接口能继承另一个接口，和类之间的继承方式比较相似。接口的继承使用extends关键字。

```java
// 文件名: Sports.java
public interface Sports
{
	public void setHomeTeam(String name);
	public void setVisitingTeam(String name);
}
// 文件名: Football.java
public interface Football extends Sports
{
    public void homeTeamScored(int points);
    public void visitingTeamScored(int points);
}
//实现Football接口的类要重写4个方法
```

## 接口的多继承

在Java中，类的多继承是不合法，但接口允许多继承。

```java
public interface Hockey extends Sports, Event{
}
```

### 包(package)

包主要用来对类和接口进行分类。当开发Java程序时，可能编写成百上千的类，因此很有必要对类和接口进行分类。用于区别类名的命名空间。

Java 使用包（package）这种机制是为了防止命名冲突，访问控制，提供搜索和定位类（class）、接口、枚举（enumerations）和注释（annotation）等。

### 包的作用

- 1、把功能相似或相关的类或接口组织在同一个包中，方便类的查找和使用。
- 2、如同文件夹一样，包也采用了树形目录的存储方式。同一个包中的类名字是不同的，不同的包中的类的名字是可以相同的，当同时调用两个不同包中相同类名的类时，应该加上包名加以区别。因此，包可以避免名字冲突。
- 3、包也限定了访问权限，拥有包访问权限的类才能访问某个包中的类。

例如一个Something.java 文件它的内容

```java
package net.java.util; 
public class Something{
}
```

那么它的路径应该是 **net/java/util/Something.java** 这样保存的。 package(包) 的作用是把不同的 java 程序分类保存，更方便的被其他 java 程序调用。

开发者可以创建包，然后在包内创建源文件和类。当你自己完成类的实现之后，将相关的类分组，可以让其他的编程者更容易地确定哪些类、接口、枚举和注释等是相关的。

由于包创建了新的命名空间（namespace），所以不会跟其他包中的任何名字产生命名冲突。使用包这种机制，更容易实现访问控制，并且让定位相关类更加简单。

## 创建包

包声明应该在源文件的第一行，每个源文件只能有一个包声明，这个文件中的每个类型都应用于它。

如果一个源文件中没有使用包声明，那么其中的类，函数，枚举，注释等将被放在一个无名的包（unnamed package）中。

### Import语句（导入包）

在Java中，如果给出一个完整的限定名，包括包名、类名，那么Java编译器就可以很容易地定位到源代码或者类。Import语句就是用来提供一个合理的路径，使得编译器可以找到某个类。

为了能够使用某一个包的成员，我们需要在 Java 程序中明确导入该包。

在 java 源文件中 import 语句应位于 package 语句之后，所有类的定义之前，可以没有，也可以有多条。

如果在一个包中，一个类想要使用本包中的另一个类，那么该包名可以省略。

## 内置数据类型（具体信息请查阅）

byte,short,int,long,float,double,boolean,char

"L"理论上不分大小写，但是若写成"l"容易与数字"1"混淆，不容易分辩。所以最好大写。

## 引用类型

- 在Java中，引用类型的变量非常类似于C/C++的指针。引用类型指向一个对象，**指向对象的变量是引用变量**。这些变量在声明时被指定为一个特定的类型，比如 Employee、Puppy 等。变量一旦声明后，类型就不能被改变了。
- 对象、数组都是引用数据类型。
- 所有引用类型的默认值都是null。
- 一个引用变量可以用来引用任何与之兼容的类型。
- 例子：Site site = new Site("Runoob")。

## Java 常量

常量在程序运行时是不能被修改的。

在 Java 中使用 final 关键字来修饰常量，声明方式和变量类似：

```
final double PI = 3.1415927;
```

类型转换暂不研究

### 多态存在的三个必要条件

- 继承
- 重写
- 父类引用指向子类对象

比如：

```
Parent p = new Child();
```

当使用多态方式调用方法时，首先检查父类中是否有该方法，如果没有，则编译错误；如果有，再去调用子类的同名方法。

区别：

Java 中没有虚函数的概念，它的普通函数就相当于 C++ 的虚函数，动态绑定是Java的默认行为。如果 Java 中不希望某个函数具有虚函数特性，可以加上 final 关键字变成非虚函数。

## 多态的实现方式

### 方式一：重写：

这个内容已经在上一章节详细讲过，就不再阐述，详细可访问：

Java 重写(Override)与重载(Overload)

### 方式二：接口

- \1. 生活中的接口最具代表性的就是插座，例如一个三接头的插头都能接在三孔插座中，因为这个是每个国家都有各自规定的接口规则，有可能到国外就不行，那是因为国外自己定义的接口类型。
- \2. java中的接口类似于生活中的接口，就是一些方法特征的集合，但没有方法的实现。具体可以看 [java接口](https://www.runoob.com/java/java-interfaces.html) 这一章节的内容。

### 方式三：抽象类和抽象方法

详情请看 [Java抽象类](https://www.runoob.com/java/java-abstraction.html) 章节。

### **抽象类**

和C++不一样，java的抽象类中可以不包含抽象方法，但是抽象类同样不能被实例化，而应该通过继承来使用。

## 抽象方法

抽象方法在父类中声明，在子类中定义。声明时在方法名后面直接跟一个分号，而不是花括号。

Abstract 关键字同样可以用来声明抽象方法，抽象方法只包含一个方法名，而没有方法体。

```java
public abstract class Employee {    
    private String name;    
    public abstract double computePay();        //
}
```

声明抽象方法会造成以下两个结果：

- 如果一个类包含抽象方法，那么该类必须是抽象类。
- 任何子类必须重写父类的抽象方法，或者声明自身为抽象类。

继承抽象方法的子类必须重写该方法。否则，该子类也必须声明为抽象类。最终，必须有子类实现该抽象方法，否则，从最初的父类到最终的子类都不能用来实例化对象。

## 抽象类总结规定

- \1. 抽象类不能被实例化(初学者很容易犯的错)，如果被实例化，就会报错，编译无法通过。只有抽象类的非抽象子类可以创建对象。
- \2. 抽象类中不一定包含抽象方法，但是有抽象方法的类必定是抽象类。
- \3. 抽象类中的抽象方法只是声明，不包含方法体，就是不给出方法的具体实现也就是方法的具体功能。
- \4. 构造方法，类方法（用 static 修饰的方法）不能声明为抽象方法。
- \5. 抽象类的子类必须给出抽象类中的抽象方法的具体实现，除非该子类也是抽象类。

