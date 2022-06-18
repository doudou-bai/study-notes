# JS高级

## 面向对象

- 面向过程 <font color='#f7acbc'>POP</font>
- 面向对象 <font color='#f7acbc'>OOP</font>

思维特点:

1. 抽取(抽象)对象公用的属性和行为组织(封装)成一个类(模板)
2. 对类进行实例化,获取类的对象

## 对象

在JavaScript中,对象是一组无序的相关属性和方法的结合,所有的事物都是对象,例如字符串,数组,数值,函数等'

对象是由属性和方法组成的

- 属性:事物的特征,在对象中用属性来表示(常用名词)
- 方法:事物的行为,在对象中用方法来表示(常用动词)

## 类

在ES6中新增加了类的概念,可以使用class关键字声明一个类,之后以这个类来实例化对象

类抽象了对象的公共部分,他泛指某一大类(class)

### 创建类

**语法:**

```javascript
class name {
	// class body
}
```

**创建实例化**

```javascript
var xx = new name()
```

<font color='orange'>注意:类必须进行实例化</font>

### 类constructor构造函数

constructor()方法是类的构函数(默认方法),用于传递参数,返回实例对象,通过new命令生成对象实例时,自动调用该方法.如果没有显示定义,类内部会自动给我们创建一个constructor()

**实例:**

```javascript
//创建类
    class Star {
      constructor(uname, age) {
        this.uname = uname;
        this.age = age;
      }
    }
    //实例化对象
    var ldh = new Star("刘德华", 18);
    var zxy = new Star("张学友", 25);
```

###  类中添加方法

**语法:**

```java
class Star {
      constructor(uname, age) {
        this.uname = uname;
        this.age = age;
      }
      //方法
      say() {
        console.log(this.uname + "您好!");
      }
    }
```

### 类的继承

 **实例:**

```java
 //1.类的继承
    class Father {
      constructor() {

      }
      money() {
        console.log(100);
      }
    }
    //2.子类
    class Son extends Father {

    }
    var son = new Son();
    son.money()
```

### super关键字

super关键字用于访问和调用对象父类上的函数.可以调用父类的构造函数,也可以调用父类的普通函数

**实例:**

```java
class Father {
      constructor(x, y) {
        this.x = x
        this.y = y
      }
      sum() {
        console.log(this.x + this.y);
      }
    }
    class Son extends Father {
      constructor(x, y) {
        super(x, y);
      }
    }
    var son = new Son(10, 30)
    son.sum();
```

**注意点**

1. 在ES6中类没有变量提升,所以必须先有类,才能通过类实例化对象   
2. 类里面的共有的属性和方法一定要加<font color='#f7acbc'>`this`</font>使用
3. 类里面的`this`指向问题
4. constructor里面的this指向实例问题,方法里面的this指向这个方法的调用者

## 构造函数

构造函数是一种特殊的函数,主要用来初始化对象,即为对象成员变量赋初始值,它总与new一起使用.我们可以把对象中一些公共的属性和方法抽取出来,然后封装到这个函数里面.

在JS中,实用构造函数时要注意以下两点:

1. 构造函数用于创建某一类对象,首字母要大写
2. 构造函数要和new一起使用才有意义

new在执行时会做四件事情:

1. 在内存中创建一个新的空对象
2. 让this指向这个新的对象
3. 执行构造函数里面的代码,给这个新对象添加属性和方法
4. 返回这个新对象(所以构造函数里面不需要`return`)

##  实例成员

1. 实例成员就是构造函数内部通过`this`添加的成员
2. 实例成员只可以通过实例化对象进行访问

## 静态成员

1. 在构造函数本身上添加的成员 
2. 静态成员只能通过构造函数来访问  

## 构造函数的问题

构造函数方法很好用,但是存在浪费内存的为问题

## 构造函数原型prototype 

1. 构造函数通过按进行分配的函数是所有对象所共享的 
2. JavaScript规定,每一个构造函数都有一个prototype属性,指向另一个对象.注意你这个prototype就是一个对象,这个对象的所有属性和方法,都会被构造函数所拥有

**示例:**

```
对象.prototype.函数名字 = function() {}
```

**问答?**

1. 原型是什么?

   一个对象,我们也称为prototype为原型对象

2. 原型的作用是什么?

   共享方法

## 对象原型`_proto_`

对象都会有一个属性`_proto_`指向构造珊瑚的prototype原型对象,之所以我们对象可以使用构造函数prototype原型对象的属性和方法,就是因为对象有`_proto_`原型的存在

## 扩展内置对象

可以通过原型对象,对原理的内置对象进行扩展自定义的方法,比如给数组增加自定义求偶数和的功能

 **实例代码:**

```javascript
 Array.prototype.sum = function () {
      var sum = 0;
      for (let index = 0; index < this.length; index++) {
        sum += this[index];
      }
      return sum;
    }

    var arr = [1, 2, 3]
    console.log(arr.sum());
```

## 继承

 ES6之前并没有给我们提供extends继承.我们可以通过构造函数
+原型对象模拟实现继承,被称为组合继承

### call()

