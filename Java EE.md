## Servlet

servlet是JavaEE规范之一

servlet是JavaWEb三大组件之一

sservlet是运行在Java服务器端的小程序,用于接收和响应基于HTTP协议的请求

### 基本实现步骤

1. 创建一个Web的项目
2. 创建一个类继承GenericServlet
3. 重写service方法
4. 在web.xml中配置Servlet
5. 部署并且启动项目
6. 通过浏览器测试 

**不需要导入任何Jar包**

### 实现servlet的程序

1. 创建类实现Servlet接口
2. 实现Servlet方法,处理请求,响应数据
3. 到web.xml文件中配置servlet的访问地址

### 实现方式

1. 第一种
   - 实现Servlet接口,实现所有的抽象方法,该方式支持最大程度的自定义
2. 第二种
   - 继承GenericServlet抽象类,必须重写service方法,其他方法可选择重写.该方法让我们开发servlet变得简单,但是这种方法和HTTP协议无关
3. 第三种
   - 继承HttpServlet抽象类,需要重写doGet和doPost方法,该方法表示请求和响应都需要和HTTP协议相关

```java
package cn.doudou.servlet;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

/**
 * Create By 王嘉浩
 * Time 2020/8/5 16:35
 */
@WebServlet(name = "ServletMyServlet",urlPatterns ="/servletMyServlet" )
public class ServletMyServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html;charset=UTF-8");
        PrintWriter out = response.getWriter();
        out.println("<h1>测试</h1>");

    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request, response);
    }
}

```

配置web.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <!--servlet标签给Tomcat配置程序-->
    <servlet>
        <!--给Servlet起一个别名-->
        <servlet-name>HelloServlet</servlet-name>
        <!--是全类名-->
        <servlet-class>cn.doudou.servlet.HelloServlet</servlet-class>
    </servlet>


    <servlet-mapping>
        <servlet-name>HelloServlet</servlet-name>
        <!--访问地址-->
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
</web-app>
```

### 生命周期

- ```
  init 初始化方法Servlt创建时执行 只执行一次
  ```

- ```
  service 每一次请求都要执行 执行多次
  ```

- ```
  destroy 服务器关闭时执行 只执行一次
  ```

- ```
  getServletConfig 获得Servlet的配置对象
  ```

- ```
  getServletInfo 获得Servlet的一些信息 一般不用
  ```

### servlet3.0注解配置

直接写注解

好处:支持注解配置

```
@WebServlet(urlPatterns = "/访问地址")
```

### Servlet体系结构

1. GenericServlet 抽象类

   ```java
   @WebServlet(urlPatterns = "/demo2")
   public class RequestDemo2 extends GenericServlet {
       @Override
       public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
   
       }
   }
   ```

   1. HttpServlet 抽象类

      ```java
      @WebServlet(urlPatterns = "/demo3")
      public class RequestDemo3 extends HttpServlet {
          @Override
          protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
              doGet(req, resp);
          }
      
          @Override
          protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
              super.doPost(req, resp);
          }
      }
      ```

      

### 相关配置

- ```
  urlPatterns 定义一个或多个访问路径
  ```

- ```
  urlPatterns
  
  配置演示
  /xxx
  /xxx/xxx
  /xxx.do
  ```

### Servlet线程安全问题

- 由于Servlet采用的是单里的设计模式,也就是整个应用中只有一个实例对象.所以我们只需要分析整个唯一的实例对象中的类成员是都线程安全
- 模拟用户登录功能来查看Servlet线程是否安全

### Servlet映射方式

1. 第一种
   - 具体名称的方式.访问的资源路径必须和映射配置完全相同
2. 第二种
   - / 开头+通配符的方式.只要符合目录结构即可,不用考虑结尾是什么 
3. 第三种
   - 通配符 +  固定格式结尾的方式.只要符合固定结尾的格式即可,不用考虑前面的路径



### 继承GenericServlet实现方式-代码实现

```java
public class HelloServlet extends GenericServlet {

    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        System.out.println("servlet执行了");
    }
}
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <!--servlet标签给Tomcat配置程序-->
    <servlet>
        <!--给Servlet起一个别名-->
        <servlet-name>HelloServlet</servlet-name>
        <!--是全类名-->
        <servlet-class>cn.doudou.servlet.HelloServlet</servlet-class>
    </servlet>


    <!--访问地址映射-->
    <servlet-mapping>
        <servlet-name>HelloServlet</servlet-name>
        <!--访问地址-->
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
</web-app>
```

HttpServlet实现方式-代码实现

```java
public class ServletDemo02 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("方法执行了!");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

