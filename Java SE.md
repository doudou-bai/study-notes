# Java基础语法

​	**Java精华 封装 继承 多态**

<img src="C:\Users\Mi\Desktop\新建文件夹\Java\Img\路线\Java学习路线.png" style="zoom:40%;" />

## Java的基础语法格式

[修饰符] class 类名 {

​	程序代码

}

## 输出语句

System.out.println ("代码");

## 注释

- 单行注释	//
- 多行注释   /**/
- 文档注释   
  - /*
  - *
  - */

## Java中标识符

标识符可以由任意顺序的大写字母，数字，下划线（_）$组成，不能以数字开头

## Java中的常量和变量

**注意变量必须先声明在赋值**

变量的定义

变量类型  变量名  [=初始值];

```
示例：int  a  =  1；
```

### 变量数据类型

- 数据类型

  - 基本数据类型

    - 数值型
      - 整数类型(byte,short,long,int)
      - 浮点类型(float,double<默认>)
    - 字符型(char)
    - 布尔型(boolean)

  - 引用数据类型

    - 类(class)

    - 接口(interface)

    - 数组

    - 枚举(enum)

    - 注解(Annotation)


###  变量的类型转换

1. 自动类型转换

   ### 下图由低到高

   ```java
   低  ------------------------------------>  高
   
   byte,short,char—> int —> long—> float —> double 
   ```

2.强制类型转换

目标类型  变量名  =  (目标类型)  值;

示例: byte  b  =  (byte)  num;

### 变量的作用域

1. 局部变量
2. 全局变量

### Java中的常量

1. 整型常量

2. 浮点数常量

   2e3f  3.6d  0f  3.84d  5.022e+23f

3. 字符常量

   'a'  '1'  '&'  '\r'

4. 字符串常量

   "HelloWorld"  "123"  "Welcome  \n  xxx"  ""

5. 布尔常量

   ​	true   false

6. null常量

   final 常量类型  常量名  [=初始值]； 

### Java中的运算符