调用这个函数,并且修改函数运行时的this指向

```javascript
fun.call(thisArg,arg1,arg2,....)
```

- thisArg:当前调用函数this的指向对象 
- arg1,arg2:传递的其他参数

**代码实例 -调用方法**

```javascript
 // call方法
    function fn() {
      console.log("我想赚钱!");
    }
    //原始调用方法
    // fn();
    //call()调用函数
    fn.call();
```

**代码实- 改变this指向**

```javascript
// call方法
    function fn() {
      console.log("我想赚钱!");
      console.log(this);
    }
    var o = {
      name: 'andy'
    }
    //改变this指向
    fn.call(o);
```

##  借用父类构造函数继承属性

```javascript
//父构造函数
    function Father(uname, age) {
      // this指向父构造函数的实例
      this.uname = uname;
      this.age = age;
    }
    //子构造函数
    function Son(uname, age) {
      // this指向子构造函数的实例
      Father.call(this, uname, age);
    }
    var son = new Son("刘德华", 18);
    console.log(son);
```

## 借用原型对象继承方法

```javascript
    //父构造函数
    function Father(uname, age) {
      // this指向父构造函数的实例
      this.uname = uname;
      this.age = age;
    }
    Father.prototype.money = function () {
      console.log(1000000);
    }
    //子构造函数
    function Son(uname, age) {
      // this指向子构造函数的实例
      Father.call(this, uname, age);
    }
    //实例化Father赋值给自类的原型对象
    Son.prototype = new Father();
    // 如果利用对象的形式修改了原型对象,别忘了利用constructor指回原来的构造函数
    Son.prototype.constructor = Son;
    Son.prototype.exam = function () {
      console.log("孩子要考试！");
    }
    var son = new Son("刘德华", 18);
    console.log(son);
    console.log(Father.prototype);
    console.log(Son.prototype.constructor);
```

## ES5新增方法概述

- 数组方法
- 字符串方法
- 对象方法

### 数组方法

**迭代(遍历)方法:**

- forEach() 

  ```javascript
  array.forEach(function(currentValue,index,arr){})
  ```

- map()  

- filter()

  ```javascript
  var arr = [1, 56, 45];
      var newArr = arr.filter(function (value, index, arr) {
        return value >= 20;
      })
      console.log(newArr);
  ```

- some()

  ```javascript
   var arr = [10, 30, 4];
      var newArr = arr.some(function (v, index) {
        return v >= 20;
      })
      console.log(newArr);
  ```

- every() 

## 函数进阶

###  函数的定义方法

1. 函数声明方式dunction关键字(命名函数)
2. 函数表达式(匿名函数)
3. new Function()  

###  函数的调用方式

1. 普通函数
2. 对象的方法
3. 构造函数
4. 绑定事件函数
5. 定时器函数
6. 立即执行函数

###  函数内的this的指向

这些this的指向,是当我们调用函数的时候确定的.调用方式的不同确定了this的指向不同一般指向我们的调用者

| 调用方式     | this指向                                  |
| ------------ | ----------------------------------------- |
| 普通函数调用 | window                                    |
| 构造函数调用 | 示例对象 原型对象里面的方法也指向实例对象 |
| 对象方法调用 | 该方法所属对象                            |
| 事件绑定方法 | 绑定事件对象                              |
| 定时器函数   | window                                    |
| 立即执行函数 | window                                    |

**改变this的指向**

1. call()

   ```
   fun.call(this,arg1,arg2,....)
   ```

2. bind()

3. apply()

   ```
   fun.apply(thisArg,[argsArray])
   ```

   

### 严格模式

**什么是严格模式?**

JavaScript除了提供正常模式外,还提供了严格模式(strictmode).ES5的严格模式是采用具有限制性

JavaScript变体的一种方式,即在严格的条件下运行JS代码

严格模式在IE10以上版本的浏览器才会被支持,旧版本浏览器会被忽略

严格模式对正常的JavaScript语义做了一些更改:

1. 消除了JavaScript语法的一些不合理,不严谨之处,减少了一些怪异的行为
2. 消除代码运行的一些不安全之处,保证代码运行的安全
3. 提高编译期效率,增加运行速度
4. 禁用了在ECMAScript的未来版本中可能会定义的一些语法,为未来版本的JavaScript做好铺垫.比如一些保留字如:`class`  `enum`  `export`  `extends`  `import`  `sduper`不能做变量名

#### 开启严格模式

严格模式可以应用到整个脚本或个别函数中.因此在使用时,我们可以将严格模式分为脚本开启严格模式和为函数开启严格模式两种情况

1. 为脚本开启严格模式

   ```
   为整个脚本文件开启严格模式,需要在所有语句之前放一个特定语句 "use strict" ; (或 'use strict' ;).
   ```

   ```javascript
   <!-- 为整个脚本开启严格模式 -->
     <script>
       'use strict';
       //下面JS代码就是按照严格模式进行执行;
     </script>
     <script>
       (function () {
         'use strict';
       })();
     </script>
   ```

2.  为函数开启严格模式

   ```
   要给某个函数开启严格模式,需要把'use strict' ; (或 "use strict" ;) 声明放在函数体所有语句之前
   ```

