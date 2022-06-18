Vue-Element-Admin后台管理系统

- 登录篇

1. 修改request.js里面的baseUrl
2. 修改request.js里面的成功状态码
3. 修改user.js里面的请求地址

- 动态路由

1. 在router/index.js中只需要基础的路由,其他的都可以删了
2. 在store/modules/user.js中,有个getInfo方法查询了用户基本信息,返回了用户菜单列表
3. 修改store/gettes.js里面的内容
4. 在strc/router文件夹下新建2个文件每个文件添加一行代码定义导入方法

```
src/router/_import_development.js
//开发环境导入组件
module.exports = file => require('@/views/' + file + '.vue').default // vue-loader at least v13.0.0+
 
---------------------------------------------------------------------
 
src/router/_import_production.js
//生产环境导入组件
module.exports = file => () => import('@/views/' + file + '.vue')
```

​	5.在路由钩子中过滤路由,生成新路由 核心在src目录下的permission.js中，router.beforeEach路由钩子

```javascript
import Layout from '@/layout'
//获取组件的方法
const _import = require('./router/_import_' + process.env.NODE_ENV)



 if (store.getters.menus.length === 0) {
            await store.dispatch('user/getInfo').then(res => {
              const menus = filterAsyncRouter(res.menus);
              console.log(menus);
              router.addRoutes(menus) // 2.动态添加路由
              global.antRouter = menus // 3.将路由数据传递给全局变量，做侧边栏菜单渲染工作 *
            })
          }



// 遍历后台传来的路由字符串，转换为组件对象
function filterAsyncRouter (asyncRouterMap) {
  const accessedRouters = asyncRouterMap.filter(route => {
    if (route.component) {
      if (route.component === 'Layout') {
        route.component = Layout
      } else {
        route.component = loadView(route.component) // 导入组件
      }
    }
    if (route.children && route.children.length) {
      route.children = filterAsyncRouter(route.children)
    }
    return true
  })

  return accessedRouters
}


//路由懒加载
export const loadView = (view) => {
  return (resolve) => require([`@/views${view}.vue`], resolve)
}

```

​	6.合并路由 src\layout\components\Sidebar\index

```
 routes () {
      return this.$router.options.routes.concat(global.antRouter)
    },
```

**如果配置后点击登录后一堆错误则去request文件中查看下方代码**

```
//原代码
return Promise.reject(new Error(res || 'Error'))
//现代码
return Promise.reject(new Error(res.msg || 'Error'))
```

