## Shiro

### 快速入门

- pom.ml文件导包

  ```xml
     <dependencies>
          <dependency>
              <groupId>junit</groupId>
              <artifactId>junit</artifactId>
              <version>4.12</version>
              <scope>test</scope>
          </dependency>
          <!-- shiro依赖 -->
          <dependency>
              <groupId>org.apache.shiro</groupId>
              <artifactId>shiro-core</artifactId>
              <version>1.4.0</version>
          </dependency>
          <dependency>
              <groupId>org.apache.shiro</groupId>
              <artifactId>shiro-web</artifactId>
              <version>1.4.0</version>
          </dependency>
          <!-- 日志依赖 -->
          <dependency>
              <groupId>org.slf4j</groupId>
              <artifactId>slf4j-api</artifactId>
              <version>1.7.12</version>
          </dependency>
          <dependency>
              <groupId>org.slf4j</groupId>
              <artifactId>slf4j-log4j12</artifactId>
              <version>1.7.12</version>
          </dependency>
          <dependency>
              <groupId>log4j</groupId>
              <artifactId>log4j</artifactId>
              <version>1.2.16</version>
          </dependency>
          <dependency>
              <groupId>commons-logging</groupId>
              <artifactId>commons-logging</artifactId>
              <version>1.2</version>
          </dependency>
          <!-- ============ Servlet ============ -->
          <dependency>
              <groupId>javax.servlet.jsp</groupId>
              <artifactId>jsp-api</artifactId>
              <version>2.1</version>
              <scope>provided</scope>
          </dependency>
          <dependency>
              <groupId>javax.servlet</groupId>
              <artifactId>jstl</artifactId>
              <version>1.2</version>
          </dependency>
          <dependency>
              <groupId>javax.servlet</groupId>
              <artifactId>javax.servlet-api</artifactId>
              <version>3.1.0</version>
              <scope>provided</scope>
          </dependency>
  
          <!-- ============== SpringMVC ============== -->
          <dependency>
              <groupId>org.springframework</groupId>
              <artifactId>spring-webmvc</artifactId>
              <version>4.3.6.RELEASE</version>
          </dependency>
  
          <!-- lombok -->
          <dependency>
              <groupId>org.projectlombok</groupId>
              <artifactId>lombok</artifactId>
              <version>1.18.4</version>
              <scope>provided</scope>
          </dependency>
  
          <!-- spring -->
          <dependency>
              <groupId>org.springframework</groupId>
              <artifactId>spring-context-support</artifactId>
              <version>4.3.6.RELEASE</version>
          </dependency>
  
          <!--  AOP  -->
          <dependency>
              <groupId>org.springframework</groupId>
              <artifactId>spring-aspects</artifactId>
              <version>4.3.6.RELEASE</version>
          </dependency>
  
          <!-- spring-jdbc(会传递tx) ，context-support ,aspects-->
          <dependency>
              <groupId>org.springframework</groupId>
              <artifactId>spring-jdbc</artifactId>
              <version>4.3.6.RELEASE</version>
          </dependency>
          <dependency>
              <groupId>org.springframework</groupId>
              <artifactId>spring-web</artifactId>
              <version>4.3.6.RELEASE</version>
          </dependency>
  
          <!-- spring+mybatis集成依赖 -->
          <dependency>
              <groupId>org.mybatis</groupId>
              <artifactId>mybatis-spring</artifactId>
              <version>1.3.1</version>
          </dependency>
  
          <!-- MyBatis -->
          <dependency>
              <groupId>org.mybatis</groupId>
              <artifactId>mybatis</artifactId>
              <version>3.4.5</version>
          </dependency>
          <!-- mysql驱动 依赖 -->
          <dependency>
              <groupId>mysql</groupId>
              <artifactId>mysql-connector-java</artifactId>
              <version>5.1.25</version>
          </dependency>
  
          <!-- druid依赖 -->
          <dependency>
              <groupId>c3p0</groupId>
              <artifactId>c3p0</artifactId>
              <version>0.9.1.2</version>
          </dependency>
      </dependencies>
      <build>
          <resources>
              <resource>
                  <directory>src/main/java</directory>
                  <includes>
                      <include>**/*.xml</include>
                  </includes>
                  <filtering>false</filtering>
              </resource>
              <resource>
                  <directory>src/main/resources</directory>
                  <includes>
                      <include>**/*.properties</include>
                      <include>**/*.xml</include>
                      <include>**/*.org</include>
                      <include>**/*.txt</include>
                      <include>**/*.ini</include>
                  </includes>
                  <filtering>false</filtering>
              </resource>
          </resources>
      </build>
  ```

