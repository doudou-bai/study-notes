#  Spring

## Spring的简介

- 源自于建筑学 ,隶属于土木工程,后发展到软件工程领域
- 软件工程框架 :经过验证的具有一定功能的 半成品软件

## Spring的概述

- spring是什么

  ```
  Spring是极其优秀的开源的JavaEE框架
  ```

  ```
  Spring是分层的Java SE/EE应用full-stack轻量级开源框架,以IOC和AOP为内核,提供了展现层Spring MVC和持久层Spring Jdbc业务层事务管理等众多的企业级应用技术,还能整合开源世界众多注明的第三方框架和类库,逐渐成为使用最多的Java EE企业级应用开源狂框架
  ```

- spring的两大核心

- spring的发展历程和优势

- spring体系结构

程序的耦合及解耦

- 曾经案例中问题
- 工程模式解耦

IOC概念和spring中IOC

- spring中基于xml的IOC环境搭建

## Spring程序开发步骤

1. 导入Spring开发包坐标
2. 编写Dao接口和实现类
3. 创建Sping核心配置文件
4. 在Spring配置文件中配置实现类
5. 使用Spring的API获得Bean实例

## 入门程序

- pom.xml 引入坐标

  ```xml
      <dependencies>
          <dependency>
              <groupId>org.springframework</groupId>
              <artifactId>spring-context</artifactId>
              <version>5.0.3.RELEASE</version>
          </dependency>
  
          <!-- https://mvnrepository.com/artifact/commons-logging/commons-logging -->
          <dependency>
              <groupId>commons-logging</groupId>
              <artifactId>commons-logging</artifactId>
              <version>1.2</version>
          </dependency>
          <dependency>
              <groupId>junit</groupId>
              <artifactId>junit</artifactId>
              <version>4.12</version>
              <scope>test</scope>
          </dependency>
  
      </dependencies>
  ```

- 在resources创建对应Spring的xml文件

  ```xml
  <?xml  version="1.0"  encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans.xsd
        ">
  
  
      <!--配置User类的对象创建-->
      <bean id="user" class="cn.doudou.spring5.User"/>
  
  </beans>
  ```

- 在Java目录下创建包`cn.doudou.spring5`

- 创建User类

  ```Java
  package cn.doudou.spring5;
  
  /**
   * Create By 王嘉浩
   * Time 2020/6/12
   */
  
  public class User {
      public void add(){
          System.out.println("........add........");
      }
  }
  
  ```

- 在test目录下创建对应的包和测试类

  ```Java
  package cn.douduo.spring5;
  
  import cn.doudou.spring5.User;
  import org.junit.Test;
  import org.springframework.context.ApplicationContext;
  import org.springframework.context.support.ClassPathXmlApplicationContext;
  
  /**
   * Create By 王嘉浩
   * Time 2020/6/12
   */
  
  public class TestSpring5 {
  
      @Test
      public void testAdd() {
          ApplicationContext ac = new ClassPathXmlApplicationContext("application.xml");
          User user = (User) ac.getBean("user");
          user.add();
      }
  }
  
  ```

## IOC

- `控制反转,把创建对象的过程交给Spring框架`

- `把对象的创建和调用都交给sprig框架`

### IOC的底层和原理

- XMl的解析,工厂模式,反射

### 工厂模式的实现

- User

  ```java
  package cn.doudou.spring5;
  
  /**
   * Create By 王嘉浩
   * Time 2020/6/12
   */
  
  public class User {
      public void add(){
          System.out.println("........add........");
      }
  }
  
  ```

- 工厂类

  ```
  package cn.doudou.spring5;
  
  /**
   * Create By 王嘉浩
   * Time 2020/6/12
   */
  public class Main {
      public static User user(){
          return new User();
      }
  }
  
  ```

- 测试类

  ```java 
  package cn.douduo.spring5;
  
  import cn.doudou.spring5.Main;
  import cn.doudou.spring5.User;
  import org.junit.Test;
  import org.springframework.context.ApplicationContext;
  import org.springframework.context.support.ClassPathXmlApplicationContext;
  
  /**
   * Create By 王嘉浩
   * Time 2020/6/12
   */
  
  public class TestSpring5 {
  
      @Test
      public  void Testgongchang(){
          User user = Main.user();
          user.add();
      }
  }
  
  ```