#### 严格模式的变化

严格模式对JS的语法和行为,都做了一些改变

##### 变量规定

1. 在正常模式中,如果一个变量没有声明就赋值,默认就是全局变量.严格模式禁止这种用法,变量都必须先用var 命令进行声明,然后在使用 
2. 严禁删除已经声明的变量.例如,delete x;语法是错误的.

##### 严格模式下this的指向问题

1. 以前在全局作用域函数中的this指向window对象
2.  <font color='#f7acbc'>在严格开模式下全局作用与中的this是undefined</font>
3. 以前构造函数时不加new也是可以调用,当普通函数,this指向全局对象
4. 严格模式下,如果构造函数不加new 调用,this会报错
5. new实例化的构造函数指向创建的对象实例
6. 定时器this还是指向window
7. 事件 对象还是指向调用者

##### 函数变化

1. 函数不能有重名的参数
2. 函数必须声明在顶层,新版本的JS会引入"块级作用域"(ES6中已引入) 为了 与新版本接轨 不允许在非函数的代码块内声明函数 

## 高阶函数

高阶函数是对其他函数进行操作的函数,他<font color='#f7acbc'>接收函数作为参数</font>或将<font color='#f7acbc'>函数作为返回值</font>输出

```javascript
//高阶函数
    function fn(a, b, callback) {
      console.log(a + b);
      callback && callback();
    }
    fn(1, 2, function () {
      console.log("测试回调函数");
    });
```

## 闭包

### 变量作用域

变量根据作用域的不同分为两种:全局变量环和局部变量

1. 函数内部可以使用全局变量
2. 函数外部不可以使用局部变量 
3. 当函数执行完毕,本作用域内的局部变量会销毁  

### 闭包

闭包(closure)指有权访问另一个函数作用域中变量的函数

**闭包的主要作用**

<font color='#f7acbc'>延伸了变量的作用范围</font>

### 闭包案例

```javascript
  <ul class="nav">
    <li>榴莲</li>
    <li>臭豆腐</li>
    <li>鲱鱼罐头</li>
    <li>大猪蹄子</li>
    <li>麻辣烫</li>
    <li>面条</li>
  </ul>
  <script>
    var lis = document.querySelector(".nav").querySelectorAll('li');
    for (let index = 0; index < lis.length; index++) {
      //利用for循环创建了4个立即执行的函数
      (function (i) {
        lis[index].onclick = function () {
          console.log(i);
        }
      })(index);
    }
  </script>
```

### 循环中的定时器

```javascript
 <ul class="nav">
    <li>榴莲</li>
    <li>臭豆腐</li>
    <li>鲱鱼罐头</li>
    <li>大猪蹄子</li>
    <li>麻辣烫</li>
    <li>面条</li>
  </ul>
  <script>
    var lis = document.querySelector(".nav").querySelectorAll('li');
    for (let index = 0; index < lis.length; index++) {
      (function (i) {
        setTimeout(function () {
          console.log(lis[i].innerHTML);
        }, 3000)
      })(index)
    }
  </script>
```

### 打车价格

```javascript
<script>
    /*
    闭包案例-3 打车价格
    打车起步13(3公里内) 之后每公里多收5元
    如果有拥堵情况 会多收取10元拥堵费
    */
    var car = (function () {
      //起步价
      var start = 13;
      //总价
      var total = 0;
      return {
        //正常总价
        price: function (n) {
          if (n <= 3) {
            total = start;
          } else {
            total = start + (n - 3) * 5
          }
          return total;
        },
        //拥堵费用
        yd: function (flag) {
          return flag ? total + 10 : total;
        }
      }
    })();
    //调用函数
    console.log(car.price(5));
    console.log(car.yd(true));
  </script>
```

## 递归

### 什么是递归？

如果一个函数在内部可以调用其本身,那么这函数就是递归函数 

### 递归求n的阶乘

```javascript
function fn(i) {
      if (i == 1) {
        return 1;
      }
      return i * fn(i - 1)
    }
    console.log(fn(10));
```

 

## 正则表达式

### 什么是正则表达式

正则表达式(Regular Expression) 是用于匹配字符串中字符的模式.在JS中,正则表达式也是对象

### 特点

1. 灵活点,逻辑性和功能性非常的强
2. 可以迅速的用极其简单的方式达到字符串的复杂控制  
3. 对于刚接触的人来说,比较晦涩难懂 

### 创建正则表达式

 在JavaScript中,可以通过两种方式创建一个正则表达式

1. 通过调用RegExp对象的构造函数创建

   ```javascript
   var 变量名 = new RegExp(/表达式/);
   ```

2. 通过字面量创建 

   ```javascript
   var 变量名 = /123/;
   ```

### 测试正则表达式

test()正则对象方法,用于检测字符串是否含有该规则,该对象会返回true或false,其参数是测试字符串 

```javascript 
regexObj.test(str)
```

1. regexObj 是写的正则表达式
2. str 是要检测的文本
3. 就是检测str文本是否符合我们写的正则表达式规范

