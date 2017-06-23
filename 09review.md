# 复习
## 封装：
将类的状态信息隐藏在类的内部，通过该类提供的方法来实现对隐藏信息的操作和访问；   
### 具体步骤：
- 修改属性的可见性来限制对属性的访问，为每个属性创建一对赋值（setter）方法和取值（getter）方法，用于对这些属性的存取；- 在赋值方法中，加入对属性的存取控制语句；
- 测试类通过调用setter方法，为对象的各个属性赋值；
使用封装，增加了数据访问限制，增强了程序的可维护性；

## 构造方法：
构造方法的名字和类名相同，没有返回值类型，构造方法的作用就是在创建对象时执行一些初始化操作，如给成员属性赋初值；   

## 方法重载：
一个类中包含。两个或两个以上方法，且它们的方法名形同，方法参数个数或参数类型不同，则称该方法为重载。成员方法和构造方法都可以进行重载；   

构造方法重载是方法重载的典型示例；   
通过调用不同的构造方法来表达对象的多种初始化行为；   

## 关键字static：
static可以用来修饰属性、方法和代码块。static修饰的变量属于这个类所有，即由这个类创建的所有对象共用同一个static变量。    
通常把static修饰的属性和方法称为类的属性（类变量）、类方法。不使用static修饰的属性和方法，属于单个对象，称为实例属性（实例变量）、实例方法。    
##### 声明为static的方法有以下几条限制：
- 它们仅能调用其他的static方法。
- 它们只能访问static数据。
- 它们不能以任何方式引用this或super。

## 继承:
是java中实现代码重用的手段之一，java中只支持单继承，即每个类只能有一个直接父类。继承表达式是is a 的关系；   
#### 子类可以从父类中继承到：
- 继承public和protected修饰的属性和方法，不管子类和父类是否在同一个包里；
- 继承默认权限修饰符修饰的属性和方法，但子类和父类必须在同一个包里；
- 无法继续父类的构造方法；
- 子类重写父类方法：
在子类中可以根据需求对从父类继承的方法进行重新编写，称为方法的重写。方法重写必须满足如下要求：    
- 重写方法和被重写方法必须具有相同的方法名；
- 重写方法和被重写方法必须具有相同的参数列表；
- 重写方法和返回值类型必须和被重写方法的返回值类型相同或者是其子类；
- 重写方法不能缩小被重写方法的访问权限；
## super关键字：
super代表对当前对象的直接父类对象的默认引用。在子类中可以通过super关键字来访问父类的成员；   
super必须是出现在子类中（子类的方法和构造方法中），而不是其他位置；  
可以访问父类的非private成员；  
### 继承关系中构造方法的执行：  
子类的构造方法中没有通过this显式调用自身的其他构造方法，没有用super显式调用父类的构造方法时，则系统会默认先调用父类的无参构造方法；    
#### 关键字this和super：
- 在构造方法中如果有this或super语句出现，只能是第一条语句。
- 在一个构造方法中不允许同时出现this和super语句；
- 在类方法中不允许出现this或super关键字；
- 在实例方法中this和super语句不要求是第一条语句，但可以共存；
#### 抽象类和抽象方法：
一个只定义一个被它的所有子类共享的通用形式的类，由每个子类自己去填写细节。这样的类决定了子类所必须实现的方法和本性；    
- 抽象类和抽象方法都通过abstract关键字来修饰；   
- 抽象类不能实例化，抽象类中可以没有、可以有一个或多个抽象方法，甚至可以全部方法都是抽象方法；    
- 抽象方法只有方法声明，没有方法实现，有抽象方法的类必须声明为抽象类，子类必须重写所有的抽象方法才能实例化，否则子类还是一个抽象类；
### final修饰符：
- 用final修饰的类，不能再被继承；
- 用final修饰的方法，不能被子类重写；
- 用final修饰的变量（包括成员变量和局部变量）将变成常量，只能赋值一次；
- final修饰引用型变量，变量不可以再指向另外的对象，但所指对象的内容却是可以改变的。
## 多态：
简单来说，多态是具有表现多种形态的能力的特征；   
同一个实现接口，使用不同的实例而执行不同的操作；   
#### 如何实现多态：
##### 子类到父类的转换（向上转型）
将一个父类的引用指向一个子类对象，称为向上转型，自动类型转换；   
此时通过父类引用变量调用的方法是子类覆盖或继承父类的方法，不是父类的方法；  
此时通过父类引用变量无法调用子类特有的方法；     
宠物类：   
 