### Ioc的接口

**BeanFactory**:Ioc 开发人员进行使用,是spring内部的使用接口,不提供外部使用.`加载配置文件的时候不会创建对象,使用的时候才会创建`

**ApplicationContext**:是BeanFactory的子接口,一般是由开发人员使用`加载配置文件的时候就创建对象`

**ApplicationContext**:接口的实现类

```
ClassPathXmlApplicationContext:在当前路径
FileSystemXmlApplicationContext:文件的全路径
```

IOC操作Bean管理

**什么是Bean管理?**

- Bean管理只的是两个操作

- Spring创建对象
- Spring注入属性

**IOC和DI有什么区别?**

DI是IOC的一种依赖实现

### Set注入

- 创建类 属性 使用set方法

- 配置文件

  ```xml
  <?xml  version="1.0"  encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans.xsd
        ">
  
      <!--配置User类的对象创建-->
      <bean id="user" class="cn.doudou.spring5.User">
          <!--属性的注入-->
          <property name="name" value="天龙八部"/>
      </bean>
  
  </beans>
  ```

  

- 在测试中测试 创建对象 调用方法  

### 有参构造注入

- 创建对象 使用有参数构造方法

- 配置文件

  ```xml
  <?xml  version="1.0"  encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans.xsd
        ">
  
      <!--配置User类的对象创建-->
      <bean id="user" class="cn.doudou.spring5.User">
          <!--有参数构造方法-->
          <constructor-arg name="name" value="王嘉浩"/>
      </bean>
  
  </beans>
  ```

  ```xml
  <!--通过index进行构造-->
  <constructor-arg index="0" value="1"/>
  ```

- 测试 运行

### p名称空间注入

- 添加p空间

  ```xml
  xmlns:p="http://www.springframework.org/schema/p
  ```

- 配置文件

  ```
  <bean id="user" class="cn.doudou.spring5.User" p:name="name"/>
  ```

- 测试 运行

### xml注入null值

- 配置文件

  ```xml
  <?xml  version="1.0"  encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:p="http://www.springframework.org/schema/p"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans.xsd
        ">
  
      <!--配置User类的对象创建-->
      <bean id="user" class="cn.doudou.spring5.User">
          <property name="name">
              <null/>
          </property>
      </bean>
  
  </beans>
  ```

- 测试 运行

### xml注入特殊符号

- 配置文件

  ```xml
   <!--配置User类的对象创建-->
      <bean id="user" class="cn.doudou.spring5.User">
          <property name="name">
              <value>
                  <![CDATA[<<王嘉浩>>]]>
              </value>
          </property>
      </bean>
  ```

- 测试 运行

### 注入属性-外部bean

- 创建dao包

- 创建sevice

- 在service注入dao

- 配置文件

  ```xml
  <bean name="userservice" class="cn.doudou.spring5.service.UserServcie">
          <property name="dao" ref="userdao"/>
      </bean>
      <bean name="userdao" class="cn.doudou.spring5.dao.UserDao"/>
  
  ```

- 测试 运行

### 注入属性-内部bean和级联赋值

- 员工实体类

  ```java
  package cn.doudou.spring5;
  
  /**
   * Create By 王嘉浩
   * Time 2020/6/12
   */
  public class Emp {
      private String name;
      private String gender;
      private Dept dept;
  
      public void setDept(Dept dept) {
          this.dept = dept;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public void setGender(String gender) {
          this.gender = gender;
      }
      public  void add(){
          System.out.println(name+"::"+gender+"::"+dept);
      }
  
      @Override
      public String toString() {
          return "Emp{" +
                  "name='" + name + '\'' +
                  ", gender='" + gender + '\'' +
                  ", dept=" + dept +
                  '}';
      }
  }
  
  ```

