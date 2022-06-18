# ECMAScript6

## 什么是ECMAScript6

ECMAScript6.0(简称ES6) 是JavaScript语言的下一代标准,2015年6月正式发布.它的目标,是使得JavaScript可以编写复杂的大型应用程序,成为企业级的开发语言.

## 基本语法

- es6定义变量

```javascript
//let有作用域 let只可以声明一次
let a = 1;
//var 全局都可以使用 var可以声明多次
var b = 2;
```

- const声明常量(只读变量) 不可以改变 必须初始化操作 否则报错

```javascript
const a = 1;
```

- 解构赋值

```javascript
let a = 1, b = 2, c = 3
console.log(a, b, c);
//es6
let [x, y, z] = [1, 2, 3]
console.log(x, y, z);
//对象
let user = { name: "Admin", age: 12 }
//传统
let name1 = user.name
let age1 = user.age
console.log(name1, age1);
//es6
let { name, age } = user;
console.log(name, age);
```

- 模板字符串

```javascript
 let name = "Admin"
    let age = 12

    let info = `My Name is ${name},
     Age is ${age + 8}`
    console.log(info);
```

- 定义对象

```java
 	 //传统
    const name = "Admin"
    const age = 20
    const user1 = { name: name, age: age }
    console.log(user1);
    //es6
    const user2 = { name, age }
    console.log(user2);
```

- 对象扩展运算符

```javascript
    let persion1 = { name: "Admin", age: 50 }
    //复制操作
    let user1 = { ...persion1 }
    console.log(user1);

    //对象合并
    let age = { age: 20 }
    let name = { name: "lll" }
    let user2 = { ...age, ...name }
    console.log(user2);
```

- 箭头函数

```javascript
    //传统
    var f1 = function (a) {
      return a;
    }
    console.log(f1(3));
    //es6
    var f2 = a => a
    console.log(f2(4));
```

