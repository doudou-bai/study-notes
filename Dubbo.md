## Dubbo

### 软件架构

- 单体架构

  - 所有功能在一个项目内 All in one

  - 优点:

    架构简单:开发成本低,开发周期短,适合小型项目

  - 缺点:

    **维护,扩展,难**

- 垂直架构

  - 优点:

    数据栈可以扩展

  - 缺点:

    **不利于维护,开发,扩展**

- SOA架构

  - 优点:

    可以重用,维护性高

  - 缺点:

    **系统之间的业务不同,很难确认功能或者模块是重复读的**

- 微服务架构

  - 优点:

  - 服务层可以独立,抽取的力度更细,采用轻量级框架协议传输,有利于提高开发效率

  - 缺点:

    维护成本高,对技术成本高,团队的的挑战大

### Apache Dubbo

提供了三个核心能力:面向接口的远程方法调用,只能容错和负载均衡,以及服务自动注册和发现

### Dubbo命令

- 启动

  ```
  ./zkServer.sh start
  ```

- 停止

  ```
  ./zkServer.sh stop
  ```

- 查看服务状态

  ```
  ./zkServer.sh status
  ```


### 环境搭建

- 导入jar

  ```xml
   <dependency>
              <groupId>com.alibaba</groupId>
              <artifactId>dubbo</artifactId>
              <version>2.6.2</version>
          </dependency>
  
          <dependency>
              <groupId>org.apache.curator</groupId>
              <artifactId>curator-framework</artifactId>
              <version>2.12.0</version>
          </dependency>
  ```

- 提供端口

- 配置

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:dubbo="http://code.alibabatech.com/schema/dubbo" xmlns:context="http://www.springframework.org/schema/c"
         xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
  		http://dubbo.apache.org/schema/dubbo http://dubbo.apache.org/schema/dubbo/dubbo.xsd
  		http://code.alibabatech.com/schema/dubbo http://code.alibabatech.com/schema/dubbo/dubbo.xsd">
  
      <!--指定当前应用的服务-->
      <dubbo:application name="provider"/>
      <!--指定注册中心的位置-->
      <dubbo:registry address="zookeeper://127.0.0.1:2181"/>
      <!--指定通信规则-->
      <dubbo:protocol name="dubbo" port="20080"/>
      <!--暴露那个服务-->
      <dubbo:service interface="cn.doudou.service.HelloWord" ref="helloServiceImpl"/>
      <bean id="helloServiceImpl" class="cn.doudou.service.impl.HelloWordImpl"/>
      <!--监控中心-->
      <dubbo:monitor protocol="registry" ></dubbo:monitor>
  </beans>
  ```

- 消费方

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:dubbo="http://code.alibabatech.com/schema/dubbo"
         xmlns:context="http://www.springframework.org/schema/context"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
         http://www.springframework.org/schema/beans/spring-beans.xsd
          http://www.springframework.org/schema/context
          http://www.springframework.org/schema/context/spring-context.xsd
  		http://dubbo.apache.org/schema/dubbo
  		http://dubbo.apache.org/schema/dubbo/dubbo.xsd
  		http://code.alibabatech.com/schema/dubbo
  		http://code.alibabatech.com/schema/dubbo/dubbo.xsd">
      <context:component-scan base-package="cn.doudou.service.impl"/>
      <!--指定当前应用的服务-->
      <dubbo:application name="consumer"/>
      <!--指定注册中心的位置-->
      <dubbo:registry address="zookeeper://127.0.0.1:2181"/>
      <!--服务-->
      <dubbo:reference interface="cn.doudou.service.HelloWord" id="helloWordImpl"/>
      <dubbo:monitor protocol="registry" ></dubbo:monitor>
  </beans>
  ```

  ### SpringBoot Dubbo搭建
  
  - pom.xml
  
    ```xml
     <dependency>
                <groupId>org.apache.dubbo</groupId>
                <artifactId>dubbo-spring-boot-starter</artifactId>
                <version>2.7.3</version>
                <exclusions>
                    <exclusion>
                        <groupId>org.slf4j</groupId>
                        <artifactId>slf4j-log4j12</artifactId>
                    </exclusion>
                </exclusions>
            </dependency>
    
            <dependency>
                <groupId>org.apache.dubbo</groupId>
                <artifactId>dubbo</artifactId>
                <version>2.7.3</version>
            </dependency>
    
            <dependency>
                <groupId>org.apache.curator</groupId>
                <artifactId>curator-framework</artifactId>
                <version>4.0.1</version>
            </dependency>
    
            <dependency>
                <groupId>org.apache.curator</groupId>
                <artifactId>curator-recipes</artifactId>
                <version>2.8.0</version>
            </dependency>
    
            <dependency>
                <groupId>org.apache.zookeeper</groupId>
                <artifactId>zookeeper</artifactId>
                <version>3.4.13</version>
                <type>pom</type>
                <exclusions>
                    <exclusion>
                        <groupId>org.slf4j</groupId>
                        <artifactId>slf4j-log4j12</artifactId>
                    </exclusion>
                </exclusions>
            </dependency>
    
            <dependency>
                <groupId>com.101tec</groupId>
                <artifactId>zkclient</artifactId>
                <version>0.10</version>
            </dependency>
    ```
  
  - 创建提供商接口
  
  - 启动测试
  
  - 打开浏览器 localhost:7001 账号root 密码root

### Dubbo 配置

- 启动时检查

  ```
  <dubbo:consumer check = "false" timeout = "" //超时设置 retries = "" //重试次数  sdub = "全类型//本地存根>
  ```

- 注册中心检查

  ```
  <dubbo:registry check = "false">
  ```

  