- 部门实体类

  ```java
  package cn.doudou.spring5;
  
  /**
   * Create By 王嘉浩
   * Time 2020/6/12
   */
  public class Dept {
      private String dName;
  
      public void setdName(String dName) {
          this.dName = dName;
      }
  
      @Override
      public String toString() {
          return "Dept{" +
                  "dName='" + dName + '\'' +
                  '}';
      }
  }
  
  ```

- 配置文件

  ```xml
  <?xml  version="1.0"  encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:p="http://www.springframework.org/schema/p"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans.xsd
        ">
      <bean id="emp" class="cn.doudou.spring5.Emp">
          <property name="name" value="王嘉浩"/>
          <property name="gender" value="男"/>
          <property name="dept">
              <bean class="cn.doudou.spring5.Dept">
                  <property name="dName" value="Java开发"/>
              </bean>
          </property>
      </bean>
  
  </beans>
  ```

- 测试 运行

### xml注入集合

- 创建实体类

  ```java
  package cn.doudou.spring5;
  
  import java.util.Arrays;
  import java.util.List;
  import java.util.Map;
  import java.util.Set;
  
  /**
   * Create By 王嘉浩
   * Time 2020/6/12
   */
  public class Stu {
      private String[] course;
      private List<String> list;
      private Map<String, String> map;
      private Set<String> sets;
  
      public void setSets(Set<String> sets) {
          this.sets = sets;
      }
  
      public void setCourse(String[] course) {
          this.course = course;
      }
  
      public void setList(List<String> list) {
          this.list = list;
      }
  
      public void setMap(Map<String, String> map) {
          this.map = map;
      }
      public void sout(){
          System.out.println(Arrays.toString(course));
          System.out.println(list);
          System.out.println(map);
          System.out.println(sets);
      }
  
      @Override
      public String toString() {
          return "Stu{" +
                  "course=" + Arrays.toString(course) +
                  ", list=" + list +
                  ", map=" + map +
                  ", sets=" + sets +
                  '}';
      }
  }
  
  ```

- 配置文件

  ```xml
  <?xml  version="1.0"  encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:p="http://www.springframework.org/schema/p"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans.xsd
        ">
      <bean id="stu" class="cn.doudou.spring5.Stu">
          <!--数组注入-->
          <property name="course">
              <array>
                  <value>arr1</value>
                  <value>arr2</value>
                  <value>arr3</value>
              </array>
          </property>
          <property name="list">
              <list>
                  <value>list1</value>
                  <value>list2</value>
                  <value>list3</value>
              </list>
          </property>
          <property name="map">
              <map>
                  <entry key="map1" value="map1"/>
                  <entry key="map2" value="map2"/>
                  <entry key="map3" value="map3"/>
              </map>
          </property>
          <property name="sets">
              <set>
                  <value>set1</value>
                  <value>set2</value>
                  <value>set3</value>
              </set>
          </property>
       </bean>
  </beans>
  ```

- 测试 运行

### FactoryBean

`Spring中有两种bean 一种普通bean 一种工厂bean FactoryBean`

普通bean: 定义什么类型就返回什么类型

工厂bean:定义什么类型可能返回别的类型

### Bean的作用域

`默认情况下是单实例对象`

设置多实例对象

**在创建bean xml的里面加"scope"**

取值

- singleton 单实例 在加载时创建
- prototype 多实例 在调用的时候创建
- request  
- session

### Bean的生命周期

- 通过构造器创建bean实例
- 为bean的属性设置值或者对其他bean的引用
- 调用bean的初始化方法
- bean可以使用了
- 当容器关闭时,调用bean的销毁的方法

### xml自动装配

- 配置文件 根据名称

  ```xml
   <bean id="dept" class="cn.doudou.spring5.Dept" />
      <bean id="emp" class="cn.doudou.spring5.emp" autowire="byName"/>
  ```

- 配置文件 根据类型

  ```xml
   <bean id="dept" class="cn.doudou.spring5.Dept" />
      <bean id="emp" class="cn.doudou.spring5.emp" autowire="byType"/>
  ```

### xml引入外部文件

```xml
<context:property-placeholder location="外部文件路径"/>
```



### 注解



`Bean管理`

```
@Controller
```

```
@Component
```