1. ##### 算数运算符

   - 正号  +

   - 负号  -
   - 加  +
   - 减  -
   - 除  /
   - 乘  *
   - 除(即算数中整除的结果  /
   - 取模(即算数中求余数)  %
   - 自增(前)  ++
   - 自减(后)  ++
   - 自减(前)  ——
   - 自减(后)  ——

2. ##### 赋值运算符

   - 赋值  =
   - 加等于  +=
   - 减等于  -=
   - 乘等于  *=
   - 除等于  /=
   - 模等于  %=

3. ##### 比较运算符

   - 相等于  ==
   - 不等于  ！=
   - 小于  <
   - 大于  >
   - 小于等于  <=
   - 大于等于  >=

4. ##### 逻辑运算符

   - 与  &
   - 或  |
   - 异或  ^
   - 非  ！
   - 短路与  &&
   - 短路或  ||

5. ##### 位运算符

   - 按位与  &
   - 按位或  |
   - 取反  ~
   - 按位异或   ^
   - 左移  <<
   - 右移  >>
   - 无符号右移  >>>

6. ##### 条件运算符

   - ###### 	三元表达式

   - (boolean_expr) ? true_statement : false_statement;

7. ##### 运算符的优先级

   - ###### 从高到低

   - .  []  ()  

   - ++  --  ~  !

   - (*)  /  %

   - (+)  -

   - <<  >>  >>>

   - <  >  <=  >=

   - ==  !=  

   - &

   - ^

   - |

   - &&

   - ||

   - ?:

   - =  *=  /=  %=  +=  -=  <<=  >>=  >>>=  &*=  ^=  |=

8. ##### 选择结构语句

   - ###### if  条件语句

   - if  语句

   - 示例:  if(判断语句){

       执行语句;

     }

   - if...else语句

   - 示例:if(判断条件){

     执行语句1;

     }else if(判断条件){

     执行语句;

     }

   - if..else  if...else  else

   - 示例:if(判断条件){

     执行语句;

     }else  if(判断条件){

     执行语句;

     }......else{

     语句;

     }

9. ##### switch条件语句

   - ​	switch(控制表达式){

     case  目标值1;

     执行语句1;

     break;

     case  目标值2;

     执行语句2;

     break;

     case  目标值3;

     执行语句3;

     break;

     default：

     ​	执行语句n+1

     break;

     }

10. ##### 循环结构语句

    - while循环语句

    - 示例:

      - while(循环条件){

        执行语句

        .

        .

        .

        }

11. ##### do.......while循环语句

    - do.....while

    - 示例

      - do{

        执行语句

        .

        .

        .

        }while  语句(循环条件)；
    
12. ##### for  循环语句

    - for(初始化表达式；循环条件；操作表达式){

      执行语句

      .

      .

      .

      }

13. ##### 跳转语句

    - break  语句
      - 条件满足，跳出循环
    - contiune  语句
      - 跳过本次循环，执行下次循环

### 数组

1. ##### 数组的定义

   - 数组类型  []  数组名  =  new  数组类型  {数组长度};
   - 数组类型  []  数组名  =  new  数组类型  []  {数组元素0，数组元素1.......};
   - 数组类型  []  数组名  =  {数组元素0，数组元素1.....};

2. ##### 数组的类型

   - 数据类型															默认初始化
   - byte short int lont                                                     0
   - float double                                                              0.0
   - char                                                                    一个空字符，即‘\u0000’
   - boolean                                                                     falae
   - 引用数据类型                                                   null  表示变量不引用任何东西 

3. ##### 多维数组

   - 示例  int []  []  arr = new int [3]  [4];
   
     ------
   

# 设计模式

一共有23种设计模式

# 面向对象(上)

面向对象的三大特点: 封装  继承  多态

### 类的定义

1.导包

​	import 包名称.类名称；

​	对于和当前类属于一个包的情况，可以省略语句不写；

2.创建

​	类名称 对象名 = new 类名称（）；

3.使用

​	使用成员变量：

​		对象名.对象名；

​	使用成员方法：

​		对象名.对象名（）；

示例:

[修饰符] class 类名 (extends 父类名)  [implements] {

//类体，包括类的成员变量和方法

}数组类型  []  数组名  =  new  数组类型  {数组长度};

### 声明(定义)成员变量

示例:

[修饰符]  数据类型  变量名  [=值]；

### 声明(定义)成员方法

示例:

[修饰符]  [返回值类型]  方法名  ([参数类型  参数名1，参数类型  参数名2....]){

//方法体

.

.

.
return  返回值；    //方法的返回值为void时，return及其返回值可以省略

}

- 修饰符  ：public  private  protected  
- 静态修饰符 ：static  final
- 返回值类型：void  也可以用类名表示
- 参数类型： 用于限定调用方法时传入的数据类型
- 参数名：是一个变量，用于接收调用方法是传入的数据
- return：返回
- 返回值：被return 语句返回的值，该值会返回给调用者

### 对象的创建与使用

- 示例

  - 类名  对象名称  =  new  类名();

    内存图如下

    ![](D:\md\img\对象创建内存图.png)

  ### 成员变量的初始值

  - 成员变量类型						初始值							成员变量类型						初始值
  - byte                                             0                                     double                                 0.0
  - short                                           0                                        char                       空字符，‘\u0000’
  - int                                                0                                     boolean                             false
  - long                                             0                                 引用数据类型                          null
  - float                                           0.0  

  ### 访问控制符 

  ​	如下图       

  ![](D:\md\img\访问控制符.png)

  ### 访问控制级别

  如下图

  ![](D:\md\img\访问控制级别.png)                                                         


## 类的封装

使用get set 方法封装

实现封装格式：

```java
//定义一个私有的name

private String name;

//定义一个私有的age

private int age;

//使用get set方法

public String getName() {
    return name;
}

public void setName(String name) {
    this.name = name;
}

public int getAge() {    
    return age;
}

public void setAge(int age) {
    this.age = age;
}
```

## 方法的重载和递归

方法的重载格式

```java
//实现两个整数相加

public static int add01(int a, int b) {
    
    return a + b;
    
}

//实现三个整数相加

public static int add02( int a, int b, int c) {
    
    return a + b + c;
    
}

//实现两个小数相加

public static double add03(double x, double y) {
    
    return x + y;
    
}

//创建main方法开始调用
public static void main(String[] args) {
    
    int sun1 = add01(2,3);
    int sun2 = add02(1,2,3);
    int sun3 = add03(4.6,2.3);
}
```

## 方法的递归

格式：

```java
//实现递归求1-n的和

public static int getsun(int n) {
    
    if (n == 1) {
        
        //条件满足，递归结束
        
        return 1;
    }
    int temp = getsun(n - 1);
    
    return temp + n;

}

public static void main(String[] args) {
    
    int sun = getsun(365);
    
    System.out.println(sun);
}
```

## 构造方法

### 构造方法的定义

[修饰符]  方法名  ([方法列表])  {

//方法体

}

##### 无参构造方法

```java
public class Person {
    
    public Person(){
        
        System.out.println("无参构造方法");
        
    }
    
}

```

##### 有参构造方法

```java
public class Person {
    
    int age;
    
    public Person(int a) {
        
        age = a;
    
    }
    
    //定义方法
    
    public void speak() {
        
        System.out.println("年龄是" + age);
    
    }
    
    //实例化对象
    
    public class Person02 {
        
        public static void main(String[] args) {
            
            Person p = new Person(18);
            
            p.speak();
        }   
    }
}
```

##### 构造方法的重归

```java
public class Person {

//声明String类名的变量name

String name;

//声明int类型的age

int age;

//声明有参构造

public Person(int a) {

age = a;

}

public Person(String n, int a) {

name = n;

age = a;

}

//定义speak方法 

public void speak() {

System.out.println("我今年" + age + "岁了");

}

//定义say方法

public void say() {

System.out.println("我叫" + name);

}

//创建示例化对象

public class Person02 {

public static void main(String[] args) {

Person p1 = new Person(10);

Person p2 = new Person("小明", 30); 

p1.speak(); 

p2.say();

}
 
}

}

```

##### 两种构造方法

在Java代码中如果不写构造方法，系统自动送一个，每个类至少有一个构造方法

###### 第一种写法

class Person {

}

###### 第二种写法

class Person{

​	public Person  ()  {

​    }

}

### this关键字

调用自身的方法

格式：

```java
public class Person {
    
    int age;
    
    public Person(int age) {
        
    this.age = age;
        
    }
    
}
```

### static关键字

在Java 中，定义一个static关键字，他用于修饰类的成员，如成员变量，成员方法以及代码块等，被static修饰的成员具备一些特殊性。 共享

### 静态变量

静态变量内存分配图

![](D:\md\img\对象创建内存图.png)

静态变量可以用一下语法实现

类名.变量名

### 静态方法

静态方法可以用一下语法实现

类名.方法

实例化对象名.方法

### 静态代码块

语法：

ststic {

....

}

### 权限修饰符

> **public >protected>(defaut)>private**		

------

|              | public | protected | (defaut) | private |
| ------------ | ------ | --------- | -------- | ------- |
| 同一个类     | YES    | YES       | YES      | YES     |
| 同一个包     | YES    | YES       | YES      | NO      |
| 不同包子类   | YES    | YES       | NO       | NO      |
| 不同包非子类 | YES    | NO        | NO       | NO      |



# 面向对象(下)

## 类的继承

继承格式：

[修饰符] class  子类名 extends 父类名{

//程序核心代码

}

注意：以下的不能出现是错误写法

calss A

class B

class C extends A,B//C类不能同时继承A类和B类

#### 访问方式

直接访问

new 子类对象访问 = 左边是谁就优先用谁

间接访问

用方法访问

局部变量 直接写

本类的成员变量 this.成员变量名

父类的成员变量 super.成员变量名

#### 重写父类方法

```java
//定义一个父类

public class Demo01 {
    
   public void shout() {
        
        System.out.println("我是Demo01的shout方法");
    
    }
}
    
//定义继承子类
    
public class Demo02 extends Demo01 {
        
     public void shout() {
            
         System.out.println("我是Demo02的shout方法");
        
        }
    
    }


//定义测试类

public class Demo03 {
    
    public static void main(String[] args) {
        
        Demo01 d2 = new Demo01.Demo02();
        
        d2.shout();
        
    }
```

#### super关键字

super.成员变量

super.成员方法([参数1，参数2.....])

```java
//定义一个Animal类

public class Animal {
    
    String name = "动物";
    
    //定义动物的叫声方法
    
    void shout() {
        
        System.out.println("动物发出的叫声");
    
    }

}

 //定义一个狗继承animal类

public class Dog{
        
   String name = "犬类";

     //重写方法
        
   void  shout(){
            
     //访问父类的成员方法
            
    super.shout();
            
        }
        
    }

    //定义测试类

    class  Demo01{
        
        public static void main(String[] args) {
            
            Dog dog = new Dog();
            
            dog.shout();
            
        }
        
    }

```

### Object类

|          方法声明          |                           功能描述                           |
| :------------------------: | :----------------------------------------------------------: |
| boolean equals(Object obj) |                   判断某个对象与此是否相等                   |
| final Class<?> getClass()  |                    返回此Object的运行时类                    |
|       int hashCode()       |                       返回对象的希玛值                       |
|     String toString()      |                    返回该对象的字符串表示                    |
|      void finalize()       | 垃圾回收器调用此方法来清理没有被任何引用变量所引用对象的资源 |

 toString方法

```java
//定义一个Animal类

public class Animal {
    
      String name = "动物";
    
    //定义动物的叫声方法
    
    void shout() {
        
        System.out.println("动物发出的叫声");
    
    }

}
//定义测试类
public class Demo02 {
    
    public static void main(String[] args) {、
        
        Animal animal = new Animal();
                                            
        System.out.println(animal.toString());
                                            
    }
    
}

结果：Animal@282ba1e
```

### final关键字

1. final修饰的类不能继承
2. final修饰的方法不能被子类重写
3. final修饰的变量(成员变量和局部变量)时常量，只能赋值一次

#### final关键字修饰类

```java
//使用final关键字修饰Anim类

final class Animal{

}

//Dog类继承Aminal类

class Dog extends Animal {
    
    //出现报错   不能继承

}
```

#### final关键字修饰方法

对于类，方法来说 abstract关键字和final关键字不能同时使用 矛盾

```java
//定义Animal类

class Animal{
    
    //使用final关键字修饰shout()方法
    
    public  final  void shout(){
    
    }
    
}
//定义Dog类继承Animal类

class Dog extends Animal{
    
    //重写Animal类的shout()方法
    
    //不能被覆盖重写
    
    public void shout(){
    
    }

}

//定义测试类public class Example{

public static void main(String[] args) {
    
    Dog dog = new Dog();//创建Dog类的示例对象

    }
}
```

#### final关键字修饰变量

没有final 有默认值 有final就没有默认值

```java
public class Example {
    
    public static void main(String[] args) {
        
        final int num = 2;//第一次可以赋值
        
        num = 4;//不能被再次赋值，再次赋值会报错
    
    }
    
}
```

### 抽象类和接口

##### 抽象类

//定义抽象类

[修饰符] abstract class 类名 {

//定义抽象方法

[修饰符]  abstract  方法返回值类型 方法名 ([参数列表]);

//其他方法或属性

}

##### 接口

java 7

1.常量

2.抽象方法

java 8

3.默认方法

4.静态方法

java 9

5.私有方法

**[修饰符] interface 接口名 [extends 父接口1，父接口2，....]{**

**[public] [static] [fianl] 常量类型 常量名 = 常量值;**

**[public ] [abstract] 方法返回值类型  方法名 ([参数列表]);**

**[public] default 方法返回值类型 方法名 ([参数列表]){**

//默认的方法的方法体

}

[public] static 方法返回值类型 方法名  ([参数列表]){

//类方法的方法体

}

}

##### 接口-抽象方法

**public abstract void 名称 (参数);**

##### 接口-实现类

**public class 实现类名称 implements 接口名称 {**

**//代码块**

覆盖重写所有方法

**}**

//把必须要用实现类

##### 接口—默认方法

从java8开始可以定义默认方法

```java
public interface  demo01 {
    
public default 方法名称(参数列表)
{
 	//方法体   
    可以加大括号
	}


		}
//ps:接口当中的默认方法可以解决接口升级的问题
```

##### 实现多接口

[修饰符] class类名 [extends 父类名] [impleements 接口 1，接口 2，....]{

......

}

##### 接口-定义静态方法

```java
public class dingyi { 
    
    public static 返回值类型 方法名称（参数列表）    {  
    
        //方法体   
    }
    
}
//不能定义实现类调用 接口名称.静态方法名
```

##### 接口-私有方法

**private void  名称(参数)**

**{**

​	**//方法体**

**}**

##### 接口-私有方法调用

接口名称.方法名

##### 接口-常量定义

必须使用public private final

定义格式

public static final 数据类型 常量名称 = 数据值；

一旦赋值不能修改

数值不能变的常量名称要完全大写 多个单词用下划线

##### 继承父类并实现多个接口

使用接口的时候，需要注意

1.接口是没有**静态代码块**的或者**构造方法**

2.一个类的直接父类是唯一的，但是一个类可以同时实现多个接口

格式

 public class MyInterfaceImpl implments  MyInterfaceA,MyInterfaceB{

//覆盖重写所欲抽象方法

}

3.如果实现类所实现的多个接口当中，存在重复的抽象方法，那么值需要覆盖重写一次即可

4.如果实现类没有覆盖重写所有接口当中的所有接口方法，那么实现类就必须是一个抽象类

5.如果是实现类实现的多个接口当中，存在重复的欧仁方法，那么实现类一定要对冲突的默认方法进行覆盖重写

6.一个 类如果直接父类当中的方法和接口的方法产生了冲突，优先用父类的方法

##### 接口之间的多继承

1.类与类之间是单继承 的，直接父类只有一个

2.类与接口之间是多实现的，一个类可以实现多个接口

3.接口与接口之间是多继承的

代码实现：

```java
//定义接口A
public interface AAA {
    
    public static void sayA()  
        
    {  
        
        System.out.println("AAAA");   
        
    }
    
}
//定义接口B
public interface BBB {
    
    public static void sayB()  
        
    {  
        
        System.out.println("BBBB");   
        
    }
    
}
//定义实现类 也可以覆盖重写
public class main implements AAA , BBB{
    
    public static void main(String[] args) {
        
        AAA.sayA();
        
        BBB.sayB();
        
    }

}
```

##### 接口-总结

1.成员变量其实就是常量 格式 

[public] [static] [final] 数据类型 常量名称 = 数据值;

​	注意：常量必须要进行赋值，而且一旦赋值不能改变

​				 常量名称完全大写，用下斜线进行分割

2.接口中最终要的就是抽象方法。格式

[public] [abstract] 返回值类型 方法名称 （参数列表）；

​	注意：实现类必须要覆盖接口所有的抽象方法，除非实现类是抽象类

3.从java 8 开始。接口允许定义默认方法，格式

[public] default 返回值类型 方法名称(参数列表){方法体}

​	注意：默认方法也可以被覆盖重写

4.从java  8 开始，接口允许定义静态方法，格式

[public] static 返回值类型 方法名称(参数列表){方法体}

5.从Java 9 开始，接口允许定义私有方法，格式

普通私有方法：private 返回值类型 方法名称 (参数列表){方法体}

静态私有方法：private static返回值类型 方法名称(参数列表){方法体}

​	注意：private的方法只有接口自己才能调用，不能被实现类或别人使用

### 多态性

父类引用指向子类对象

**父类名称 对象名 = new 子类名称(  )**

**接口名称 对象名  = new 实现类名称(  )**

new谁就优先用谁 子类没有就向上找

##### 多态性-成员变量

1.直接对象名访问

2.间接通过成员方法访问

##### 多态性-成员方法

访问规则 new谁就优先用谁 子类没有就向上找

 编译看左边 运行看右边 成员变量不在这个里面

##### 多态-对象的向上转型

父类名称 对象名  = new 子类名称();

##### 多态-对象的向下转型

对象的向下转型 其实就是还原的动作

格式:

子类名称 对象名 = (子类名称) 父类对象

将父类对象，还原成为本来的子类对象

##### 对象-instanceof

判断

格式： 

```java
//动议一个抽象类Animal

public abstract class Animal {
    
    abstract void shout();//定义抽象shout()方法

}
//定义Cat类继承Animal抽象类

public class Cat extends Animal {
    
    //实现shout()方法
    
    public void shout() {
        
        System.out.println("喵喵");
        
    }
    
}
//定义Dog类继承Animal抽象类

class Dog extends Animal{
    
    //首先shout方法
    
    public void shout(){
        
        System.out.println("汪汪...);
                           
    }
                           
}
//定义测试类
                           
public class Example{
    
    public static void main(String[] args) {
        
        Animal an1 = new Cat();
        
        Animal an2 = new Dog();
        
        an1.shout();
        
        an2.shout();
        
    }
    
}
```

### 内部类

1.成员内部类

2.局部内部类(包括匿名内部类)

##### 成员内部类-定义 

内用外 随意访问 外用内 需要内部类对象

```java
//定义外部类

public class Outer {
    
    int m = 0;
    
    //定义瓦埃布成员方法
    
    void test1(){
        
        System.out.println("外部成员方法");
    
    }
    
    //定义成员内部类Inner
    
    class INner{
        
        int n = 1;
        
        //定义内部类方法，访问外部内的成员变量和方法
        
        void show1(){
            
            System.out.println("外部类成员变量"+m);
            
            test1();
        }
        
        void show2(){
            
            System.out.println("内部类成员的方法");
        
        }
        
    }
    
    void test2(){
        
        Inner inner = new Inner(); 
        
        System.out.println("内部类成员变量"+inner.n);
        
        inner.show2();
    
    }

}

//定义测试类public class Example{

public static void main(String[] args) {
    
    Outer outer = new Outer();//创建外部类对象
    
    Outer.Inner inner = outer.new INner();//创建内部类对象
    
    inner.show1();//测试在成员内部类中访问外部类成员变量和方法
    
    inner.show2();//测试在外部类中访问内部类成员变量和方法

    }

}
```

##### 成员内部类-使用

1.间接方式

2.直接方式

外部类名.内部类名  变量名 = new 外部类名 () .new 内部类名();

##### 内部类-同名变量访问

1.外部类 外部类名称.this.变量名

2.内部类 this.变量名

##### 内部类-局部内部类定义

如果一个类在一个方法内部的，那么这就是以后个局部内部类

只有当前的所属方法可以用它，除了这个方法就不能用了

定义一个类的时候权限修饰符规则

| 外部类     | public/default                   |
| ---------- | -------------------------------- |
| 成员外部类 | public/protected/default/private |
| 局部内部类 | 什么都不写                       |

修饰符	class	外部类名称{

​	修饰符	返回值	外部类方法名称	(参数列表)

{

​		class	局部内部类名称

​		{

​			//代码块

​		}

​	}

}

##### 局部内部类

只能在局部使用

##### 静态内部类

外部类名 . 静态内部类名 变量名 = new 外部内名 . 静态内部类名();

##### 匿名内部类

接口名称	对象名 = new 父接口(){

//匿名对象类实现部分

}

new	接口名{



}.方法名;

只能使用一次

##### String类

**String方法**

```java
cahr charAt [int index]
```

```java
int lenght ();
```

```java
char [] to CharArray();
```

```java
int indexOf(String str);
```

```java
boolean endsWith(String str);
```

```java
String[] split (String reg);
```

```java
String substring (int index);
```

```java
String (cahr[] arr);
```

##### String的构造方法

把字节数组转换为字符串

```java
String (byte [] bytes)
```

把字节数组的一部分转换为字符串 offset:数组的开始索引 lenght:转换的字节个数

```java
String (byte [] bytes, int offset, int lenght)
```



##### Object类

**toString**方法	打印对象的属性 //看一个类是否重写了toString，直接打印这个类的对象即可，如果没有重写toString方法那么打印的是对象的地址值

**equals**方法	其他区对象与此对象是否相等

equals方法，默认比较的是两个对象的地址值，没有意义

Objects equals方法 可以防止空指针指针异常

##### Dale类

System.currentTimeMillis()	当前系统时间到现在有多少毫秒

构造方法 Date 名字 = new Date();

##### DateForat类

对Date日期进行格式化

SimpleDateFormat()  

格式化代码演示 ：

```java

import java.text.SimpleDateFormat;

import java.util.Date;

public class deo01 {
    
    public static void main(String[] args) {
        
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH-mm-ss");
        
        Date d = new Date();
        
        //让d调用format方法
        
        String a = sdf.format(d);
        
        System.out.println(d); 
        
        System.out.println(a);
        
    }
    
}
```

解析

```java

import java.text.ParseException;

import java.text.SimpleDateFormat;

import java.util.Date;

public class deo01 {
    
    public static void main(String[] args)
        
        throws ParseException
        
    {
        
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH-mm-ss");
        
        Date date = sdf.parse("2000-09-09 12-23-32");
        
        System.out.println(date);
    
    }
    
}
```

##### Calendar类

成员方法

get() 返回对应的值

getInstance()

set() 进行设置日期

add() 把指定的字段增加减少指定的值

getTime() 把日历对象转换为日期对象

##### System类

System.currentTimeMillis()	获取毫秒值 可以进行程序测试

arraycopy()	将指定数组的内容拷贝到指定目标数组

##### StringBuilder原理

介绍：字符串缓冲区，可以提高字符串的操作效率

StringBuilder在内存中始终是一个数组占空间少，效率高

超出范围 会自动扩容

StringBuilder构造方法、

```java
public class demo {

public static void main(String[] args)

{

//StringBuilder构造方法

//空参数构造方法

StringBuilder bu1 = new StringBuilder();

System.out.println(bu1);

//有参数构造方法

StringBuilder bu2 = new StringBuilder("bjjj");

System.out.println(bu2);

	}

}
```

StringBuilder常用方法

.append 添加内容

##### 包装类

基本数据类型，使用起来非常方法，但是没有对应的方法来操作这些基本类型数据

可以使用一个类，把基础类型的数据装起来，在类定义一些方法，这个类叫做包装类

我们可以使用类中的方法来操作这些基本类型的数据

装箱

把基本类型的数，包装到包装类中(基本类型的数据-->包装类)

构造方法

```java
public class demo {

public static void main(String[] args)

{

//装箱 构造方法 int 类型 重写了同toString方法

Integer in1 = new Integer(1);
    
    System.out.println(in1);
    
    //String 类型 装箱
    
    Integer in2 = new Integer("wangdoudou");
    
    System.out.println(in2);
    
    //静态方法
    
    Integer in3 = Integer.valueOf(1);
    
    System.out.println(in3);
    
    Integer in4 = Integer.valueOf("2");
    
    System.out.println(in4);

	}

}
```

拆箱

在包装类中去除基本类型的数据(包装类-->基本类型的数据)

成员方法

```java
public class demo {
    
    public static void main(String[] args)
    
    {
        
        //装箱 构造方法 int 类型 重写了同toString方法
        
        Integer in1 = new Integer(1);
        
        System.out.println(in1);
        
        //String 类型 装箱
        
        Integer in2 = new Integer("wangdoudou");
        
        System.out.println(in2);
        
        //静态方法
        
        Integer in3 = Integer.valueOf(1);
        
        System.out.println(in3);
        
        Integer in4 = Integer.valueOf("2");
        
        System.out.println(in4);
        
        //拆箱
        
        int i1  = in1.intValue();
        
        System.out.println(i1);
        
        int i2 = in2.intValue();
        
        System.out.println(i2);
    
    }

}
```

自动装箱与自动拆箱

基本类型的数据和包装类之间可以自动相互转换

自动装箱

```java
public class 自动 {
    
    public static void main(String[] args)
    
    {
        
        //自动装箱
        
        Integer in = 1;
        
        //自动拆箱
        
        in = in + 2;
    
    }

}
```

基本类型与字符串之间的相互转换

基本类型-->字符串	String

​	1.基本类型的值+“ ”

​	2.包装类的静态方法toString(参数)不是object()重载

​		static String toString(int t)返回的是一个表示指定整数的String 对象

​	3.String类的静态方法

​		返回int参数的字符串表示形式

字符串(String)-->基本类型

​	使用包装类的静态方法parsexxx("数值类型的字符串")；

​	Integer类  static int parseInt(String s);

​	Double类 static double parseDouble(String s);

代码演示

```java
public class xainghu {
    
    public static void main(String[] args)
    
    {
        
        //基本类型    字符串
        
        int i1 = 100;
        
        String s1 = i1+"";
        
        System.out.println(s1+200);
        
        String s2 = Integer.toString(100);
            
            System.out.println(s2+200);
        
        String s3 = String .valueOf(100);
        
        System.out.println(s3+200);
        
        //字符串   基本类型
        
        int ig1 = Integer.parseInt(s1);
        
        System.out.println(ig1-10);
    
    }

}
```

##### Runtime类

使用

Runtime rt = Runtime.getRuntime();

创建并得到Runtime

.availableProcessors()	处理器的个数

.freeMemory()	空闲内存的数量

.maxMemory()	最大可用内存数量

### Collection集合

集合和数组的区别 经济和可以变 数组不可以变

学习 集合的目标

1.会使用集合存储数据

2.会遍历集合，把数据取出来

3.掌握每种集合的特性

#### 集合常用方法

- add 添加元素
- remove 移除指定元素
- clear 清空指定元素
- contains 判断元素是否存在
- isEmpty 判断集合是否为空
- size 集合的长度

### LIst集合

有序的集合(存储和取出元素顺序相同)

允许存储重复的元素

有索引，可以使用普通的for循环遍历 

- Vector集合

- ArrayList集合
- LinkedList集合 

Set接口

不允许存储重复元素

没有索引(不能使用普通的for循环遍历)

- TreeSet集合	无序集合
- HashSet集合   无序集合
- LinkedHashSet集合    有序集合

集合框架的学习方法

1. 学习顶层：学习顶层接口/抽象类共性的方法，所有的子类都可以使用
2. 使用底层：底层不是接口就是抽象类，无法常进啊对象使用，需要使用底层的子类创建对象使用

##### collection集合常用的方法

public boolean add(E e)	把给定的对象添加到当前集合中

public void clear()	清空集合中所有的元素

public boolean remove(E e)	把给定的对象在当前集合中删除

public Boolean contains(E e)	判断当前集合中是否包含给定的对象

public boolean isEmpty()	判断当前集合是否为空

public  int size()	返回集合包含元素的个数

public Object[] toArray()	把集合中的元素，存储到数据中

##### Iterator接口

是 一个接口无法直接使用 需要使用接口的实现类对象

代码实现：

```java
import java.util.Collection;

public class Iterator {
    
    public static void main(String[] args)
    
    {
        
        Collection<String> coll = new java.util.ArrayList<>(); 
        
        coll.add("姚明");
        
        coll.add("篮球");
        
        coll.add("麦迪");
        
        coll.add("艾弗森");
        
        coll.add("詹姆斯");
        
        java.util.Iterator<String> it = coll.iterator();
        
        while (it.hasNext())
        
        {
            
            String next = it.next();
            
            System.out.println(next);
        
        } 
        
        System.out.println("===============");
        
        //for方式
        
        for (java.util.Iterator<String> it2 = coll.iterator();it2.hasNext();)
        
        {
            
            String e = it2.next();
            
            System.out.println(e);
        
        }
    
    }

}
```

##### 增强for循环

底层使用的也是迭代器 使用for循环的格式 简化了迭代器的书写

代码演示

```java
import java.util.ArrayList;

public class for增强 {
    
    public static void main(String[] args)
    
    {
        
        demo01();
        
        demo02();
    
    }
    
    private static void demo02()
    
    {
        
        ArrayList<String> list =  new ArrayList<>();
        
        list.add("AAA");
        
        list.add("BBB");
        
        list.add("CCC");
        
        list.add("DDD");
        
        for (String s : list)
        
        {
            
            System.out.println(s);
        
        }
    
    }
```

### 泛型

定义

修饰符 class 类名 <代表反省的变量>{	}

代码实现

```java
public class dingyi<E>

{

		private E a;

		public void setA(E a)

	{

		this.a = a;
		
	}

		public E getA()

	{ 

		return a;

	}

}
//测试
public class dingyimain {
    
    
    public static void main(String[] args)
    
    {
        
        
        dingyi<String> d = new dingyi();
        
        
        d.setA("123");
        
        
        System.out.println(d.getA());
        
        
        dingyi<Integer> d1 = new dingyi<>();
        
        
        d1.setA(12);
        
        
        System.out.println(d1.getA());
        
        
    }
    
    
}

```

##### 泛型-方法定义

修饰符 <泛型> 返回值类型 方法名 (参数列表(使用泛型))

{

//含有发发逆行的方法，在调用方法的使用确定泛型的数据类型

//传递什么类型的参数，泛型就是什么类型

}

##### 泛型-静态方法定义

修饰符 static <泛型> 返回值类型 方法名 (参数列表(使用泛型))

{



}

##### 泛型-接口定义

```java
public interface impl<E>

{
    
    public abstract  void method(E e);

}

public class implmain implements impl<String>{

    @Override
    
    public void method(String s)
        
    {
        
        System.out.println(s);
        
    }
    
}

public class ceshi {
    
    public static void main(String[] args)
        
    {
        
        implmain im = new implmain();
        
        im.method("dou");
        
    }
    
}

```

##### 泛型通配符

？：代表任意的数据类型

使用方式

不能创建对象使用

只能作为方法的参数使用

##### 数据结构

栈	先进后出

队列	先进先出	

数组	

​	查询快

​	增删慢

链表

​	查询慢	每次查询元素都必须从头开始

​	增删快	链表结构增加/删除一个元素 对链表整体结构没有影响 所以增删快

红黑树

 1.节点可以是红色的黑色的

2.根节点是黑色的

3.叶子节点(空接点)是黑色的

4.每个红色的节点的字节都是黑色的

5.任何一个节点到其每一个叶子节点的所有路径上黑色点数相同

### List集合

Java.util.List

Java.util.Set

##### List接口介绍

java.util.List接口继承自Collection接口

List接口的特点

1. 它是一个元素有序的集合
2. 它是一个带有索引的集合
3. 集合中可以有重复的元素   可以用equals方法对比是否重复

##### ArrayList集合

注意：此实现不是同步的

##### LinkedList集合

addfirst()	添加首位

addlast()	添加最后

clear()	清空集合的元素

isEmpty()	判断集合是否为空

pop()	增加/删除首位元素

1. 底层是一个链表结构 查询慢 增删快
2. 里边包含了大量操作首尾的方法

注意：使用LinkedList集合特有的方法，不能使用多态

##### Vector集合

基本淘汰 记住就行

### Set集合

不允许存储重复元素

没有索引 没有带索引的方法 不能使用for循环的遍历

##### HashSet集合

java.util.HashSet是Set接口的实现类

是一个无序的集合，存储元素和去除元素有可能不一样

底层是一个哈希表接口	查询速度非常快

代码演示

```java
package HashSet;

import java.util.HashSet;

import java.util.Iterator;

import java.util.Set;

public class indexx

{
    
    public static void main(String[] args)
    
    {
        
        Set<Integer> set = new HashSet<>();
        
        set.add(1);
        
        set.add(2);
        
        set.add(3);
        
        set.add(3);
        
        set.add(4);
        
        System.out.println(set);
        
        //使用迭代器遍历
        
        Iterator <Integer> it = set.iterator();
        
        while (it.hasNext())
        
        { 
            
            Integer  n = it.next();
            
            System.out.println(n);
        
        }
        
        //使用增强for循环
        
        for (int i:set)
        
        { 
            
            System.out.println(i);
        
        }
    
    }
```

##### 哈希值

1. 是一个十进制的整数，有系统随机给出(就是对象的地址，是一个逻辑地址，不是数据实际存储的物理地址)
2. 在Object类有一个方法，可以获取对象的哈希值 
3. hashCode()                    返回该对象的哈希值

  HashSet集合存储数据的结构(哈希表)

jdk1.8版本之前:哈希值 = 数组 + 链表

jdk1.8版本之后

​	哈希值 = 数组 + 链表；

​	哈希值 = 数组 + 红黑树(提高查询的速度)；

哈希表的特点:速度快

1. 重地   1179395
2. 通话   1179395        两个元素不同 但是哈希值相同 哈希冲突  

如果链表的位数超过了8位就会制动转为红黑树的结构 提高查询速度

##### HashSet存储自定义类型的元素

```java
package HashSet;public class 存储自定义的类型
{
    
    private String Name;
    
    private int age;
    
    public 存储自定义的类型(String name, int age)
    
    {
        
        Name = name;
        
        this.age = age;
    
    }
    
    @Override
    
    public String toString()
    
    {
        
        return "存储自定义的类型{"+
            
            "name = "+Name +'\''+
            
            ",age" +age +
            
            '}';
    
    }
    
    public 存储自定义的类型(){};
    
    public void  setName(String Name)
    
    {
        
        this.Name = Name;
    
    }
    
    @Override
    
    public boolean equals(Object obj)
    
    {
        
        return super.equals(obj);
    
    }
    
    @Override
    
    public int hashCode()
    
    {
        
        return super.hashCode();
    
    }
    
    public String getName()
    
    {
        
        return Name;
    
    } 
    
    public void setAge(int age)
    
    {
        
        this.age = age;
    
    } 
    
    public int getAge()
    
    {
        
        return age;
    
    }

}

package HashSet;

import java.util.HashSet;

public class mian

{
    
    
    public static void main(String[] args)
    
    {
        
        HashSet<存储自定义的类型> set = new HashSet<>();
        
        
        存储自定义的类型 a1 = new 存储自定义的类型("doudou1",12);
        
        
        存储自定义的类型 a2 = new 存储自定义的类型("doudou1",12);
        
        
        存储自定义的类型 a3 = new 存储自定义的类型("doudou3",56);
        
        
    set.add(a1);
        
        
    set.add(a2);
        
        
    set.add(a3);
        
        
        System.out.println(set);
        
        
    }
    
    
}

```

##### LinkedHashSet集合

具有可预知迭代顺序的set接口的哈希表和链表列表实现

无序集合

##### 可变参数

jdk1.5以后

修饰符	返回值类型	方法名	(参数类型...形参名){	}

等价于

修饰符	返回值类型	方法名	(参数类型[]	形参名){	}

使用前提

当方法的参数列表数据类型已经确定，但是参数的个数不确定，就可以使用可变参数

可变参数的注意事项

1. 一个方法的参数列表，只能有一个可变参数
2. 如果方法的参数有哦多个，那么可变参数必须写在参数的末尾

##### Collections常用功能

Collections.addAll(	)	往一个集合中添加多个元素

Collections.shuffle(	)	打乱集合顺序

Collections.sort(	)	进行升序排列	使用前提 被排序的集合相互的元素必须 实现Comparable方法

Collections.sort(集合,new Comparator<类型>)	排序

### Map集合

java.util.Map<k,v>

双列集合

1. Map集合是一个双列集合，一个元素包括两个值，(一个key，一个value)
2. Map集合中的元素，，key和value的类型可以相同，也可以不同
3. Map集合中的元素，key是不允许重复的，value是可以重复的
4. Map集合中的元素，key和value是一一对应

Collection中集合称为单列集合，Map中的集合称为双列集合

需要注意的是，Map中的集合不能包含重复的键，值可以重复，每个键只能对应一个值

##### 常用子类

Hash Map<k,v> 特点

1. Hash Map集合底层是哈希表 查询速度特别快

   1. jdk1.8之前 数组+单向链表
   2. jdk.18以后 数组+单向链表/红黑树（链表的长度超过8）提高查询的速度

2. Hash Map集合是一个无序的集合 存储元素和取出的顺序有可能不一样

   java.util.linkedHashMap<k,v>集合	extends	HashMap<k,v>集合

LinkedHashMap特点

1. LinkedHAshMap集合底层是一个哈希表+链表（保证迭代的顺序）
2. LinkeHsahMap集合是一个无需的集合，存储元素和取出元素的顺序是一致的

##### Map集合中的常用方法

put<k key, v value>	将指定的值映射到指定键关联

remove(object key)	删除集合中的元素 

get(object	key)	得到相应的值

containskey(objeca	key) 判断集合中包含指定的值

##### Map集合遍历

```java
import java.util.HashMap;

import java.util.Iterator;

import java.util.Map;

import java.util.Set;

public class li3

{
    
    public static void main(String[] args)
    
    {
        //创建多态HasMap集合
        
        Map<Integer, String > map =  new HashMap<>();
        
        map.put(01,"qq");
        
        map.put(02,"ww");
        
        map.put(03,"ee");
        
        map.put(04,"rr");
        
        map.put(05,"tt");
        //存储5个元素
        
        Set<Integer> set = map.keySet();
        //把map集合的key值给set集合
        
        Iterator<Integer> iterator = set.iterator();
        //通过set集合使用iterator方法创建迭代器
        
        while (iterator.hasNext())
            //使用while循环是否有下一个元素
        
        {
            Integer next = iterator.next();
            
            //使用迭代器把元素取出赋值给next
            
            String s = map.get(next);
            
            //通过key找到值并赋值给s
            System.out.println(next+"="+s);
            //进行结果输出
        
        }
    }
    
}

```

##### Entry键值对对象

作用:当Map集合一创建,那么就会在Map集合中创建一个Entry对象用来记录键和值	键值对对象 键与值的映射关系

 代码演示

```java
import java.util.HashMap;

import java.util.Iterator;

import java.util.Map;

import java.util.Set;

public class Entrybl {
    
    public static void main(String[] args)
        
    {
        
        Map <String,Integer> map = new HashMap<>();
        
        map.put("tt",1);
        
        map.put("rr",2);
        
        map.put("ee",3);
        
        map.put("qq",4);
        
        map.put("ww",5);
        
        System.out.println(map);
        
        Set<Map.Entry<String, Integer>> set = map.entrySet();
        
        Iterator<Map.Entry<String, Integer>> iterator = set.iterator();
        
        while(iterator.hasNext())
            
        {
            
            Map.Entry<String, Integer> next = iterator.next();
            
            String key = next.getKey();
            
            Integer val = next.getValue();  
            
            System.out.println(key+"===>>"+val);
            
        }
        
        System.out.println("==================");
        
        //增强for遍历
        
        for (Map.Entry<String, Integer> entry:set)
            
        {
            
            String key = entry.getKey();
            
            Integer val = entry.getValue();
            
            System.out.println(key+"===>"+val);
            
        }
        
    }
     
}
```

##### LinkedHashMap集合

java.util.LinkedHashMap<k,v> extends HashMap<k,v>

Map接口的哈希表和链表实现,具有可预知的迭代顺序

底层原理

哈希表+链表(记录元素的顺序)

key允许重复 无序

##### Hashtable<k,v>接口

java.util.Hashtable<k,v>集合	implement Map<k,v>接口

Hashtable	底层也是一个哈希表,是一个线程安全的集合,是单线程的集合,速度慢

HashMap集合,底层也是一个哈希表 是一个线程不安全的集合,是多线程的集合,速度快

HashMap集合(之前学习的所有集合)可以存储null值,null

Hashtable集合不允许存储空 null

#####  JDK9对集合添加的优化

java9 添加了集中集合工厂方法,更方便创建少量元素的集合 map实力 新的list set map的静态工厂方法可以更方便地创建集合不可变实例

of(	)		方法 一次性添加多个元素

使用前提	当集合中存储的元素已经确定,不再改变时使用

注意

1. of方法只适用于list接口set接口 map接口 不能适用于接口的实现类
2. of方法返回值是一个不能改变的集合,集合不能在使用add put添加元素 会抛出异常
3. set接口和map接口电泳of方法的时候,不能有重复的元素,否则会抛出异常

## Debug追踪

 可以让代码逐行执行 查看代码的执行过程 调试程序中出现的bug
执行

1. f8	逐行执行程序
2. f7进入到方法中
3. shift+f8  跳出去
4. f9    跳到下一个断点处,如果没有下个断点,南无结束程序
5. ctrl+f2  退出debug模式
6. console 切换到控制台

## 异常

##### 概念

**异常**:指的是程序执行过程中 出现非正常的情况,最终导致JVM的非正常停止

在java等面向对象的编程语言中,异常本身是一个类,产生异常就是创建异类并抛出了一个异常对象,java处理异常的方式是中断处理

异常指的并不是语法错误,语法错了,编译不通过,不会产生字节码文件,根本不运行

##### 异常体系

异常机制其实就是帮助我们找到程序中的问题,异常的根类是java.lang.Thowable其下有两个子类

Java.lang.Error与java.lang.Exception,平时说的异常是指java.lang.Exception

| Throwable                        |                                      |
| :------------------------------- | ------------------------------------ |
| Error工程师不能处理,只能尽量避免 | Exception由于使用不当导致,可以避免的 |

##### Throwable体系

- Error:严重错误Error,无法通过吃力的错误,只能事先避免,好比绝症
- Exception:表示异常:异常产生后程序员可以通过代码的方式纠正,是程序继续运行,是必须要处理的,好比发烧感冒

Thorwable中的常用方法

- public void printStacktrace()	打印异常的详细信息

包含了异常的类型,异常的原因,还包括异常出现的位置,在开发和调试阶段,都得使用pintStackTrace

- public  String  getMessage()获取发生异常的原因
- 提示用户的时候,就提示错误原因
- public String  toString () 获取异常的类型和异描述信息(不用)

出现异常 不要紧张 把异常的简单类名 拷贝到API中查看

##### 异常分类

java.lang.Throwable 类是java语言中所有错误或者异常的超类

​	Exception编译器异常 进行编译(写代码)java程序中出现的问题

​	RuntimeException 运行期异常,java程序运行过程中出现的问题

异常就相当于程序得了一个小毛病,把异常处理掉,程序就可以正常执行

Error 错误

​	错误就相当于程序得了一个无法治愈的毛病,必须修改源代码,程序才能正常执行\

### 异常的处理

Java异常处理的五个关键字 try catch finally throw throws

##### 抛出异常throw

在java中,提供了以哦个throw关键字塔用来抛出一个指定的对象.那么,抛出一个异常具体如何操作呢?

1. 创建一个异常对象,封装一些信息(信息可以自己编写)
2. 需要将这个异常对象告知调用者.通过关键字throw就可以完成.throw异常对象
   1. throw用在方法内,用来抛出一个异常对象,将这个对象传递到调用者处,并结束当前方法的执行

**作用**

可以使用throw关键字在指定的方法中抛出指定的异常

**注意**

1. throw关键字必卸载方法的内部
2. throw关键字后边new的对象必须是Exception或者是Exception的子类对象
3. throw关键字抛出的异常对象,我们必须处理这个异常对象
   1. throw关键字后边创建的是RuntimeException的子类对象,我们可以不处理,默认交给JVM处理(打印异常对象,中断程序)
   2. throw关键字后边创建的是编译异常(写代码的时候报错),我们就必须处理这个异常,要么throw要么try...catch

以后工作中我们首先必须对夫妇擦混敌过来的参数及逆行校验

如果参数不合法,我们就必须使用抛出异常的方式,告知方法的调用者,传递的参数有问题

**使用格式**

throw new 异常类名(参数);

##### 运行期异常

1. throw  new NullPointerException("对不起,数组不能为空");
2. throw new ArrayIndexOutOfBoundsException("数组越界异常");

##### 编译异常

throw  new FileNotFoundException("文件找不到异常");

##### Objects非空判断

public static <T> T requireNonNull(T  obj)	查看指定引用对象不是null

代码演示

```java
package 异常分类;

import java.util.Objects;

public class Objects非空判断

{
    
    public static void method(Object obj)
    
    {
        
        Objects.requireNonNull(obj);
    
    }; 
    
    public static void main(String[] args)
    
    {
        
        method(null);
    
    }

}
```

**Objects.requireNonNull的重载方式**

 Objects.requireNonNull(对象,字符串);

##### 声明异常throws

**声明异常**:将问题标识出来,报告给调用者.如果方法内通过throw抛出来了编译ga时异常,而没有捕获处理(稍后讲解ga)那么必须通过throw及逆行声明,让点用着去处理.

关键字throw运用于表示当前方法不处理异常,而是提醒该方法的调用者来处理异常,(抛出异常)

**声明异常的格式**

修饰符 返回值类型 方法名(参数) throw 异常类名1,异常类名2...{	};

**注意*:*****

注意: 

1. throw 关键字必须写在方法声明处
2. throw关键字后边声明的异常必须是Exception的子类
3. 方法内部如果抛出了多个异常对象,那么直接声明傅雷与IC即可
   1. 如果抛出的多个异常对象有子类关系,那么就必须声明异常即可
4. 调用一个声明抛出异常的方法,我们就必须的处理声明的异常,要么继续使用throw声明抛出,交给方法的调用者处理,最终交给JVM要么try....cath自己处理

捕获异常try....catch

如果异常出现的话,会立即终止程序,所以我们得处理异常

1. 该方法不处理,而是声明抛出异常,由该方法的调用者来处理(throw);
2. 该方法中使用try-catch的语句块来处理异常

**try**-**catch**的方式捕获异常

- 捕获异常:Java中对异常有针对性的语句进行捕获可以对出现的异常进行指定法昂是的处理

- 格式:
  try{

  可能产生异常的代码

  }catch(定义一个异常变量,用来接收try中抛出的异常对象)

  {

  异常的处理逻辑,异常对象之后,怎么处理异常对象

  一般在工作中,会把异常对象记录之后到一个日志中

  }...catch(异常类名,变量名){

  

  }

Throwable**类中定义了一些查看方法**

- public String getMessage():获取异常的面熟信息,原因(提示给用户的时候)就提示错误原因.
- public String toString ():获取异常的类型和异常面熟信息(不用)
- public void printStackTrace():打印异常的跟踪栈和异常描述信息并输出到控制台

##### finally代码块

**finally:**有一些特定的代码无论异常是否发生,都需要执行,另外,因为异常会引发程序跳转,导致有些语句执行不到,而finally就是解决这个问题的.在finally代码块中存放的代码都是一定会被执行的.

当我们在try语句中打开一些物理资源(磁盘文件/网络连接/数据库连接等),我们都得使用完之后,最终关闭打开的资源

**finally**的语法:

try...catch...finclly:自身需要处理异常,最终还得关闭资源

**注意**

1. finally不能单独使用,必须和trt一起使用
2. finally一般用于资源释放(资源回收),无论程序是否出现异常, 最后都要资源释放

##### 异常注意事项

- 多个异常使用捕获又该怎么处理呢?
  1. 多个异常分别处理
  2. 对各异常一次捕获,多次处理
  3. 多个异常一次捕获一次处理
- 运行时异常被抛出就可以不处理,既不捕获也不声明抛出
- 如果finally有return语句,永远返回finally中的结果,避免该情况
- 如果父类抛出了多个异常,子类覆盖父类方法时,只能抛出相同的异常或者是他的子集
- 父类方法没有抛出异常,子类覆盖该方法时也不可抛出异常.此时子类产生该异常,只能捕获处理,不能声明抛出
- 在try/catch后可以追加finally代码块,其中的代码一定会被执行,通常用于资源回收

##### 自定义异常的练习

为什么需要自定义异常类

**什么是自定义异常类**:

在开发中根据自己的业务的异常情况开定义异常类

自定义一个业务逻辑异常:PegisterException.一个注册异常类

异常类如何定义:

1. 自定义一个编译期异常,自定义类 并继承与java.lang.Exception
2. 自定义一个 运行期异常的异常类:自定义类 并继承与java.lang.RuntimeException

注意:

1. 自定义异常类一般都是以Exception结尾,说明该类是一个异常类
2. 自定义异常类,必须的继承Exception或者RuntimeException
   1. 继承Exception:那么自定义异常类就是一个编译期异常,如果方法内部抛出了编译期异常,就必须处理这个异常要么throw要么try...catch
   2. 基础RuntimeException:那么自定义的异常类就是一个运行期异常,无需处理,交给虚拟机处理(中断处理)



## 多线程

##### 并发与并行

- **并发**:指两个或多个时间同一时间段内发生
- **并行**:指两个或多个事件在同一时刻发生(同时发生)

##### 线程与进程

- **进程**:是指一个内存中运行的应用程序,每个进程迪欧有一个独立的内存空间,一个应用程序一颗同时运行多个进程;进程也是程序的一次执行过程,是系统运行程序的基本单位;系统运行一个程序即使一个进程从创建.运行到消失的过程
- **线程**:线程是进程的一个执行单元,负责当前进程中程序的执行,一个进程至少有一个线程.一个进程中可以有多个线程的,这个应用程序也可以称之为多线程程序
- 简而言之:一个程序运行后至少有一个进程,一个进行可以包含多个线程

##### 线程调度

- 分时调度
  - 所有线程轮流使用cpu的使用权,平均分配每个线程占用cpu的时间
- 抢占式调度
  - 有限让优先级高的线程使用cpu.如果线程的优先级相同,那么会随机选择一个(线程随机性),Java使用的为抢占式调度

##### 创建线程类

1. 定义Thread类的子类,并重写该类的tun()方法,改run()方法就代表线程选哟完成的任务,因此把run()方法称为线程执行体
2. 创建Thread子类的实例,即可创建线程对象
3.   调用线程对象的start()方法来启动改线程

##### Thread类

**构造方法**:

- public Thread()	分配一个新的线程对象
- public Thread (String name)   分配一个指定目标的新的线程对象
- public Thread(Runnable target)  分配一个带有指定目标的线程对象
- public Thread (Runnable target, String  name)   分配一个带有指定目标新的线程对象并指定名字

##### 常用方法

- public String getName()	获取当前线程的名称
- public String setName()	设置当前线程的名称
-  public void start()	导致此线程开始执行 java虚拟机调用此线程的run方法
- puiblic void run()   此线程要执行的任务在此处定义代码
- public static void sleep(long  millis)使当前正在执行的线程一指定的毫秒数暂停(暂停是停止执行)
- public static Thread currentThread()  返回对当前正在执行的线程对象的引用
- yield() 释放cpu的执行权
- join() 在线程a调用b的join方法,此时线程a就进入阻塞状态,直到线程b执行完成后,线程a才结束阻塞状态
- stop() **已过时** 结束线程
- isAlive() 判断线程是否存活

##### 创建线程方式二

java.lang.Runnable

1. 定义Runnable接口的实现类,并重写改接口的run()方法,该run()方法体同样是该线程的线程执行体.
2. 创建Runnable实现类的实例,并以实例作为Thead的target来创建Thread对象,该Thread对象才是真正的线程对象
3. 调用线程对象的start()方法来启动线程

##### 创建线程的方式三

```java
 new Thread(){
      @Override
      public void run() {}
};
```

##### 线程中断

public boolean isInterrupted()	中断线程执行

public void interrupt()	中断线程执行

##### 线程强制执行

public final void join(){}		线程强制执行

##### 线程的礼让

public static void yield()

##### 线程优先级

从理论上讲线程的优先级越高越有可能先执行

- 最高优先级: public static final int MAX_PRIORITY  10;
- 中等优先级: public static final int NORM_PRIORITY  5;
- 最低优先级: public static final int MIN_PRIORITY  1;

**涉及方法**

- getPriority() 返回线程优先级
- setPriority(int 被我Priority) 改变线程的优先级 

##### 匿名线程

代码演示

```java
public class nimingneibulei

{

	public static void main(String[] args)

{

	new Thread()

{ 

	@Override

	public void run()

{
    
    for (int i = 0; i <= 20; i++)
        
    {
        System.out.println(Thread.currentThread().getName() + "黑啊吗");
        
    }
    
    }
    
    }.start();
        
        Runnable r = new Runnable()
        
        {
            
            @Override
            
            public void run()
            
            {
                
                for (int i = 0; i <= 20; i++)
                
                {
                    
                    System.out.println(Thread.currentThread().getName()+"lal");
                
                }
            
            }
        
        };
        
        new Thread(r).start();
    
    }

}
```

## 线程安全

1. 同步代码块
2. 同步方法
3. 锁机制

##### 同步代码块

- **同步代码块**:synchronized关键字可以用于方法中的某个区域中,表示只对这个区块的资源实行互斥访问

- 格式

- synchronized(同步锁)
  {

  ​	需要同步代码

  } 

##### 同步方法

**同步方法**:使用synchronized修饰的方法,就叫做同步方法,保证过该A线程执行该方法的时候.其他线程只能在方法外等着

##### 静态方法 

在同步方法的修饰前加一个static

## 线程状态

##### 线程状态概述

当线程被创建并启动以后,他既不是一启动就进入了执行状态,也不是一直处于执行状态.在线程的声明周期中,有几种状态呢?在API中java.lang,Thread.State这个枚举中给出了六种线程状态:



| 线程状态               | 导致状态发生条件                                             |
| ---------------------- | ------------------------------------------------------------ |
| NEW(新建)              | 线程刚被创建,倒是并未启动.还没有调用start方法                |
| Runnable(可运行)       | 线程可以在java虚拟机中运行的状态,可能正在运行自己代码,也有可能没有,这取决于操作系统处理器 |
| Blocked(锁阻塞)        | 当一个线程试图获取一个对象锁,而该对象锁被其他的线程持有,则该线程进入Blocked状态;当该线程持有锁时,该线程将变成Runnable状态 |
| Waiting(无限等待)      | 一个线程在等待另一个线程执行一个(唤醒)动作时,该线程进入Waiting状态.进入这个状态是不能自动唤醒的,必须等待另一个线程调用notify或者notiyAll方法才能唤醒 |
| TimedWaiting(计时等待) | 同waiting状态,有几个方法有-超时参数,调用他们即将进入TimedWaiting状态.这一状态将一直保持到超时期满或者收到唤醒通知.带有超时参数的常用方法有Thread.sleep,Object.wait |
| TEminated(被终止)      | 因为run方法正常退出死亡,或者因为没有捕捉的异常终止了run方法而死亡 |

## 线程的状态图

![](C:\Users\Mi\Desktop\新建文件夹\Java\Img\流程\线程流程图.jpg)

## Blocked运行状态图

![](C:\Users\Mi\Desktop\新建文件夹\Java\Img\流程\Blocked运行状态图.jpg)

## Waiting(无限等待状态)



Waiting状态在API中介绍:一个正在无限期待等待另一个线程执行一个特别的(唤醒)动作的线程处于这一状态.

## TimedWaiting(计时等待)

TimedWaiting在API中描述为:一个正在限时等待另一个线程执行一个(唤醒)动作的线程处于这一状态.单独理解这句话,真是玄之又玄,其实我们在之前的操作中已经接触过这个状态了,在哪里呢?

进入到TimeWaiting(计时等待)有两种方式

1. 进入selpp(Long m)方法,在毫秒值结束之后,线程水总进入到Runnable/Blocked状态
2. 使用wait(Long m)方法,wait方法如果在毫秒值结束之后,还没有被notify唤醒,就会自动醒来,线程水下进入到Runnable/Blocked状态

**唤醒方法**

void notify()唤醒在此对象监视器上等待的单个线程

void notifyAll()唤醒在此对象监视器上的等待所有线程

## 等待唤醒机制

##### 线程间通信

**概念**多个线程在处理同一个资源,但是处理的动作(线程的任务)却不相同

为什么要处理线程通信

多个线程并执行时,在默认情况下cpu是随机切换线程的,当我们需要多个线程来共同完成一件任务,并且我们希望他们有规律的执行,那么多线程之间需要一些协调通信,以此来帮我们达到多线程共同操作一份数据

**如何保证线程间通信有效利用资源**:

多个线程在处理一个资源,并且任务不同时,需要线程通信来帮助解决线程之间对同一个变量的使用或操作.就是多个线程在操作同一份数据时,避免对同一共享变量的争夺.也就是我们需要通过一定的手段使各个线程能有效的利用资源.而这种手段即----等待唤醒机制

**等待唤醒机制**

什么是等待唤醒机制

这是多个线程间的一种**协作**机制.谈到线程我们经常想到的是线程间的**竞争**(**race**),比如去争夺锁,但这并不是故事的全部,线程间也会协作机制,就好比在公司里和你的同时们,你们可能存在晋升时的竞争,但更多时候你们更多是一起合作以完成某种任务

就是在一个线程进行了规定操作后,就进入等待状态(**wait()**),等待其他线程执行完成他们的指定代码过后 再将其唤醒(**notify()**);在有多个线程进行等待,如果有需要,可以使用**notifyAll()**来唤醒所有的等待线程

wait/notify就是线程间的一种协作机制

**等待唤醒的方法**

等待唤醒机制就是用于解决线程间通信的问题的,使用到3个方法 如下

1. wait:  线程不在活动,不参与调度,进入wait set中,因此不会浪费cpu资源,也不会去竞争锁了,这时的线程状态即是WAITING.它还要等着别的线程执行一个特别的动作,也即是通知(notify)在这个对象上等待的线程从wait set中释放出来,重新进入到调度队列(ready queue)中
2. notify:  则选取所通知对象的waitset中的一个线程释放,例如::餐馆有空位置了,等待就餐最久的顾客先入座
3. notifyAll:   则释放锁通知对象的waitset上的全部线程

注意:

哪怕至同治了一个等待的线程,被通知线程也不能立即回复执行,因为它当初中断的地方是在同步块内,而此刻他已经不持有锁,所以它需要再次尝试去获取锁(很可能面临其他线程的竞争),成功后才能在当初调用wait方法之后的地方恢复执行

**总结如下**

- 如果能获取锁,线程就从WAITING状态变成 RUNNABLE状态
- 否则,从wait set出来,又进入entry set,线程就从WAIYTING状态又变成BLOCKED状态

**调用*****wait和notify方法需要注意的细节****

1. wait方法与notry方法必须要有同一个锁对象调用.因为:对应的锁对象可以通过notify唤醒使用同一个锁对象调用的wait方法后的线程
2. wait方法与notify方法是属于Object类的方法的,因为,锁对象可以是任意对象,而任意对象的所属类都是继承了Object类的.
3. wait方法与notify方法必须要同步在代码块或者是同步函数中使用.因为:必须要通过锁对象调用者2个方法

##   同步问题

#####  lock锁

java.util.concurrent.loks.lock机制提供了比synchronized代码块和synchronized方法更广泛的锁定操作,同步代码块/同步方法具有的功能lock都有,初次之外更强大,更体现面向对象

lock锁也称同步锁,加锁与释放锁方法化了,如下

- public void lock()	加同步锁
- public void unlock()  释放同步锁

1. synchronized(同步对象)

{

同步代码操作

}

只要在方法定义上加上synchronized就可以

## 线程池

##### 线程池思想概述

​	我们使用线程的时候就去创建一个线程,这样实现起来非常差简便,但是就会有一个问题:

​	如果并发的线程数量很多,并且每个线程都是执行一个时间很短的任务就结束了,这样频繁创建线程就会大大降低系统的效率,因为频繁创建线程和销毁线程需要时间

​	当程序第一次启动的时候,创建多个线程,保存到袷集合中当我们想要使用多线程的时候,就可以从集合中取出来线程使用

​	合理利用线程池能够带来三个好处

1. 降低资源消耗,减少了创建和销毁线程的次数,每个工作线程都可以被重复利用,可以执行多个任务
2. 提高相应速度,当任务到达时,热恶奴我可以不需要的等到线程创建就可以立刻执行
3. 提高线程的可管理性,可以根据系统的承受能立,调整线程池中工作线程的数目,防止因为消耗过多的内存,而把服务器累趴下(每个线程需要大约1mb,线程开的越多,消耗的内存也就越大,最后死机)

线程池 JDK1.5之后提供的

Execcutors类中的静态方法:

static ExecutorService newFixedThreadPool(int nThreads)创建一个可以重用固定线程数的线程池

返回值:ExecutorService接口,返回的是EcecutorService 

面向接口编程 

```java
java.util.concurrent.ExcutorAervice:线程池接口
```

用来从线程池中获取线程,调用start方法,执行线程任务

submit(Runnable task)提交一个Runnable任务用于执行

void shutdown()	关闭/销魂线程池的方法

## Lambda表达式

##### 函数式编程思想概述

在数学中,**函数**就是有输入量,输入量的一套计算方案,也就是拿什么东西做什么事情,相对而言,面向对象过分强调,必须通过对象的形式来做事情,而函数时思想则尽量忽略面向对象的复杂语法-----**强调做什么,而不是以什么形式做** 

##### 冗余的Runnable代码

##### **传统写法**

当需要启动一个线程去完成任务时,通常会使用Java.lang.Runnable接口来定义任务内容,并使用java.lang.Thread类来启动该线程.

**代码演示**

```java
package lambda;

public class demo01 {
	public static void main(String[] args) {
		new Thread(() -> {
								System.out.println(Thread.currentThread().getName() + "刚刚创建了线程");
		}).start();
	}
}

```

##### Lambda标准格式

lambda省去了面向对象的条条框框,格式由3部分组成:

- 一些参数
- 一个箭头
- 一段代码

Lambda表达式的标准格式为:

```java
(参数类型 参数名称) -> {代码语句}
```

可以省略的内容

1. (参数列表):括号中参数列表的数据类型,可以省略不写

2. (参数列表):括号中的参数如果只有一个,那么类型和()都可以省略

3. {一些代码}:如果{}中的代码只有一行,无论是否有返回值,都可以省略({},return,分号)

   注意:要省略{},return,分号必须一起省略

## String类

### **常用方法**

- length() 返回字符串的长度
- charAt(int index) 返回字符串的当前索引字符
- isEmpty() 字符串是否为空
- toLowerCase() 转换字符串为大写
- toUpperCase() 转换字符串为小写
- trim() 去除字符串首尾空格 中间不变
- equals() 比较字符串的内容
- equalsIgnoreCase() 忽略大小写比较
- concat() 连接的意思 拼接
- compareTo() 字符串排序
- substring() 截取字符串
- endsWith(String str) 字符串是否以指定字符串结束
- startsWith(String str) 字符串是否以指定字符串开始
- startsWith(String str ,int index) 字符串是否以位置的指定字符串开始
- contains() 判断当前字符串是否包含此字符串
- indexOf() 返回字符串第一次出现的索引位置 未找到返回-1
- lastOf() 返回字符串最后次出现的索引位置 未找到返回-1
- replace() 替换字符串
- replaceAll() 匹配的字符串使用正则表达式替换
- rewplaceFist() 只替换第一个
- matches() 匹配
- split() 分割字符串

### String类与其他结构之间的转化

- String转Integer

```java
String s1 = "123";
Integer.parseInt(s1);
```

- 其他转String

```java
int a = 1;
String b = a+"";
```

- String转换char[]

```java
String s1 = "123";
char[] chars = s1.toCharArray();
```

- char[]转String

```java
char[] chars = new char[]{'q', 'w', 'e', 't'};
String s = new String(chars);
```

- String转byte[]

```java
String s = "wjiljq";
byte[] bytes = s.getBytes();
```

- byte[]转String

```java
byte[] bytes = new byte[]{70, 85};
String s = new String(bytes);
```

## StringBuffer&StringBuilder

### 区别

- String 不可变的字符序列
- StringBuffer 可变的字符序列 线程安全 效率低
- StringBuilder 可变的字符序列 线程不安全 效率高

### 常用方法

- append() 添加数据
- delete(int start,int end) 删除指定位置的数据
- replace(int start,int end,String str) 指定位置替换
- insrrt(int offset,String str) 在指定位置插入数据
- reverse() 字符序列逆转
- indexOf() 返回指定位置的字符
- substring() 截取数据
- length() 返回长度
- charAt()  查询数据出现的位置
- setCharAt() 设置数据

## Java8之前日期

### System类

#### 常用方法

- currentTimeMillis() 获得时间戳

### Date类

`java.util.Date`

#### 构造器的使用

构造器一

```java
Date date = new Date();
```

构造器二

```java
Date date = new Date(1555274554545L);
```

#### 方法

- toString() 返回年月日 时分秒 地区
- getTime() 返回时间戳

`java.sql.Date`

构造器

```java
Date date  = new Date(45451524156521L);
```

**方法同上**

## SimpleDateFormat

#### 方法

- format() 格式化时间
- parse() 解析字符串

## Calendar

实例化

- 创建子类GregorianCalendar的对象
- 地哦按用静态方法getInstance()

### 常用方法

- get()
- set()
- add()
- getTime()
- setTime()

## File类

### 概述

```
java.ioFile类是文件和目录路径名的抽象表示,主要用于文件和目录创建,查找和删除等操作.
```

### 构造方法

与系统有关的路径分隔符,为了方便,它被表示为一个字符串

```java
static String pathSeparator 
```

与系统有关的路径分隔符

```
static char pathSeparatorChar
```

与系统有关的默认名称分隔符,为了让方便,它被表示一个字符串

```
static String separator	路径分隔符 window:分号 linux: 冒号
```

与系统 有关的默认名称分隔符

```
sttaic char separtorChhar 文件名称分隔符 window:反斜杠\ liunx:正斜杠/
```

路径:

- 绝对路径:是一个完整的路径
  - ​	以盘符开始的路径

- 相对路径:是一个简化的路径
  - 相对指的是相对于当前项目的根目录
  - 如果使用当前的根目录,历经可以简化书写
- 注意
  - 路径是不区分大小写的
  - 路径的文件名称分隔符window使用反斜杠,反斜杠是转义字符,2个反斜杠代表一个反斜杠

```java
File(String pathname)//通过将给定路径名字字符转换为抽象路径来创建一个File实例
```

### 常用方法

返回此File的绝对路径名字字符串

```java
public String getAbsolutePath();
```

将此File转换为路径名字字符串

```java
public String getPath();
```

返回由File表示的文件或目录的名称

```java
public String getName();
```

返回由此File表示的文件长度

```java
public long lenght();
```

此File是的文件或目录是否真实存在

```java
public boolean exists();
```

此File表示的是否为目录

```java
public boolean isDirectory();
```

此File表示的是否为文件

```java
public boolean isFile();
```

当且仅具有该名称的文件尚不存在时,创建一个新的空文件.

```java
public boolean createNewFile();
```

删除由此File表示的文件或目录

```java
public boolean delete();
```

创建由此File表示的目录

```java
public boolean mkdir();
```

创建由此表示的目录,包括任何必需但不存在的父目录

```java
public boolean mkdirs();
```

删除

```java
public boolean delete();
```

### 目录遍历

返回一个String数组,表示该File目录中的所有子文件或目录

```java
public String list();
```

返回一个File数组,表示该File目录中的所有子文件或目录

```java
public File[] listFiles();
```

## 递归

- **递归:**指在当前方法内调用自己的这种现象

- **递归的分类**
  - 递归分为两种,直接递归和简介递归
  - 直接递归称为方法自身调用自己
  - 间接递归可以A方法带哦用B方法,B方法调用C方法,C方法调用A方法
- **注意事项:**
  - 递归一定要条件限制限制,保证递归能够停止下来,否则会发生栈内存溢出
  - 在递归中虽然有限定条件,但是递归次数不能太多.否则也会发生栈内存溢出
  - 构造方法,禁止递归

使用递归遍历文件夹

```java
import java.io.File;

public class demo04 {
    public static void main(String[] args) {
        File f = new File("D:");
        show(f);
    }

    private static void show(File dir) {
        File[] files = dir.listFiles();
        for (File file : files) {
            if (file.isDirectory()) {
                show(file);
            } else {
                System.out.println(file);
            }
        }
    }

}

```

文件搜索

```java
import java.io.File;

public class demo04 {
    public static void main(String[] args) {
        File f = new File("D:\\Java\\Java资料\\probject");
        show(f);
    }

    private static void show(File dir) {
        File[] files = dir.listFiles();
        for (File file : files) {
            if (file.isDirectory()) {
                show(file);
            } else {
                String name = file.getName();
                String s = name.toLowerCase();
                boolean b = s.endsWith(".java");
                if (b == true) {
                    System.out.println(file);
                }
            }
        }
    }

}
```

优化

```java
//链式编程
import java.io.File;

public class demo04 {
    public static void main(String[] args) {
        File f = new File("D:\\Java\\Java资料\\probject");
        show(f);
    }

    private static void show(File dir) {
        File[] files = dir.listFiles();
        for (File file : files) {
            if (file.isDirectory()) {
                show(file);
            } else {
                /*String name = file.getName();
                String s = name.toLowerCase();
                boolean b = s.endsWith(".java");*/
                if (file.getName().toLowerCase().endsWith(".java")) {
                    System.out.println(file);
                }
            }
        }
    }

}

```

##### 文件过滤器优化

java.io.FileFileter是一个接口,是File的过滤器.该接口的对象可以传递给File类夫人list Files(FileFilter)作为参数,接口中只有一个方法

##### 过滤文件的方法

测试pathname否应该包含当前File目录中,符合则返回true

```
boolean accept (File pathname)
```

```
File [] listFiles(FilenameFileter filter)
```

##### 抽象方法

java.io.FileNameFilter接口:实现此接口的类 实例可过滤文件名

作用:用于过滤文件名称

测试指定文件是否应该在包含在某一文件列表中

参数:

File dir:构造方法中传递的被遍历的目录

String name:使用ListFiles方法遍历目录,获取的每一个文件/文件夹的名称

注意

两个过滤器接口是没有实现类的,需要我们自己写实现类,重写过滤的方法accept,在方法中定义过滤的



```
boolean accept(File dir, String name) 
```

## IO概述

### 什么是Io

生活中,你肯定经历过这样的场景.当你编辑一个文本文件,忘记了ctrl+s,可能文件就白白编辑了,当你电脑上插入一个u盘,可以把一个视频,拷贝到电脑硬盘里,那么数据就是在那些设备上呢?

我们把这种数据的传输,可以看作是一种数据的流动,按照流动的方向,以内存为基准,分为**输入input**和**输出ouput**,即流向内存是输入流,流出内存是输出流.

Java中I/O操作主要是指使用java.io包下的内容,进行输入,输出操作.输入也叫做读取数据,输出也叫做写出数据

### I/O的分类

根据数据的流向分为:输入流和输出流

- **输入流:**把数据从其他设备上读取到内存中的流
- **输出流:**把数据从内存中写出到其他设备上的流
- 格局数据的类型分为:字节流和字符流
- **读得懂就用字符流 读不懂就用字节流**
- 不知道使用那些 就使用字节流

### 字节流

#### 字节输出流[OutputStream]

java.io.OutputStrem抽象类是表示字节输出流的所有类的超类,,将指定的字节信息输出到目的地,它定义了字节输出流的基本共性功能的方法

关闭此输出流释放与此流相关的任何系统资源;

```java
public void closee()
```

刷新此输出流并强制任何缓冲的任何输出字节被写出

```java
public  void flush()
```

将b.lenght字节从指定的字节数组写入此输出流

```java
public void waite(byte [] b)
```

从将指定的字节数组写入len字节,从偏移量off开始输出到此输出流

```java
public void waite(byte [] b,int off , int len)
```

将指定的字节输出流 

```java
public abstract void waite(int b)
```

#### 构造方法

创建一个具有指定名称的文件中写入数据的输出文件流

```java
FileOutoutStream(String name)
```

创建一个向指定File对象表示的文件中写入数据的文件输出流

```java
FileOutputStream(File file)
```

参数:写入数据的目的

String name:目的地的是一个文件的路径

File file:目的地是一个文件

构造方法的作用:

1. 创建一个FileOutputStream对象
2. 会根据构造方法中传递的文件/文件路径,创建一个空的文件
3. 会把FileOutputStream对象指向创建好的文件

写入字符串的方法:可以使用String类中的方法把字符串,转换为字节数组

```java
byte [] getBytes()
```

#### 数据的追加续写

创建文件输出流以写入有指定的File对象表示的文件

```java
public tr(File file, boolean append)
```

创建文件输出流以指定的名称写入文件

```
public FileOutputStream(String name, boolean appnd)
```

true 代表追加数据,false 代表清楚原有数据

换行符号

- windows \r \n
- linux \n
- mac \r

### 字节输入流

**java.io.InputStream**:抽象类是表示字节输入流的所有类的超类,可以读取字节信息到内存中.它定义了字节输入流的基本共性功能方法

关闭此输入流释放与此流相关联的任何系统资源部

```java
public void close()
```

从输入流读取数据的下一个字节

```java
public abstract int read()
```

从输入流中读取一些字节数,并将它们存储到字节数组b中

```java
public int read(byte  [] b)
```

**注意**:close方法,当完成流的操作时,必须调用此方法,从文件中读取字节

##### FileInputStream类

java.io.FileInputStream类是文件输入流,从文件中读字节.

##### 构造方法

通过打开与实际文件的连接来创建一个FileInputStream,该文件由文件系统中的File对象file命名

```java
FileInputStream(File file)
```

通过打开与实际文件的连接来创建一个FileInputStream,该文件由文件系统中的路径名name命名

```java
FileInputStream(String name)
```

当你创建一个流对象时,必须传入一个文件路径.该路径下,如果没有该文件,会抛出**FileNotFoundException**

### 字符输入流

FileReader

java.io.Reader:字符输入流,是字符输入流的最顶层的父类,定义了一些共性的成员方法 ,是一个抽象类

共性的成员方法

读取单个字符并返回

```java
int read();
```

将字符读入数组

```java
int read(char[] cbuf);
```

关闭此输入流释放与此流相关联的任何系统资源部

```java
public void close();
```

### 字符输出流

java.io.Write抽象类是表示用于写出字符流所有的超类,将指定的字符信息写道目的地.它定义了字节输出流的基本共性 功能方法

写入单个字符

```java
coid  write(int c)
```

写入字符数组

```java
void write (char [] cbuf)
```

写入字符数组的某一部分,off数组的开始索引,len写的字符个数

```java
abstract void write(char [] cbuf, int off, int len)
```

写入到字符串

```java
void write(String str)
```

写入字符串的某一部分,off字符串的开始索引,len写的字符个数

```java
void write (String str, int off ,int len)
```

刷新该流的缓冲

```java
void flush();
```

关闭此流,但要先刷新他

```java
void close();
```

flush方法和close方法的区别:

- flush:刷新缓冲区,流对象可以继续使用
- close:先刷新缓冲区,然后通知系统释放资源,流对象不可以 在被使用了

##### 使用try-catch_finally处理流中的异常

代码演示:

```java
import java.io.FileWriter;
import java.io.IOException;

public class demo03 {
    public static void main(String[] args) {
        FileWriter f = null;
        try {
            f = new FileWriter("A:\\java1\\8\\48.txt");
            f.write(98);
        } catch (IOException e) {
            System.out.println(e);
        } finally {
            if (f != null) {
                try {
                    f.flush();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }


    }
}

```

##### JDK7和JDK9流中异常的处理

JDK7的新特性

- 在try的后边可以增加一个(),在括号中可以定义流对象

- 那么这个流对象的作用域就在try中有效

- try中的代码执行完毕,会自动把

- 流对象释放不用写finally类了

格式:

```java 
try(定义流对象){

}catch(){

}
```

代码演示;

```java
import java.io.FileWriter;
import java.io.IOException;

public class demo04 {
    public static void main(String[] args) {

        try (FileWriter fw = new FileWriter("A:\\java1\\8\\77.txt")) {
            fw.write(99);
        } catch (IOException e) {
            System.out.println(e);
        }


    }
}

```

JDK9的新特性:

- try的前边可以定义流对象

- 在try后边的()中可以直接引入流对象的名称

- 在try代码执行完毕之后,流对象也可以释放掉,不用写finally

- ```java
  A a = new A();
  B b = new B();
  try(a,b){
  
  }cathch(){
  
  }
  ```

  

```java
import java.io.FileWriter;
import java.io.IOException;

public class demo05 {
    public static void main(String[] args) throws IOException {
        FileWriter fw = new FileWriter("D:\\java1\\8\\67.txt");
        try (fw) {
            fw.write(99);
        } catch (IOException e) {
            System.out.println(e);
        }


    }
}

```

## 属性集

##### 概述

java.util.Properties继承与Hashtable,来表示一个持久的属性集,它使用键值结构存储数据,每个键及其对应值都是一个字符串.该类也被许多Java类使用,比如获取系统属性是,System.ge,tproperties方法就是返回一个properties对象

##### Properties类

构造方法

创建一个空的属性列表

```java
public Properties()
```

##### 基本的存储方法

保存一对属性

```java
public Object setProperty(String key, String value)
```

使用此列表中指定的键搜索属性值

```java
public String getProperty(String key)
```

所有键的名称的集合

```java
public Set<String> stringPropertyNames()
```

可以把集合中的临时数据写入到硬盘中

```java
void store(OutputStream out, String comments)
```

```java
void store(Write write, String commments)
```

OutputStream字节输出流不能写中文

Write write 字符输出流 可以写中文

String comments 注释:用来解释说明保存的文件是干嘛用的 不能使用中文 一般使用空字符串

load方法 把硬盘保存的文件读取到内存中使用

```java
void load(InputStream inStream)
```

## 缓冲流

### 概述

缓冲流,也叫做高效流,是对4个基本FiileXxx流的增强,所以也是4个流的,按照数据类型分类:

- 字节缓冲流:BufferedIputStream,BufferedOutputStream
- 字符缓冲流BufferedReader,BufferedWriter
- 缓冲流的基本原理,是在创建流对象时,会创建一个内置的默认一个内置的默认大小的缓冲区数组,通过缓冲区读写,减少系统Io次数,从而提高读写的效率

### 字符缓冲流

构造方法

创建一个新的缓冲输入流

```java
public BufferedInputStream(InputStream in)
```

创建一个新的缓冲输入流

```java
public BufferedOutputStream(OutputStream out)
```

### 字节输出流

构造方法

创建一个新的缓冲输出流

```java
public BufferedOutputStream(OutputStream out)
```

创建一个新的缓冲输出流,以将具有指定缓冲区大小的数据写入到指定的底层输出

```java
ButteredOutStream(OutputStream out, int size)参数:
```

参数:

OutputStream out字节输出流

 我们可以传递FileOutStream,缓冲流会给FileOutputStream增加一个缓冲区,提高FileOutputStream的写入效率

int  size:指定缓冲流内部缓冲

去的大小,不指定就默认大小

###  字符缓冲流

构造方法

创建一个新的缓冲输出流

```java
public BufferedReader(Reader in)
```

创建一个新的缓冲输出流

```java
public BuffereddWriter(Writer out)
```

构造举例,代码如下

```java
//创建字符缓冲输入流
BufferedReader br = new BufferedReader(new FileReader(文件路径));
//创建字符缓冲输出流
BufferedWriter bw = new BufferedWriter(new FileWriter(文件路径));
```

构造方法

BufferedWriter(Writer out)使用一个使用默认大小输出缓冲区的缓冲字符输出流.

bufferedWriter(Writer out, int sz)创建一个给定大小输出缓冲区的新年缓冲字符输出流

参数;

Writer out字符输出流

我们可以传递

FileWriter,缓冲流会给File]Writer增加一个缓冲区,提高FileWriter的写入速度