```

```xml
    <servlet>
        <servlet-name>servletdemo02</servlet-name>
        <servlet-class>cn.doudou.servlet.ServletDemo02</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>servletdemo02</servlet-name>
        <url-pattern>/servletdemo02</url-pattern>
    </servlet-mapping>

```

## ServletConfig

- servletConfig是Servlet的配置参数对象,在Servlet的规范中,为每一个Servlet都提供一些初始化的配置.所以,每个Servlet都有一个自己的ServletConfig
- 作用:在Servlet的初始化时,把一些配置信息转递给Servlet
- 生命周期:和Servlet 相同

### 配置方式

- 在<servlet>标签中,通过<init-param>标签来配置,有两个字标签
- <param-name>:代表初始化参数的key
- <param-value>:代表初始化参数的value

```xml
    <servlet>
        <servlet-name>servletdemo04</servlet-name>
        <servlet-class>cn.doudou.servlet.ServletDemo04</servlet-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
        
        <init-param>
            <param-name>desc</param-name>
            <param-value>This is ServletConfig</param-value>
        </init-param>
    </servlet>
```

### 常用方法

| 返回值              | 方法名                        | 说明                     |
| :------------------ | ----------------------------- | ------------------------ |
| Strig               | getInitParameter(String Name) | 根据参数名称获取参数的值 |
| Enumeration<String> | getInitParameterNames()       | 获取所有参数名称的枚举   |
| String              | getServletName()              | 获取Servlet的名称        |
| ServletContext      | getServletContext()           | 获取servletContext对象   |

## ServletContext

- ServletContext是应用上下文对象(应用域对象).每一应用中只有一个ServletContext对象
- 作用:可以配置和获得应用的全局初始化参数,可以实现Servlet之间的数据共享
- 生命周期:应用一加载则创建,应用停止则销毁

- 获取MIME类型

  - ​	MIME类型:在互联网通信中定义的一种文件数据类型

    ​		格式: 大类型/小类型 text/html image/jsp

    获取:String getMimeType(String file)

- 域对象 共享数据

  - setAttribute(String name,Object value);
  - getAttribute(String name);
  - removeAttribute(String name); 

- 获取文件的真实路径

  ​	getRealPath(String s);

通过 resquest对象获取

```java
resquest.getServletContext()
```

通过HTTPServlet对象获取

```java
this.getServletContext()
```

### 配置方式

- 在<web-app>标签中,通过<context-param>标签来配置.有两个子标签 
- <param-name>:代表全局初始化参数的key
- <param-value>:代表全局初始化参数的value

```xml

    <context-param>
        <param-name>encoding</param-name>
        <param-value>UTF-8</param-value>
    </context-param>

    <context-param>
        <param-name>desc</param-name>
        <param-value>描述</param-value>
    </context-param>
```

### 常用方法

| 返回值 | 方法名                                 | 说明                                     |
| ------ | -------------------------------------- | ---------------------------------------- |
| String | getInitParameter(String name)          | 根据名称获取全局配置的参数               |
| String | getContextPath()                       | 获取当前应用的访问虚拟目录               |
| String | getRealPath(String path)               | 根据虚拟目录获取应用部署的磁盘的绝对路径 |
| void   | setAttribute(String name,Object value) | 向应用域对象中存储数据                   |
| Object | getAttribute(String name)              | 通过名称获取应用域对象中的数据           |
| void   | removeAttribute(String name)           | 通过名称移除应用域对象中的数据           |



## ServletResponse

设置响应码

```
void setStatus(int sc);
```

设置响应头

```
void setHeader(String name,String value);
```

获取字符数据

```java
getWrite();
getOutputStream()字节输出流
```


输出字符数据

```java
write();
```

设置流的默认编码

```java
 resp.setCharacterEncoding("utf-8");