```
@Service
```

```
@Repository
```

`扫描组件`

```xml
<context:component-scan base-package=""/>
```

`只扫描那些包`

```xml
    <context:component-scan base-package="" use-default-filters="false">
        <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
    </context:component-scan>
```

`不扫描那些包`

```xml
    <context:component-scan base-package="" >
        <context:exclude-filter type="annotation" expression=""/>
    </context:component-scan>
```

`属性注入`

```
@AutoWired	根据类型
```

```
@Qualifier	根据属性的名称
```

```
@Resource	可以根据类型也可以根据名称
```

```
@Value	注入普通属性
```

`配置类`

```
@Configuration
```

`扫描注解`

```
@ComponentScan
```

## AOP

`面向切面,不修改源代码对源代码进行扩展`

### 底层原理

`Aop的底层使用的是动态代理`

有接口情况,使用JDk动态代理 接口实现类的代理对象

没有接口情况,使用CGLIB动态代理 子类实现

### AOP(JDk的动态代理)

- 创建接口

  ```java
  package cn.doudou.spring5;
  
  /**
   * Create By 王嘉浩
   * Time 2020/6/14
   */
  public interface UserDao {
      public int add(int a, int b);
      public String updata(String id);
  }
  
  ```

- 实现类

  ```java
  package cn.doudou.spring5;
  
  /**
   * Create By 王嘉浩
   * Time 2020/6/14
   */
  public class UserDaoImpl implements UserDao {
      @Override
      public int add(int a, int b) {
          return a + b;
      }
  
      @Override
      public String updata(String id) {
          return id;
      }
  }
  
  ```

- 代理类

  ```java
  package cn.doudou.spring5;
  
  import java.io.LineNumberReader;
  import java.lang.reflect.InvocationHandler;
  import java.lang.reflect.Method;
  import java.lang.reflect.Proxy;
  import java.util.Arrays;
  
  /**
   * Create By 王嘉浩
   * Time 2020/6/14
   */
  public class JDKProxy {
      public static void main(String[] args) {
          Class[] interfaces = {UserDao.class};
          UserDao dao = (UserDao) Proxy.newProxyInstance(JDKProxy.class.getClassLoader(), interfaces, new UserDaoproxy(new UserDaoImpl()));
          dao.updata("王嘉浩");
      }
  }
  
  class UserDaoproxy implements InvocationHandler {
  
      private Object object;
  
      public UserDaoproxy(Object object) {
          this.object = object;
      }
  
      //增强的逻辑
      @Override
      public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
          //执行前
          System.out.println("方法之前执行....." + method.getName());
          //执行当前方法
          int invoke = 0;
          if (method.getName().equals("add")) {
              invoke = (int) method.invoke(object, args);
              System.out.println("add");
              return invoke;
          }
          if (method.getName().equals("updata")) {
              System.out.println("updata");
              return Arrays.toString(args);
          }
          //执行后
          System.out.println("方法执行后....." + object);
          return null;
      }
  }
  //可以根据自己的需求进行代理的实现,上面只是演示
  ```

### AOP术语

- 连接点	类里面的那些方法可以被增强
- 切入点    实际增强的方法
- 通知(增强)     实际增强的逻辑部分
  - 前置通知
  - 后置通知
  - 环绕通知
  - 异常通知
  - 最终通知
- 切面   把通知应用到切入点过程

### xml

```xml
<dependency>
            <groupId>aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.5.4</version>
        </dependency>
```

### 切入点表达式

**作用:知道对那个类里面的那个方法进行增强**

#### 语法:

```
execution(  [权限修饰符]  [返回类型]  [类全路径]  [方法名称]  [参数列表]  )
```

#### xm配置头

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
                           http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd
">
    <!--开启注解扫描-->
    <context:component-scan base-package="cn.doudou.aop.*"/>
    <!--开启aspectj代理对象-->
    <aop:aspectj-autoproxy></aop:aspectj-autoproxy>
