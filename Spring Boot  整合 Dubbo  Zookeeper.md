# Spring Boot  整合 Dubbo  Zookeeper

- api接口定义

  - 创建包 定义接口

- provider 提供方 项目

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
            <dependency>
                <groupId>cn.doudou</groupId>
                <artifactId>bootdubbo-api</artifactId>
                <version>1.0-SNAPSHOT</version>
            </dependency>
    ```

  - service

    **实现api的接口 业务的定义**

  - 配置文件

    ```properties
    #spring项目名
    spring.application.name=dubbo_auto_configuration_provider_demo
    #Dubbo provider configuration
    dubbo.application.name=dubbo_provider
    dubbo.registry.protocol=zookeeper
    dubbo.registry.address=zookeeper://127.0.0.1:2181
    dubbo.protocol.name=dubbo
    dubbo.protocol.port=20880
    #扫描注解包通过该设置将服务注册到zookeeper
    dubbo.scan.base-packages=cn.doudou.service
    
    ```

  - 消费方项目定义

    - 定义controller

      - @Reference//必须加,否则报错
      - 定义service的接口

    - 复制api的service

    - 配置文件

      ```properties
      server.port=8082
      #spring项目名
      spring.application.name=bootdubbo-cont
      dubbo.registry.address=zookeeper://127.0.0.1:2181
      dubbo.protocol.name=dubbo
      dubbo.protocol.port=20880
      #扫描注解包通过该设置将服务注册到zookeeper
      dubbo.scan.base-packages=cn.doudou.controller
      
      ```

      

    

    

    

    

    

    

    

    