int sz 指定缓冲区的大小,不写默认大小

#### **特有成员方法**

写入一个行分隔符.会根据不同的操作系统,获取不同的行分隔符

```java
void newLine()
```

#### 字符缓冲输入流

构造方法

​	BufferedReader(Reader in)创建一个使用默认大小输入缓冲字符输入流

​	BufferedReader(Reader in, int sz)创建一个使用指定大小输入缓冲区的缓冲字符输入流  

#### 特有的成员方法

读取一行文本

```java
String readLine()
```

## 转换流

##### **字符集charset**:也叫做编码表,是一个系统所支持的所有的字符的集合,包括各国文字,表单符号,图形符号,数字等.

![](C:\Users\Mi\Desktop\新建文件夹\Java\Img\流程\字符集.png)

 

- ASCII字符集
  - ASCII(American Standard Code for Information Interchange,美国信息交换标准代码)是基于拉丁字母的一套电脑编码系统,用于显示英语,主要包括控制字符(回车键 退格 换行键等)和可现实字符(英文大小写字符,阿拉伯数字和西文符号)
  - 基本的ASCII字符集,使用7为(bits)表示一个字符,共128字符,ASCII的扩展字符集使用8位(bits)表示一个字符,共256字符,方便支持欧洲常用字符
- ISO-8859-1字符集:
  - 拉丁码表,别名Latin-1,用于显示欧洲使用的语言,包括荷兰,丹麦,德语,意大利语,西班牙语等.
  - ISO-8859-1使用单字节编码,兼容ASCII编码