```java
public abstract class Pet {
  String petname;

  public Pet(String petName) {
    this.petName = petName;
   }
  public abstract void eat();
 }
//狗狗类：
public class Dog extends Pet {
 
  public Dog(String petName) {
   super(petName);
  }

public void eat() {
  System.out.println("我喜欢啃骨头！");
  }

  public void playFlyDisc() {
  System.out.println("接。。。接飞盘");
  }
}

//测试类：
  public class PetTest {

  public static void main(String[] args) {
   Pet pet = new Dog("叮叮");
   pet.eat();  //会调用Dog类的eat()方法，而不是pet的eat()方法；
   pet.playFlyDisc(); //无法调用子类特有的方法，错误；
   }
}
```
##### 使用父类作为方法形参实现多态：
主人类： 
   
```java
public class Master {
 
   public void feed(Pet pet) {
         pet.eat();
   }
}

//测试类：

public class MasterTest {

public static void main(String[] args) {
  Master master = new Master();
  Pet pet = new Dog("叮叮");
  master.feed(pet)；
 
  }
}
```

##### 父类到子类的转型（向下转型）：

当向上转型后，将无法调用子类特有的方法。但是如果需要调用子类特有的方法。可通过把父类再转换为子类来实现；    
将一个指向子类对象的父类引用赋给一个子类的引用，称为向下转型，此时必须进行强制类型转换；  
测试类：   
将1中的测试类修改一下：  
  
```java
public class PetTest {

  public static void main(String[] args) {
/*向上转型实现多态*/
   Pet pet = new Dog("叮叮");
   pet.eat();  //会调用Dog类的eat()方法，而不是pet的eat()方法；
// pet.playFlyDisc(); //无法调用子类特有的方法，错误；
  /*向下转型实现多态*/
 Dog dog = (Dog)pet;
 dog.playFlyDisc();
  /*（如果还有一个猫类型，则：
     Cat cat = (Cat) pet;
     cat.eat();
    是错误的，因为不能将一个狗类型的对象，转换成一个猫类型的对象）*/
     
   }
}

```
将2中的主人类和测试类修改一下：   
主人类：   

```java
public class Master {
 
   public void feed(Pet pet) {
         pet.eat();
   }

   public void play(Pet pet) {
      Dog dog = (Dog) pet;
      dog.playFlyDisc();
   
}

//测试类：

public class MasterTest {

public static void main(String[] args) {
  Master master = new Master();
  Pet pet = new Dog("叮叮");
  master.feed(pet)；
  master.play(pet);
 
  }
}

```

`结论：类型转换时必须转换为父类指向的真实子类类型，不是任意强制类型转换；`


### instanceof运算符：
语法：  
 
```
对象 instanceof 类或接口
```
该运算符用来判断一个对象是否属于一个类或者实现了一个接口，结果为true或false；   
应用：   
主人类：
   
```java
public class Master {

   ...........

public void play(Pet pet) {

     if(pet instanceof Dog) {
           Dog dog = (Dog)pet;
           dog.playFlyDisc();
     }else if(pet instanceof Cat) {
           Cat cat = (Cat)pet;
           cat.playLineBall();
     }
}

//测试类：
public class MasterTest {

public static void main(String[] args) {
  Master master = new Master();
  Pet pet1 = new Dog("叮叮");
  Pet pet2 = new Cat("喵喵");
  master.feed(pet1)；
  master.feed(pet2);
  master.play(pet1);
  master.play(pet2);
 
  }
}
```

如果抽象类中所有的方法都是抽象方法，就可以用接口来表示；     
用接口代替这样的抽象类，是因为：    
##### 接口有比抽象类更好的特性：
- 可以被多继承；
- 设计和实现完全分离；
- 更自然的使用多态；
- 更容易搭建程序框架；
- 更容易更换实现；
.........

语法：   
```java
public interface MyInterFace {
  public void exercise();
  //其他方法
 }
```

`（所有的方法都是： public abstract.故省略；）`

### 接口特性：
接口不可以实例化，  常作为类型使用；     
实现类必须实现接口的所有方法， 抽象类除外；    
实现类可以实现多个接口； 即java中的多继承；   
接口中的变量都是静态常量；    

#### 用程序描述USB接口：
分析：   
- USB接口本身没有实现任何功能；
- USB接口规定了数据传输的要求；
- USB接口可以被多种USB设备实现；
##### 可以使用Java接口来实现：
```
编写USB接口    根据需求设计方法；
实现USB接口    实现所有方法；
使用USB接口    用多态的方式使用；
```

编码实现：   
```java      
//编写接口：    
public interface UsbInterface {
     /**
      *USB接口提供服务。
     */
     void service();
 }
 
//实现接口：

public class UDisk implements UsbInterface {
  public void service() {
   System.out.println("连接USB接口，开始传输数据。");
   }
}

//使用接口：

UsbInterface uDisc = new UDisk();
uDisk.service();
```

使用继承可以抽象出父类，然后由子类进行扩展，而接口则是更彻底的抽象、使得程序的复用性得到大大提高。因此很多软件在进行架构设计时都提倡使用“面向接口”编程；     


