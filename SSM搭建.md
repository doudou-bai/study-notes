# SSM搭建

### 搭建流程:

### pom.xml的jar包

- 版本约束

  ```xml
     <properties>
          <spring.version>5.0.2.RELEASE</spring.version>
          <slf4j.version>1.6.6</slf4j.version>
          <log4j.version>1.2.12</log4j.version>
          <shiro.version>1.2.3</shiro.version>
          <mysql.version>5.1.6</mysql.version>
          <mybatis.version>3.4.5</mybatis.version>
      </properties>
  ```

- jar包导入

  ```xml
      <dependencies>
          <!--  spring  -->
             <!--  必须是1.8 以上否则报错  -->
          <dependency>
              <groupId>org.aspectj</groupId>
              <artifactId>aspectjweaver</artifactId>
              <version>1.8.13</version>
          </dependency>
          <dependency>
              <groupId>org.springframework</groupId>
              <artifactId>spring-aop</artifactId>
              <version>${spring.version}</version>
          </dependency>
  
          <dependency>
              <groupId>org.springframework</groupId>
              <artifactId>spring-context</artifactId>
              <version>${spring.version}</version>
          </dependency>
  
          <dependency>
              <groupId>org.springframework</groupId>
              <artifactId>spring-context-support</artifactId>
              <version>${spring.version}</version>
          </dependency>
  
          <dependency>
              <groupId>org.springframework</groupId>
              <artifactId>spring-web</artifactId>
              <version>${spring.version}</version>
          </dependency>
  
          <dependency>
              <groupId>org.springframework</groupId>
              <artifactId>spring-orm</artifactId>
              <version>${spring.version}</version>
          </dependency>
  
          <dependency>
              <groupId>org.springframework</groupId>
              <artifactId>spring-beans</artifactId>
              <version>${spring.version}</version>
          </dependency>
  
          <dependency>
              <groupId>org.springframework</groupId>
              <artifactId>spring-core</artifactId>
              <version>${spring.version}</version>
          </dependency>
  
          <dependency>
              <groupId>org.springframework</groupId>
              <artifactId>spring-test</artifactId>
              <version>${spring.version}</version>
          </dependency>
  
          <dependency>
              <groupId>org.springframework</groupId>
              <artifactId>spring-webmvc</artifactId>
              <version>${spring.version}</version>
          </dependency>
  
          <dependency>
              <groupId>org.springframework</groupId>
              <artifactId>spring-tx</artifactId>
              <version>${spring.version}</version>
          </dependency>
  
          <dependency>
              <groupId>junit</groupId>
              <artifactId>junit</artifactId>
              <version>4.12</version>
              <scope>test</scope>
          </dependency>
  
          <dependency>
              <groupId>mysql</groupId>
              <artifactId>mysql-connector-java</artifactId>
              <version>${mysql.version}</version>
          </dependency>
  
          <dependency>
              <groupId>javax.servlet</groupId>
              <artifactId>servlet-api</artifactId>
              <version>2.5</version>
              <scope>provided</scope>
          </dependency>
  
          <dependency>
              <groupId>javax.servlet.jsp</groupId>
              <artifactId>jsp-api</artifactId>
              <version>2.0</version>
              <scope>provided</scope>
          </dependency>
  
          <dependency>
              <groupId>jstl</groupId>
              <artifactId>jstl</artifactId>
              <version>1.2</version>
          </dependency>
  
          <!--  log  start  -->
          <dependency>
              <groupId>log4j</groupId>
              <artifactId>log4j</artifactId>
              <version>${log4j.version}</version>
          </dependency>
  
          <dependency>
              <groupId>org.slf4j</groupId>
              <artifactId>slf4j-api</artifactId>
              <version>${slf4j.version}</version>
          </dependency>
  
          <dependency>
              <groupId>org.slf4j</groupId>
              <artifactId>slf4j-log4j12</artifactId>
              <version>${slf4j.version}</version>
          </dependency>
          <!--  log  end  -->
          <dependency>
              <groupId>org.mybatis</groupId>
              <artifactId>mybatis</artifactId>
              <version>${mybatis.version}</version>
          </dependency>
  
          <dependency>
              <groupId>org.mybatis</groupId>
              <artifactId>mybatis-spring</artifactId>
              <version>1.3.0</version>
          </dependency>
  
          <dependency>
              <groupId>c3p0</groupId>
              <artifactId>c3p0</artifactId>
              <version>0.9.1.2</version>
              <type>jar</type>
              <scope>compile</scope>
          </dependency>
  </dependencies>
  ```

- dao层

  - Mybatis框架

- service层

- domain层

  - 实体类

- controller层

  - SpringMVC框架

