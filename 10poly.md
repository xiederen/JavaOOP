# 多态
## 多态：
`可替换性 可扩充性 接口性 灵活性 和 简化性`  
多态：事物不同时期的不同状态；   
多态：同一个引用类型，使用不同的实例而执行不同的操作；  
多态是源于生活的；   
抽象类：是指高度的抽象提取共性部分，只声明方法的存在，而不具体实现它的类，是一个概念性的描述；    
抽象类的定义，就是为了让子类来继承的；    
抽象类是不能用new关键字实例化的；     
定义抽象类的语法比较简单，就是在class关键字之前加一个abstract关键字；
抽象方法只是声明方法的存在，并不给出具体的实现；    
具体的实现由继承它的子类通过重写来实现；   
抽象方法的语法也简单，就是在方法返回值前加关键字abstract，且没有{}括号及方法体，由分号结束；      
当然，抽象类中也可以没有抽象方法；   
#### 使用抽象类的注意事项：
- 抽象类不能实例化；
- 子类如果不是抽象类，则必须重写抽象类中的全部抽象方法；
- abstract修饰符不能喝final修饰符一起使用；
- abstract修饰的抽象方法没有方法体；
- private关键字不能修饰抽象方法；

#### 子类中继承自抽象类的方法是方法重写；
```
父类类型  父类变量名  = new 子类类型（）；
Pet pet = new Dog();
```
这是一种对象的类型转换，有点类似之前学过的基本数据的转换；   
前面定义了一个父类型的对象pet，但是 new Dog（），实例化的却是子类类型， 这里就叫做向上转型；   
向上转型：类型转换是自动进行的，并且运行的时候，父类型引用的类型变量，执行的是子类的重写后的方法，而不是父类自己的方法；   
对象运行时，会出现两种类型：编译时类型和运行时类型；    
比如代码` Pet pet = new Dog();`   
运行时会生成一个pet变量，该变量的编译时类型，就是宠物类Pet；运行时类型就是Dog类型；     
也就是说，编译时类型由声明该变量的类型决定；   
运行时类型由实际赋给该变量的对象决定；   
##### 向上转型：
经过了向上转型，Pet对象的类型是父类的类型，所以只能访问父类具有的方法，不能调用子类当中父类不存在的方法；    
##### 向下转型：
向下转型就是父类类型转换为子类类型；   
向下转型不能自动完成转型，所以需要进行强制类型转换；   
也就是说向下转换需要强制类型转换；   
```
子类类型  子类变量名 = （子类类型）  父类变量名；
Dog d = (Dog)pet;
```
当我们把父类强制类型转换为子类后，就可以访问子类特有的方法了；   
向下转型是不是只要有继承关系的类型，就可以父类转换为子类？   
向下转型在抽象类（父类）中实现，转换为某个子类的类型后，调用该子类的方法；   
**注意**：在抽象类中向下转型的子类类型应和主方法main（）中向上转型时的子类类型应一致；       
向下转型的时候，必须是父类指向的真实的子类类型；    
在转型之前，可以先使用instanceof运算符去判断一下；   
比如：在把父类强制转换成子类时，可能出现类型转换异常，ClassCastException的情况；    
解决办法很简单，就是在强制类型转换之前（在抽象类中），通过instanceof运算符检查一下对象的真实类型，然再进行相应转换后，这样就避免了异常情况的发生，有效的提高代码的健壮性；     
##### instanceof运算符语法：
```
<引用变量> instanceof <类/接口名称>
```
在执行时，判断对象是不是后面的类，或者子类、实现类的实例，返回值是boolean类型；     
如果是，就返回true，否则返回的是false；    
子类要继承抽象类，或者说继承父类，（超类），在生成类界面中，在superclass框的右侧，单击browing,在顶框中输入要查找的类，找到后，确定，就继承成功了；     

### 多态的使用 有两方面：
一，使用父类作为方法的形参；   
举例：   
某超市要实现打印商品价格的功能：     
```java
//定义商品类Goods类，
public class Goods {
public void price(){
System.out.println("打印商品的价格");
   }
}
//食物类 Foods类：
public class Foods extends Goods {
  public void price() {
     System.out.println("打印食品类的价格");
    }
}
//电视类 TVs类：
public class TVs extends Goods {
   public void price() {
   System.out.println("打印电视类商品的价格");
   }
}
//测试类 Test类：
public class Test {

   public static void main(String[] args) {
    Goods g = new Goods();
    Foods f = new Foods();
    TVs t = new TVs();
    showPrice(g);
    showPrice(f);
    showPrice(t);
  }
   static void showPrice(Goods g) {
     g.price();
    }
}
```
二，使用父类作为方法的返回值类型；    
比如有个商品工厂 ，它会根据客户的不同需求，来创建不同类型的商品，然后再将此商品的价格打印出来；   
```java
//商品工厂类 Factory类：
public class Factory {
 
   Goods getGoods(String str) {
     if(str.equals("food")) {
            return new Foods();
     }
      else {
             return new TVs();
           }
      }
}

//测试类 Test类：
public class Test {

public static void main(String[] args) {
  Factory f = new Factory();
  Goods p1 = f.getGoods("food");
  p1.price();
  Goods p2 = f.getGoods("tvs");
  ps.price();
   }
}

```
##### 向上转型语法：
```
<父类型> <引用变量名> = new <子类型> ();
```
##### 向下转型语法：
```
<子类型> <引用变量名> = (<子类型>) <父类型的引用变量>;
```
### 多态的实现：
先定义一个父类（A类），在父类中有若干个方法，0个，1个，或，多个；（父类也可以是抽象类，即父类中的方法只给出了方法名，而没有方法体；)  
定义多个子类，在子类中重写父类的方法；       
再定义一个类（B类），在该类中接收A类；   
在测试类中，在主函数中，创建B类对象，A类对象（向上转型）；调用B的方法实现；   

```java
//宠物类：
public abstract class Pet {
private String name;
private String sex;
private int health;
abstract void toHospital();//去医院看病是宠物特有的                               方法；
}

//狗狗类：
public class Dog extends Pet {
  
   void toHospital() {
           System.out.println("打针、吃药");
     }
}


//小鸟类：
public class Brid  extends Pet {
  
   void toHospital() {
           System.out.println("吃药、疗养");
     }
}
//医生类：

public class Doctor {
  public void cure(Pet pet) {//给宠物看病是医生特有                                 的方法；
       if(pet.getHealth() < 50) {
                pet.toHospital();
                pet.setHealth(60);
          }
     }
}
测试类：
public class Test {
  public static void main(String[] args) {
   Doctor doc = new Doctor();
   Pet pet1 = new Dog();
   doc.cure(pet1);
   Pet pet2 = new Bird();
   doc.cure(pet2);
```
`（学会结合现实生活，分析对象，类，以及他们特有的属性，方法）；`    
简单的说:   
多态的实现，就是通过在父类中定义一个方法；在子类中重写这个方法；通过向上转型，令父类变量可以指向多个子类；通过父类变量来调用父类，子类都有的方法，来实现对不同子类的方法的调用；      
父类可以是抽象的，父类中的方法也须是抽象的；   