- GBxxx字符集
  - GB就是国标的意思,是为了现实中文而设计的一套字符集
  - **GB2312**简体中文码表.一个小于127的字符的意义与原来相同,但两个大于127的字符连在一起时.就表示一个汉字,这样大约可以组合乐包括7000多个简体汉字,此外数学符号.罗马希腊的字母.日文的假名们都编进入了,连在ASCII里本来就有的数字 标点 字母都统统重新编写了两个字节长的编码,这就是常说的"全角"字符,而原来在127号以下的那些就叫做"半角"字符了.
  - **GBK**最常用的中文编码表.是在G吧2标准基础上的扩展规范.使用了双字节编码方案,共收录了21003个汉字,完全兼容Gb2312标准,同时支持繁体汉字以及日韩字等
  - **GB18030**最新的中文码表.共收录文字70244个,采用多字节编码,每个字节可以有1个 2个 4个字节组成,支持中国国内少数的文字,同时支持繁体字以及日韩字等
- **unicode字符集**
  - Unicode编码系统为表达任意语言的任意字符而设计,是业界的一种标准,也称为统一码.标准万国码
  - 它最多使用4个字节的数字来表示每个字母 符号 或者是文字.有三种编码方案,UTF-8,UTF-16h和,UTF-32.最为常用的是,UTF-8编码
  - UTF-8编码,可以用来表示Unicode标准中任何字符,它是电子邮件,网页及其他存储传送文字的应用中,优先采用的拜编码.互联网工程工作小组(IETF)要求所有互联网协议都必须支持UTF-8编码,所以.我们开发web应用,也要使用UTF-8的编码,它使用一至四个字节为每个字节编码,编码规则:
    - 128个US-ASCII字符,只需一个字节编码
    - 拉丁文等字符,需要二个字节编码
    - 大部分常用字(含中文),使用三个字节编码
    - 其他极少使用Unicode辅助字符,使用四字节编码

