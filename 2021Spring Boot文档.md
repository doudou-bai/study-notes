# Spring Boot

## 基础版

- SpringBoot是由Pivotal团队提供的全新的框架,设计目的是用来简化Spring应用的初始化搭建以及开发过程
- **Spring程序与SpringBoot程序对比**

| 类/配置文件            | Spring   | SpringBoot |
| ---------------------- | -------- | ---------- |
| pom文件中的坐标        | 手工添加 | 勾选添加   |
| web3.0配置类           | 手工添加 | 无         |
| Spring/SpringMVC配置类 | 手工添加 | 无         |
| 控制器                 | 手工添加 | 手工添加   |

**注意:<font color='#7fb80e'>基于idea开发SpringBoot程序需要确保联网并且能够加载到程序框架结构</font>**

- Spring程序**<font color='#f7acbc'>缺点</font>**
  - 依赖设置繁琐
  - 配置繁琐
- SpringBoot程序**<font color='#f7acbc'>优点</font>**
  - 起步依赖(简化依赖配置)
  - 自动配置(简化常用工程相关配置)
  - 辅助功能(内置服务器....)

### 官方开发步骤

1. 创建SpringBoot的项目

2. 加入坐标

   ```xml
   	//父坐标
   	<parent>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-parent</artifactId>
           <version>2.5.4</version>
           <relativePath/>
       </parent>
   	//web坐标
   	<dependency>
   		<groupId>org.springframework.boot</groupId>
   		<artifactId>spring-boot-starter-web</artifactId>
   	</dependency>
   ```

3. 编写代码

4. 启动项目

5. 打开浏览器输入`http://127.0.0.1:8080/`+`项目路径`进行访问测试

### 阿里云开发步骤

1. 创建项目的时候修改<font color='#f7acbc'>Custom</font>

   ```
   https://start.aliyun.com
   ```

2. 其他与官方一样

  

## 基础配置

### 属性配置

- 修改服务器端口

  ```
  server.port=8080
  ```

- 修改banner

  ```
  spring.main.banner-mode=off
  ```

- 日志

  ```
  logging.level.root=error
  ```

  

