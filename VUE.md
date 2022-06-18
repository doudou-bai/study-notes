## VUE

https://www.bilibili.com/video/BV1YE411A746?p=45

**v-on可以使用@代替**

### 快速入门案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>快速入门</title>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>
<body>
<div id="app">
    {{message}}
</div>
<script>
    //创建vue对象
    new Vue({
        el: "#app",
        data:{
            message:"Hello vue",
            age:"12333"
        }
    });
</script>
</body>
</html>
```

### 插值表达式

**格式:**

```
{{数值}}
```

### 点击事件

```
v-on:click=""
```

**示例:**

```html
<!DOCTYPE html>
<html lang="en" xmlns:v-on="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>
<body>
<div id="app">
    {{message}}
    <button v-on:click="func1('Vue')">点击</button>
</div>
<script>
    new Vue({
        el: "#app",
        data: {message: "Hello"},
        methods: {
            func1: function (msg) {
                this.message = msg;
            }
        }
    });
</script>
</body>
</html>
```

### 键盘按下事件

```
v-on:keydown=""
```

**示例:**

```html
<!DOCTYPE html>
<html lang="en" xmlns:v-on="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <style>
        div {
            width: 500px;
            background-color: honeydew;
        }
    </style>
</head>
<body>
<div id="app" v-on:mouseover="fun1">
    <textarea v-on:mouseover="fun2($event)"></textarea>
</div>
<script>
    new Vue({
        el: "#app",
        methods: {
            fun1: function (event) {
                alert("div");

            },
            fun2: function (event) {
                alert("文本域");
                event.stopPropagation();
            }
        }
    });
</script>
</body>
</html>
```

### 事件修饰符

```
.stop
```

```
.prevent
```

```
.capture
```

```
.self
```

```
.once
```

```
v-text 
```

```
v-html
```

```
v-bind 给html属性赋值 简化直接 :
```

### 按键修饰符

```
.enter
```

```
.tab
```

```
.esc
```

```
.delete (删除 和 退格)
```

```
.space
```

```
.up
```

```
.down
```

```
.left
```

```
.right
```

```
.ctrl
```

```
.alt
```

```
.shift
```

```
.meta
```

### 循环

```
v-for
```

示例:

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>
<body>
<div id="app">
    <ul>
        <li v-for="(item) in arr">{{item}}</li>
    </ul>
</div>
<script>
    new Vue({
        el:"#app",
        data:{
            arr:[6,4,5,1,5,4,4,5,6]
        }
    });
</script>
</body>
</html>

### v-model

获取json数据给表单赋值

### 表单域修饰符

- number 转换为数字
- trim 去掉开始和结尾的空格
- lazy 将input事件切换为change事件

```
<input v-model.number="age" type="number">
```

### 自定义指令-全局指令

```Vue
  // 自定义指定的创建
        Vue.directive(
            'focus', {//指令的名称
            //固定写法
            inserted: function (el) {
                //el表示指令所绑定的元素
                el.focus();
            }
        });
```

使用指令

```html
<input type="text" v-model.number='age' v-focus>
```

修改背景颜色

```vue
// 自定义指定的创建
        Vue.directive(
            'color', {//指令的名称
            //固定写法
            bind: function (el, binding) {
                //el表示指令所绑定的元素
                el.style.backgroundColor = binding.value;
                console.log(binding.value);
            }
        });
```

```html
 <input type="text" v-model.number='age' v-color="color">