##### InputStreamReader流

转换流java.io.InputStreamReader,是Reader的子类,是从字节流到字符流的桥梁,它读取字节并使用指定的字符集将其解码为字符,他的字符集可以由名称指定,也可以指定平台的默认字符集

构造方法

创建一个使用默认字符集的字符流.

```java 
InputStreamReader(InputStream in)
```

创建一个指定的字符集的字符流

```java
InputStreamReader(InputStream in,String charsetName)
```

参

##### OutputStreamWriter流

构造方法

创建使用默认字符编码的OutputreamWriter

```java
OutputStreamWriter (OutputStream out)
```

创建使用指定字符集的OutputStreamWriter

```java
OutputStreamWriter(OutputStream out, String charsetName)
```

参数:

OutputStream out 字节输出流,可以用来写转换之后的字节到文件中

String charsetName:指定的编码名称,不区分大小写,可以是utf-8/UTF-8,GBK/gbj不指定默认 utf-8

## 序列化流

##### 概述

Java提供了一种对象序列化的机制.用一个字节序列可以表示为一个对象,该字节序列包含该对象的数据,对象的类型和对象小红存储的属性等信息.字节序列化写道文件之后,相当于文件中持久保存了一个对象的信息.

反之,该字节序列还可以从文件中读取回来,重构对象,对它进行反序列化.对象的数据.对象的类型和对象中存储的数据信息,都可以用来在内存中创建对象.看图理解序列化:

