# 异常
程序中的异常也是要在程序运行中才会偶尔发生。如果程序还没有运行，编译就报错，这种不叫异常，而叫编译错误，通常是语法上的错误。      
我们需要先修改程序再编译运行。   
程序中的这些异常情况，我们不能置之不理，否则一旦发生了异常，可能就导致程序运行失败，甚至破坏重要数据。程序中对异常提前想好处理方案就是异常处理；   
异常是程序中偶然发生的错误现象，而且是运行时发生的错误；它不是由程序的语法错误导致的，而是由一些偶然的或外在的原因导致的；    
而异常处理就是对这些异常提前想好的解决方案，当异常发生时，异常处理的代码就要开始执行；    

## 异常是有类型的；
java中的异常有很多很多种类型；    
异常在java中也被封装成各种类型，而且这些异常类型之间是有继承关系的；  

### 算术异常
```
java.lang.ArithmeticException
```
### 输入类型不匹配异常：
```
java.util.InputMismatchException
```
### 异常类继承层次：
异常的继承层次，最上面也是Object类型，   
Throwable是所有异常类的父类，它也继承自Object类，   
注意：Throwable是一个类，不是接口；    
#### Throwable有两个直接的子类  ：
Exception 和 Error    
##### Exception：
就是异常的意思；   如果出现的异常都是 
`***Exception，说明他们都是Exception的子类；`   
##### Error ：
就是错误的意思；Error这个分支的异常，是由于java虚拟机内部错误导致的；通常比较少见；如果真的出现了这种异常，我们程序员也无能为力；所以，对于Error这个分支的异常，通常在程序中我们不用去过多的关注；   
如果Error在程序中出现了，我们可以检查一下java虚拟机是否发生了什么问题；或者我们的配置环境有什么问题；   
我们在程序中主要关心的是Exception这个分支的异常；   
Exception极其子类是我们在程序中经常遇到的；    

在Exception的异常分支中，异常又被分为两个很重要的分支：      
- 运行时异常 -- RuntimeException
- 已检查异常 -- Checked Exception
```
RuntimeException 是一个具体的异常类型， RuntimeException下面还有很多的子类；      
RuntimeException及其子类都是可以不进行捕获和处理的；即，程序在运行时，如果抛出 RuntimeException，可以不对其进行处理；   
Checked Exception只是一个名词，并没有这个类型，它是很多种异常类型的总称，Checked Exception则必须在程序中捕获，处理；
```
异常结果图：
```java
                      Object
                        |
                   Throwable
             /                    \
            /                    Exception
           /                 /   / \
        Error     SQLException  /   \              
       /    \                ......  \        
AWTError  ThreadDeath            RuntimeException
                                / |     |    |
                              /   |     |    |
          ArithmeticException     |     |    |
                                  /     | ........
               NullPointerException     |
                                        |
                              NumberFormatException

```
#### 常见异常类型：
- ArithmeticException   算术异常；   
当有在数学计算上的错误时，这种异常就会发生；  
- ArrayIndexOutBoundsException  数组越界异常；   
如果操作超出了数组的长度范围，就会抛出这种异常；  
- NullPointerException  空指针异常；   
如果使用了一个空的对象，调用方法，属性，就会抛出空指针异常；即我们使用的引用没有指向任何一个对象；    
如果我们使用的数组没有初始化，即没有给它（引用变量）一个具体的有长度的数组，使用时，也会抛出异常；   
- ClassNotFoundException  类找不到的异常；    
我们试图使用的类类型是不存在的；我们没有引入相应的jar文件，没有引入响应的jar包，或者由于程序员的疏忽，    
把 包名或者类名写错了，就会引发这种异常；    
- NuberFormatException  数字格式化异常；
当把一个不是数字格式的字符串转化成数字时，就会引发这种异常   
- InputMismatchException  输入类型不匹配异常   
用户给出的类型和系统需要的类型是不一样的，就会引发这种异常；   