```

```vue
 new Vue({
            el: '#app',
            data: {
                color: 'red'
            },
```

其实就是获取元素的dom使用css的属性功能进行改变原有dom的属性

局部指令

```vue
 directives: {
                color: {
                    bind: function (el, binding) {
                        //el表示指令所绑定的元素
                        el.style.backgroundColor = binding.value;
                        console.log(binding.value);
                    }
                }

            }
```

### 计算属性

```vue
 computed: {
                reverseString: function () {
                    //首先对字符串进行分割然后进行翻转最后拼接
                    return this.msg.split('').reverse().join('');
                }
            }
```

使用

```html
<div>
            {{reverseString}}
        </div>
```

### 侦听器

数据变化时执行异步或开销较大的操作

```
 watch: {
                firstName: function (val) {
                    this.fullName = val + '' + this.lastName;
                },
                lastName: function (val) {
                    this.fullName = + this.firstName + '' + val;
                }
            }
```

```
data: {
                firstName: "",
                lastName: "",
                fullName: ""
            },
```

使用v-model进行绑定侦听器

案例 用户输入账号后进行判断用户是否可以使用

```vue
methods: {
                checkName: function (uname) {
                    var that = this;
                    setTimeout(function () {
                        //模拟接口调用
                        if (uname == "admin") {
                            that.tip = "当前用户名已经存在,请更换!"
                            this.color = 'red';
                        } else {
                            that.tip = "用户名可以使用!"
                        }
                    }, 2000);
                },
                gBColor: function (color) {

                }
            },
            watch: {
                uname: function (val) {
                    //调用后台接口验证用户名
                    // this.checkName(val);
                    this.checkName(val);
                    this.tip = "正在验证";

                }

            }
```

```
 <input type="text" v-model='uname'>
```



```
data(){
uname: '',
tip: '',
}
```

### 过滤器

对数据进行处理 满足特定的需求

- 自定义过滤器

```
 //过滤器
        Vue.filter('upper',function(val){
            return val.charAt(0).toUpperCase()+val.slice(1);
        });
```

使用

```
 <input type="text" v-model='msg'>
        <span>{{msg | upper | color}}</span>
        <span :abc =' msg | upper'>测试数据</span>
```

自定义过滤器

```
filters:{
                upper:function(val){
                    return val.charAt(0).toUpperCase()+val.slice(1);
                }
            }
```

**使用同上**

时间格式化的操作

```vue
 <script>
        new Vue({
            el: "#app",
            data:{ 
                date: new Date()
            },
            filters:{
                format:function(val,arg){
                    console.log(arg);
                    if(arg == 'yyyy-MM-dd' ){
                        var ret = '';
                        ret += val.getFullYear()+"-"+(val.getMonth()+1)+"-"+val.getDate();
                        return ret;
                    }
                    return val;
                }
            }
        })
    </script>
```

```ht'ml
<span>
          {{date | format('yyyy-MM-dd')}}
      </span>
```

### 生命周期

- 挂载(初始化相关属性)
  - beforeCreate
  - created
  - beforeMount
  - mounted
- 更新(元素或组件的变更操作)
  - beforeUpdate
  - upDated
- 销毁(销毁相关属性)
  - beforeDestroy
  - destroyed

### 组件开发

- 标椎
- 分治
- 重用
- 组合



### vue-cli脚手架工具

- 下载安装node.js

- 安装cli

  ```
  npm isntall vue-cli -g
  ```

- 创建vue项目 文件夹

  ```
  mkdir 文件夹
  cd 创建的文件夹
  ```

- 查看可以用模板

  ```
  vue list
  ```

- 初始化

  ```
  vue init webpack-simple environmental-governance
  ```

- 进入目录

  ```
  cd 目录名字
  ```

- 安装

  ```
  npm install
  ```

- 开发模式运行

  ```
  npm run dev
  ```


### webpack-simple结构

- index.html   
- main.js 是整个vue项目的入口函数
- App.vue   以.vue为扩展名的文件实际上就是一个vue对象 也称之为vue组件

### Vue文件的组成部分

- template	html 代码
- script          js代码
- style           css代码

### 全局注册 模块

模块

```vue
<template>
  <div id="app">{{title}}</div>
</template>
<script>
export default {
  name: "context",
  data() {
    return {
      title: "底部导航测试版权所有"
    };
  }
};
</script>
<style scoped>
</style>
```

注册全局组件

```js
import Vue from 'vue'
import App from './App.vue'
import Header from './components/Header.vue'
import Context from './components/Context.vue'

//全局注册2个组件 可以把组件拿来当标签一样使用
Vue.component('MyHeader',Header);
Vue.component(  'MyContext',Context);

new Vue({
  el: '#app',
  render: h => h(App)
})

```

使用 在App.vue使用

```vue
<template>
  <div id="app">
   <MyHeader></MyHeader>
   <MyContext></MyContext>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
    
    };
  }
};
</script>

<style>
</style>

```

### 本地注册 模块

```vue
<template>
  <div id="app">
      <!--使用组件-->
    <MyHeader></MyHeader>
    <MyContext></MyContext>
  </div>