```

告诉浏览器本次使用什么解码

```java
 resp.setHeader("content-type","text/html;charset = utf-8");
```

简单的形式设置编码

```java
resp.setContentType("text/html;charset = utf-8");
```

获取字节输出流

```java
getOutputStream()
```

输出字节数据

```java
write();
```

重定向

```
sendRedirect("/资源路径")
```

**验证码**

```java
import javax.imageio.IIOImage;
import javax.imageio.ImageIO;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.awt.*;
import java.awt.image.BufferedImage;
import java.io.IOException;
import java.util.Random;

/*
 * yzm类继承父类HttpServlet类
 * 实现父类 覆盖重写的方法
 * @WebServlet("")设置访问路径
 *覆盖重写doPost方法
 *覆盖重写doGet方法
 *设置doGet方法内部 执行doPost方法 this.doPost(req,resp)
 *设置验证码图片的宽和高   int w = 100; int h = 50;
 *
 *  */
@WebServlet("/yzm")
public class yzm extends HttpServlet {
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //设置宽高
        int w = 100;
        int h = 50;
        //获取图片对象 设置宽和高 还有属性
        BufferedImage img = new BufferedImage(w, h, BufferedImage.TYPE_INT_RGB);
        //获取画板 返回画板对象
        Graphics graphics = img.getGraphics();
        //获取颜色 设置验证码背景颜色
        graphics.setColor(Color.pink);
        //设置的位置
        graphics.fillRect(0, 0, w, h);
        //设置验证码的边框属性
        //设置画笔颜色
        graphics.setColor(Color.orange);
        //设置的位置信息 宽和高各减1
        graphics.drawRect(0, 0, w - 1, h - 1);
        //设置验证码的文字信息
        String str = "abcdefghigkimnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
        //使用随机数 利用fro循环进行循环5次
        Random ran = new Random();
        for (int i = 1; i <= 5; i++) {
            //设置文字颜色
            graphics.setColor(Color.black);
            //利用索引进行文字的获取
            int index = ran.nextInt(str.length());
            char c = str.charAt(index);
            //把获取的文字输出到验证码内
            graphics.drawString(c + "", w / 5 * i, h / 2);
            //设置验证码文字的颜色
            graphics.setFont(new Font(index + 1 + "", 25, 20));
        }
        //获取设置干扰线
        //设置干扰线的颜色
        graphics.setColor(Color.gray);
        for (int a = 1; a <= 20; a++) {
            int y1 = ran.nextInt(w);
            int y2 = ran.nextInt(w);
            int h1 = ran.nextInt(h);
            int h2 = ran.nextInt(h);
            graphics.drawLine(y1,h1,y2,h2);
        }
        //书写到前端页面 传入参数img 设置图片类型 jpg 获取resp的字节输入出流
        ImageIO.write(img, "jpg", resp.getOutputStream());
    }

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doPost(req, resp);
    }
}