### 异常串讲：
异常的分类：   
- Throwable: Exception 和Error类的父类；
- Error: 仅靠程序本身无法恢复的严重错误；
- Exception:由JAVA应用程序抛出和处理的非严重错误；
- RuntimeException:运行时异常，不要求程序必须对它们做出处理；
- Checked Exception:程序必须处理该类异常；

常见的异常类型：     
|异常类名 |                        说明|
|---|--|
|Exception|异常层次结构的根类|
|ArithmeticException|算术错误情形，如以零作除数|
|ArrayIndexOutBoundsException|数组下标越界|
|NullPointException|尝试访问null对象成员|
|ClassNotFoundExcepton|不能加载所需的类|
|InputMismatchException|欲得到数据类型与实际输入类型不匹配|
|IllegalArgumentException|方法接收到非法参数|
|ClassCastException|对象强制类型转换出错|
|NumberFormatException|数字格式转换异常，如把“abc"转换成数字；|

异常类的核心方法：
|方法名|                              说明|
|----|---|
|void printStackTrace()  |  输出异常的堆栈信息|
|String getMessage() |  返回异常信息描述字符串，是printStackTrace()输出信息的一部分；|

#### Java的异常处理时通过5个关键字来实现的：
```
 try catch finally  throw  throws
```
##### 捕获异常：
- try : 执行可能产生异常的代码；
- catch ： 捕获异常并进行处理；
- finally ： 无论是否产生异常，代码总能执行；
##### 声明异常：
- throws： 声明方法可能要抛出的各种异常；
##### 抛出异常：
- throw： 手动抛出异常；

#### 使用try-catch捕获异常，分为三种情况：
第一种情况：   
```java
 public void method() {

  try {
   //代码段（此处不会产生异常）
  }catch(异常类型ex) {
    //对异常进行处理的代码段，此时，不做处理；
   }
    //代码段
  }
```
try中的代码段不会发生异常，此时不执行catch中的代码段，而直接执行try-catch块后的代码段；

第二种情况：
```java
public void methd() {
  try {
   //代码段1
   //产生异常的代码段2
   //代码段3
} catch (异常类型 ex) {
     //对异常进行处理的代码段4
    }
    //代码段5
}
```
异常是一种特殊的对象，类型为java.lang.Exceptoin 或其子类；   
在try语句块中，执行完代码段1，执行代码段2时，发生异常，产生异常对象，此时，不再执行代码段3，而是与catch语句块中的异常类型进行匹配，若匹配成功，则执行catch语句块中的代码段，对异常进行如理；之后，程序继续执行，执行try-catch块后的代码段；   

第三种情况：    
```java
public void methd() {
  try {
   //代码段1
   //产生异常的代码段2
   //代码段3
} catch (异常类型 ex) {
     //对异常进行处理的代码段4
    }
    //代码段5
}
```
在try语句块中，执行完代码段1，执行代码段2时，发生异常，产生异常对象，此时，不再执行代码段3，而是与catch语句块中的异常类型进行匹配，若匹配不成功，则程序中断执行，catch语句块中的代码段和try-catch块后的代码段都将不被执行；   

##### finally块的使用：
在try-catch块后加入finally块，可以确保无论是否发生异常，finally块中的代码总能被执行；

##### 多重catch块：
一段代码可能会引发多种类型的异常,这时就要使用多重catch块的方式来进行异常处理；
当引发异常时，会按顺序来查看每个catch语句，并执行第一个与异常类型匹配的catch语句；
执行其中一条catch语句后，其后的catch语句将被忽略；
```java
public void method() {
  try {
     //代码段
     //产生异常（异常类型2）
     //代码段
   } catch(异常类型1 ex) {
   //对异常进行处理的代码段  
  } catch（异常类型2 ex) {
   //对异常进行处理的代码段
  }  catch(异常类型3  ex) {
   //对异常进行处理的代码段
   }
  //代码段
 }
```
执行try语句块，产生异常对象，查看第一个catch语句，类型不匹配，查看第二个catch语句，类型匹配，执行其中的处理异常的代码段，第三个catch语句块被忽略，执行catch语句块后的代码段；

在安排catch语句的顺序的时候，首先应该捕获最特殊的异常，然后再逐渐一般化，即先子类后父类；

除了系统抛出异常外，有些问题需要程序员自行抛出异常；

在方法体中使用throw关键字抛出异常；在方法名之后用throws关键字声明抛出的异常类型；   
调用者要么用try-catch进行异常处理。要么用throws继续抛出异常；

Java语言中通过throws声明某个方法可能抛出的各种异常；    
可以同时声明多个异常，之间由逗号隔开；   

一个方法用throws关键字声明异常时，调用者需通过try-catch捕获并处理异常； 或，用throws关键字继续抛出；    
但，最好在main方法或之前处理，最好别在main方法中继续用throws关键字继续抛出给java虚拟机，导致程序运行错误；   