异常就是程序在运行过程中可能会发生的不正常的现象，异常有很多种，还有一个继承关系，最上面的是Throwable，最常用的是Exception和它 的子类；   
Error这个分支的异常我们在程序中不可以捕获和处理；   
RuntimeException是可以选择不进行捕获和处理；    

#### 使用try-catch处理异常：
在编写程序时，如果代码会抛出已检查异常，那么编译器就会要求你必须对异常进行捕获和处理；如果是`RuntimeException`异常，可以不进行捕获和处理；   
当我们需要对异常进行捕获和处理时可以使用两个关键字 `try` 和`catch` ;`try` 和 `catch `实际上是两个代码块；`try`块用来包裹会产生异常的代码；`catch`块是用来处理try块中发生的异常的；我们说异常是可能会发生的；  
  
- 如果`try`块中没有发生异常；那么执行完`try`块中的代码后，会直接执行`catch`块后的代码；`catch`块中的代码会被忽略；     
- 如果`try`块中发生了异常，并且异常的类型与`catch`块中的异常类型是匹配的，就可以进入`catch`块中；在`catch`块中可以编写处理异常的代码； 
```       
（try块->发生异常 -> 产生异常对象 ->异常类型匹配 ->进入catch块 ->catch块 ->程序继续执行 ->try/catch块后的代码）   
```
- 如果`try`块中发生了异常，但发生的异常类型与`catch`块中的异常类型不一致的话，就不会进入到`catch`块；程序就会终止运行；`catch`块之后的代码也不会运行了；
```
（try块->发生异常 -> 产生异常对象 ->异常类型不匹配 ->程序中断运行）；
```
说明：一旦发生了异常，`try`块中发生异常的地方之后的代码就不会执行了；要么进入`catch`块，要么终止程序运行；    
java提供了捕获处理异常的机制，但如何捕获处理还是程序员的事；   
程序没有发生异常时，我们是基本感觉不到`try/catch`块的存在的；   
程序发生异常时，`try/catch`块就起作用了；处理完异常后，程序还是可以继续向下执行的；   

我们将可能产生异常的代码放在`try`块中，如果发生异常，异常就会被java虚拟机捕获，并且被java虚拟机封装成异常对象；然后java虚拟机会将这个异常对象跟`catch`中的异常类型进行匹配，如果异常一致，就可以进入`catch`块；在`catch`块中可以编写异常处理的代码；    
代码放在`catch`块中，执行效率会有所降低；   
所以尽量别把过多的代码放在`catch`块中；  

有时，我们希望无论程序是否发生异常，有些事情一定要做；`finally`块用来放置这些必须执行的代码；   
##### finally块的作用：
无论`try`块中是否发生异常，也无论`catch`块中是否可以捕获异常，`finally`块都要至少执行一次；
如果`try`块中有`return`语句，`finally`块还是要执行的；如果有`finally`块，java虚拟机会先执行`finally`块中的代码，回头再执行`return`语句；在`catch`块中也有`return`语句，也是一样的；但如果`finally`块中有`return`语句，那么`finally`块会直接返回，而不会再去执行`try`块或`catch`块中的`return`语句了；

##### 使finally块不执行：
- 强制使程序中断:
停止方式：停电；关闭程序；ECLIPSE控制台停止按钮；   
- 通过代码的方式终止代码的运行：
在java中，终止程序的运行，可以使用System.exit(int);    
这条语句；参数是一个状态码；   
一个非零的状态码，表示不正常的退出；    
如果是正常的退出，可以使用  System.exit(0);   
如果使用 System.exit(-1); 或者 其他的数字；表示的是非正常状态的退出；   
在try块中终止程序的运行，可以使用 System.exit(0);    
在catch块中终止程序的运行,可以使用 System.exit(-1);    
但是，运行效果是一样的，都是终止程序运行；    
这个状态码会最终返回给java虚拟机；    
finally块可以单独和try块使用，即省略catch块；    
try - finally     