```

## ServletRequst

- request对象和Response对象的原理

  request和Response对是服务器创建的

  request对象是来获取请求消息,Response对象是设置响应消息

- request 对象继承体系

  ServletRequest

  HttpServletRequest

- request功能:

  - 获取请求消息数据

    - 获取请求行的数据

      获取请求方式: GET

      ```java
      String getMethod();
      ```

    - 获取虚拟目录

      ```java
      String getContextpath();
      ```

    - 获取Servlet路径:

      ```java
      String getServletPath();
      ```

    - 获取get方式的请求参数

      ```java
      String getQueryString();
      ```

    - 获取请求的url

      ```java
      String getRequestURL();
      ```

    - 获取协议以及版本号

      ```java
      String getProtocol()
      ```
  
    - 获取客户机的IP地址
  
      ```java
      String getRemoteAddr()
      ```
  
  - 获取请求头的的数据
  
    ```java
    String getHeader(String name)
    Enumeration<String>getHeadernames()获取所有的头的数据
    ```
  
  - 获取流对象
  
    ```java
    BufferedReader getReader()获取字符输入流
    ```
  
    ```java
    ServletInputStream getUnputStream()获取字节输入流
    ```
  
  - 获取请求体数据
  
    ```
    get
    ```
  
- 其他功能

  - 获取请求参数 通用

    - 根据参数名称获取参数值

      ```java
      String getparameter(String name)
      ```

    - 根据参数名称获取参数值的数组

      ```java
      String[] getParameterVAlues(String name)
      ```

    - 获取所有请求参数的名称

      ```java
      Enumeration<String> getParameterNames()
      ```

    - 获取所有参数的map的集合

      ```java
      Map<String,String[]> getParameterMap()
      ```

    - 中文乱码问题

    - get方式不会乱码

    - post方式乱码解决

      ```java
      setCharacterEncoding("编码格式")设置流的编码
      ```

  - 请求转发

    - 步骤:

      ```java
      RequestDispatcher getRequestDispatcher(String path)通过request对象获取请求转发对象
      ```

      ```java
      forward(ServlwtReques request,ServletResponse response)使用RwequestDispatchaer对象来进行转发 
      ```

    - 特点:

      - 浏览器地址栏没有发生变化
      - 只能转发当前服务器内部的资源中
      - 转发是一次请求

  - 共享数据

    - 域对象:一个有左右范围的对象,可以在范围内共享数据

    - request域:代表依次请求的范围,一般用于请求转发的多个资源中共享数据

      - 方法:

        ```java
        setAttribute(String name,Object obj)
        ```

        ```java
        getAttitude(String name)
        ```

        ```java
        removeAttribute(String name)
        ```

  - 获取ServletContext

    ```java
    ServletContext getServletContext()
    ```

案例:用户登录

BeanUtils工具类,简单数据封装

用于封装JavaBean的

1. 要求
   1. 类逆序被public修饰
   2. 必须提供空参的构造方法
   3. 成员变量必须使用private修饰
   4. 提供公共setter和getter方法
2. 功能 封装数据 
3. 方法
   1. setProperty()
   2. getProperty()
   3. populate

## 回话技术

​	客户端会话技术Cookie

​		概念:客户端会话技术,将数据保存到客户端

​	服务器会话技术Session

快速入门

使用步骤

1. ​	创建Cokkie对象,绑定数据

   ```java
   new Cookie (String name,String value)
   ```

2. 发送Cookie对象

   ```java
   response.addCookie(Cookie cookie)
   ```

3. 获取Cookie,拿到数据

   ```java
   Cookie[] request.getCookies()
   ```

Cookie的细节

1. 一次可不可以发送多个cookie?

   1. 创建多个cookie对象,多次调用 发送

2. cookie在浏览器中保存多长时间?

   1. 默认情况下:浏览器关闭后,cookie销毁

   2. 持久化的存储

      ```java
      setMaxAge(int seconds)
      正数:将cookie数据写到硬盘中.持久化存储,cookie存活时间
      负数:默认值 ,Cookie在当前浏览器内存中,当浏览器关闭,则cookie被销毁
      0:删除cookie信息
      ```

3. cookie能不能存储中文?

   1. 在tomcat 8之前 cookie中不能直接存储中文数据.
      1. 需要将中文数据转码---一般采用URL转码
   2. 在tomcat 8会后支持中文数据.

4. cookie获取范围多大?

   1. 假设在一个tomcat服务器,部署了多个web项目,那么在这些web项目中cookie能不能共享
   2. 默认情况下cookie不能共享
   3. setPath(String path)设置cookie的获取范围,默认情况下是虚拟目录
   4. setDomain(String path) 不同服务器的共享

5. Cookie的特点和作用

## Session

概述:服务器会话技术,在一次会话的多次请求间共享数据,将数据保存在服务器端的对象中

快速入门

获取HttpSession对象  

```
HttpSession session = request.getSession();
```

使用HttpSession对象

```
Object getAttribute(String name) 获得session对象数据

void setAttribute(String name,Object value) 设置对象session数据

