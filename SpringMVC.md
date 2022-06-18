# Spring MVC

## 介绍

Spring MVC是Spring Framework 的一部分,是基于实现MVC的轻量级的Web框架

MVC是一种软件架构的思想,润健按照模型 视图  控制器来进行划分

- M:Model 模型层 JavaBean 作用是处理数据

- V:View 视图层 工程中的html 或jsp页面,作用是与用户进行交互,展示数据

- C:Controller 控制层 工程中的servlet 作用是接收和响应浏览器

## 什么是Spring MVC

Spring Mvc 是Spring的一个后续产品 是Spring的一个子项目

Spring Mvc是Spring为表述层开发提供的一整套完备解决方案.目前业界普遍选择了Spring MVC作为JavaEE项目的表述层进行开发的首选方案

> 三层架构分为表述层(表示层) 业务逻辑层 数据访问层 

## Spring MVC的特点

- Spring 家族原生产品 与IOC容器等基础设施无缝对接
- 基于原生的Servlet,通过了功能强大的前端控制器DispatcherServlet,对请求和响应进行统一处理
- 表述层分领域需要解决的问题全访问覆盖,提供全面解决方案
- 代码清新简洁,大幅度提升开发效率
- 内部组件化程度高,可插拔组件即插即用 想要什么功能配置即可
- 性能卓越,尤其适合现代大型 超大型互联网项目要求

## Hello World

#### 搭建环境

```xml
<dependencies>
        <!--Spring MVC-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.3.1</version>
        </dependency>
        <!--日志-->
        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
            <version>1.2.3</version>
        </dependency>
        <!--Servlet API-->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.1.0</version>
            <scope>provided</scope>
        </dependency>
        <!--Spring 和 Thymeleaf整合包-->
        <dependency>
            <groupId>org.thymeleaf</groupId>
            <artifactId>thymeleaf-spring5</artifactId>
            <version>3.0.12.RELEASE</version>
        </dependency>
    </dependencies>
```

web.xml

```xml
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns="http://java.sun.com/xml/ns/javaee"
         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
         version="3.0">

<web-app>
  <display-name>Archetype Created Web Application</display-name>

  <!--配置前端控制器-->
  <servlet>
    <servlet-name>dispatcherServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath:springmvc.xml</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
    <servlet-name>dispatcherServlet</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>

  <!--配置解决中文乱码的过滤器-->
  <filter>
    <filter-name>characterEncodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
      <param-name>encoding</param-name>
      <param-value>UTF-8</param-value>
    </init-param>
  </filter>
  <filter-mapping>
    <filter-name>characterEncodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>

</web-app>

```

springmvc.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans" xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="        http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/mvc
       http://www.springframework.org/schema/mvc/spring-mvc.xsd
       http://www.springframework.org/schema/context
       http://www.springframework.org/schema/context/spring-context.xsd">
    <!-- 开启自动扫包 配置需要扫描的包是哪些 -->
    <context:component-scan base-package="cn.doudou"></context:component-scan>
    <!-- 配置视图解析器  jsp的文件位置-->
    <bean id=" " class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <!--文件夹名字 前缀-->
        <property name="prefix" value="/WEB-INF/jsp/"></property>
        <!--文件后缀-->
        <property name="suffix" value=".jsp"></property>
    </bean>
    <!-- 配置spring开启注解mvc的支持     <mvc:annotation-driven></mvc:annotation-driven>-->
    <mvc:annotation-driven/>
    <!--&lt;!&ndash;不拦截静态资源&ndash;&gt;
   <mvc:resources location="/" mapping="/**/*.js"/>-->
    <!--不在处理静态资源 过滤掉静态资源-->
    <mvc:default-servlet-handler/>
</beans>
```

## 注解的作用

- 控制器类
  ```
  @Controller
  ```

- 通用请求注解

  ``` 
  @RequestMapping  
  属性:
  	path 	映射的路径
  	value{}映射的路径
  	method	请求方式
  	params	用于指定请求参数的条件
  	headers	用于指定限制请求消息头的条件
  ```

- Get方式请求

  ```
  @GetMapping
  ```

- Post方式请求

  ```
  @PostMapping
  ```

- 把请求中指定名称的参数给控制器的形参赋值

  ```
  @RequestParams
  	属性:
  		value:	请求参数的名称
  		required	请求参数中是否必须提供此参数,默认为true,表示必须提供,没有则报错
  ```

- 用于获取请求体的内容  可以返回内容

  ```
  @RequestBody
  
  get方式不可以用
  ```

- 用于绑定URL的占位符

  ```
  @PathVaribale
  	属性:
  		value:用于指定个url中占位符
  		required:是否必须提供占位符 
  ```

- 基于HiddentHttpmethodFile的示例

- 用于获取请求消息头

  ```
  @RequestHeader
  	属性:
  		value:	提供消息头
  		required:	必须有此消息头
  ```

- 用于把指定cookie名称传入控制器方法参数

  ```
  @CookieValue
  	属性:
  		value:	指定coolie名称
  		required:	必须有cookie
  ```

- 用于修饰方法和参数

  ```
  @ModelAttribute
  	属性:
  		value:制动得到数据的key
  ```

- 用于多次执行控制器方法的参数共享

  ```
  @SessionAttributes
  	属性:
  		value:用于指定错入的属性名称
  		type:用于指定存入的数据类型
  ```

  

#### 请求参数的绑定

直接拼字符串

#### 返回值分类

- 返回值是字符串

  ```
  @RequestMapping("/hi")
      public String testString ()
      {
          System.out.println("testString执行了");
          return "hi";
      }
  ```

- void返回值  默认是 请求路径的数据

- 返回值是ModelAndView对象

  ```
   @RequestMapping("/testModelAndView")
      public ModelAndView testModelAndView ()
      {
          ModelAndView mv = new ModelAndView();
          mv.addObject("msg","model");
          mv.setViewName("hi");
          return mv;
      }
  ```

- 转发和重定向

  ```
     @RequestMapping("/testforward")
      public String testforward() {
          //转发
          // return "forward:/WEB-INF/pages/hi.jsp";
          //重定向
          return "redirect:/re.jsp";
      }
  ```

- ResponseBody响应json数据

## 文件上传

```
  <!--    文件上传-->
    <bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
        <property name="maxInMemorySize" value="10485760"/>
    </bean>
```

## 拦截器

```
<!-- 配置拦截器信息--> <mvc:interceptors>     <mvc:interceptor>         <mvc:mapping path="/user/*"/>         <bean class="cn.doudou.interceptor.myinterceptor"></bean>     </mvc:interceptor> </mvc:interceptors>
```

```java
public class myinterceptor implements HandlerInterceptor {    @Override    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {        String msg =(String) request.getSession().getAttribute("msg");        System.out.println(msg);         if (msg != null){            request.getRequestDispatcher("/WEB-INF/pages/hello.jsp").forward(request,response);        }else {            request.getRequestDispatcher("/WEB-INF/pages/sb.jsp").forward(request,response);        }    }    @Override    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) {        System.out.println("拦截器执行");        return true;    }}
```