##### 多重catch块：
用来解决一个try块中可能引发多种异常的情况；   
使用方法：在原来的catch块后面，再加上若干个catch块；   
每个catch块处理一种类型的异常；   
多重catch块的执行：如果try块中发生了异常；java虚拟机会将异常类型依次与catch块中的类型进行匹配，如果匹配上了某个catch块，就会进入，然后执行该catch块中的代码；而后面的catch块就不会被执行；    
如果所有的catch块都没有匹配上，程序就会终止；    
任何catch块执行之后，都会讲直接执行try/catch块后的代码；    
多重catch异常类型的摆放要求：因为java虚拟机会从第一个catch异常类型依次向后匹配，所以，java虚拟机是不允许将父类的异常类型放在子类的前面的；如果这样，编译就不能通过；     
如果即想让程序可以根据不同的异常有不同的处理，又想让程序不至于因为发生的异常没有应对的catch而终止运行；应该使用多重catch，然后在最后一个catch中使用Exception类型；

在catch块，finally块是否会发生异常，如果发生异常，怎么办？    
在catch块，finally块中也是可能发生异常的，如果处理异常的代码涉及到不确定的因素，   
比如说，一个文件对象已经创建，在写入时发生异常，在catch块中可能要撤销写入的操作，在finally块中可能要关闭文件对象，那么，关闭撤销文件对象，这个时候可能就有可能引发多种异常；对象不存在，就可能发生空指针异常，文件操作失败，可能是IO异常；    
其实，在catch块，和finally块中处理异常的方式，还是使用try/catch处理异常；  
try/catch语句也是可以嵌套使用的；     
 
##### 用throws声明抛出异常：
存在异常，自己不处理，让调用者处理；    
让调用者明白存在异常；      

throws的语法是在方法声明之后，大括号开始之前；    
语法：  
```
访问修饰符 返回值类型 方法名（） throws 异常类型1，异常类型2，.....{ }
```
它表示该方法可能会抛出某些类型的异常；可以抛出多个异常类型，类型之间用逗号隔开，没有顺序的要求；    
当某个方法调用一个声明会抛出某些异常的方法的时候，在调用者中要对声明抛出异常类型的方法的异常进行异常处理；处理的方式是使用 try/catch进行处理；或者在调用者再次使用throws抛出异常；    
如果一直往外抛，抛到了程序的入口，main方法，还是声明抛出异常，就会抛给java虚拟机；java虚拟机会将异常的信息输出到控制台上；    
使用throws抛出异常时，应该在某个调用者中对这个异常进行处理；如果一直都是使用throws向外抛出的话，最终抛到程序的入口，main方法继续往外抛，程序就会终止运行；    

有时，程序本身虽然没有发生任何的异常，但出于某些原因，我们可能希望自己主动地引发某些类型的异常；这时可以使用throw关键字；    
##### 由程序自行抛出异常：
语法：  
```java
throw new Exception()
throw new Exceptoin()(String message)
```
- throw ：  表示程序会主动地抛出某个类型的异常；抛出的位置是在方法体内；抛出异常时，要抛出一个异常的对象；这个对象需要程序员在编码时创建；创建异常对象时，可以使用一个字符串的参数，这个参数是异常的信息；它可以由`e.getMessage()`得到，返回的是一个字符串；也可以通过`e.printStackTrace()`输出；      
注意：`e.getMessage()`只是得到异常信息这个字符串；要输出的话，还要借助于`System.out.print();`方法来进行输出；而`e.printStackTrace()`可以直接输出异常的信息；   
### 可以抛出的异常类型：
只能是`Exception`及其子类；也就是， 已检查异常；和` Runtime`异常；     
除非抛出的异常是`RuntimeException`，否则一定要有`try/catch`处理；或者是在方法声明中声明抛出该异常，即用`throws`抛出该异常；所以，使用`throw时`，通常是结合
`try/catch` 或者是 `throws` 一起来使用的；
除非`throw`的异常是`RuntimeException`类型，或者是它的子类，我们可以直接抛出，而不进行任何的处理；   