void removeAttribute(String name); 删除session对象数据
```

**细节**

- 当客户端关闭后,服务器闭关闭,两次获取Session是否为同一个?
  - 默认情况下,不是同一个
- 客户端不关闭,服务器关闭后,两次获取的session是同一个吗?
  - 不是同一个
  - session的钝化
  - 在服务器正常关闭之前,将Session对象序列化到硬盘上
  - Session的活化
  - 在服务器启动后,将session文件转化为内存中的
- session的失效时间
  - 默认失效时间30分钟
  - session对象调用自杀方法 invalidate
  - 选择性配置 session-config

sessiopn特点:

1. session用于存储一次会话的多次请求的数据,存在服务器端;
2. session可以存储任意类型,任意大小的数据

session与Cookie的区别

session存储数据在服务器,Cookie在客户端

session没有数据大小限制,cookie有

session数据安全,cookie相对不安全

## JSP

1. 概念

   java Server Pages: java服务器页面 

   JSP脚本

   1. <%		%>:
   2. <%!	    %>:
   3. <%=       %>:

2. JSP的内置对象

   request

   response

   out:可以将数据输出到页面上
   
   **指令**
   
   ​	作用,用于配置JSP页面,导入资源文件
   
   ​	格式:<%@指令名称 属性名1 = 属性值1%>
   
   ​	分类:
   
   ​	pape 配置页面
   
   ​		contentType
   
   ​	include  导入文件
   
   ​	taglib 导入资源
   
   **注释**
   
   **内置对象**
   
   1. pageContext
   2. request
   3. session
   4. application
   5. response
   6. page
   7. out
   8. config
   9. exception
   
   

MVC开发模式

​	M:model 模型

​	V:view 视图

​	C controller 控制器

El表达式

​	概念:Expression Land 表达式语言

​	作用:替换在jsp页面上java的代码

​	语法:${ };

​	忽略el表达式  \

使用:

1. 运算

   1. 算术运算符 + - * /(div) %(mod)

   2. 比较运算符

   3. 逻辑运算符&&and ||or  !not

   4. 空运算符 empty

      用于判断字符串 集合 数组对象是否为空null

2. 获取值

   1. el只能从与对象中获取值

      语法${域名称.键名}

   2. ${键名}

   3. 获取对象的值

      ${域名称.键名.属性名}

   4. list集合

      ${域名称.键名[索引]}

   5. map集合:

      ${域名称.键名称.key名称}

      ${域名称.键名称["key名称"]}

3. 隐式对象

   el表达式有11个隐式对象

   pageContext:获取其他8个隐式对象

   ​	${pageContext.request.cotextPath}动态获取虚拟目录

JSTI标签 

JavaServer Pages Tag Library jsp标椎标签库

​	是由Apache组织提供开源的免费的jsp标签

作用:用于简化和替换jsp页面上的java代码

使用步骤:

1. 导入jar包
2. 引入标签库 taglib指令
3. 使用标签
4. 常用的JSTL标签
   1. if 相当于java代码的if语句
   2. choose 相当于java代码的switch语句
   3. foreach 相当于java代码for语句

三层架构

MVC

## Filter:过滤器

步骤:

1. 定义一个类,实现接口Filter
2. 复写方法
3. 配置拦截路径
   1. web.xml
   2. 注解 @WebFilter("过滤路径")

过滤器细节:

1. web.xml配置

2. 过滤器执行流程

3. 过滤器生命周期方法

4. 过滤器配置详解

   1. 具体的资源路径/index.jsp
   2. 拦截目录/user/*
   3. 后缀名拦截*.jsp
   4. 拦截所有资源 /*

   拦截方式配置:资源被访问的方式

   1. ​	注解配置
      1. dispatchertypes 
         1. REQUEST 默认值
         2. FORWARD  转发
         3. INCLUDE 包含访问
         4. ERROR  错误跳转
         5. ASYNC  异步访问
   2. web.xml配置

5. 过滤器链
   执行顺序

   

## Listtener:监听器

概念:web三大组件之一
事件监听机制

一类是:生命周期监听器

- ServletContextListener 
- ServletRequestListener
- HttpSessionListener

一类是:属性监听器

- ServletRequestAttributeListener
- ServletContextAttributeListener 
- HttpSessionAttributeListener

一类是:对象监听器

- HttpSessionAttributeListener
- HttpSessionBindingListener