- resources文件夹

  - applicaltionConfig.xml<Spring框架的xml>

    - 头部约束

      ```xml
      <?xml version="1.0" encoding="UTF-8" ?>
      <beans xmlns="http://www.springframework.org/schema/beans"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xmlns:aop="http://www.springframework.org/schema/aop"
             xmlns:tx="http://www.springframework.org/schema/tx"
             xmlns:context="http://www.springframework.org/schema/context"
             xmlns:contxt="http://www.springframework.org/schema/util"
             xsi:schemaLocation="http://www.springframework.org/schema/beans
              http://www.springframework.org/schema/beans/spring-beans.xsd
              http://www.springframework.org/schema/tx
              http://www.springframework.org/schema/tx/spring-tx.xsd
              http://www.springframework.org/schema/aop
              http://www.springframework.org/schema/aop/spring-aop.xsd
              http://www.springframework.org/schema/context
              http://www.springframework.org/schema/context/spring-context.xsd 			
              http://www.springframework.org/schema/util 									
              http://www.springframework.org/schema/util/spring-util.xsd
          http://www.springframework.org/schema/beans ">
      </beans>
      ```
  ```
    
    - 开启注解扫描排除controller
    
      ```xml
       <!--开启注解扫描-->
          <context:component-scan base-package="cn.doudou">
              <!--配置那些注解不扫描-->
        <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
          </context:component-scan>
  ```
  
  ​    
  
    ```
      context:component-scan
      context:exclude-filter
    ```
  
    - 加载jdbcConfig配置文件
    
      ```xml\
      <context:property-placeholder location="classpath:jdbcConfig.properties"/>
      ```
  
- 数据库的4大属性
  
  ```XML
       <bean id="comboPooledDataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
              <property name="driverClass" value="${jdbc.driver}"/>
              <property name="jdbcUrl" value="${jdbc.url}"/>
              <property name="user" value="${jdbc.username}"/>
              <property name="password" value="${jdbc.password}"/>
      </bean>
  ```

    - 使用SqlSessionFactoryBean创建工厂对象
    
      ```xml
      <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
              <property name="dataSource" ref="comboPooledDataSource"/>
      </bean>
      ```

    - 开启包的映射

      ```xml
       <bean id="mapperScannerConfigurer" class="org.mybatis.spring.mapper.MapperScannerConfigurer">
             <property name="basePackage" value="cn.doudou.dao"></property>
          </bean>
      ```
  
- 配置事务spring
  
  配置事务管理器
  
  ~~~xml
  ```xml
   <!--事务管理器-->
      <bean id="dtaSourceTransactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
          <property name="dataSource" ref="comboPooledDataSource"></property>
      </bean>
  ```
  ~~~
  
  事务的通知
  
    ```xml
     <tx:advice id="txAdvice" transaction-manager="dtaSourceTransactionManager">
              <tx:attributes>
                  <tx:method name="find*" read-only="true"/>
                  <tx:method name="*" isolation="DEFAULT"/>
              </tx:attributes>
        </tx:advice>
    ```
  
  ~~~xml
  配置aop增强
    
  ```xml
  <aop:config>
          <aop:advisor advice-ref="txAdvice" pointcut="execution(* cn.doudou.service.Impl.AccountServiceImpl.*(..))"/>
      </aop:config>
  ```
  ~~~
  
    
  
- jdbcConfig.properties<jdbc的外部配置文件>
  
    ```properties
    jdbc.driver=com.mysql.jdbc.Driver
  jdbc.url=jdbc:mysql://localhost:3306/acc
  jdbc.username=root
  jdbc.password=0009
  ```
  
  - springmvc.xml<SpringMVC的xml文件>
  
    - 头部约束
  
      ```xml
    <?xml  version="1.0"  encoding="UTF-8"?>
      <beans xmlns="http://www.springframework.org/schema/beans"
             xmlns:mvc="http://www.springframework.org/schema/mvc"
           xmlns:context="http://www.springframework.org/schema/context"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
      http://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/mvc
      http://www.springframework.org/schema/mvc/spring-mvc.xsd
      http://www.springframework.org/schema/context
      http://www.springframework.org/schema/context/spring-context.xsd">
      ```
    
      
  
    - 开启注解扫描只扫描controller
    
    - ```xml
     <!--开启注解扫描-->
          <context:component-scan base-package="cn.doudou">
              <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
          </context:component-scan>
      ```
      
      ```
      context:component-scan
      context:include-filter
      ```
    
  - 配置视图解析器
    
      ```xml
      <!-- 配置视图解析器 -->
            <bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
              <property name="prefix" value="/WEB-INF/pages/"></property>
              <property name="suffix" value=".jsp"></property>
          </bean>
          <!-- 配置spring开启注解mvc的支持     <mvc:annotation-driven></mvc:annotation-driven>-->
          <mvc:annotation-driven ></mvc:annotation-driven >
          <!--不拦截静态资源-->
          <mvc:resources location="/" mapping="/**/*.js"/>
      ```
    
    - 排除静态资源
    
    ```xml
    <mvc:resources mapping="/css/" location="/css/**"/>
    <mvc:resources mapping="/js/" location="/js/**"/>
    <mvc:resources mapping="/images/" location="/images/**"/>
    ```
    
    - 开启扫描
    
      ```xml
        <mvc:annotation-driven/>
      ```
    
  - web.xml配置
  
    - 头部约束
  
      ```xml
      
      <?xml version="1.0" encoding="UTF-8"?>
      <web-app xmlns="http://java.sun.com/xml/ns/javaee"
               xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
               xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
                http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
               version="3.0">
      </web-app>
      
      ```
    
  
    - 前端控制器
    
      ```xml
       <servlet>
              <servlet-name>dispatcherServlet</servlet-name>
              <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
              <!--加载springmvc的配置文件-->
              <init-param>
                  <param-name>contextConfigLocation</param-name>
                  <param-value>classpath:springmvc.xml</param-value>
              </init-param>
              <!--启动服务器创建该Servlet-->
              <load-on-startup>1</load-on-startup>
          </servlet>
         <servlet-mapping>
              <servlet-name>dispatcherServlet</servlet-name>
              <url-pattern>/</url-pattern>
      </servlet-mapping>
      ```
    
    - 解决中文乱码
    
      ```xml
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
      ```
    
    - 配置文件的路径
    
      ```xml
       <context-param>
              <param-name>contextConfigLocation</param-name>
              <param-value>classpath:applicaltionConfig.xml</param-value>
      </context-param>
      ```
  
      
    
    - 配置spring的监听器,默认只加载WEB-INF目录下的配置文件  需要自己设置文件位置
    
      ```xml
       <listener>
              <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
        </listener>
      ```
    
      