</template>


<script>
/* 本地注册组件 */
import Header from "./components/Header.vue";
import Context from "./components/Context.vue";

export default {
  name: "app",
  data() {},
  components:{
    "MyHeader":Header,
    "MyContext":Context

  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
</style>

```

### 组件间的参数传递

父传子

父组件

```vue
<template>
  <div id="app">
    <MyHeader></MyHeader>
    <!-- 参数 -->
    <MyContext :MyTitle="msg"></MyContext>
  </div>
</template>


<script>
/* 本地注册组件 */
import Header from "./components/Header.vue";
import Context from "./components/Context.vue";

export default {
  name: "app",
  data() {
    return{
      /* 设置参数 */
        msg:"hello vue!"
    }
  },
  components:{
    "MyHeader":Header,
    "MyContext":Context

  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
</style>

```

子组件

```vue
<template>
  <div id="app">
    <div class="dv">{{title}}
      <ul>
        <li>2222222</li>
        <li>2222222</li>
        <li>2222222</li>
        <li>2222222</li>
        <li>2222222</li>
        <li>2222222</li>
        <li>{{MyTitle}}</li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  name: "context",
  /* 参数定义 */
  props:[  "MyTitle"],
  data() {
    return {
      title: "底部导航测试版权所有"
    };
  }
};
</script>
<style scoped>
.dv{
  width: 20%;
  background: rosybrown;
  position: absolute;
  height: 100%;
}
</style>
```

子组件2

```vue
<template>
  <div id="app">
    <div class="dv">
      {{title}}
      <ul>
        <li>2222222</li>
        <li>2222222</li>
        <li>2222222</li>
        <li>2222222</li>
        <li>2222222</li>
        <li>2222222</li>
        <li>{{MyTitle}}</li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  name: "context",
  /* 参数定义 */
  props: {
    MyTitle: {
      type: String, //类型
      required: true,
      default: "XX" //默认值
    }
  },
  data() {
    return {
      title: "底部导航测试版权所有"
    };
  }
};
</script>
<style scoped>
.dv {
  width: 20%;
  background: rosybrown;
  position: absolute;
  height: 100%;
}
</style>
```

子传父

子组件

```vue
<template>
  <div id="app">
    <div class="dv">
      <button @click="doClick()">点我</button>
      {{title}}
      <ul>
        <li>2222222</li>
        <li>2222222</li>
        <li>2222222</li>
        <li>2222222</li>
        <li>2222222</li>
        <li>2222222</li>
        <li>{{MyTitle}}</li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  name: "context",
  /* 参数定义 */
  props: {
    MyTitle: {
      type: String,
      required: true,
      default: "XX"
    }
  },
  data() {
    return {
      title: "底部导航测试版权所有"
    };
  },
  methods:{
    doClick(){
      /* 定义参数的传递 */
      this.$emit('newName',"Hello JS");
    }
  }
};
</script>
<style scoped>
.dv {
  width: 20%;
  background: rosybrown;
  position: absolute;
  height: 100%;
}
</style>
```

父组件

```vue
<template>
  <div id="app">
    <MyHeader></MyHeader>
    <!-- 参数 -->                接收参数
    <MyContext :MyTitle="msg"  @newName="msg=$event"></MyContext>
  </div>
</template>


<script>
/* 本地注册组件 */
import Header from "./components/Header.vue";
import Context from "./components/Context.vue";

export default {
  name: "app",
  data() {
    return{
      /* 设置参数 */
        msg:"hello vue!"
    }
  },
  components:{
    "MyHeader":Header,
    "MyContext":Context

  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
</style>

```

### Vue发送Ajax请求

安装axios

```
npm install --save axios vue-axios
```

引入

```
import axios from 'axios'
import VueAxios from 'Vue-Axios'

Vue.use(VueAxios, axios);
```

使用

Get请求

```vue
this.axios({
        method: "get",
        url: "" + 拼接参数,
      }).then(function(res) {});
```

Post请求

```
this.axios({
        method: "post",
        url: "",
        data: {}
      }).then(function(res) {});
```

### 跨域问题

在浏览器进行ajax请求的时候会出现跨域问题<mvc框架解决跨域问题>

```xml
<mvc:cors>

    <mvc:mapping path="/api/**"
        allowed-origins="*"
        allowed-methods="GET, PUT"
        allowed-headers="header1, header2, header3"
        exposed-headers="header1, header2" allow-credentials="false"
        max-age="123" />

    <mvc:mapping path="/resources/**"
        allowed-origins="http://domain1.com" />

</mvc:cors>
```

```
@CrossOrigin//开启跨域注解
```

### 路由

安装路由

```
npm install vue-router -s
```

安装插件 什么插件都要执行

```
npm install
```

设计路由界面

创建路由表

```js
//在src文件下创建routes.js文件
//暴露对应的路由信息
import Home from './views/Home.vue';
import Product from './views/Products.vue';

export const routes = [
    {
        path: '/Home',
        component: Home,
    },
    {
        path: '/Product',
        component: Product,
    }
]
```

在main.js中使用路由模块以及注册路由表

```js
import Vue from 'vue'
import App from './App.vue'
import VueRouter from 'vue-router'//引入路由模块
import { routes } from './routes'//引入静态路由表  routes.js 文件


//使用路由模块
Vue.use(VueRouter)


//创建一个路由的实例对象
const router = new VueRouter({
  routes: routes
})

new Vue({
  el: '#app',
  //把routes放在vue实例中
  router,
  render: h => h(App)
})

```

创建路由链接和路由视图

```html
  <div id="app">
    <div>
      <span>
        <!-- 路由的链接 -->
        <router-link to="/Home">首页</router-link>
      </span>
      <span>
        <router-link to="/Products">商品列表</router-link>
      </span>
    </div>
    <router-view></router-view>
  </div>
```

### 参数的传递

路由之间的参数传递

设置参数

```js
import Home from './views/Home.vue';
import Products from './views/Products.vue';

export const routes = [
    {
        path: '/Home',
        component: Home
    },
    {
        path: '/Products/:id',//加上:id
        component: Products
    }
]
```

传递参数

```
   <router-link to="/Products/1">
```

接收参数

```
  data() {
    return {
      id: this.$route.params.id
    };
  }
```

### 路由之间的跳转的方式

```
<router-link to="路由地址">
```

js方式进行路由跳转

定义一个按钮 设置一个function

```js
//方法
  methods:{
    btufn(){
      this.$router.push("/Products/1");
    }
  }
```

可以到另外一个路由中进行参数的获取

### 资源打包

```
npm run build
```

### Webpack-Vue工程项目

创建项目

```
vue init webpack 项目名称

最好选择no
```

进入目录

```
cd 目录名称
```

安装vue-router

```
npm i vue-router@3.5.2 -S
```

安装element-ui

```
npm i element-ui -S
```

安装SASS加载器

```
npm install sass-loader node-sass --save-dev
```

安装axios

```
npm install --save axios vue-axios
```

安装依赖

```
npm install
```

启动项目

```
npm run dev 
```

在src新建文件夹

```
views router
```

在views中新建vue文件

```vue
<template>
  <div id="app">
      login
  </div>
</template>

<script>
export default {
  components: {},
  name:"Login",
  data() {
    return {};
  },
  computed: {},
  watch: {},
  methods: {},
  //生命周期 - 创建完成（可以访问当前this实例）
  created() {},
  //生命周期 - 挂载完成（可以访问DOM元素）
  mounted() {}
};
</script>
<style scoped>
</style>
```

在main.js中配置

```js
import VueRouter from 'vue-router'
import Login from './views/Login.vue'
//导入上面创建的路由配置目录
import router from './router'


Vue.use(VueRouter);

/* eslint-disable no-new */
new Vue({
  el: '#app',
  //配置路由
  router,
  components: { App },
  template: '<App/>'
})

```

在router文件夹创建文件 index.js

```js
import Vue from 'vue';
//导入路由组件
import Router from 'vue-router'

import Login from '../views/Login'
import { component } from 'vue/types/umd';

//安装路由
Vue.use(Router);

//配置路由

export default new Router({
    routes: [
        {
            //路由路径
            path: "/Login",
            //路由名称
            name: 'Login',
            //跳转到组件
            component: Login
        }
        
    ]
})
```

app.vue文件

```vue
<template>
  <div id="app">
    测试webpack
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: "App"
};
</script>

<style>
</style>

```

### WebPack

命令

```
npm run build
```

如果发布到tomcat是空白页面配置如下内容

**在build/webpack.prod.conf.js中增加publicPath:'./'**

![问题1](D:\MD文档笔记\img\webpack\问题1.png)

**修改config/index.js将assetsPublicPath值改为./**

![问题2](D:\MD文档笔记\img\webpack\问题2.png)

**build/util.js中增加publicPath:'../../'**



![问题3](D:\MD文档笔记\img\webpack\问题3.png)

### Vue3 坑

使用vue3的时候会有各种错误 

打开.eslintrc.js文件在rules中加入

```
 "space-before-function-paren": 0,
    'semi': 0,
```

如果还报错 就检查 是不是多逗号删了就可以

觉得烦就关闭

创建vue.config.js文件

加入

```
// vue.config.js
module.exports = {
    lintOnSave: false
}
```

https://www.bilibili.com/video/BV1h7411N7bg?p=10&spm_id_from=pageDriver

# VueX

Vuex是实现组件全局状态(数据)管理的一种机制,可以方便的实现组件之间数据的共享

### 安装

```
npm install vuex --save
```

### 导入

```
import Vuex from 'vuex'
Vue.use(Vuex)
```

### 创建store对象

```vue
const store = new Vuex.Store({
	//state中存放的就是全局共享的数据
	state:{ count : 0 }
})
```

### 将store对挂载到Vue实例中

```vue\
import store from './store'
new Vue({
  el: '#app',
  router,
  //挂载route
  store,
  components: {
    App
  },
  template: '<App/>'
})
```

### Vuex的核心概念

- State
- Mutation
- Action
- Getter

### State

State提供唯一的公共数据源,所有共享的数据都要统一放到State的State中进行存储

组件访问State中数据的第一种方式:

```
this.$store.state.全局数据名称
```

组件访问State中数据的第二种方式

```
//1.从vuex中按需导入mapState函数
import { mapState } from 'vuex'
```

通过刚才导入的mapState函数,将当前组件需要的全局映射,映射为当前组件的computed计算属性:

```
//2.将全局数据,映射为当前组件的计算属性
computed: {
	...mapState(['count'])
}
```

### Mutation

Mutation用于变更Store中的数据.

- 只能通过Mutation变更Store的数据,不可以直接操作Store中的数据
- 通过这种方式虽然操作起来稍微繁琐一些,但是可以集中监控所有数据的变化 

```js
//定义Mutation
const store = new Vuex.Store({
	 state: {
    count: 0
  },
  mutations: {
   add(state) {
   	//变更状态
   	state.count++
   }
  }
})
```

```
 this.$store.commit('函数名');
```

传递数据

```
this.$store.commit('函数名',参数);
```

另一种调用方法

```
//1.从vuex中按需导入mutations函数
import { mapMutations } from 'vuex'
```

```
//2.将指定的的mutations函数,映射为前组件的methods方法
methods:{
	...mapMutations(['函数名'],['函数名'])
}
```

### Action

触发actions异步任务

```js
actions: {
    addAsync(context) {
      setTimeout(() => {
        context.commit('add');
      }, 500);
    },
    addNAsync(context, step) {
      setTimeout(() => {
        context.commit('addN', step);
      }, 1000);
    },
  },
```

```js
 btuHandler2 () {
      this.$store.dispatch('addAsync')
    },
    btuHandler3 () {
      this.$store.dispatch('addNAsync', 5)
    }
```

第二种方法

```
//1.从vuex中按需导入mapActions函数
import { mapActions } from 'vuex'
//通过刚才导的mapAcctions函数,将需要的actions函数,映射为当前组件的methods方法:
methods: {
	...mapActions(['函数1','函数2'])
}
```

### Getter

Getter用于对store中的数据进行加工处理形成新的数据

1. Getter可以对Store中已有的数据加工形成新的数据,类似Vue的计算属性
2. Store中数据发生变化,Getter的数据也会跟着变化

```js
 getters: {
    showNum: state => {
      return '最新的数据是:' + state.count
    }
  },
 showNum(state) {
      return '最新的数据是:' + state.count
    }
  },
```

第一种方式

```
this.$store.getters.名称
```

第二种使用方式

```
import { mapGetters } from 'vuex'

computed: {
	...mapGetters(['showNum'])
}
```