![字符集](C:\Users\Mi\Desktop\新建文件夹\Java\Img\流程\字符集.png)

##### ObjectoutputStream类

java.io.ObjectOutputStream类,将Java对象的原始数据类型写到文件,实现对象的持久存储

构造方法

创建一个指定OutputStream的ObjectOutputStream.

```java
public ObjectOutputStream(OutStream out)
```

参数:

OutStream out 字节输出流

特有方法

将指定的对象写入ObjectOutput

void writeObject(Object obj)

##### ObjectInputStream类

ObjectInputStream反序列化流,将之前使用ObjectOutputStream序列化的原始数据和恢复为对象



创建一个类的时候需要类继承implements Serializable接口



构造方法

创建一个指定InputStream的ObjectInputStream

```java
public ObjectInputStream(InputStream in)
```

反序列化操作

读取一个对象

```java
public final Object readObject()
```

特有成员方法

从ObjectInputDStream读取对象 

```java
Object readObject()
```

##### 瞬态关键字

transient关键字

被transient修饰 的成员不能序列化

```java
private static final long serialVersionUID = 序列化号    ;
```

## 打印流

概述

平时我们在控制台打印输出,是调用print方法和println方法完成的,这两个方法都来自于java.io.printStream类,该类能够方便打印各种数据类型的值,是一种便捷的输出方式

##### PrintStream类

构造方法

使用指定的文件名创建一个新的打印流

```java
public printStream(String fileName)
```

特点

1. 只负责数据的输出,不负责数据的读取
2. 与其他输出流不同,永远不会抛出 IOException
3. 有特有的方法 print println

注意:

如果使用继承自父类的write方法写数据,那么擦好看数据的时候会查询编码表 97->a

如果自己特有的方法print println 写什么输出什么

可以改变输出语句的目的地(打印流的流向)

输出语句,默认在控制台输出

使用

重新分配"标准"输出流

```java
static void setOut(printStream out)
```

## 网络编程

##### 软件的结构

**c/s结构**:全称为Cilent/Server结构,是指客户端和服务器端的结构

**b/s结构**:全称为Browser/Server结构,是指浏览器和服务器结构

##### 网络通信协议

**网络通信协议**:通过计算机可以是多台计算机实现连接,位于同一个网络的计算机在进行连接和通信时需要遵守一定的规则,这就好比在道路中行驶的汽车要遵守交通规则一样,在计算机网络中,这些连接和通信的额规则被称为网络通信协议,他对数据的传输格式,传输速率,传输步骤等做了同一的规定,通信双方必须同时遵守才能完成数据交换.

**TCP/IP协议**:传输控制协议/因特网互联协议(Ttansmission Control Protocol / Internet Protocol)是Internet最基本.最广泛的协议,.它定义了计算机如何连接因特网,以及数据如何在他们自建传输的标准.它的内部包含一系列的用于处理数据通信的协议,并采用了4层模型,每一层都会呼叫他的 下一层所提供的协议来完成自己的需求.

![](C:\Users\Mi\Desktop\新建文件夹\Java\Img\流程\网络协议.png)

上图中,TCP/IP协议中的四层分别是应用层 传输层 网络层和链路层吗,每层分别负责不同的童子尿功能

链路层:链路层是用于定义物理传输道通道,通常是对某些网络连接的设备的驱动协议,例如光纤,网线提供的驱动

网络层:网络层是整个TCP/IP协议的核心,它主要用于将传输的数据进行分组,将分组数据发送到目标计算机或网络

运输层:主要使网络程序进行通信,在进行网络通信时.可以采用TCP/IP协议,也可以采用UDP协议