</beans>
```



### AspectJ注解

- ```java
   //前置通知
      @Before(value = "execution(* cn.doudou.spring5.aop.User.add(..))")
      public void before() {
          System.out.println("前置通知....");
      }
  ```

   
  
- ```java
  //后置通知
  @After(value = "execution(* cn.doudou.spring5.aop.User.add(..))")
  public void after(){
      System.out.println("后置通知....");
  }
  ```
  
- ```java
   
      //最终通知 
      @AfterReturning(value = "execution(* cn.doudou.spring5.aop.User.add(..))")
          public void AfterReturning(){
              System.out.println("最终通知....");
          }
      
  ```

- ```java
   //异常通知
   @AfterThrowing(value = "execution(* cn.doudou.spring5.aop.User.add(..))")
       public void AfterThrowing(){
           System.out.println("异常....");
       }
   ```

- ```java
     //环绕通知
       @Around(value = "execution(* cn.doudou.spring5.aop.User.add(..))")
       public void Around(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {
           System.out.println("环绕前....");
           proceedingJoinPoint.proceed();
           System.out.println("环绕后....");
       }
   ```

- ```java
    //切入点抽取
       @Pointcut(value = "execution(* cn.doudou.spring5.aop.User.add(..))")
       public void poin(){
      
       }
   //调用
      //前置通知
       @Before(value = "poin()")
       public void before() {
           System.out.println("前置通知....");
       }
   ```

- ```
   @Order(1) 可以对多个增强类进行优先的设置 数字越小越优先 越大越后
   ```

- ```
   @EnableAspectJAutoProxy(proxyTargetClass = true)  //基于完全注解开发使用 等价于   <!--开启aspectj生成代对象-->
       <aop:aspectj-autoproxy/>
   ```

### 基于Aspect J 案例

- 创建类

  ```java
  package cn.doudou.spring5.aop;
  
  import org.aspectj.lang.annotation.Before;
  import org.springframework.stereotype.Component;
  
  /**
   * Create By 王嘉浩
   * Time 2020/6/14
   */
  @Component
  public class User {
  
      public void add() {
          System.out.println("add......");
      }
  }
  
  ```

- 配置文件

  ```xml
   <!--注解扫描-->
      <context:component-scan base-package="cn.doudou.spring5"/>
      <!--开启aspectj生成代对象-->
      <aop:aspectj-autoproxy/>
  ```

- 代理类

  ```java
  package cn.doudou.spring5.aop;
  
  import org.aspectj.lang.ProceedingJoinPoint;
  import org.aspectj.lang.annotation.*;
  import org.springframework.stereotype.Component;
  
  /**
   * Create By 王嘉浩
   * Time 2020/6/14
   */
  @Component
  @Aspect
  public class UserProxy {
      //前置通知
      @Before(value = "execution(* cn.doudou.spring5.aop.User.add(..))")
      public void before() {
          System.out.println("前置通知....");
      }
      @After(value = "execution(* cn.doudou.spring5.aop.User.add(..))")
      public void after(){
          System.out.println("后置通知....");
      }
      @AfterReturning(value = "execution(* cn.doudou.spring5.aop.User.add(..))")
      public void AfterReturning(){
          System.out.println("最终通知....");
      }
      @AfterThrowing(value = "execution(* cn.doudou.spring5.aop.User.add(..))")
      public void AfterThrowing(){
          System.out.println("异常....");
      }
      //环绕通知
      @Around(value = "execution(* cn.doudou.spring5.aop.User.add(..))")
      public void Around(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {
          System.out.println("环绕前....");
          proceedingJoinPoint.proceed();
          System.out.println("环绕后....");
      }
  }
  
  ```

- 测试 运行

### Aspect J配置文件

- 创建类

  ```java
  package cn.doudou.spring5.aopxml;
  
  /**
   * Create By 王嘉浩
   * Time 2020/6/14
   */
  public class Book {
      public void buy(){
          System.out.println("buy.....");
      }
  }
  
  ```

- 创建代理类 代理方法

  ```java
  package cn.doudou.spring5.aopxml;
  
  /**
   * Create By 王嘉浩
   * Time 2020/6/14
   */
  public class BookProxy {
      public void  before(){
          System.out.println("付钱.....");
      }
  }
  
  ```

- 配置文件

  ```xml
   <bean id="book" class="cn.doudou.spring5.aopxml.Book"/>
      <bean id="bookproxy" class="cn.doudou.spring5.aopxml.BookProxy"/>
      <!--配置aop-->
      <aop:config>
          <!--切入点-->
          <aop:pointcut id="b" expression="execution(* cn.doudou.spring5.aopxml.Book.buy(..))"/>
          <!--配置切面-->
          <aop:aspect ref="bookproxy">
              <!--method增强的方法 pointcut-ref切入点 -->
              <aop:before method="before" pointcut-ref="b"/>
          </aop:aspect>
      </aop:config>
  ```

- 测试 运行

### JdbcTemplate

pom

```xml
  <!-- https://mvnrepository.com/artifact/com.alibaba/druid -->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.1.23</version>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.45</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>5.0.3.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
           <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.0.3.RELEASE</version>
        </dependency>
```

`增删改`

- 配置文件

  ```xml
   <!--数据库-->
      <bean id="datasource" class="com.alibaba.druid.pool.DruidDataSource">
          <property name="username" value="root"/>
          <property name="url" value="jdbc:mysql:///acc"/>
          <property name="password" value="0009"/>
          <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
      </bean>
      <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
          <property name="dataSource" ref="datasource"/>
      </bean>
      <context:component-scan base-package="cn.doudou.spring5.jdbc"/>
  ```

- dao

  ```java
  package cn.doudou.spring5.jdbc.dao.impl;
  
  import cn.doudou.spring5.jdbc.dao.AccDao;
  import cn.doudou.spring5.jdbc.pojo.Account;
  import org.springframework.beans.factory.annotation.Autowired;
  import org.springframework.jdbc.core.JdbcTemplate;
  import org.springframework.stereotype.Component;
  
  /**
   * Create By 王嘉浩
   * Time 2020/06/14 16:42
   */
  @Component
  public class AccDaoImpl implements AccDao {
      //注入JdbcTemplate
      @Autowired
      private JdbcTemplate jdbcTemplate;
  
      public void add(Account account) {
          int update = jdbcTemplate.update("insert into account values (?,?,?)", account.getId(), account.getName(), account.getMoney());
      }
  }
  
  ```

- service

  ```java
  package cn.doudou.spring5.jdbc.service;
  
  import cn.doudou.spring5.jdbc.dao.AccDao;
  import cn.doudou.spring5.jdbc.pojo.Account;
  import org.aspectj.lang.annotation.Around;
  import org.springframework.beans.factory.annotation.Autowired;
  import org.springframework.jdbc.core.JdbcTemplate;
  import org.springframework.stereotype.Service;
  
  /**
   * Create By 王嘉浩
   * Time 2020/06/14 16:43
   */
  @Service
  public class AccServcie {
      @Autowired
      private AccDao dao;
  
      public void  add(Account a){
          dao.add(a);
      }
  }
  
  ```

- 测试 运行

  ```java
  package cn.douduo.spring5;
  
  import cn.doudou.spring5.jdbc.pojo.Account;
  import cn.doudou.spring5.jdbc.service.AccServcie;
  import org.junit.Test;
  import org.springframework.beans.factory.annotation.Autowired;
  import org.springframework.context.ApplicationContext;
  import org.springframework.context.support.ClassPathXmlApplicationContext;
  
  /**
   * Create By 王嘉浩
   * Time 2020/06/14 16:51
   */
  public class TestAcc {
  
      @Test
      public void test1() {
          ApplicationContext ac = new ClassPathXmlApplicationContext("application3.xml");
          AccServcie accService = (AccServcie) ac.getBean("accServcie", AccServcie.class);
          Account account1 = new Account();
          account1.setId(4);
          account1.setName("王");
          account1.setMoney(78F);
          accService.add(account1);
      }
  }
  
  ```

- 注 : 修改 和 删除只需要修改SQL语句就可以完成

`查询`

- dao

  ```java
      @Override
      public List<Account> findAll() {
          List<Account> query = jdbcTemplate.query("select * from account", new BeanPropertyRowMapper<Account>(Account.class));
          return query;
      }
  ```

- 剩下的别的一样

- 测试运行

`批量添加方法 修改方法 删除方法` 

```java
jdbcTemplate.batchUpdate
```

## 事务

事务四个特性

- 原子性
- 一致性
- 隔离性
- 持久性

### xml配置

```xml
<!-- 定义事务 -->
<bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
		<property name="dataSource" ref="dataSource" /><!-- ref:引入数据源  -->
</bean>
 
<!-- 配置 Annotation 驱动，扫描@Transactional注解的类定义事务 <!-- 启动事物注解 transaction-manager的值必须和上面这个bean的id一样---->
<tx:annotation-driven transaction-manager="transactionManager" proxy-target-class="true" />
```

### 注解配置

```
@Transactional注解的属性:

1）事物的传播行为：propagation，即当前事物方法被另一个事物方法调用时如何使用事物，默认取值为REQUIRED，即使用调用的方法的事物。

2）事物的隔离级别：isolation:指定事务的隔离级别，最常用的取值为：READ_COMMITTED，读以提交。

3）事务回滚：

    （1）noRollbackFor、noRollbackForClassName：对这个异常不进行回滚 通常情况下取默认值即可。

    （2）rollbackFor、rollbackForClassName：对这个异常进行回滚 通常情况下取默认值即可。

4）只读事务：readOnly，只能读取数据，可以帮助数据库引擎优化。如果是只读，应设置：readOnly=true

5）强制回滚时间：timeout:指定强制回滚的时间，单位秒，如该方法执行了5秒，而该属性设置的是2秒，如果到2秒了，该方法还没有执行完，该事务也会对该方法进行强制回滚。
```

```java
/**
     * 事物注解
     * 使用propagation 指定事物的传播行为，即当前事物方法被另一个事物方法调用时如何使用事物，默认取值为REQUIRED，即使用调用方法的事物
     * REQUIRES_NEW：使用自己的事物，调用的事物方法的事物被挂起。
     * isolation:指定事务的隔离级别，    最常用的取值为：READ_COMMITTED，读以提交
     * noRollbackFor:对这个异常不进行回滚 通常情况下取默认值即可。
     * rollbackFor:对这个异常进行回滚
     * readOnly:只读事务，只能读取数据，可以帮助数据库引擎优化。如果是只读，应设置：readOnly=true
     * timeout:指定强制回滚的时间，单位秒，如该方法执行了5秒，而该属性设置的是2秒，如果到2秒了，该方法还没有执行完，该事务也会对该方法进行强制回滚。
     */
    @Transactional(propagation=Propagation.REQUIRED,isolation=Isolation.READ_COMMITTED,
            noRollbackFor={UserException.class},noRollbackForClassName="UserException",
            rollbackFor={UserException.class},rollbackForClassName="UserException",
            readOnly=false,timeout=100)
    public void updatUser(){
        System.out.println("需要用到事务的方法");
    }
```

## @Nullable注解

可以使用在方法上面,属性上面,参数上面,表示方法返回值可以为空,属性值可以为空,参数值可以为空

## WebFlux

#### 介绍:

1. WebFlux是Spring5添加的新的模块,用于web开发的,功能SpringMVC类似的,webflx使用当前一种比较流行响应式编程出现的框架
2. 是一种异步非阻塞的框架
   1. 异步 同步
   2. 非阻塞 阻塞

#### 代码

```java
package cn.doudou.demoreactor8.javaReactor8;

import java.util.Observable;

/**
 * @BelongsPackage: cn.doudou.demoreactor8.javaReactor8
 * @Author: 王嘉浩
 * @Description:
 * @CreateTime: 2022-01-16 14:03
 * @Email: douoai@163.com
 */
public class ObserverDemo extends Observable {
    public static void main(String[] args) {
        ObserverDemo observer = new ObserverDemo();
        //添加观察者
        observer.addObserver((o, arg) -> {
            System.out.println("发生了变化");
        });

        observer.addObserver((o, arg) -> {
            System.out.println("收到通知");
        });
        //数据变化
        observer.setChanged();
        //通知
        observer.notifyObservers();
    }
}

```