- web.xml

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xmlns="http://java.sun.com/xml/ns/javaee"
           xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
           version="2.5">
      <!--mvc的配置-->
      <servlet>
          <servlet-name>mvc</servlet-name>
          <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
          <init-param>
              <param-name>contextConfigLocation</param-name>
              <param-value>classpath:springmvc.xml</param-value>
          </init-param>
          <load-on-startup>1</load-on-startup>
      </servlet>
  <!--	拦截的路径-->
      <servlet-mapping>
          <servlet-name>mvc</servlet-name>
          <url-pattern>/</url-pattern>
      </servlet-mapping>
  	<!--shiro的配置-->
      <filter>
          <filter-name>shiroFiler</filter-name>
          <filter-class>org.apache.shiro.web.servlet.ShiroFilter</filter-class>
      </filter>
      <filter-mapping>
          <filter-name>shiroFiler</filter-name>
          <url-pattern>/*</url-pattern>
      </filter-mapping>
      <listener>
          <listener-class>org.apache.shiro.web.env.EnvironmentLoaderListener</listener-class>
      </listener>
  	<!--Spring的配置-->
      <listener>
          <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
      </listener>
      <context-param>
          <param-name>contextConfigLocation</param-name>
          <param-value>classpath:applicationContext.xml</param-value>
      </context-param>
      <filter>
          <filter-name>encoding</filter-name>
          <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
          <init-param>
              <param-name>encoding</param-name>
              <param-value>UTF-8</param-value>
          </init-param>
      </filter>
      <filter-mapping>
          <filter-name>encoding</filter-name>
          <url-pattern>/*</url-pattern>
      </filter-mapping>
  </web-app>
  ```

- 编写数据库文件

- 创建applicaltionContext.xml

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:aop="http://www.springframework.org/schema/aop"
         xmlns:tx="http://www.springframework.org/schema/tx"
         xmlns:context="http://www.springframework.org/schema/context"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
                             http://www.springframework.org/schema/beans/spring-beans.xsd
                             http://www.springframework.org/schema/aop
                             http://www.springframework.org/schema/aop/spring-aop.xsd
                             http://www.springframework.org/schema/tx
                             http://www.springframework.org/schema/tx/spring-tx.xsd
                             http://www.springframework.org/schema/context
                             http://www.springframework.org/schema/context/spring-context.xsd">
  
      <!-- 导入外部参数文件 -->
      <context:property-placeholder location="classpath:jdbc.properties"/>
  
      <!-- 连接池：druid -->
      <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
          <!-- 基本属性 url、user、password -->
          <property name="jdbcUrl" value="${jdbc.url}"/>
          <property name="driverClass" value="${jdbc.driver}"/>
          <property name="user" value="${jdbc.user}"/>
          <property name="password" value="${jdbc.password}"/>
      </bean>
  
  
      <bean id="sqlSessionFactory04" class="org.mybatis.spring.SqlSessionFactoryBean">
          <property name="dataSource" ref="dataSource"/>
          <property name="typeAliasesPackage" value="cn.doudou.pojo"/>
      </bean>
  
      <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
          <property name="basePackage" value="cn.doudou.dao"/>
      </bean>
  
  
      <!-- 配置注解扫描：让spring去发现注解，进而实现对应的功能 -->
      <context:component-scan base-package="cn.doudou">
          <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
      </context:component-scan>
  
  
      <bean id="tx" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
          <property name="dataSource" ref="dataSource"/>
      </bean>
      <tx:annotation-driven transaction-manager="tx"/>
  </beans>
  ```

- jdbc.properties

  ```
  jdbc.user=root
  jdbc.password=0009
  jdbc.url=jdbc:mysql://localhost:3306/shiro?useUnicode=true&characterEncoding=utf8&useServerPrepStmts=true&cachePrepStmts=true
  jdbc.driver=com.mysql.jdbc.Driver
  ```

- spring-mvc.xml

  ```xml
  <beans 	xmlns="http://www.springframework.org/schema/beans"
            xmlns:context="http://www.springframework.org/schema/context"
            xmlns:mvc="http://www.springframework.org/schema/mvc"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://www.springframework.org/schema/beans
  							http://www.springframework.org/schema/beans/spring-beans.xsd
  							http://www.springframework.org/schema/context
  							http://www.springframework.org/schema/context/spring-context.xsd
  							http://www.springframework.org/schema/mvc
  							http://www.springframework.org/schema/mvc/spring-mvc.xsd">
  
      <!-- 告知springmvc  哪些包中 存在 被注解的类
           use-default-filters="false"  遇到到 @Controller  @Service  @Repository  @Component类，都会忽略
      -->
      <context:component-scan base-package="cn.doudou">
          <!-- 只扫描  有@Controller注解的类 -->
          <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
      </context:component-scan>
      <!-- 注册注解开发驱动 -->
      <mvc:annotation-driven></mvc:annotation-driven>
  
      <!-- 视图解析器
  	     作用：1.捕获后端控制器的返回值="index"
  	          2.解析： 在返回值的前后 拼接 ==> "/index.jsp"
  	 -->
      <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
          <!-- 前缀 -->
          <property name="prefix" value="/"></property>
          <!-- 后缀 -->
          <property name="suffix" value=".jsp"></property>
      </bean>
      <!-- 在项目中 自动添加一个 映射{"/**" : DefaultServletHttpRequestHandler}
           请求进入前端后，会先匹配自定义的Handler，如果没有匹配的则进入DefaultServletHttpRequestHandler。
           DefaultServletHttpRequestHandler会将请求转发给Tomcat中名为"default"的servlet。
           最终实现了静态资源的访问
      -->
      <mvc:default-servlet-handler/>
  
     <!-- <bean class="cn.doudou.utils.Ex"></bean>-->
  </beans>
  ```

  

- shiro.ini

  ```ini
  [main]
  # 没有登录时
  shiro.loginurl = /user/login
  # 权限不足
  shiro.unauthorizedUrl = /user/404
  # 登录后跳出
  shiro.redirectUrl = /
  #声明密码⽐对器
  credentialsMatcher=org.apache.shiro.authc.credential.HashedCredentialsMatcher
  credentialsMatcher.hashAlgorithmName=sha-512
  credentialsMatcher.hashIterations=1000
  #true=hex格式	false=base64格式
  credentialsMatcher.storedCredentialsHexEncoded=false
  #⽐对器关联给realm,则realm中对⽤户做身份认证时，可以使⽤加密⽐对器，对密⽂做⽐对
  realm = cn.doudou.realm.Myrealm
  realm.credentialsMatcher=$credentialsMatcher
  #realm关联给securityManager
  # 声明自定义的realm
  securityManager.realm=$realm
  
  
  
  
  
  [urls]
  /user/findAll = authc,perms["user:query":]
  /login/logout = logout
  #/user/login/page = anon
  #/user/login/logic = anon
  #/user/query = authc
  #/user/update = authc,roles["manager","seller"]
  #/user/delete = authc, perms["user:update","user:delete"]
  #/user/logout = logout
  
  ```

- 编写实体类   pojo

- dao层

- service

- realm

  ```java
  package cn.doudou.realm;
  
  import cn.doudou.pojo.User;
  import cn.doudou.service.PermissionService;
  import cn.doudou.service.RoleService;
  import cn.doudou.service.UserService;
  import com.mchange.lang.ByteUtils;
  import org.apache.shiro.authc.AuthenticationException;
  import org.apache.shiro.authc.AuthenticationInfo;
  import org.apache.shiro.authc.AuthenticationToken;
  import org.apache.shiro.authc.SimpleAuthenticationInfo;
  import org.apache.shiro.authz.AuthorizationInfo;
  import org.apache.shiro.authz.SimpleAuthorizationInfo;
  import org.apache.shiro.realm.AuthorizingRealm;
  import org.apache.shiro.subject.PrincipalCollection;
  import org.apache.shiro.util.ByteSource;
  import org.springframework.web.context.ContextLoader;
  
  import javax.naming.Context;
  import java.util.List;
  import java.util.Set;
  
  public class Myrealm extends AuthorizingRealm {
      /**
       * @param principalCollection
       * @return
       */
      protected AuthorizationInfo doGetAuthorizationInfo(PrincipalCollection principalCollection) {
          String username = (String) principalCollection.getPrimaryPrincipal();
          RoleService roleService = ContextLoader.getCurrentWebApplicationContext().getBean("roleService", RoleService.class);
          PermissionService permissionService = ContextLoader.getCurrentWebApplicationContext().getBean("permissionService", PermissionService.class);
          //查询权限
          Set<String> roles = roleService.findAllUserName(username);
          Set<String> permissions = permissionService.findAllPermissionByName(username);
          //封装对象
          SimpleAuthorizationInfo simpleAuthorizationInfo = new SimpleAuthorizationInfo(roles);
          simpleAuthorizationInfo.addStringPermissions(permissions);
          return simpleAuthorizationInfo;
      }
  
      /**
       * 查询权限信息 并返回即可,不用做任何比对
       * 何时触发
       *
       * @param token
       * @return
       * @throws AuthenticationException
       */
      protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken token) throws AuthenticationException {
          String useranme = (String) token.getPrincipal();
          //查询用户信息
          UserService userService = ContextLoader.getCurrentWebApplicationContext().getBean("userService", UserService.class);
          User user = userService.findByName(useranme);
          //判断是否为空
          if (user == null) {
              return null;//
          }
          return new SimpleAuthenticationInfo(user.getUsername(), user.getPassword(), ByteSource.Util.bytes(user.getSalt()),this.getName());
      }
  }
  
  ```

- controller层

- 加密

  ```
    String salt = UUID.randomUUID().toString();
          Integer item = 1000;
          String sha512Hash = new Sha512Hash(password, salt, item).toBase64();
          return sha512Hash;
  ```

### shiro标签

- 导入标签库

  ```
  <%@taglib prefix="shiro" uri="http://shiro.apache.org/tags" %>
  ```

- 已登录

  ```
  shiro:authenticated
  	属性:
  		用户名:
  	 	<shoro:principal/>
  		
  ```

- 登录

  ```
  shiro:notAuthenticated
  	属性:
  		用户名:
      		<a href="${pageContext.request.contextPath}/user/login">请登录</a>
  ```

- 记住我

  ```
  shiro:user
  ```

- 游客

  ```
  shiro:guest
  ```

- 任何一种角色

  ```
  shiro:hasAnyRoles
  ```

- 指定角色

  ```
  shiro:hasRole
  ```

- 不是指定角色

  ```
  shriro:lacksRole
  ```

- 指定权限

  ```
  shiro:hasPermission
  ```

- 没有指定权限

  ```
  shiro:lacksPermission
  ```


### Session

核心对象

​	    基本功能

- SimpleSession

   生产Session

- SimpleSessionFactory 

  默认实现类

- SessionDAO 

    创建管理

- DefaultSessionManager