应用层:主要负责应用程序的协议,例如THHP协议,FTP协议等.

##### 协议分类

通信的协议还是比较复杂的,java.net包中包含的类和接口,它们提供低层次的通信细节.我们可以直接使用这些类和接口,来专注与网络程序的开发而不用考虑通信的细节

java.net包中提供了两种常见的网络协议的支持

- **UDP:**用户数据报协议(User Datagram Protocol) .UDP是无连接通信协议,即在数据传输时,数据的发送端和接收端不建立逻辑的联系.简单来说,当一台计算机向另外一台计算机发送数据时,发送端不会确认接收端是否存在,就会发出数据,同样接收端在收到数据时,也不会向发送端反馈是否所收到数据.

  由于使用UDP协议消耗资源小,用心效率高,所以通常会用于音频,shipin和饥饿普通数据的传输例如视频会议都会使用UDP协议,因为这种情况即使偶尔丢失一两个数据包,也不会对接收结果产生太大的影响

  但是在使用UDP协议传输数据时,由于UDP的面向无线连接性,不能保证数据的完整性,因此在传输重要数据时不建议使用UDP协议

特点:数据被限制在64kb以内,超出这个范围就不能发送了

数据报(Datagram)网络传输的基本单位

- **TCP:**传输控制协议(Transmission Control Protocol).TCP协议时面向连接的通信协议,即传输数据之前,在发送端和接收端建立逻辑连接,然后传输数据,他提供了两台计算机之间的无差错的数据传输

在TCP连接中必须明确客户端和服务端,由客户端向服务端发出连媒介请求,每次连接的创建都要经过三次握手

三次握手:TCP协议中,在发送数据的准备阶段,客户端与服务器之间的三次交互,以保证连接的可靠

- 第一次握手,客户端向服务器端发送连接请求,等待服务器确认
- 第二次握手服务器端向客户端回送一个相应,通知客户端收到了连接请求
- 第三次握手,客户端再次向服务器端发送确认消息,确认连接.

##### IP地址

**IP地址**:指互联网协议地址(Internet Protocol Address)俗称IP.IP地址用来给网络中的计算机设备做唯一的编号.

##### IP地址分类

- IPv4:是一个32位二进制的数,通常被分为4个字节,表示成a.b.c.d的形式,例如192.168.1.1其中a,b,c,d都是0~255之间的十进制的整数,南无最多可以表示42亿个
- IPv6:由于互联网的蓬勃发展,IP地址的需求量愈来愈大,但是网络四肢资源有限,使得IP的分配越发紧张.为了扩大地址空间,通过IPv6重新定义了地址空间,采用128位地址长度,每16个字节一组,分成8组十六进制数,表示成了1111:1111:1111:1111:1111:1111:1111:1111,号称可以位全世界的每一粒沙子编写一个网址这样就解决了网络地址资源数量不够的问题

##### 常用命令

查看本机IP地址,在控制台输入:

```
ipconfig
```

查看网络是否连通.,在控制台输入:

```
ping 空格 IP地址
Ping 220.181.57.216
```

##### 端口号

网络的通信,本质是两个进程的通信.每台计算机都有很多的进程,那么在网络通信时,如何区分这些进程呢?\

如果说IP地址可以唯一表示网络中的设备吗,那么端口号就可以标识设备中的进程了

- **端口号**:用两个字节表示的整数,他的取值范围时0~65535.其中,0-1023之间的端口号用于一些知名的网络服务和应用,普通的应用程序需要在1024以上的端口号.如果端口号被另外一个服务或应用所占用,会导致当前程序启动失败

利用协议+IP地址+端口号三元组合,就可以标识网络中的进程了,那么进程间的通信就可以利用这个标识与其它进程进行交互

## TCP通信程序

TCP通信能实现两台计算机之间的数据交互,通信的两端,要严格区分为客户端(Cilent)与服务器端(Server)

两端通信时步骤:

服务器端程序,需要实现启动,等待客户端的连接

客户端主动连接服务器端,连接成功才能通信.服务器端不可以主动连接客户端

在java中,提供了两个类用于实现TCP通信程序

1. 客户端:java.net.Socket类表示.创建Socket对象,向服务器发出请求,服务器端响应请求,两者建立连接开始通信
2. 服务端:java.net.ServerSocket类表示.创建ServerSocket对象,相当于开启一个服务,并等待客户端的连接

##### Socket类

Socket类 :该类实现客户端套接字,套接字指的是两台设备之间通讯的端点

构造方法

创建套接字对象并将其连接到指定主机上的指定端口号,如果指定的host时null,则相当于指定地址为回送该地址

```java
public Socket(String host, int port)
```

回送地址127.x.x.x是本机回送地址(Loopback Address)主要用于网络软件测试以及本地机进程间通信,无论什么程序,一旦使用回送地址发送数据,立刻返回,不进行任何网络传输 

成员方法

返回此套接字的输出流

```java
OutputStream getOutputStream()
```

返回此套接字的输入流

```java
InputStream getInputStream()
```

关闭套接字

```java
void close()
```

##### ServerSocket类

构造方法

创建绑定到特定端口的服务器套接字

```java
ServerSocket(int port)
```

服务器必须明确一件事情,必须知道是哪个客户端请求的服务器

所以可以使用accept方法互殴去到请求的客户端对象Socket

成员方法

侦听并接受到此套接字的连接

```java
Socket accept()
```

禁止此套接字的输出流

```java
shutdownOutput()
```

## 函数式接口

**概述**

函数式接口在Java中是指:有且只有一个抽象方法的接口

**格式:**
只要确保接口中有且仅有一个抽象方法即可

```java
修饰符	interface	接口名称{
public abstract 返回值类型 方法名称(可选参数信息);
//其他非抽象方法内容
}
```

注解@**FunctionalInterface**

作用:可以检测接口是否为函数式接口

​		是:编译成功

​		否:编译失败(接口中没有抽象方法抽象方法的格式大于1个)

##### 函数式接口的使用(作为参数使用)

代码实现

```java
//函数式接口

package 使用;

public interface demo01 {
public abstract  void show();
}

//实现类
package 使用;

public class demo01impl implements demo01{
    @Override
    public void show() {
        System.out.println("sxdksxkjkaskljasjklasdc");
    }
    //demo实现类 把实现类作为参数

}


//main方法
package 使用;

public class canshuceshi {
    public static void main(String[] args) {
        d(new demo01impl());
    }
    public static void d(demo01 d)
    {
        d.show();
    }
}


//使用lambda表达式
    d(()->{
            System.out.println("啦啦啦啦");
        });

//简化lambda表达式
d(()->System.out.println("啦啦啦啦"));
```

##### 函数式接口作为方法的参数

代码实现

```java
package lambda作为参数和返回值;

public class demo01 {
    public static void startThread(Runnable run) {
        new Thread(run).start();
    }

    public static void main(String[] args) {
        startThread(new Runnable() {
            @Override
            public void run() {
                System.out.println(Thread.currentThread().getName() + "启动线程");
            }
        });
        startThread(() ->
                System.out.println(Thread.currentThread().getName() + "启动线程"));
    }

}

```

##### 常用的函数式接口

JDk提供了大量的常用的函数式接口以丰富Lanbda的典型使用场景,他们主要在java.util.function包被提供

## Supplier接口

java.util.function.Suppiler<T>接口包含了一个无参数的方法:T get().用来获取一个泛型参数指定类型的对象数据.由于这是一个函数式接口.这也就意味着看对应的Lambda表达式需要对外提供一个符合泛型类型的对象数据

代码实例:

```java
package lambda作为参数和返回值;

import java.util.function.Supplier;

public class demo03 {
private static int getnum(Supplier<Integer> function)
{
    return function.get();
}

    public static void main(String[] args) {
        int a  = 1;
        int b  = 10;
        System.out.println(getnum(()->a+b));
    }
}

```



## Consumer接口

java.util.function.Consumer<T>正好与Supplier接口相反,他并不是生产一个数据,二十消费一个数据.其数据类型由泛型决定

**抽象方法​ accept: ​**

**默认方法 andThen;**

## Predicate接口

有时候我们需要对某种数据及逆行判断,从而得到一个Boolean值结果.这是可以用java.util.function.Predicate<T>接口

抽象方法:**test

**默认方法:and**

既然是条件判断,就会在与或非三种常见的逻辑关系,其中将两个Predict条件使用逻辑连接起来实现并且时,就可以使用default方法and

**默认方法:or**

与and的"与"类似,默认方法or实现逻辑关系中的"或"

只要由一个条件为true结果就是true 

**默认方法:negat   e**

非 取反

## Function接口

java.util.function.Function<T,R>接口用来根据一个类型的数据得到另一个类型的数据,前者为前置条件,后者为后置条件

**抽想方法:apply**

Function接口中最主要的抽象方法为R apply(T t),根据类型t二点参数获取类型R的结果

**默认方法:andThen**

## Stream流

**filter 过滤**

**forEach 消费接口**

**流式思想概述**

注意:请暂时忘记对传统IO流的固有印象

重要的是要什么,不是做什么

Stream流是一个来自数据元的元素队列

- 元素是特定类型的对象,形成一个队列.Java中的Stream并不会存储元素,而是按需计算
- 数据源流的来源.可以是计划金额,数组等

和以前的Collaboration操作不同,Stream操作还有两个基础的特征

- Pipelining:中间操作都会返回流对象本身.这样多操作可以串联成一个管道,如同流式风格(fluentstyle)这样做可以对操作进行优化,比如延迟执行(laziness)和短路(short-circuiting)
- 内部迭代:以前对集合遍历都是通过Iterator或者增强for的方式,显示的在集合外部进行迭代,这叫做外部迭代.Stream提供了内部迭代的方式,流可以直接调用遍历方法

当使用一个流的时候,通常包含三个步骤:获取一个数据源(source)->数据转换->执行操作获取想要的结果,每次转换原有Stram对象不改变,返回一个新的Stream对象(可以多次转换),这就允许对其操作可以向链条一样排列,变成一个通道

### 生成方式

Stream流的使用

- 生成流 
  - 通过数据源(集合,数组等)生成流
  - list.stream()
- 中间操作
  - 一个流后面可以跟随零个或者多个中间操作,其目的主要是打开流,做出某种程度的数据过滤/映射,然后返回一个新的流,交给下一个操作使用
  - filter()
- 终结操作
  - 一个流只能有一个终结操作,当这个操作执行后,流就被使用"光"了,无法再使用,所以这必定是流的最后一个操作
  - forEach()

Stream流的常见生成方式

- Collection体系的集合可以使用默认方法stream()生成流
  - default Stream<E> stream()
- Map体系的集合间接的生成流
- 数组可以通过Stream几口的静态方法of(T...value)生成流

```java

        //list集合
        ArrayList<String> list = new ArrayList<>();
        Stream<String> listStream = list.stream();

        //map集合
        HashSet<String> set = new HashSet<>();
        Stream<String> setStream = set.stream();

        //map集合
        Map<String, String> map = new HashMap<>();
        //键
        Stream<String> mapKeyStream = map.keySet().stream();
        //值
        Stream<String> mapValueStream = map.values().stream();
        //键值对
        Stream<Map.Entry<String, String>> entryStream = map.entrySet().stream();

        //数组
        String[] arr = {"Hello", "Java", "Loop"};
        Stream<String> arrStream = Stream.of(arr);
        Stream<String> stringStream = Stream.of("Hello", "Java", "Loop");
        Stream<Integer> intStream = Stream.of(10, 20, 30);
```

### 获取流

java.util.stream.Stream<T>是Java 8 新加入的最常用的流接口.(这并不是一个函数接口)

获取一个流非常简单,有下面几种常用的方法:

- 所有的Collection集合都可以通过stream默认方法获取流
- Stream就扣的静态方法of可以获取数组对应的流

### 常用方法

nums.stream().filter(num->num != null).cont().

​               创建                         转换                聚合

流模型的操作很丰富,这里介绍一些常用的API,这些方法可以被分为两种

- **延迟方法**:返回值类型依然是Stream接口自身类型的方法,因此支持链式调用.(除了中介方法外,其余方法均为延迟方法)
- **终结方法**:返回值类型不再是Stream接口自身类型的方法,因此不再支持类似StringBuilder那样的链式调用.终结方法包括coun和forEach方法

### 逐一操作:forEach

虽然方法名字叫forEach,但是与for循环中的"for-each"昵称不同

```java
void forEach(Consumer<? super T> action)
```

该方法接收一个Consumer接口函数,会将每一个流元素交给该函数进行处理

### 复习Consumer接口

```java
java.util.function.Consumer<T>接口是一个消费型接口
Consumer接口包含抽象方法void accept(T t),意思为消费一个指定泛型的数据
```

### 过滤:filter

可以通过filter方法将一个流转换成另一个子集流.

```java
Stream<T> filter (Predicate<? super T> predicate);
```

该接口接收一个Predicate函数式接口参数(可以是一个Lambda或方法引用)作为筛选条件

### 特点

Stream流属于管道流,只能被消费一次

### **映射:map**

如果需要将流中的元素映射到另一个流中,可以使用map方法

```java
<R> Stream<R> map(Function<? super T, ? extends R>mapper);
```

该接口需要一个Function函数式接口参数,可以将当前流中的T类型数据转换为另一种R类型的流

返回一个IntStream其中包含给函数应用用于此流的元素的结果

mapToInt(ToIntFunction mapper)

```
//转换数据案例 String->int
        list.stream().map(Integer::parseInt).forEach(System.out::println);
        list.stream().mapToInt(Integer::parseInt).forEach(System.out::println);
```

### 求和

```java
   int sum = list.stream().mapToInt(Integer::parseInt).sum();
        System.out.println(sum);
```



### 复习Function接口

此前我们已经学习过java.util.stream.Function函数式接口,其中唯一的抽象方法为

```java
R apply(T t)
```

这可以将一种T类型转换为R类型,而这种转换的动作,就成为"映射";

### 统计个数:count

正如旧集合Collection当中的size方法一样,流提供count方法来数一数其中的元素个数

```java
long count();
```

该方法返回一个long值代表元素个数(不在像就集合那样是int值)

### 取用前几个:limit

limit方法可以对流进行截取,只取用前n个

```java
Stream <T> limit (long maxSize)
```

### 跳过前几个:skip

如果希望跳过前几个元素,可以使用skip方法获取一个截取子厚的新流

```java
Stream<T> skip(long n)
```

### 组合:concat

如果有两个流,希望合并成为一个新的流,那么

可以使用Stream接口的静态方法concat

```java
static <T> STream concat (Stream<? extends T> a, Stream<? extends T>b)
```

备注:这是一个惊天方法,与java,lang,Stream当中的concat方法是不同的

### 组合:不重复

合成流并且去除重复

```java
Stream.concat(limit, skip).distinct().forEach(System.out::println);
```

### 排序

```java
//按照字母顺序排列输出
        list.stream().sorted().forEach(System.out::println);
        //按照母长度输出
        list.stream().sorted((s1, s2) ->
                {
                    int num = s1.length() - s2.length();
                    int num2 = num == 0 ? s1.compareTo(s2) : num;
                    return num2;
                }
        ).forEach(System.out::println);
```

### 收集流的操作

对数据使用Stream流的方式操作完毕后,我想把流中的数据收集到集合中,该怎么办呢?

