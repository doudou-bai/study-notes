

# Vue

## Vue是什么

**一套用于构建用户界面的渐进式JavaScript框架**

## Vue的特点

1. 采用组件化的模式,提高代码复用率 让代码更好维护
2. 声明式编码,让编码人员无需直接操作DOM提高开发效率
3. 使用虚拟DOM+优秀的Diff算法尽量服用DOM节点

## 关闭Vue 的提示

```javascript
Vue.config.productionTip = false
```

## MVVM模型

1. M模型Model : 对应data中的数据
2. V视图View : 模板
3. VM视图模型ViewModel Vue实例对象

### 总结

1. data中所有的属性,最后都出现在了vm身上
2. vm身上所有的属性 以及Vue原型所有属性在Vue模板中都可以使用

## 数据代理

### 定义:

**通过一个对象代理另一个对象中属性的操作(读/写)**

原生代码示例:

```javascript
  let number = 18;
    let person = {
      name: "张三",
      sex: "男"
    }
    /* 
    参数一 对象名称
    参数二 属性名称
    参数三 对应的值或其他
    */
    Object.defineProperty(person, 'age', {
      // value: number,
      // enumerable: true,//控制属性是否可以枚举 默认false
      // writable: true,//控制属性是否可以修改  默认false
      // configurable: true//控制属性是否可以被删除  默认false

      //当有人读取person的age 属性的时候 get函数就会自动调用 且返回值就是age的值
      get() {
        return number;
      },

      //当有人修改person的age属性的时候 set函数就会自动调用 且会收到修改的具体值
      set(val) {
        number = val;
        console.log(val);
      }
    })
    console.log(person);
```

## 事件处理

**v-on 可以使用@代替**

点击事件	v-on:click 

### 事件修饰符

- prevent : 阻值默认事件
- stop : 阻止事件冒泡
- once : 事件只触发一次
- capture : 使用事件的捕获方式
- self : 只有event.target是当前操作的元素是才出发事件
- passive : 事件的默认行为立即执行 无需等待事件回调执行完毕

### 键盘事件

- keydown
- keyup

### 键盘修饰符

- enter 回车
- delete 删除
- esc 退出
- space 空格
- tab 换行
- up 上
- down 下
- left 左
- right 右

##  计算属性

格式:

```javascript
computed:{
    fullName:{
        //当有人读取fullName时候,get就会被调用,且返回值就作为fullName的值
        //get什么时候调用? 1.初次读取fullName时 2.所依赖的数据发生变化时
        get(){
             
        }
        //set什么时候调用? 当fullName被修改时
         set(){
            
        }
    }
}
```

## 监事属性

格式:

```javascript
watch: {
        isHot: {
            //开启深度监视
            deep:true,
          //handler什么时候调用? 当isHot发生改变时候
          handler(newValue, oldValue) {
            console.log("参数被修改");
          }
        }
      }
```