##### throws（声明抛出异常） 和 throw（主动抛出异常）的区别：
- 作用不同：  
throw ：用于程序员自行产生并抛出异常；  
throws ： 用于声明该方法内抛出了异常；   
- 使用的位置不同：  
throw：位于方法体内部，可以作为单独语句使用；   
throws ： 必须跟在方法参数列表的后面，不能单独使用；   
- 内容不同：  
throw ： 抛出一个异常对象，且只能是一个；   
throws ： 后面跟异常类，且可以跟多个异常类；  
  
小窍门： 如果后面跟S，即throws，说明它后面可以跟多个类型；如果后面没有S，即throw，说明它后面只能跟一个对象；    

当程序中的某些异常，系统不能主动抛出的时候，就需要由程序员使用throw关键字主动地抛出这个异常；抛出的这个异常，要么放在try语句块中，由try/catch语句，进行处理，要么在这个方法的声明处使用throws关键字抛出这个异常，然后在调用者里再使用try/catch语句处理这个异常；
```java
public class Person {
        //姓名
 String name =" ";
       //年龄
int age = 0;
       //性别
String sex;
public String getSex() {
        return sex;
    }
public void setSex(String sex) throws Exception {
        if("男".equals(sex) || "女".equals(sex))
            this.sex = sex;
        else 
            throw new Exception("性别必须为男或者女");
    }
       
       
}

public void print() {
System.out.println(this.name ＋＂（＂＋this.sex+","+this.age+"岁")");
   }
}


class Test  {
public static void main(String[] args) {
 Person person = new Person();
try {
   perosn.setSex("Male");
   person.print();
 } catch (Exception e) {
   e.printStackTrace();
   }
}
}
```
throw抛出的异常，一般是，    
自定义异常；    
系统异常不能满足需要的时候，就可以使用自定义异常；    
自定义异常主要用在框架当中，   
自定义异常 语法：    
```
继承Throwable
继承Exception
继承RuntimeException
```
和其他的子类；   
一般继承`Exception`和`RuntimeException`，继承`Throwable`和继承`Exception`的效果是一样的；    
如果不要求调用者一定要处理抛出的异常，就继承`RuntimeException`；其余的就可以直接继承`Exception`；   

继承了`Exception`，或者是`RuntimeException`，或者是其他的`Exception`类型之后，就完成了一个自定义异常类型的定义了，但是，要自定义异常和普通异常有相同的创建方式，
需要有几个构造方法，并且继承父类的实现；    
`Throwable`和`Exception`中都创建了这四个构造方法，自定义异常也应该有这四个构造方法；这样，在创建自定义异常对象的时候，所使用的方法就和其他异常是一样的；   
```java
//构造方法1
public MyException() {
super();
 }
//构造方法2
public MyException(String message) {
super(message);
 }
//构造方法3
public MyException(String message,Throwable cause) {
super(message,cause);
 }
//(表示根据指定的原因，构建新的异常对象，但是更换了异常信息；）


//构造方法4
public MyException() {
super(cause);
 }

//（表示指定的原因，构建异常对象，使用已有的异常信息，也就是cause中指定的异常信息，通过getCause方法可以获取，printStackTrace也可以将这些信息输出出来；）
```
##### 自定义异常：
```java
public class GenderException extends Exception {
        public GenderException (String msg){
            super(msg);
        }
}

//人类：
public class Person {
        //姓名
 String name =" ";
       //年龄
int age = 0;
       //性别
String sex;
public String getSex() {
        return sex;
    }
public void setSex(String sex) throws            GenderException {
        if("男".equals(sex) || "女".equals(sex))
            this.sex = sex;
        else 
            throw new GenderException("性别必须为男或者女");
    }
       
       
}

public void print() {
System.out.println(this.name ＋＂（＂＋this.sex+","+this.age+"岁")");
   }
}

//测试类：
public class Test  {
public static void main(String[] args) {
 Person person = new Person();
try {
   perosn.setSex("Male");
   person.print();
 } catch (GenderException e) {
   e.printStackTrace();
   }
}
}
```
##### 编写并使用自定义异常：
```java
public class MyException extends Exception {
  public MyException {
    super();
  }

 public MyException(String message) {
  super(message);
 }
public static void main(String[] args) throws MyException  {
 throw new MyException("我的自定义异常对象");
    }
}
```
自定义异常类，在程序运行时，无法通过系统来抛出，所以，如果要抛出自定义异常，程序员需在方法体中通过throw关键字来抛出，在catch语句块中捕获；而系统的异常类型，无需throw关键字；