- R collect(Collector collector)



```java
public class demo8 {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        list.add("林青霞");
        list.add("周杰伦");
        list.add("张杰");
        list.add("张无忌");
        list.add("可乐");
        list.add("雪碧");

        //list
        Stream<String> stringStream = list.stream().filter(s -> s.length() == 3);
        List<String> collects = stringStream.collect(Collectors.toList());
        for (String collect : collects) {
            System.out.println(collect);
        }

        //set
        Set<Integer> set = new HashSet<>();
        set.add(10);
        set.add(20);
        set.add(30);
        set.add(40);
        set.add(50);

        Stream<Integer> setStream = set.stream().filter(age -> age > 25);
        Set<Integer> collect = setStream.collect(Collectors.toSet());
        for (Integer integer : collect) {
            System.out.println(integer);
        }

        //map
        String[] strArr = {"张杰,30", "刘晓,39", "王祖贤,25"};
        Stream<String> arrStream = Stream.of(strArr).filter(s -> Integer.parseInt(s.split(",")[1]) > 28);
        Map<String, Integer> collect1 = arrStream.collect(
                Collectors.toMap(
                        s -> s.split(",")[0],
                        s -> Integer.parseInt(s.split(",")[1])
                )
        );
        Set<String> keys = collect1.keySet();
        for (String string : keys) {
            Integer value = collect1.get(string);
            System.out.println(string + "," + value);
        }
    }
}
```

## 方法引用

### 方法引用符号

双冒号**::**为引用运算符,**而他所在的表达式被称为方法引用**.如果Lambda要表达的函数方案已经存在与某个方法的实现中,那么则可以通过双冒号来引用该方法作为Lambda的替代者

### 语义分析

System.out对象中有一个重载的println(String)方法签好就是我们需求的.那么对于printString方法函数式接口参数,对比下面两种写法

- Lambda表达式写法:s -> System.out.println(S)
- 方法引用写法:System.out::println

第一种语义是指,拿到参数之后经Lambda之手,继承传递给System.out.println方法去处理

第二种等效写法的语义是指,直接让System.out中的println方法来取代Lambda.两种写法的执行效果完全不同,而第二种方法引用的写法复用了已有方案,更加简洁

注意:Lambda传递的参数一定是方法引用中的那个可以接收的类型,否则会抛出异常

//定义接口 

```java
public interface demoi {
    void print(String s);
}

```

//转换为大写方法

```java
public class zahunhaun {
    public void sayDa(String s)
    {
        System.out.println(s.toUpperCase());
    }
}

```

//定义测试类

```java
public class ceshi {
    public static void printString(demoi d)
    {
        d.print("Heelo World");
    }

    public static void main(String[] args) {
        zahunhaun zh = new zahunhaun();
        printString(zh::sayDa);
    }
}

```

### 通过类名称引用静态方法

//接口

```java
public interface demoi {
    int print(String s);
}

```

//定义静态类

```java
package abs;

public class absnum1 {
    public static void sa(int a)
    {
        System.out.println(Math.abs(a));
    }
}
```

//main方法

```java
package abs;

import java.util.Calendar;

public class ceshi {
    public static  int d(int num, jk c){
        return c.absNum(num);
    }

    public static void main(String[] args) {
        absnum1 a= new absnum1();
       int number = d(-78,(n)->{
            return Math.abs(n);
        });
        System.out.println(number);
        System.out.println(d(-89,Math::abs));
    }
}

```

### 通过super引用成员方法

如果存在继承关系,当Lambda中需要出现super调用时,也可以使用方法引用进行代替. 

//接口

```java
package superq;

public interface jiekou {
    void say();
}

```

//父类

```java
package superq;

public class fu {
    public  void sayHello()
    {
        System.out.println("你好,我是爸爸");
    }
}

```

//子类测试类

```java
package superq;

public class zi extends fu {
    @Override
    public  void sayHello(){
        System.out.println("你好,握手儿子");
    }
    public static void mythod(jiekou j)
    {
        j.say();
    }
  public void show()
  {
      mythod(super::sayHello);

  }

    public static void main(String[] args) {
        new zi().show();
    }
}

```



### 类的构造器引用

由于构造器的名称与类名完全不一样,并不固定,所以构造器引用使用**类名称::new**的格式表示,

### 数组的构造器引用ASy

数组也是Object的子类对象,所以具有构造器,只是语法不同.如果对应到Lambda的场景中时,组要一个函数式接口

//接口

```java
package 数组构造;

public interface jiekou {
    int [] Arr(int lenght);
}

```

//定义demo

```java
package 数组构造;

public class demo {
    public static int[] Array(int len, jiekou j) {
        return j.Arr(len);
    }

    public static void main(String[] args) {
      /*int[] a =  Array(5, ((len) -> {
            return new int[len];
        }));*/
        int[] a = Array(10, int[]::new);
        System.out.println(a.length);
    }
}

```

## Junit测试

### 测试分类

- 黑盒测试  不需要写代码
- 白盒测试  需要写代码

### Hunit使用:白盒测试

1. 定义一个测试类(测试用例)
   1. 建议:
      1. 测试类名:被测试的类名Test  加类名
      2. 包名 xxx.xxx.xx.xx.test
2. 定义测试方法:可以独立运行
   1. 建议:
      1. 方法名:test 测试的方法名
      2. 返回值: void
      3. 参数列表 :无参数
3. 给方法加@Test
4. 导入Junit环境



断言:Assert.assertEquals(期待数据,真实数据)

### 初始化方法

用于资源的申请

```java
@Befor
public void init(){

}
```

### 释放资源方法

在所有的测试方法执行完后都会自动执行该方法

```java
@After
public void Close(){

}
```

## 反射:框架设计的灵魂

框架:半成品软件.可以在框架的基础上进行软件开发,简化编码

反射:将类的各个组成部分封装为其他对象,就是反射机制

好处:

1. 可以在程序运行过程中,操作这些对象
2. 可以解耦,提高程序的可扩展性

**获取class对象的方式:**

1. Class.forName("全类名");将字节码文件加载到内存,返回Class对象
2. 类名.Class:通过类名的属性class获取
3. 对象.getClass();getClass()方法在Object类中定义着

### Class对象

对象对象获取所有public修饰的成员变量

```java
Field[] getFields():
```

获取指定名称的public修饰的成员变量

```java
Field[] getField(String name)
```

获取所有的成员变量,不考虑修饰符

```java
Field[] getDeclaredFields()
```

获取指定的成员变量

```java
Field[] getDeclaredField(String name)
```

 设置值

```java
set();
```

获取值

```java
get()
```

暴力反射 用于设置为私有的

```java
setAccessible(true)
```

### 获取构造方法

获得公共的构造方法

```java
Constructor<?> [] getConstructors()
```

获得单个

```java
Constructor<T> getDeclaredConstructor(类<?>...parameterTypes)
```

获得单个 公共

```java
Constructor<T> getConstructor(类<?>...parameterTypes)
```

获得所有的构造方法

```java
Constructor <?> [] getDeclaredConstructors()
    参数:
你要获取构造方法的参数个数和数组数据类型对应的字节码文件对象
```

### 获取成员方法

```java
Method[] getMethods()
```

```java
Method getMethod(String name,类<?>...parameterTypes)
```

```java
Method[] getDeclaredMethods()
```

```java
Method getDeclaredMethod(String name,类<?>...parameterTypes)
```

### 获取类名

```java
String getName()
```

### Constructor方法介绍

新建实例

```java
Object newInstance()
```



## 枚举

- 枚举类的理解:类的对象只有有限个,确定的我们称之为枚举类
- 当需要定义一组常量时,强烈建议使用枚举类
- 如果枚举类中只有一个对象,则可以作为作为单利模式的实现方式

### 定义

- JDK5.0 之前,自定义枚举类
- JDK5.0 可以使用enum关键字定义枚举类

代码1

```java
package cn.doudou.java;

/**
 * Create By 王嘉浩
 * Time 2021/9/29 11:22
 */
public class SeasonTest {
    public static void main(String[] args) {
        System.out.println(Season.SUMMER);
    }
}


//自定义枚举类
class Season {
    //声明对象的属性
    private final String seasonName;
    private final String seasonDesc;

    //私有化类的构造器
    private Season(String seasonName, String seasonDesc) {
        this.seasonDesc = seasonDesc;
        this.seasonName = seasonName;
    }

    public static final Season SPRING = new Season("春天", "春暖花开");
    public static final Season SUMMER = new Season("夏天", "夏日炎炎");
    public static final Season AUTUMN = new Season("秋天", "秋高气爽");
    public static final Season WINTER = new Season("冬天", "冰天雪地");

    @Override
    public String toString() {
        return "Season{" +
                "seasonName='" + seasonName + '\'' +
                ", seasonDesc='" + seasonDesc + '\'' +
                '}';
    }
}
```

代码2

```java
package cn.doudou.java;

/**
 * Create By 王嘉浩
 * Time 2021/9/29 11:43
 */

public class SeasonTest1 {
    public static void main(String[] args) {
        System.out.println(Season.SUMMER);
    }
}


//自定义枚举类
enum  Season1 {

    SPRING ("春天", "春暖花开"),
    SUMMER ("夏天", "夏日炎炎"),
    AUTUMN ("秋天", "秋高气爽"),
    WINTER ("冬天", "冰天雪地");

    //声明对象的属性
    private final String seasonName;
    private final String seasonDesc;

    //私有化类的构造器
    private Season1(String seasonName, String seasonDesc) {
        this.seasonDesc = seasonDesc;
        this.seasonName = seasonName;
    }



}
```

### 常用方法

- values() 返回枚举类型的对象数组.该方法可以很方便的遍历所有的枚举值
- valuesOf(String str) 可以把一个字符串转为对应的枚举对象类对象 要求字符串必须是枚举类对象的"名字"如果不是 会有运行异常
- toString() 返回当前枚举类对象常量的名称

## 注解

**概念:**给计算机看的,说明程序的

**注释**:用程序描述程序的.给程序员看的

概述描述:

- JDK1.5之后的特性
- 说明程序的
- 使用注解:@注解名称

作用分类:

- 编写文档:通过代码里标识的元数据生成的文档[生成文档doc文档]
- 代码分析:通过代码里标识的元数据对代码进行分析[使用反射]
- 编译检查:通过代码里的元数据让编译器能够实现基本的编译检查[Override]

JDk中预定的一些注解

@Override 检测被该注解标注的方法是否继承父接口

@Deprecated 该注解标识的的内容已经过时

@SuppressWarnings 压制警告

​	一般参数传递@SuppressWarnings("all")

自定义注解

格式

元注解

public @interface 注解名{}

属性:接口中可以定义的内容 成员方法

要求:

- 属性的返回值类型
  - 基本数据类型
  - String
  - 枚举
  - 注解  
- 定义了属性,在使用时需要给属性赋值
  - 定义属性时,使用default关键字给属性默认初始化值,则使用注解时,可以不进行属性的赋值
  - 如果只有一个属性需要赋值,并且属性的名称时value,则value可以省略,直接写值就可以了
  - 数组赋值时,值使用{}包括

元注解

@Targer 描述注解能够作用的位置

@Retention  描述注解被保留的阶段 

@Documented  描述注解是否被抽取到api文档中



### 注解以后在学

## JavaGUI

构造方法

构造一个新的,最初不可见的,具有指定标题的Frame对象

```java
Frame(String name)
```

设置可见

```java
setVisible(true);
```

设置宽高

```java
srtsize(int a,int b)
```

设置距离窗口多少

```java
setLocation(int a, int b)
```

创建一个按钮

```java
直接new button Jbutton
```

添加到窗体中

```java
add()
```

设置窗体的布局

```java
setLayout()
```

事件监听机制

**以后再学 不重要**

## JDBC

**驱动管理对象**

```java
DriverManager
```

​	**功能：**

1. 注册驱动
2. 获取数据库连接

mysql 5 之后的驱动jar包可以省略注册驱动的步骤

**数据库连接对象**

```java
Connection
```

**获取数据库的连接**

方法：static Connection getConnection（String URL，String user，String password）

参数

**url**：指定连接的

​	语法：jdbc ： mysql ：//ip地址：端口号/数据库名称

​	细节:如果连接的是本机的mysql服务器,并且mysql服务器的默认端口是3306,可以简写 ip和端口号可以不写

**user**：用户名

**passworld**：密码

**执行SQL对象**

**功能**

获取执行sql对象

```java
statement createStatement()

PreparedStateement prepareStatement(String sql)
```

**管理事务**

开启事务 

```java
void setAutoCommit(boolean autoCommit) 参数flase 开启
```

提交事务

```java
Commit()
```

回滚事务

```
rollback()
```

**执行sql的对象**

```java
Statement
```

执行sql 

```java
boolean execute (String sql) 了解
int executeUpdate(String sql) 掌握 执行DML语句DDl语句  返回值 影响的行数
ResuilSet executeQuert(String sql):执行DQL语句(select)
 
```

**结果集对象**

```java
ResultSet
```

游标向下移动一行

```java
next()
```

获取数据

```java
getxxx()   xxx代表数据
```

**执行SQl的对象**

```java、
PrepqredStatement
```

**sql注入问题**:

在拼接SQL时有一些SQL的特殊关键字参与字符串的拼接.会造成安全性问题

解决sql注入问题:PrepqredStatement

预编译的sql:参数使用?作为占位符

### JDBC连接池

Spring JDBC :JDBC Template

-  C3P0:数据库连接池技术
- Druid:数据库连接池实现技术,由阿里巴巴提供的

标椎接口

标椎接口:DataSource 

方法:

获取连接:getConnection()

归还连接 Connection.close()

### Druid

​     和c3p0操作一样

Spring JDBC

步骤

1. 导入jar包

2. 创建 对象.依赖于数据源DataSource

3. 调用JdbcTemplate的方法来完成CRUD的操作

   执行DML的语句.增删改查

   ```java
   UPdate()
   ```

   查询结果将结果封装为Map集合

   ```java
   queryForMap()
   ```

   查询结果将结果集封装为list集合

   ```java
   queryForList()
   ```

   查询结果,将结果封装为JavaBean对象

   ```java
   query()
       Java提供的封装对象
        new BeanPropertyRowMapper<EMP>(EMP.class)
   ```

   查询结果,将结果封装为对象

   ```
   queryForobject()
   ```


## 接口组成部分

接口的组成

- 常量
  - public static final
- 抽象方法
  - public abstract
- 默认方法(Java 8 )
- 静态方法(Java 8 )
- 私有方法(Java 9 ) 

### 接口中的默认方法

接口中的方法使用default进行修饰,背的实现类也不会报错,也可以让别的类继承进行实现,可以更好避免代码的重复

### 接口中的静态方法

**静态方法只可以被接口调用 不可以被实现类调用**

**public可以省略,static不能省略**

格式:

```java
public static 返回值类型 方法名(参数列表){}
```

范例:

```java
public static void show(){}
```

### 接口中私有方法

格式1:

```java
private 返回值类型 方法名(参数列表){}
```

范例2:

```java
private void show(){}
```

格式2:

```java
private static 返回值类型 方法名(参数列表){}
```

范例2:

```java
private sttaic void method(){}
```







最新

https://www.bilibili.com/video/BV1Bg4y1q7q2?p=291





# 版权

**Create File By Wang Jia Hao 2019-2021**

