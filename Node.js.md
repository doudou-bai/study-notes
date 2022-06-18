# Node.js

## Node.js简介

### 什么是Node.js

Node.js is aJavaScript runtime built on Chrome's V8 JavaScript engine.

Node.js 是一个基于谷歌浏览器 V8引擎的JavaSvript运行环境

### Node可以做什么

Node.js 作为一个JavaScript的运行环境,仅仅提供了基础的功能和API.然而,基于Node.js提供的这些基础能力,很多强大的工具和框架如雨后春笋,层出不穷,所以学会了Node.js 可以让前端程序胜任更多的工作和岗位

1. 基于Express框架,可以快速构建Web应用
2. 基于Electron框架,可以构建跨平台的桌面应用
3. 基于restify框架,可以快速构建API接口项目
4. 读写和操作数据库,创建使用的命令行工具辅助前端开发, ......

### Node.js 怎么学

浏览器中的JavaScript学习路径

JavaScvipt基础语法 + 浏览器内置API (DOM+BOM) + 第三方库(jquery art-template..... )

Node.js的学习路径

JavaSvript基础语法 + Node.js 内置API模块 (fs path http ...) + 第三方模块(express,mysql 等)

## Node.js环境的安装

如果希望通过Node.js来运行JavaScript代码,则必须在计算机上安装Node.js环境才行

### 查看Node.js的版本号

```
node -v
```

## 执行JS代码

1. 打开终端
2. 输入node 要执行的js文件的路径

## Fs

###  什么是fs文件系统模块

fs模块是Node.js 官方提供的,用来操作文件的模块.他提供了一系列的方法和属性,用来满足用户对文件的操作需求

### 读取指定文件中的内容

1. fs.readFile()的语法格式  

   ```javascript
   fs.readFile(path[,options],callback)
   参数解读：
   path	表示文件路径
   options	表示以什么编码格式来读取文件
   callback通过回调函数进行拿到结果
   ```

### 指定的文件中写入内容

1. fs.writeFile()的语法格式

   ```
   fs.writeFile(file,data[,options],callback)
   参数解读：
   file	表示存放路径
   data	表示写入内容
   options	表示以什么编码格式来读取文件
   callback通过回调函数进行拿到结果
   ```

### 路径动态拼接的问题

在使用fs模块操作文件时,如果提供的以./或者../开头的相对路径时,很容易出现路径拼接错误的问题

**原因:代码在运行的时候,会以执行node命令所处的目录,动态拼接处被操作文件的完整路径**

#### 解决:

若果出现这个问题,可以提供一个完整的文件存放路径

```
__dirname 表示当前文件的存放目录
```

## http模块

 http模块是Node.js 官方提供的,用来创建web 服务器的模块.通过http模块提供的http.createServer()方法,就能方便的把一台普通的电脑,变成一台web服务器,从而对外提供web资源服务

如果要希望使用http模块创建web服务器,则需要先导入它:

```javascript
const http = require('http');
```

### 进一步理解http模块的作用

服务器和普通电脑的区别在于,服务器上安装了web服务器软件,例如IIS Apache 等 通过安装这些服务器软件,就可以把一台普通电脑变成一台web服务器

在Node.js 中,我们不需要使用IIS Apache 等这些第三方的web服务器软件,因为我们可以基于Node.js提供的http模块,通过几行简单的代码,就可以轻松的手写一个服务软件,从而对外提供web服务.

### 格式:

```javascript
//引入http模块
const http = require('http');
//创建server 服务
const server = http.createServer();

server.on('request', (req, res) => {
  //返回数据
  let data = "server ";
  //设置返回头
  res.setHeader("Content-Type", "text/html; charset=utf-8");
  //返回数据
  res.end(data);
})

//启动服务 端口80 
server.listen(80, () => {
  //启动后成功后打印一句话 提示
  console.log("server running at http://127.0.0.1")
})
```

## 模块化

### 什么是模块化

模块化是指解决一个复杂问题时,自定向下把系统划分为若干模块的过程。对于整个系来说，模块就是可以组合 拆解和更换的单元

 把代码进行模块化拆分的好处：

1. 提高了代码的复用性
2. 提高了代码的可维护性
3. 可以实现按需加载

### Node.js中模块化的分类

- 内置模块 <ps path http ....>
- 自定义模块 <用户创建的js 都是自定义模块>
- 第三方模块<第三方开的模块, 使用前必须下载>

### 加载模块

使用require()方法,可以加载需要的内置模块,用户自定义模块,第三方模块进行使用 

```javascript
//加载内置的fs模块
const fs = require('fs');

//加载用户自发定义模块
const custom = require('./custom.js');

//加载第三方的模块
const moment = require('moment')
```