#### 异常链：
减少代码关联，不丢失异常信息；   
语法：   
```java
try {
   //会抛出异常的代码
}catch(***Exception e) {
 throw new ***Exception(e);
 }
```
异常链：     
可以记录一个异常是由哪个异常导致的；    

异常链：       
异常链就是在try/catch处理异常的时候，在catch里面不做细致的处理，而仅仅是将异常再次的抛出来；然后通过方法声明throws再声明该方法继续抛出某种异常，这就是异常链；就是A方法，调用B方法，B方法抛出异常，A方法使用try/catch处理了这个异常，同时在catch当中将异常再次抛出，这样就形成了异常链，     
在catch当中将异常再次抛出，需要有一个选择，就是继续抛出原有的异常，还是抛出一个新的异常？      
继续抛出原有的异常，A方法和B方法进行了关联，它们通过抛出同一种类型的异常，关联了起来，这样不便于代码的修改和维护；      
抛出一种新的异常：解决了A方法和B方法相互关联的问题，但带来了新的问题，原有的异常信息丢失了；       
异常链如何解决这个问题？      
使用异常链在抛出新的异常的同时，保留原有的异常信息；      
如何做到呢？        
自定义异常类型中的构造方法3和构造方法4都有一个参数，     
类型是throwable，参数名是cause，这就是对异常链使用的；就是我们抛出一个新的异常类型的时候，在构建这个新的异常对象的时候，可以通过这两个构造方法传入一个throwable类型的对象，
这个throwable类型的对象代表的是引起现在新的异常类型的原有的异常类型，这样，就保留了原有的异常信息；     
如果没有构造方法3和构造方法4，也可以通过throwable里的另外一个方法来添加异常链的信息，就是InitCause方法；通过InitCause方法，也可以指定引起新的异常的异常原因；
注意：如果Cause指向自己，说明该属性没有初始化，或者，该异常已经是异常的源头了；     

#### 异常链：
```java
public class MyException extends Exception {
public MyException() {
 super();
}
public MyException(String message) {
super(message);
}
publc MyException(Throwable cause){
super(cause);
}
public MyException(String message,Throwable cause){
           super(message,cause);
       }

}

//测试类：
ublic class Test {
    public static void main(String[] args) throws MyException {
        
try {
throw new Exception("Exception类型的异常");
        } catch (Exception e) {
            
throw new MyException("MyException类型的异常",e);
        }
    }

}
```
#### 异常堆栈信息：
```
（使用e.printStackTrace();输出异常堆栈信息）
（使用异常堆栈信息，分析异常的原因，发生异常的位置，等等）
请输入被除数
4
请输入除数
0
java.lang.ArithmeticException: / by zero
    at Test.divide(Test.java:34)
    at Test.main(Test.java:18)
```
异常堆栈信息：
首先是异常的类型；（java.lang.ArithmeticException）  
之后是异常的描述：（/ by zero）不能被零整除；     
再往下，就是异常的堆栈信息了；       
异常堆栈信息指出发生异常的地方； 在什么方法，在哪个类当中，在第几行；   
只产生了一个算术异常，为什么会有多处指示有异常？   
因为通过使用throws关键字，将异常抛出了来；     
java虚拟机会将异常从最开始产生的地方，一层一层的传递；异常所有的传递路径通过堆栈的方式，记录下来；     
### 堆栈的特点：后进先出，先进后出；
记录异常时，是从调用者开始的，所以，打印异常时，就是从最原始的发生异常的地点先输出来；     
故，从异常发生的最原始的地方找起，若发生异常的原始地点在别人已经写好的代码中，则继续往下找，直到自己写的代码中，找到异常代码发生的源头；    
异常链多了个 Caused by ;       



