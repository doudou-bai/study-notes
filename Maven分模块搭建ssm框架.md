# Maven分模块搭建ssm框架

## 项目<3个模块可能会有更多>

### 项目-dao

- dao层

  - 持久层接口

- domain层

  - 实体类

- resources

  - **applicaltionConfig-dao.xml**

  - 头部约束

    ```xml
        <?xml  version="1.0"  encoding="UTF-8"?>
        <beans xmlns="http://www.springframework.org/schema/beans"
               xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
               xmlns:context="http://www.springframework.org/schema/context"
               xsi:schemaLocation="http://www.springframework.org/schema/beans
                http://www.springframework.org/schema/beans/spring-beans.xsd
                http://www.springframework.org/schema/context
                http://www.springframework.org/schema/context/spring-context.xsd">
    ```

  - 配置信息

    ```xml
     <!--开启spring注解扫描-->
        <context:component-scan base-package="cn.doudou">
            <!--把controller层排除掉-->
            <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
        </context:component-scan>
        <context:property-placeholder location="classpath:jdbcConfig.properties"/>
        <bean id="comboPooledDataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
            <property name="driverClass" value="${jdbc.driver}"/>
            <property name="jdbcUrl" value="${jdbc.url}"/>
            <property name="user" value="${jdbc.username}"/>
            <property name="password" value="${jdbc.password}"/>
        </bean>
        <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
            <property name="dataSource" ref="comboPooledDataSource"/>
        </bean>
        <bean id="mapperScannerConfigurer" class="org.mybatis.spring.mapper.MapperScannerConfigurer">
            <property name="basePackage" value="cn.doudou.dao"></property>
        </bean>
    ```

  - **jdbcConfig.properties**

    ```properties
    jdbc.driver=com.mysql.jdbc.Driver
    jdbc.url=jdbc:mysql://localhost:3306/acc
    jdbc.username=root
    jdbc.password=0009
    
    ```

    

### 项目-service

- service文件夹

  - 接口
  - 实现类

- resources

  - **applicaltionConfig-service.xml**

  - 头部约束

    ```xml
    <?xml  version="1.0"  encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xmlns:aop="http://www.springframework.org/schema/aop"
           xmlns:tx="http://www.springframework.org/schema/tx"
           xmlns:context="http://www.springframework.org/schema/context"
           xsi:schemaLocation="http://www.springframework.org/schema/beans
            http://www.springframework.org/schema/beans/spring-beans.xsd
            http://www.springframework.org/schema/tx
            http://www.springframework.org/schema/tx/spring-tx.xsd
            http://www.springframework.org/schema/aop
            http://www.springframework.org/schema/aop/spring-aop.xsd
            http://www.springframework.org/schema/context
            http://www.springframework.org/schema/context/spring-context.xsd">
    ```

  - 配置

    ```xml
     <context:component-scan base-package="cn.doudou.service"/>
        <!--配置spring事务-->
        <!--事务管理器-->
        <bean id="dtaSourceTransactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
            <property name="dataSource" ref="comboPooledDataSource"></property>
        </bean>
        <!--事务的通知-->
        <tx:advice id="txAdvice" transaction-manager="dtaSourceTransactionManager">
            <tx:attributes>
                <tx:method name="find*" read-only="true"/>
                <tx:method name="*" isolation="DEFAULT"/>
            </tx:attributes>
        </tx:advice>
        <!--配置aop增强-->
        <aop:config>
            <aop:advisor advice-ref="txAdvice" pointcut="execution(* cn.doudou.service.Impl.AccountServiceImpl.*(..))"/>
        </aop:config>
    ```

    

### 项目-web

- java文件夹

  - **controller**
    - 控制器

- resources

  - **springmvc.xml**

  - 头部

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

  - 配置

    ```xml
     <!--配置mvc的注解-->
        <context:component-scan base-package="cn.doudou">
            <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
        </context:component-scan>
        <!--视图解析器-->
        <bean id="internalResourceViewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
            <property name="prefix" value="/WEB-INF/pages/"/>
            <property name="suffix" value=".jsp"/>
        </bean>
        <mvc:resources mapping="/css/" location="/css/**"/>
        <mvc:resources mapping="/js/" location="/js/**"/>
        <mvc:resources mapping="/images/" location="/images/**"/>
        <mvc:annotation-driven/>
    </beans>
    ```

  - **applicaltionConfig.xml**

  - 头部信息

    ```xml
    <?xml  version="1.0"  encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.springframework.org/schema/beans
            http://www.springframework.org/schema/beans/spring-beans.xsd">
    ```

  - 配置

    ```xml
    <import resource="classpath:applicaltionConfig-dao.xml"/>
    <import resource="classpath:applicaltionConfig-service.xml"/>
    ```

    

- webapp

  - 静态资源文件夹

- WEB-INF

  - pages

- test

  - 测试当前项目是否可用