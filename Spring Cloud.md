# Spring Cloud

https://www.bilibili.com/video/BV18E411x7eT?p=149

https://blog.csdn.net/qq_42107430/article/details/104788858

https://github.com/RingoTangs/LearningNote/blob/master/SpringCloudAlibaba/SpringCloudAlibaba.md

https://www.cnblogs.com/linchenguang/p/12827582.html

- 服务发现	Netflix Eureka(Nacos)
- 服务调用    Netflix Feign
- 熔断器   Netflix Hystrix
- 服务网关    Spring Cloud GateWay
- 分布式配置 SpringCloud Config(Nacos)
- 消息总线  SpringCloud Bus(Nacos)

## 技术

| 微服务条目                             | 落地技术                                                    |
| -------------------------------------- | ----------------------------------------------------------- |
| 服务开发                               | Spring Boot Spring Spring MVC                               |
| 服务配置与管理                         | Netflix公司的Archaius 阿里的Diamoud等                       |
| 服务注册与发现                         | Eureka Cousul zookeeper                                     |
| 服务调用                               | Rest RPC gRPC等                                             |
| 服务熔断器                             | Hystrix Envoy等                                             |
| 负载均衡                               | Ribbon Nginx等                                              |
| 服务调用接口(客户端电泳服务的简化工具) | Fegin等                                                     |
| 消息队列                               | Kafka RabbinMq ActiceMQ等                                   |
| 服务配置中心管理                       | Spring Cloud Config Chef等                                  |
| 服务路由                               | Zuul等                                                      |
| 服务监控                               | Zabbix Nagios Metrics Sprctator等                           |
| 全链路追踪                             | Zipkin Brave Dapper等                                       |
| 服务部署                               | Docker OpenStack Kubernetes等                               |
| 数据流开发包                           | Spring Cloud Stream(封装与Redis,Rebbit,kafka等发送接收消息) |
| 事件消息总线                           | Spring Cloud Bus                                            |
| ...                                    | ...                                                         |

> **Cloud升级**

- 服务注册中心
  - Eureka ` x`
  - Zookeeper` √`
  - Cousul `√`
  - Nacos`√`
- 服务调用
  - Ribbon `√`
  - LoadBalancer 未来应该会发布
  - Feign `x`
  - OpenFeign `√`
- 服务降级
  - Hystrix `x`
  - resilience4j `国外使用`
  - sentienl `√`
- 服务网关
  - Zuul `x`
  - Zuul2 `估计不会出`
  - gateway `√`
- 服务配置
  - Config `x`
  - Nacos `√`
- 服务总线
  - Bus `x`
  - Nacos `√`

> 为什么会选择SpringCloud作为微服务架构

- 选系依据
  - 整体解决方案和框架成熟度
  - 社区热度
  - 可维护性
  - 学习曲线

> 当前各大IT公司用的微服务架构那些

- 阿里Dubbo/HSF
- 京东JSF
- 新浪微博Motan
- 当当网DubboX

> 技术查看

```
https://start.spring.io/actuator/info
```

> 以下技术的版本

```xml
   <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
        <junit.version>4.12</junit.version>
        <log4j.version>1.2.17</log4j.version>
        <lombok.version>1.16.18</lombok.version>
        <mysql.version>5.1.47</mysql.version>
        <druid.version>1.1.16</druid.version>
        <mybatis.spring.boot.version>1.3.0</mybatis.spring.boot.version>
    </properties>

    <!--子模块继承之后，提供作用：锁定版本+子module不用groupId和version-->
    <dependencyManagement>
        <dependencies>
            <!--spring boot 2.2.2-->
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>2.2.2.RELEASE</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
            <!--spring cloud Hoxton.SR1-->
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>Hoxton.SR1</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
            <!--spring cloud alibaba 2.1.0.RELEASE-->
            <dependency>
                <groupId>com.alibaba.cloud</groupId>
                <artifactId>spring-cloud-alibaba-dependencies</artifactId>
                <version>2.1.0.RELEASE</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
            <dependency>
                <groupId>mysql</groupId>
                <artifactId>mysql-connector-java</artifactId>
                <version>${mysql.version}</version>
            </dependency>
            <dependency>
                <groupId>com.alibaba</groupId>
                <artifactId>druid</artifactId>
                <version>${druid.version}</version>
            </dependency>
            <dependency>
                <groupId>org.mybatis.spring.boot</groupId>
                <artifactId>mybatis-spring-boot-starter</artifactId>
                <version>${mybatis.spring.boot.version}</version>
            </dependency>
            <dependency>
                <groupId>junit</groupId>
                <artifactId>junit</artifactId>
                <version>${junit.version}</version>
            </dependency>
            <dependency>
                <groupId>org.projectlombok</groupId>
                <artifactId>lombok</artifactId>
                <version>${lombok.version}</version>
                <optional>true</optional>
            </dependency>
        </dependencies>
    </dependencyManagement>
```

## Eureka

### Eureka是什么

> Eureka 是 Netflix 开发的，一个基于 REST 服务的，服务注册与发现的组件，以实现中间层服务器的负载平衡和故障转移。
>

它主要包括两个组件：Eureka Server 和 Eureka Client

- Eureka Client：一个Java客户端，用于简化与 Eureka Server 的交互（通常就是微服务中的客户端和服务端）


- Eureka Server：提供服务注册和发现的能力（通常就是微服务中的注册中心）

服务在Eureka上注册，然后每隔30秒发送心跳来更新它们的租约。如果客户端不能多次续订租约，那么它将在大约90秒内从服务器注册表中剔除。注册信息和更新被复制到集群中的所有eureka节点。来自任何区域的客户端都可以查找注册表信息（每30秒发生一次）来定位它们的服务（可能在任何区域）并进行远程调用

> Eureka 客户端与服务器之间的通信

服务发现有两种模式：一种是客户端发现模式，一种是服务端发现模式。Eureka采用的是客户端发现模式。

> Register（注册）

Eureka客户端将关于运行实例的信息注册到Eureka服务器。注册发生在第一次心跳。

> Renew（更新 / 续借）
>

Eureka客户端需要更新最新注册信息（续借），通过每30秒发送一次心跳。更新通知是为了告诉Eureka服务器实例仍然存活。如果服务器在90秒内没有看到更新，它会将实例从注册表中删除。建议不要更改更新间隔，因为服务器使用该信息来确定客户机与服务器之间的通信是否存在广泛传播的问题。

>  Fetch Registry（抓取注册信息）
>

Eureka客户端从服务器获取注册表信息并在本地缓存。之后，客户端使用这些信息来查找其他服务。通过在上一个获取周期和当前获取周期之间获取增量更新，这些信息会定期更新(每30秒更新一次)。获取的时候可能返回相同的实例。Eureka客户端自动处理重复信息。

> Cancel（取消）
>

Eureka客户端在关机时向Eureka服务器发送一个取消请求。这将从服务器的实例注册表中删除实例，从而有效地将实例从流量中取出。

> Eureka自我保护模式
> 如果 Eureka 服务器检测到超过预期数量的注册客户端以一种不优雅的方式终止了连接，并且同时正在等待被驱逐，那么它们将进入自我保护模式。这样做是为了确保灾难性网络事件不会擦除eureka注册表数据，并将其向下传播到所有客户端。

任何客户端，如果连续3次心跳更新失败，那么它将被视为非正常终止，病句将被剔除。当超过当前注册实例15%的客户端都处于这种状态，那么自我保护将被开启。

当自我保护开启以后，eureka服务器将停止剔除所有实例，直到：

它看到的心跳续借的数量回到了预期的阈值之上，或者

自我保护被禁用

默认情况下，自我保护是启用的，并且，默认的阈值是要大于当前注册数量的15%

> Eureka VS Zookeeper
>
> Eureka保证AP

Eureka服务器节点之间是对等的，只要有一个节点在，就可以正常提供服务。

Eureka客户端的所有操作可能需要一段时间才能在Eureka服务器中反映出来，随后在其他Eureka客户端中反映出来。也就是说，客户端获取到的注册信息可能不是最新的，它并不保证强一致性

>  Zookeeper保证CP
>

Zookeeper集群中有一个Leader，多个Follower。Leader负责写，Follower负责读，ZK客户端连接到任何一个节点都是一样的，写操作完成以后要同步给所有Follower以后才会返回。如果Leader挂了，那么重新选出新的Leader，在此期间服务不可用。

> 为什么用Eureka
>

分布式系统大都可以归结为两个问题：数据一致性和防止单点故障。而作为注册中心的话，即使在一段时间内不一致，也不会有太大影响，所以在A和C之间选择A是比较适合该场景的。

### 环境搭建

#### Eureka服务注册中心 

- > pom.xml
  >

  ```xml
   		<dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
          </dependency>
  
  ```

#备注:如果引入爆红的情况,设置引入的版本号就可以解决
  ```
  
  ```xml
      <dependencies>
          <!--eureka-server-->
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
          </dependency>
          <!--boot web actuator-->
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-web</artifactId>
          </dependency>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-actuator</artifactId>
          </dependency>
          <!--一般通用配置-->
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-devtools</artifactId>
              <scope>runtime</scope>
              <optional>true</optional>
          </dependency>
          <dependency>
              <groupId>org.projectlombok</groupId>
              <artifactId>lombok</artifactId>
          </dependency>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-test</artifactId>
              <scope>test</scope>
          </dependency>
          <dependency>
              <groupId>junit</groupId>
              <artifactId>junit</artifactId>
          </dependency>
    </dependencies>
  ```

- > application.yml
  >

  ```yml
  server:
    port: #端口号
  
  eureka:
    instance:
      # eureka 服务端的实例名称
      hostname: localhost
    client:
      # false 表示不向注册中心注册自己
      register-with-eureka: false
      # false 表示自己就是注册中心， 我的职责是去维护服务实例，并不需要去检索服务
      fetch-registry: false
      service-url:
        # 设置与 Eureka Server 交互的地址查询服务和注册服务都需要依赖的这个地址
        defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/
  ```

- > 在启动类中加注解

  ```
  @EnableEurekaServer
  ```

- 测试 运行 http://localhost:端口号/

- 注:SpringBoot版本号一定要和Eureka版本号一样 一定要对照SpringBoot和SpringCloud的版本号

#### Provider向注册中心注册

- > pom.xml
  >

  ```xml
     <!--eureka-client-->
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
          </dependency>
  ```

- > application.yml
  >

  ```yml
  server:
    port: 8004
  spring:
      application:
        name: provider-service
  eureka:
    client:
      register-with-eureka: true #表示向注册中心注册自己 默认为true
      fetch-registry: true #是否从EurekaServer抓取已有的注册信息，默认为true,单节点无所谓,集群必须设置为true才能配合ribbon使用负载均衡
        service-url:
          defaultZone: http://localhost:7001/eureka/ # 入驻地址
  ```

- > 注解
  >

  ```
  @EnableDiscoveryClient
  @EnableEurekaClient   2020年
  都可以
  ```

- 测试 运行 http://localhost:服务的注册中心端口

#### Eureka集群注册中心搭建

> - 使用上面的pom文件

- 然后可以多次搭建注册中心 ,只要端口不同就可以

- 修改yml文件

  ```yml
   defaultZone: http://eureka7001.com:7001/eureka,http://eureka7002.com:7002/eureka
  ```

- 相互注册  defaultZone: http://eureka7001.com:7001/eureka/   defaultZone: http://eureka7002.com:7002/eureka/

- 向里面注册服务http://eureka7002.com:7002/ http://eureka7001.com:7001/   这个需要修改hosts文件

- 测试 运行

#### provider搭建

- pom.xml

  ```xml
  	 <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
          </dependency>
  ```

- application.yml

  ```yml
  server:
    port: 8001
  spring:
    application:
      name: provider-service
  eureka:
    client:
      register-with-eureka: true #表示向注册中心注册自己 默认为true
      fetch-registry: true #是否从EurekaServer抓取已有的注册信息，默认为true,单节点无所谓,集群必须设置为true才能配合ribbon使用负载均衡
      service-url:
       # defaultZone: http://localhost:7001/eureka/ # 入驻地址
        defaultZone: http://eureka7001.com:7001/eureka,http://eureka7002.com:7002/eureka
  ```

  

- 启动类

  ```
  @EnableEurekaClient
  ```

- controller

  ```
  #提供服务进行业务的操作
  ```

  

- 修改端口号多次启动

#### consumer搭建

- pom.xml

  ```xml
  	 <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
          </dependency>
  ```

- application.yml

  ```yml
  server:
    port: 8006
  spring:
    application:
      name: consume-service
  eureka:
    client:
      register-with-eureka: true #表示向注册中心注册自己 默认为true
      fetch-registry: true #是否从EurekaServer抓取已有的注册信息，默认为true,单节点无所谓,集群必须设置为true才能配合ribbon使用负载均衡
      service-url:
       # defaultZone: http://localhost:7001/eureka/ # 入驻地址
        defaultZone: http://eureka7001.com:7001/eureka,http://eureka7002.com:7002/eureka
  ```

- 启动类

  ```java
  package cn.doudou.consume;
  
  import org.springframework.boot.SpringApplication;
  import org.springframework.boot.autoconfigure.SpringBootApplication;
  import org.springframework.cloud.client.loadbalancer.LoadBalanced;
  import org.springframework.cloud.netflix.eureka.EnableEurekaClient;
  import org.springframework.context.annotation.Bean;
  import org.springframework.context.annotation.ComponentScan;
  import org.springframework.web.client.RestTemplate;
  
  @SpringBootApplication
  @EnableEurekaClient
  @ComponentScan(basePackages = "cn.doudou")
  public class ConsumeApplication {
  
      public static void main(String[] args) {
          SpringApplication.run(ConsumeApplication.class, args);
      }
  
      @Bean
      @LoadBalanced
      RestTemplate restTemplate() {
          return new RestTemplate();
      }
  }
  
  ```

- 创建配置类随便名字 创建下面方法

  ```java
      @Bean
      @LoadBalanced
      RestTemplate restTemplate() {
          return new RestTemplate();
      }
  ```
  
- controller

  ```java
  package cn.doudou.controller;
  
  import org.springframework.beans.factory.annotation.Autowired;
  import org.springframework.cloud.client.ServiceInstance;
  import org.springframework.cloud.client.discovery.DiscoveryClient;
  import org.springframework.web.bind.annotation.RequestMapping;
  import org.springframework.web.bind.annotation.RestController;
  import org.springframework.web.client.RestTemplate;
  
  import java.util.List;
  
  @RestController
  public class Test {
      @Autowired
      private DiscoveryClient discoveryClient;
  
      @Autowired
      private RestTemplate restTemplate;
  
      @RequestMapping("/get")
      public String dmeo(String name) {
          System.out.println(name);
          List<ServiceInstance> instances = discoveryClient.getInstances("provider-service");
          ServiceInstance serviceInstance = instances.get(0);
          String n = null;
          n = restTemplate.getForObject("http://provider-service:" + serviceInstance.getPort() + "/get?name=" + name, String.class);
          return n + "端口号" + serviceInstance.getPort();
      }
  }
  
  ```

EurekaServer的高可用

- 准备2个eurekaServer,需要相互注册

  - server 1 : 9000
  - server 2 : 9001

- 注册两个微服务

- 配置

  ```yml
  
  server:
    port: 9000
  eureka:
    client:
      #register-with-eureka: false #是否将自己注册到注册中心
      #fetch-registry: false #是否从eureka中获取注册信息
      service-url: #配置暴露服务
        defaultZone: http://127.0.0.1:9001/eureka/,http://127.0.0.1:9001/eureka/
  spring:
    application:
      name: uereka-server
  
  ```


#### 细节问题

> 在控制台显示ip
>

```yml
instance:
    prefer-ip-address: true   #注册中心中注册ip
    instance-id: ${spring.cloud.client.ip-address}:${server.port}
```

> Eureka剔除问题
>

```yml
instance:
    prefer-ip-address: true
    instance-id: ${spring.cloud.client.ip-address}:${server.port} #注册中心中注册ip
    lease-renewal-interval-in-seconds: 5 #间隔时间
    lease-expiration-duration-in-seconds: 10 #宕机时间
```

> 自我保护

为什么会产生自我保护机制？

为防止EurekaClient可以正常运行，但是与EurekaServer网络不同的情况下，EurekaServer不会立刻将EurekaClient服务剔除。

什么是自我保护机制？

默认情况下，当Eureka server在一定时间内没有收到实例的心跳，便会把该实例从注册表中删除（默认是90秒），但是，如果短时间内丢失大量的实例心跳，便会触发eureka server的自我保护机制。

比如在开发测试时，需要频繁地重启微服务实例，但是我们很少会把eureka server一起重启（因为在开发过程中不会修改eureka注册中心），当一分钟内收到的心跳数大量减少时，会触发该保护机制。可以在eureka管理界面看到Renews threshold和Renews(last min)，当后者（最后一分钟收到的心跳数）小于前者（心跳阈值）的时候，触发保护机制，会出现红色的警告：

EMERGENCY!EUREKA MAY BE INCORRECTLY CLAIMING INSTANCES ARE UP WHEN THEY'RE NOT.RENEWALS ARE LESSER THAN THRESHOLD AND HENCE THE INSTANCES ARE NOT BEGING EXPIRED JUST TO BE SAFE.

从警告中可以看到，eureka认为虽然收不到实例的心跳，但它认为实例还是健康的，eureka会保护这些实例，不会把它们从注册表中删掉。

在自我保护模式中，EurekaServer会保护服务注册表中的信息，不再注销任何服务实例。

综上，自我保护模式是一种应对网络异常的安全保护措施它的架构哲学是宁可同时保留所有微服务，也不忙保姆注销如何健康的微服务，使用自我保护模式，可以让Eureka集群更加健壮，稳定。

署于CAP 的AP分支。

**Eureka如何在注册中心禁止自我保护机制**

```yml
server:
  enable-self-preservation: false #关闭自我保护
  eviction-interval-timer-in-ms: 2000 #剔除的服务间隔
```

**Eureka在提供者禁止自我保护**

```yml
instance:
	lease-renewal-interval-in-seconds: 1 # eureka客户端向服务端发送心跳的时间间隔 单位秒 默认30
	lease-expiration-duration-in-seconds: 2 # eureka服务端在收到最后一次心跳后等待时间上限,单位为秒(默认是90秒),超时剔除服务
```

> Eureka服务发现

- controller

  ```java
      @Resource
      private DiscoveryClient discoveryClient;
      
      //方法
       @GetMapping(value = "/payment/discovery")
      public Object discovery() {
          List<String> services = discoveryClient.getServices();
          for (String service : services) {
              System.out.println(service);
          }
          List<ServiceInstance> instances = discoveryClient.getInstances("CLOUD-PROVIDER-SERVICE");
          for (ServiceInstance instance : instances) {
              System.out.println(instance.getServiceId() + "\t" + instance.getHost() + "\t" + instance.getPort() + "\t" + instance.getUri());
          }
          return this.discoveryClient;
  
      }
  ```

- 启动类

  ```
  @EnableDiscoveryClient
  ```

- 测试 运行 http://localhost:8001/payment/discovery

## Zookeeper

**问题:**zookeeper中的节点是持久还是临时的？

**答**：临时的

### 环境搭建

- 可以在linux中安装zk 或者 win 也可以

- pom

  ```xml
      <dependencies>
          <!-- SpringBoot整合Web组件 -->
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-web</artifactId>
          </dependency>
          <dependency><!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
              <groupId>com.atguigu.springcloud</groupId>
              <artifactId>cloud-api-commons</artifactId>
              <version>${project.version}</version>
          </dependency>
          <!-- SpringBoot整合zookeeper客户端 -->
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-zookeeper-discovery</artifactId>
              <!--先排除自带的zookeeper3.5.3-->
              <exclusions>
                  <exclusion>
                      <groupId>org.apache.zookeeper</groupId>
                      <artifactId>zookeeper</artifactId>
                  </exclusion>
              </exclusions>
          </dependency>
          <!--添加zookeeper3.4.9版本-->
          <dependency>
              <groupId>org.apache.zookeeper</groupId>
              <artifactId>zookeeper</artifactId>
              <version>3.4.9</version>
          </dependency>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-devtools</artifactId>
              <scope>runtime</scope>
              <optional>true</optional>
          </dependency>
          <dependency>
              <groupId>org.projectlombok</groupId>
              <artifactId>lombok</artifactId>
              <optional>true</optional>
          </dependency>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-test</artifactId>
              <scope>test</scope>
          </dependency>
      </dependencies>
  ```

- 服务提供者进zk

  ```yml
  server:
    port: 80
  spring:
    application:
      name: cloud-cousumer-order
    cloud:
      zookeeper:
        connect-string: 127.0.0.1:2181 #集群就是多个地址复制中间逗号
  ```

- 服务消费者进zk

- 创建配置类

  ```java
  package com.atguigu.springcloud.config;
  
  import org.springframework.cloud.client.loadbalancer.LoadBalanced;
  import org.springframework.context.annotation.Bean;
  import org.springframework.context.annotation.Configuration;
  import org.springframework.web.client.RestTemplate;
  
  /**
   * Create By 王嘉浩
   * Time 2020/06/ 9:25
   */
  @Configuration
  public class ApplicaltionContextConfig {
      @Bean
      @LoadBalanced
      public RestTemplate restTemplate() {
          return new RestTemplate();
      }
  }
  
  ```

- controller

  ```java
  @RestController
  @Slf4j
  public class OrderZKController {
      private static final String INVOKE_URL = "http://cloud-provider-payment";
      @Resource
      private RestTemplate restTemplate;
  
      @GetMapping("/consumer/payment/zk")
      public String paymentInfo() {
          String result = restTemplate.getForObject(INVOKE_URL + "/payment/zk", String.class);
          return result;
      }
  }
  ```

- 启动类加

  ```
  @EnableDiscoveryClient  //该注解用于向使用consul或者zookeeper作为注册中心时注册服务
  ```

- 测试 运行 http://localhost/consumer/payment/zk

## Consul

Consul是什么

Consul是一个服务网格（微服务间的 TCP/IP，负责服务之间的网络调用、限流、熔断和监控）解决方案，它是一个一个分布式的，高度可用的系统，而且开发使用都很简便。它提供了一个功能齐全的控制平面，主要特点是：服务发现、健康检查、键值存储、安全服务通信、多数据中心。

与其它分布式服务注册与发现的方案相比，Consul 的方案更“一站式”——内置了服务注册与发现框架、分布一致性协议实现、健康检查、Key/Value 存储、多数据中心方案，不再需要依赖其它工具。Consul 本身使用 go 语言开发，具有跨平台、运行高效等特点，也非常方便和 Docker 配合使用。

### 安装

- 安装直接consul双击

  - dev 开发模式
  - client  是consul代理
  - server 干活的server服务

- 打开cmd

  ```
  consul agent -dev
  consul agent -dev -client=0.0.0.0
  ```

- 访问http://localhost:8500/ui/dc1/services

- 配置文件参考

  ```yml
  server:
    port: 8080
  spring:
    application:
      name: spring-could-consul
    cloud:
      consul:
        host: 127.0.0.1 #主机地址
        port: 8500 #端口
        discovery:
          #是否主要注册
          #register: true
          #注册的示例ID
          instance-id: ${spring.application.name}-1
          #服务名称
          service-name: ${spring.application.name}
          #服务请求端口
          port: ${server.port}
          #开启ip地址注册
          prefer-ip-address: true
          #当前服务的请求ip
          ip-address: ${spring.cloud.client.ip-address}
  
  
  ```

  

### 服务提供者进consul

- pom

  ```xml
    <!--SpringCloud consul-server -->
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-consul-discovery</artifactId>
          </dependency>
  ```

- yml文件

  ```yml
  server:
    port: 8006
  spring:
    application:
      name: consul-provider-payment
  
    #consul注册中心
    cloud:
      consul:
        host: localhost
        port: 8500
        discovery:
          #hostname: 127.0.0.1
          service-name: ${spring.application.name}
  
  ```

- 启动类

  ```java
  @EnableDiscoveryClient  //该注解用于向使用consul或者zookeeper作为注册中心时注册服务
  ```

- 测试 运行 http://localhost:8006/payment/consul

### 服务消费者进consul

- pom  和上面一样

- yml文件 和最上面一样 把端口号改了就可以

- 创建配置类

  ```java
  package com.atguigu.springcloud.config;
  
  import org.springframework.cloud.client.loadbalancer.LoadBalanced;
  import org.springframework.context.annotation.Bean;
  import org.springframework.context.annotation.Configuration;
  import org.springframework.web.client.RestTemplate;
  
  /**
   * Create By 王嘉浩
   * Time 2020/06/ 9:25
   */
  @Configuration
  public class ApplicaltionContextConfig {
      @Bean
      @LoadBalanced
      public RestTemplate restTemplate() {
          return new RestTemplate();
      }
  }
  
  ```

- controller

  ```java
  package com.atguigu.springcloud.controller;
  
  import lombok.extern.slf4j.Slf4j;
  import org.springframework.web.bind.annotation.GetMapping;
  import org.springframework.web.bind.annotation.RestController;
  import org.springframework.web.client.RestTemplate;
  
  import javax.annotation.Resource;
  
  /**
   * Create By 王嘉浩
   * Time 2020/06/ 9:26
   */
  @RestController
  @Slf4j
  public class OrderConsulController {
      private static final String INVOKE_URL = "http://consul-provider-payment";
      @Resource
      private RestTemplate restTemplate;
  
      @GetMapping("/consumer/payment/consul")
      public String paymentInfo() {
          String result = restTemplate.getForObject(INVOKE_URL + "/payment/consul", String.class);
          return result;
      }
  }
  
  ```

- 启动类

  ```java
  @EnableDiscoveryClient  //该注解用于向使用consul或者zookeeper作为注册中心时注册服务
  ```

- 测试 运行 http://localhost/consumer/payment/consul

## 注册中心的总结

> Eureka、Zookeeper、Consul三个注册中心的异同点

- C:Consistency(强一致性)
- A:Availability(可用性)
- P:Partition tolerance(分区容错性)

最多只能同时较好的满足两个:

CAP理论的核心是:一个分布式系统不可能同时很好的满足一致性,可用性和分区容错性这三个需求,

因此,根据CAP原理将NoSQL数据库分成了满足CA原则,满足CP原则和满足AP原则三大类:

CA-单点集群,满足一致性,可用性的系统,通常在可扩展性不太强大

CP-满足一致性,分区容忍性的系统,通常性能不是特别高

AP-满足可用性,分区容性的系统,通常可能对一致性要求低一些

| 组件名    | 语言 | 健康检查 | 对外暴露接口 | CAP  | Springcloud集成 |
| --------- | ---- | -------- | ------------ | ---- | --------------- |
| Eureka    | Java | 可配支持 | HTPP         | AP   | 集成            |
| Zookeeper | Go   | 支持     | HTTP/DNS     | CP   | 集成            |
| Consul    | Java | 支持     | 客户端       | CP   | 集成            |

## Ribbon

### 简介

Spring Cloud Ribbon是基于Netflix Ribbon来实现的一套客户端负载均衡的工具

Spring Cloud Ribbon是一个基于HTTP和TCP的客户端负载均衡工具，它基于Netflix Ribbon实现。通过Spring Cloud的封装，可以让我们轻松地将面向服务的REST模版请求自动转换成客户端负载均衡的服务调用。Spring Cloud Ribbon虽然只是一个工具类框架，它不像服务注册中心、配置中心、API网关那样需要独立部署，但是它几乎存在于每一个Spring Cloud构建的微服务和基础设施中。因为微服务间的调用，API网关的请求转发等内容，实际上都是通过Ribbon来实现的，包括后续我们将要介绍的Feign，它也是基于Ribbon实现的工具。所以，对Spring Cloud Ribbon的理解和使用，对于我们使用Spring Cloud来构建微服务非常重要。

### 服务调用

- 在引入Eureka的时候就引入了ribbon ,可以自己在加个

  ```xml
  		<dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-netflix-ribbon</artifactId>
          </dependency>
  ```

- 在创建RestTemplate的时候,声明`@LoadBalanced`注释

  ```java
  @Configuration
  public class RestTemplateConfiguration {
      @Bean
      @LoadBalanced
      public RestTemplate restTemplate() {
          return new RestTemplate();
      }
  }
  ```

- 使用RestTemplate调用微服务,不需要拼接URl

  ```java
  //自动注入RestTemplate
      @Autowired
      private RestTemplate restTemplate;
  
      //创建方法进行测试
      @GetMapping("/getUser/{id}")
      public String get(@PathVariable("id") String id) {
          String url = "http://服务在Eureka的名字/访问路径";
          String forObject = restTemplate.getForObject(url, String.class);
          return forObject + "--" + id;
      }
  ```

  

### 负载均衡

Ribbon是一个典型的客户端的负载均衡器

- 负载均衡策略

  | 策略类                    | 命名             |                             说明                             |
  | ------------------------- | ---------------- | :----------------------------------------------------------: |
  | RandomRule                | 随机策略         |                       随机选择 Server                        |
  | RoundRobinRule            | 轮训策略         |                    按顺序循环选择 Server                     |
  | RetryRule                 | 重试策略         | 在一个配置时问段内当选择 Server 不成功，则一直尝试选择一个可用的 Server |
  | BestAvailableRule         | 最低并发策略     | 逐个考察 Server，如果 Server 断路器打开，则忽略，再选择其中并发连接最低的 Server |
  | AvailabilityFilteringRule | 可用过滤策略     | 过滤掉一直连接失败并被标记为 `circuit tripped` 的 Server，过滤掉那些高并发连接的 Server（active connections 超过配置的网值） |
  | ResponseTimeWeightedRule  | 响应时间加权策略 | 根据 Server 的响应时间分配权重。响应时间越长，权重越低，被选择到的概率就越低；响应时间越短，权重越高，被选择到的概率就越高。这个策略很贴切，综合了各种因素，如：网络、磁盘、IO等，这些因素直接影响着响应时间 |
  | ZoneAvoidanceRule         | 区域权衡策略     | 综合判断 Server 所在区域的性能和 Server 的可用性轮询选择 Server，并且判定一个 AWS Zone 的运行性能是否可用，剔除不可用的 Zone 中的所有 Server |
  | WeightedResponseTimeRule  | 权重策略         |                                                              |

- 配置 消费者的application.yml

  ```yml
  服务名:
  	ribbon: 
  		NFLoadBalancerRuleClassName: com.netflix.loadbalacer.负载均衡机制
  ```

### 替换Ribbon算法

- 不能在SpringBootApplication可以扫描到的包 可以在创建包

- 创建包myrule

- 创建配置类

  ```java
  package com.atguigu.myrule;
  
  import com.netflix.loadbalancer.IRule;
  import com.netflix.loadbalancer.RandomRule;
  import org.springframework.context.annotation.Bean;
  import org.springframework.context.annotation.Configuration;
  
  /**
   * Create By 王嘉浩
   * Time 2020/06/ 16:30
   */
  @Configuration
  public class MySelfRule {
      @Bean
      public IRule iRule() {
          return new RandomRule();//随机  可以参考上面表
      }
  
  }
  
  ```

- ```java
  @RibbonClient(name = "可以在服务注册中心查看名字", configuration = MySelfRule.class)
  ```

### 负载均衡算法

rest接口第几次请求书 % 服务器集群总数量  = 实际调用服务器位置下标 每次服务重启后rest接口计数从1开始

### 自写算法

- 在服务提供者controller

  ```java
      @GetMapping("/payment/lb")
      public String getPaymentLB() {
          return serverport;
      }
  ```

- 在服务消费者创建接口

  ```java
  package com.atguigu.springcloud.lb;
  
  import org.springframework.cloud.client.ServiceInstance;
  
  import java.util.List;
  
  /**
   * Create By 王嘉浩
   * Time 2020/06/ 18:11
   */
  public interface LoadBalancer {
      ServiceInstance instances(List<ServiceInstance> serviceInstances);
  }
  
  ```

- 创建实现类

  ```java
  package com.atguigu.springcloud.lb;
  
  import org.springframework.cloud.client.ServiceInstance;
  import org.springframework.stereotype.Component;
  
  import java.util.List;
  import java.util.concurrent.atomic.AtomicInteger;
  
  /**
   * Create By 王嘉浩
   * Time 2020/06/ 18:12
   */
  @Component
  public class MyLB implements LoadBalancer {
      private AtomicInteger atomicInteger = new AtomicInteger(0);
  
      public final int getAndIncrement() {
          int current;
          int next;
          do {
              current = this.atomicInteger.get();
              next = current >= Integer.MAX_VALUE ? 0 : current + 1;
          } while (!atomicInteger.compareAndSet(current, next));
          System.out.println("第几次访问,次数next:" + next);
          return next;
      }
  
      @Override
      public ServiceInstance instances(List<ServiceInstance> serviceInstances) {
          int index = getAndIncrement() % serviceInstances.size();
          return serviceInstances.get(index);
      }
  }
  
  ```

- controller

  ```java
   @Resource
      private LoadBalancer loadBalancer;
  
      @Resource
      private DiscoveryClient discoveryClient;   
  
  @GetMapping("/consumer/payment/lb")
      public String getPaymentLB() {
          List<ServiceInstance> instances = discoveryClient.getInstances("CLOUD-PROVIDER-SERVICE");
          discoveryClient.getInstances("CLOUD-PROVIDER-SERVICE");
          if (instances == null || instances.size() <= 0) {
              return null;
          }
          ServiceInstance serviceInstance = loadBalancer.instances(instances);
          URI uri = serviceInstance.getUri();
          return restTemplate.getForObject(uri + "/payment/lb", String.class);
      }
  ```

  

### 重试机制

-  引入Spring的重试组件

- ```xml
  <dependency>
      <groupId>org.springframework.retry</groupId>
      <artifactId>spring-retry</artifactId>
  </dependency>
  ```

- 对Ribbon进行重试配置

  ```yml
  service-product:
    ribbon:
      #NFLoadBalancerRuleClassName: com.netflix.loadbalancer.RandomRule
      ConnectTimeout: 250 # Ribbon的连接超时时间
      ReadTimeout: 1000 # Ribbon的数据读取超时时间
      OkToRetryOnAllOperations: true # 是否对所有操作都进行重试
      MaxAutoRetriesNextServer: 1 # 切换实例的重试次数
      MaxAutoRetries: 1 # 对当前实例的重试次数
  ```

## OpenFeign

Feign是一个声明式的Web Service客户端。它的出现使开发Web Service客户端变得很简单。使用Feign只需要创建一个接口加上对应的注解，比如：FeignClient注解。Feign有可插拔的注解，包括Feign注解和JAX-RS注解。Feign也支持编码器和解码器，Spring Cloud Open Feign对Feign进行增强支持Spring MVC注解，可以像Spring Web一样使用HttpMessageConverters等。

Feign是一种声明式、模板化的HTTP客户端。在Spring Cloud中使用Feign，可以做到使用HTTP请求访问远程服务，就像调用本地方法一样的，开发者完全感知不到这是在调用远程方法，更感知不到在访问HTTP请求。

功能可插拔的注解支持，包括Feign注解和JAX-RS注解。支持可插拔的HTTP编码器和解码器（Gson，Jackson，Sax，JAXB，JAX-RS，SOAP）。支持Hystrix和它的Fallback。支持Ribbon的负载均衡。支持HTTP请求和响应的压缩。灵活的配置：基于 name 粒度进行配置支持多种客户端：JDK URLConnection、apache httpclient、okhttp，ribbon）支持日志支持错误重试url支持占位符可以不依赖注册中心独立运行

- 导入依赖

  ```xml
       <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-openfeign</artifactId>
          </dependency>
  ```

- 配置调用接口

  ```java
  /**
   * 需要调用微服务名称
   * 配置需要调用微服务的接口
   *
   * @FeignClient(name = "") name 服务提供者的名称
   */
  @FeignClient(name = "provider-service")
  public interface ProviderFeign {
      @RequestMapping(value = "/get/{message}", method = RequestMethod.GET)
      public String message(@PathVariable("message") String message);
  }
  ```

- 在启动类激活feign

  ```java
  //激活Feign
  @EnableFeignClients
  ```

- 通过自动的接口调用远程微服务

  ```java
      @Autowired
      private ProviderFeign providerFeign;
      @RequestMapping("/get/{message}")
      public String dmeo(@PathVariable String message) {
          String n = null;
          n = providerFeign.message(message);
          return n ;
      }
  ```

  **注:如果正常配置,启动报错,检查:扫描的包 如果还算是报错 @EnableFeignClients(basePackages = "cn.doudou.feign") 把这个进行替换**
  
  **负载均衡提供2个以上的服务接口的就可以**
  
  配置文件
  
  ```yml
  feign:
    client:
      config:
        feignName: #定义Feign的名称
        connectTimeout: 5000 #相当于Request.Optonns
        readTimeOut: 5000 #相当于Reqest.Options
        #配置Feign的日志级别,相当于代码配置方式的Logger
        loggerLevel: full
        #Feign的错误编码器,相当于代码配置方式中的ErrorDecoder
        errorDecoder: com.example.SimpleErrorDecoder
        #配置拦截器
        百度吧
  ```
  
  ```yml
  server:
    port: 80
  
  eureka:
    client:
      register-with-eureka: false
      service-url:
        defaultZone: http://eureka7001.com:7001/eureka/,http://eureka7002.com:7002/eureka/
  
  #设置feign客户端超时时间(OpenFeign默认支持ribbon)
  ribbon:
    #指的是建立连接所用的时间，适用于网络状况正常的情况下,两端连接所用的时间
    ReadTimeout: 5000
    #指的是建立连接后从服务器读取到可用资源所用的时间
    ConnectTimeout: 5000
  ```
  
- 日志打印

  > NONE BASIC HEADERS FULL
  
  yml文件
  
  ```yml
  logging:
    level:
      # feign日志以什么级别监控哪个接口
    com.atguigu.springcloud.service.PaymentFeignService: debug
  ```
  
- 配置类

  ```java
  package com.atguigu.springcloud.config;
  
  import feign.Logger;
  import org.springframework.context.annotation.Bean;
  import org.springframework.context.annotation.Configuration;
  
  /**
   * Create By 王嘉浩
   * Time 2020/06/ 22:28
   */
  @Configuration
  public class FeignConfig {
      @Bean
      public Logger.Level feignLoggerLevel() {
          // 请求和响应的头信息,请求和响应的正文及元数据
          return Logger.Level.FULL;
      }
  
  }
  
  ```

  

- 数据压缩开启

  ```yml
  feign:
    compression:
      request:
        enabled: true #开启请求数据压缩
      response:
        enabled: true #开启响应数据压缩
  ```

  ```yml
  feign:
    compression:
      request:
        enabled: true #开启请求数据压缩
        min-request-size: 2048 #设置触发的压缩大小上限
        mime-types: text/html,application/xml,application/json #设置也说的数据类型
  ```

- 日志

  ```yml
  feign:
    client:
      server-provider:
        被调用服务的名称: FULL #输出所有日志 NULL<不输出> BASIC<生产环境追踪问题> HEADERS<记录响应> FULL<记录所有>
  logging:
    level:
      cn.doudou.feign.ProviderFeign: debug
  ```


## Hystrix

在微服务场景中，通常会有很多层的服务调用。如果一个底层服务出现问题，故障会被向上传播给用户。我们需要一种机制，当底层服务不可用时，可以阻断故障的传播。这就是断路器的作用。他是系统服务稳定性的最后一重保障。

在springcloud中断路器组件就是Hystrix。Hystrix也是Netflix套件的一部分。他的功能是，当对某个服务的调用在一定的时间内（默认10s），有超过一定次数（默认20次）并且失败率超过一定值（默认50%），该服务的断路器会打开。返回一个由开发者设定的fallback。

fallback可以是另一个由Hystrix保护的服务调用，也可以是固定的值。fallback也可以设计成链式调用，先执行某些逻辑，再返回fallback。

**重要概念**

- 服务降级  服务器忙,请稍后再试,不让客户端等待并且立刻返回一个友好的提示 fallback 
  - 程序运行异常
  - 超时
  - 服务熔断触发服务降级
  - 线程池/信号量打满也会导致服务降级
- 服务熔断  类比保险丝达到最大服务访问后,直接拒绝访问,拉闸限电,然后调用服务降级的方法并返回友好提示
- 服务限流  秒杀高并发等操作,严禁的一窝蜂过去拥挤,大家排队,一秒N个,有序进行 

**Hystrix的作用**

1. 对通过第三方客户端库访问的依赖项（通常是通过网络）的延迟和故障进行保护和控制。
2. 在复杂的分布式系统中阻止级联故障。
3. 快速失败，快速恢复。
4. 回退，尽可能优雅地降级。
5. 启用近实时监控、警报和操作控制。

 对RestTemplate的支持

- 引入依赖

  ```xml
   		<!--hystrix-->
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-netflix-hystrix</artifactId>
          </dependency>
          <!--eureka client-->
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
          </dependency>
  ```

- 激活

  ```
  @EnableEurekaClient
  @EnableCircuitBreaker
  ```

- 配置触发的降级逻辑 在类上配置注解  可以模拟一下系统的错误

  ```
   @HystrixCommand(fallbackMethod = "系统错误方法名称", commandProperties = {
              @HystrixProperty(name = "execution.isolation.thread.timeoutInMilliseconds", value = "时间")
      })
  ```

  ```java
  public String paymentInfo_TimeOutHandler(Integer id) {
          return "线程池" + Thread.currentThread().getName() + "---paymentInfo_TimeOutHandler:" + id + "8001网络好像出问题了!检查一下网络吧!";
      }
  ```

- 测试 运行

### 对Feign的支持

- 引入依赖<feign中已经集成了>

  ```xml
   		<!--openfeign-->
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-openfeign</artifactId>
          </dependency>
          <!--hystrix-->
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-netflix-hystrix</artifactId>
          </dependency>
          <!--eureka client-->
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
          </dependency>
  ```

  

- 配置开启Hystrix

  ```yml
  feign: 
  	hystrix: 
  		enabled: true
  ```

- 自定义一个实现类就是熔断的降级逻辑

  ```java
  //自定义一个类实现,现在feign的包下的类然后实现方法
     // 下面是全局fallback方法
      public String payment_Global_FallbackMethod() {
          return "Global异常处理信息，请稍后再试，/(ㄒoㄒ)/~~";
      }
  
  ```

- 添加降级方法的支持 修改feignClient注解的配置

  ```
   @HystrixCommand(fallbackMethod = "系统错误方法名称", commandProperties = {
              @HystrixProperty(name = "execution.isolation.thread.timeoutInMilliseconds", value = "时间")
      })
  ```

### 全局降级处理

- 在类上加

  ```
  @DefaultProperties(defaultFallback = "方法名字")
  ```

- 在方法上加

  ```
     @HystrixCommand
  ```

- 参考上面开启yml配置 文件

### 全局降级解耦

- 创建类实现Feign的接口

- 然后在接口上加

  ```
  @FeignClient(value = "服务名字" ,fallback = 刚才创建类的class文件)
  ```

- ```java
  package com.atguigu.springcloud.service;
  
  import org.springframework.stereotype.Component;
  
  /**
   * @auther zzyy
   * @create 2020-02-20 18:22
   */
  @Component
  public class PaymentFallbackService implements PaymentHystrixService
  {
      @Override
      public String paymentInfo_OK(Integer id)
      {
          return "-----PaymentFallbackService fall back-paymentInfo_OK ,o(╥﹏╥)o";
      }
  
      @Override
      public String paymentInfo_TimeOut(Integer id)
      {
          return "-----PaymentFallbackService fall back-paymentInfo_TimeOut ,o(╥﹏╥)o";
      }
  }
  
  ```

- 可以针对宕机处理

- yml

  ```yml
  feign:
    hystrix:
      enabled: true
  ```

- controller不需要加任何东西

### 服务熔断

> 一句话就是家里的保险丝

- ```
    //################服务熔断
      @HystrixCommand(fallbackMethod = "服务的降级方法", commandProperties = {
              @HystrixProperty(name = "circuitBreaker.enabled", value = "true"),// 是否开启断路器
              @HystrixProperty(name = "circuitBreaker.requestVolumeThreshold", value = "10"),// 请求次数
              @HystrixProperty(name = "circuitBreaker.sleepWindowInMilliseconds", value = "10000"), // 时间窗口期
              @HystrixProperty(name = "circuitBreaker.errorThresholdPercentage", value = "60"),// 失败率达到多少后跳闸
      })
  ```

- ```java
   public String paymentCircuitBreaker(@PathVariable("id") Integer id) {
          if (id < 0) {
              throw new RuntimeException("******id 不能负数");
          }
          String serialNumber = IdUtil.simpleUUID();
    
          return Thread.currentThread().getName() + "\t" + "调用成功，流水号: " + serialNumber;
      }
    
      public String paymentCircuitBreaker_fallback(@PathVariable("id") Integer id) {
          return "id 不能负数，请稍后再试，/(ㄒoㄒ)/~~   id: " + id;
      }
    
  ```

- ```java
      //====服务熔断
      @GetMapping("/payment/circuit/{id}")
      public String paymentCircuitBreaker(@PathVariable("id") Integer id)
      {
          String result = paymentServcie.paymentCircuitBreaker(id);
          return result;
      }
  ```

### hystrix监控

- pom.xml

  ```xml
   <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-actuator</artifactId>
          </dependency>
  
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-netflix-hystrix</artifactId>
          </dependency>
  
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-netflix-hystrix-dashboard</artifactId>
          </dependency>
  ```

- 配置

  ```yml
  management:
    endpoints:
      web:
        exposure:
          include: '*'
  ```

- 注解

  ```
  @EnableCircuitBreaker
  ```

- 访问地址

  ```
  http://localhost:8003/actuator/hystrix.stream
  ```

### 搭建Hystrix DashBoard监控

- pom.xml

  ```xml
   		 <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-netflix-hystrix-dashboard</artifactId>
          </dependency>
  ```

- 激活

  ```
  @EnableHystrixDashboard
  ```

- 测试地址

  ```
  http://localhost:8003/hystrix
  ```

### 聚合监控Turbine

### Sentinel组件

## Gateway网关

Spring cloud gateway是spring官方基于Spring 5.0、Spring Boot2.0和Project Reactor等技术开发的网关，Spring Cloud Gateway旨在为微服务架构提供简单、有效和统一的API路由管理方式，Spring Cloud Gateway作为Spring Cloud生态系统中的网关，目标是替代Netflix Zuul，其不仅提供统一的路由方式，并且还基于Filer链的方式提供了网关基本的功能，例如：安全、监控/埋点、限流等。

> 三大核心概念

- 路由 Route  路由是构建网关的基本模块,它有ID,目标URL.一系列的断言和过滤器组成,如果断言为true则匹配该路由
- 断言 Rredicate
- 过滤 Filter

### 环境搭建

- pom

  ```xml
   <!--gateway-->
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-gateway</artifactId>
          </dependency>
  ```

- yml 代码

  ```yml
  
  server:
    port: 9527
  
  spring:
    application:
      name: cloud-gateway
    cloud:
      gateway:
        discovery:
          locator:
            enabled: true #开启从注册中心动态创建路由的功能，利用微服务名进行路由
        routes:
          - id: payment_routh #payment_route    #路由的ID，没有固定规则但要求唯一，建议配合服务名
            uri: http://localhost:8001          #匹配后提供服务的路由地址
           # uri: lb://cloud-payment-service #匹配后提供服务的路由地址
            predicates:
              - Path=/payment/get/**         # 断言，路径相匹配的进行路由
  
          - id: payment_routh2 #payment_route    #路由的ID，没有固定规则但要求唯一，建议配合服务名
            uri: http://localhost:8001          #匹配后提供服务的路由地址
            #uri: lb://cloud-payment-service #匹配后提供服务的路由地址
            predicates:
              - Path=/payment/lb/**         # 断言，路径相匹配的进行路由
              #- After=2020-02-21T15:51:37.485+08:00[Asia/Shanghai]
              #- Cookie=username,zzyy
              #- Header=X-Request-Id, \d+  # 请求头要有X-Request-Id属性并且值为整数的正则表达式
  
  eureka:
    instance:
      hostname: cloud-gateway-service
    client: #服务提供者provider注册进eureka服务列表内
      service-url:
        register-with-eureka: true
        fetch-registry: true
        defaultZone: http://eureka7001.com:7001/eureka
  ```

- 代码配置

  ```java
  package com.atguigu.springcloud.config;
  
  import org.springframework.cloud.gateway.route.RouteLocator;
  import org.springframework.cloud.gateway.route.builder.RouteLocatorBuilder;
  import org.springframework.context.annotation.Bean;
  import org.springframework.context.annotation.Configuration;
  
  /**
   * Create By 王嘉浩
   * Time 2020/06/ 10:05
   */
  @Configuration
  public class GetwayConfig {
      @Bean
      public RouteLocator customRouteLocator(RouteLocatorBuilder routeLocatorBuilder) {
          RouteLocatorBuilder.Builder routes = routeLocatorBuilder.routes();
          routes.route("path_route_atguigu",
                  r -> r.path("/guonei")
                          .uri("http://news.baidu.com/guonei")).build();
          return routes.build();
      }
  }
  
  ```

### 动态路由的搭建

- pom

  ```xml
   <!--eureka-client-->
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
          </dependency>
              <!--gateway-->
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-gateway</artifactId>
          </dependency>
  ```

- yml

  ```yml
  
  server:
    port: 9527
  
  spring:
    application:
      name: cloud-gateway
    cloud:
      gateway:
        discovery:
          locator:
            enabled: true #开启从注册中心动态创建路由的功能，利用微服务名进行路由
        routes:
          - id: payment_routh #payment_route    #路由的ID，没有固定规则但要求唯一，建议配合服务名
            uri: lb://CLOUD-PROVIDER-SERVICE #匹配后提供服务的路由地址
            predicates:
              - Path=/payment/get/**         # 断言，路径相匹配的进行路由
  
          - id: payment_routh2 #payment_route    #路由的ID，没有固定规则但要求唯一，建议配合服务名
            uri: lb://CLOUD-PROVIDER-SERVICE #匹配后提供服务的路由地址
            predicates:
              - Path=/payment/lb/**         # 断言，路径相匹配的进行路由
              #- After=2020-02-21T15:51:37.485+08:00[Asia/Shanghai]
              #- Cookie=username,zzyy
              #- Header=X-Request-Id, \d+  # 请求头要有X-Request-Id属性并且值为整数的正则表达式
  
  eureka:
    instance:
      hostname: cloud-gateway-service
    client: #服务提供者provider注册进eureka服务列表内
      service-url:
        register-with-eureka: true
        fetch-registry: true
        defaultZone: http://eureka7001.com:7001/eureka
  
  
  
  ```

  测试 运行

### **Predicate**的使用

- After Route Predicate **在什么时间以后可以访问**

  ```yml
   predicates:
              - Path=/payment/lb/**         # 断言，路径相匹配的进行路由
              - After=2020-06-22T15:45:06.979+08:00[Asia/Shanghai]
  ```

- Before Route Predicate **在什么时间以前可以访问**

- Between Route Predicate **在两个时间中间**

-  Cookie Route Predicate **cookie必须有**

- Header Route Predicate **请求头 属性名称 正则表达式**

  ```yml
   - Header=X-Request-Id, \d+  # 请求头要有X-Request-Id属性并且值为整数的正则表达式
  ```

- Host Route Predicate

-  Method Route Predicate

- Method Route Predicate

- Query Route Predicate

-  总结

### 自定义过滤器

```java
package com.atguigu.springcloud.config;

        import org.springframework.cloud.gateway.route.RouteLocator;
        import org.springframework.cloud.gateway.route.builder.RouteLocatorBuilder;
        import org.springframework.context.annotation.Bean;
        import org.springframework.context.annotation.Configuration;

/**
 * Create By 王嘉浩
 * Time 2020/06/ 10:05
 */
@Configuration
public class GetwayConfig {
    @Bean
    public RouteLocator customRouteLocator(RouteLocatorBuilder routeLocatorBuilder) {
        RouteLocatorBuilder.Builder routes = routeLocatorBuilder.routes();
        routes.route("path_route_atguigu",
                r -> r.path("/guonei")
                        .uri("http://news.baidu.com/guonei")).build();
        return routes.build();
    }
    @Bean
    public RouteLocator customRouteLocator2(RouteLocatorBuilder routeLocatorBuilder) {
        RouteLocatorBuilder.Builder routes = routeLocatorBuilder.routes();
        routes.route("path_route_atguigu",
                r -> r.path("/guoji")
                        .uri("http://news.baidu.com/guoji")).build();
        return routes.build();
    }
}

```

## Spring Cloud Config分布式配置中心

Spring Cloud Config 为微服务机构中的微服务提供集中化的外部配置支持,配置服务器为各个不同的微服务应用的所有环境提供了一个中心化的外部配置

### 服务端环境搭建

- pom

  ```xml
  <dependencies>
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-config-server</artifactId>
          </dependency>
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
          </dependency>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-web</artifactId>
          </dependency>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-actuator</artifactId>
          </dependency>
          <dependency>
              <groupId>org.projectlombok</groupId>
              <artifactId>lombok</artifactId>
              <optional>true</optional>
          </dependency>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-test</artifactId>
              <scope>test</scope>
          </dependency>
      </dependencies>
  ```

- 启动类

  ```java
  package com.atguigu.springcloud;
  
  import org.springframework.boot.SpringApplication;
  import org.springframework.boot.autoconfigure.SpringBootApplication;
  import org.springframework.cloud.config.server.EnableConfigServer;
  import org.springframework.cloud.netflix.eureka.EnableEurekaClient;
  
  /**
   * Create By 王嘉浩
   * Time 2020/06/ 11:18
   */
  @SpringBootApplication
  @EnableConfigServer
  public class ConfigCenterMain3344 {
      public static void main(String[] args) {
          SpringApplication.run(ConfigCenterMain3344.class, args);
      }
  }
  ```

- yml

  ```yml
  server:
    port: 3344
  spring:
    application:
      name: config-center
    cloud:
      config:
        server:
          git:
            uri: https://github.com/doudou-bai/cloud-config.git  #地址
            search-paths: /** #搜索的目录
        label: master
  
  #服务注册到eureka地址
  eureka:
    client:
      service-url:
        defaultZone: http://localhost:7001/eureka
    #
  ```

- 打开github 或者 码云

- 创建仓库

- 在本地创建仓库

- 添加文件 application开头的

  ```
  http://localhost:3344/master/application-dev.ymlgit init
  git status
  git add .
  git commit -m "相当于注释"
  git remote add origin https://github.com/doudou-bai/cloud-config.git
  git remote -v
  git push origin master
  ```

- 测试 访问http://localhost:3344/master/application-dev.yml

- http请求地址和资源文件映射如下:

  /{application}/{profile}[/{label}]
  /{application}-{profile}.yml
  /{label}/{application}-{profile}.yml
  /{application}-{profile}.properties
  /{label}/{application}-{profile}.properties

### 客户端环境搭建

- pom

  ```xml
      <dependencies>
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-config</artifactId>
          </dependency>
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
          </dependency>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-web</artifactId>
          </dependency>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-actuator</artifactId>
          </dependency>
  
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-devtools</artifactId>
              <scope>runtime</scope>
              <optional>true</optional>
          </dependency>
          <dependency>
              <groupId>org.projectlombok</groupId>
              <artifactId>lombok</artifactId>
              <optional>true</optional>
          </dependency>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-test</artifactId>
              <scope>test</scope>
          </dependency>
      </dependencies>
  ```

- bootstrap.yml **必须是这个名字**

  ```yml
  server:
    port: 3355
  spring:
    application:
      name: config-client
    cloud:
      config:
        label: master # 分支名称
        name: application #配置文件名称
        profile: dev #读取后缀名称
        uri: http://localhost:3344 #配置中心地址
  #服务注册到eureka地址
  eureka:
    client:
      service-url:
        defaultZone: http://localhost:7001/eureka
    #
  ```

- controller

  ```java
  package com.atguigu.springcloud.controller;
  
  import org.springframework.beans.factory.annotation.Value;
  import org.springframework.cloud.context.config.annotation.RefreshScope;
  import org.springframework.web.bind.annotation.GetMapping;
  import org.springframework.web.bind.annotation.RestController;
  
  /**
   * @auther zzyy
   * @create 2020-02-21 18:08
   */
  @RestController
  @RefreshScope
  public class ConfigClientController
  {
      @Value("${config.info}")
      private String configInfo;
  
      @GetMapping("/configInfo")
      public String getConfigInfo()
      {
          return configInfo;
      }
  }
  ```

- 测试 运行

### 手动刷新

- pom

  ```xml
      <dependencies>
          <!--  &lt;!&ndash;添加消息总线RabbitMQ支持&ndash;&gt;
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-starter-bus-amqp</artifactId>
            </dependency>-->
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-config</artifactId>
          </dependency>
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
          </dependency>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-web</artifactId>
          </dependency>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-actuator</artifactId>
          </dependency>
  
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-devtools</artifactId>
              <scope>runtime</scope>
              <optional>true</optional>
          </dependency>
          <dependency>
              <groupId>org.projectlombok</groupId>
              <artifactId>lombok</artifactId>
              <optional>true</optional>
          </dependency>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-test</artifactId>
              <scope>test</scope>
          </dependency>
      </dependencies>
  ```

- yml

  ```yml
  server:
    port: 3355
  spring:
    application:
      name: config-client
    cloud:
      config:
        label: master # 分支名称
        name: application #配置文件名称
        profile: dev #读取后缀名称
        uri: http://localhost:3344 #配置中心地址
  #服务注册到eureka地址
  eureka:
    client:
      service-url:
        defaultZone: http://localhost:7001/eureka
  # 暴露监控端点
  management:
    endpoints:
      web:
        exposure:
          include: "*"
  
  ```

- 在controller加@RefreshScope

- 可以修改刷新一下

- 在cmd运行

  ```
  curl -X POST "http://127.0.0.1:3355/actuator/refresh"
  ```


## Spring cloud Bus

什么是总线?

在微服务架构的系统中,通常会使用轻量级的消息代理来构建一个公用的消息主题,并让系统所有微服务都连接上来,由于该主题中产生的消息会被所有的示例监听和消费,所以他为消息总线.在总线的各个实例们都可以方便地广播一些需要让其他连接该主题上的示例都知道的消息.

基本原理？

ConfigClient实例都监听MQ中同一个topic(默认是SppringcloudBus).当一个服务刷新数据时候,他会把这个信息放入带Topic中,这样其他监听同一Topic的服务就能得到通知,然后去更新自身的配置

### 配置RabbitMQ

- **下载erlang** 地址：http://erlang.org/download/otp_win64_21.3.exe 傻瓜式安装即可

- **安装RabbitMQ**地址：https://www.rabbitmq.com/install-windows.html

> 进入rabbitmq安装目录下的sbin目录：输入

```html
 rabbitmq-plugins enable rabbitmq_management
```

- 双击RabbitMQ service start
- 访问地址 localhost:15672 账号 密码 guest



### 环境搭建

- pom

  ```xml
  <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-bus-amqp</artifactId>
          </dependency>
  ```

- config服务端yml

  ```yml
  server:
    port: 3344
  spring:
    application:
      name: config-center
    cloud:
      config:
        server:
          git:
            uri: https://github.com/doudou-bai/cloud-config.git  #地址
            search-paths: /** #搜索的目录
        label: master
    rabbitmq:
      host: localhost
      port: 5672
      username: guest
      password: guest
  #服务注册到eureka地址
  eureka:
    client:
      service-url:
        defaultZone: http://localhost:7001/eureka
  #########
  
  # 暴露bus刷新配置的端点
  management:
    endpoints:
      web:
        exposure:
          include: "bus-refresh"
  
  ```

- 消费端yml

  ```yml
  server:
    port: 3355
  spring:
    application:
      name: config-client
    cloud:
      config:
        label: master # 分支名称
        name: application #配置文件名称
        profile: dev #读取后缀名称
        uri: http://localhost:3344 #配置中心地址
    rabbitmq:
      host: localhost
      port: 5672
      username: guest
      password: guest
  #服务注册到eureka地址
  eureka:
    client:
      service-url:
        defaultZone: http://localhost:7001/eureka
  # 暴露监控端点
  management:
    endpoints:
      web:
        exposure:
          include: "*"
  
  
  ```

- 修改git内容

- 刷新

  ```
  curl -X POST "http://localhost:3344/actuator/bus-refresh/config-client:3355"
  ```

- 查看3344端口内容

- 查看3355端口内容

- 查看3366端口内容

上面是**全局通知**，但如果我们想**定点通知**该如何做呢？

**定点通知：**只通知3355，不通知3366

实现方法：cmd 刷新3344

```html
curl -X POST "http://localhost:配置中心的端口号/actuator/bus-refresh/微服务名字:端口号"
```

## Spring Cloud Stream

### 消息驱动之生产者

- pom.xml

```xml
 <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-stream-rabbit</artifactId>
        </dependency>    
```

- yml

  ```yml
  server:
    port: 8801
  
  spring:
    application:
      name: cloud-stream-provider
    cloud:
      stream:
        binders: # 在此处配置要绑定的rabbitmq的服务信息；
          defaultRabbit: # 表示定义的名称，用于于binding整合
            type: rabbit # 消息组件类型
            environment: # 设置rabbitmq的相关的环境配置
              spring:
                rabbitmq:
                  host: localhost
                  port: 5672
                  username: guest
                  password: guest
        bindings: # 服务的整合处理
          output: # 这个名字是一个通道的名称
            destination: studyExchange # 表示要使用的Exchange名称定义
            content-type: application/json # 设置消息类型，本次为json，文本则设置“text/plain”
            binder: defaultRabbit # 设置要绑定的消息服务的具体设置
  
  eureka:
    client: # 客户端进行Eureka注册的配置
      service-url:
        defaultZone: http://localhost:7001/eureka
    instance:
      lease-renewal-interval-in-seconds: 2 # 设置心跳的时间间隔（默认是30秒）
      lease-expiration-duration-in-seconds: 5 # 如果现在超过了5秒的间隔（默认是90秒）
      instance-id: send-8801.com  # 在信息列表时显示主机名称
      prefer-ip-address: true     # 访问的路径变为IP地址
  
  ```

- 创建接口 servcie

  ```java
  package com.stguigu.springcloud.service;
  
  /**
   * Create By 王嘉浩
   * Time 2020/06/ 8:26
   */
  public interface IMessageProvider {
      public String send();
  }
  
  ```

- 创建实现类

  ```java
  package com.stguigu.springcloud.service;
  
  import org.springframework.beans.factory.annotation.Autowired;
  import org.springframework.cloud.stream.annotation.EnableBinding;
  import org.springframework.cloud.stream.messaging.Source;
  import org.springframework.messaging.MessageChannel;
  import org.springframework.messaging.support.MessageBuilder;
  
  import javax.annotation.Resource;
  import java.util.UUID;
  
  /**
   * Create By 王嘉浩
   * Time 2020/06/ 8:27
   */
  @EnableBinding(Source.class)//定义消息的管道
  public class MessageProviderImpl implements IMessageProvider {
      //消息发送消息
      @Resource
      private MessageChannel output;
  
      @Override
      public String send() {
          String s = UUID.randomUUID().toString();
          output.send(MessageBuilder.withPayload(s).build());
          System.out.println("*********"+s);
          return null;
      }
  }
  
  ```

- 创建controlr

  ```java
  package com.stguigu.springcloud;
  
  import com.stguigu.springcloud.service.IMessageProvider;
  import org.springframework.web.bind.annotation.GetMapping;
  import org.springframework.web.bind.annotation.RestController;
  
  import javax.annotation.Resource;
  
  /**
   * Create By 王嘉浩
   * Time 2020/06/ 8:47
   */
  @RestController
  public class SendMessageController {
      @Resource
      private IMessageProvider messageProvider;
  
      @GetMapping("/sendMessage")
      public String sendMessage() {
         return messageProvider.send();
      }
  }
  
  ```

- 启动 eureka 

- 启动 Rabbit

- 启动项目

- 测试 运行

- 到http://localhost:15672/#/查看

### 消息驱动之消费端

- pom

  ```xml
  <dependencies>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-web</artifactId>
          </dependency>
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
          </dependency>
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-stream-rabbit</artifactId>
          </dependency>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-actuator</artifactId>
          </dependency>
          <!--基础配置-->
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-devtools</artifactId>
              <scope>runtime</scope>
              <optional>true</optional>
          </dependency>
          <dependency>
              <groupId>org.projectlombok</groupId>
              <artifactId>lombok</artifactId>
              <optional>true</optional>
          </dependency>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-test</artifactId>
              <scope>test</scope>
          </dependency>
      </dependencies>
  ```

- yml

  ```yml
  server:
    port: 8802
  
  spring:
    application:
      name: cloud-stream-consumer
    cloud:
      stream:
        binders: # 在此处配置要绑定的rabbitmq的服务信息；
          defaultRabbit: # 表示定义的名称，用于于binding整合
            type: rabbit # 消息组件类型
            environment: # 设置rabbitmq的相关的环境配置
              spring:
                rabbitmq:
                  host: localhost
                  port: 5672
                  username: guest
                  password: guest
        bindings: # 服务的整合处理
          input: # 这个名字是一个通道的名称
            destination: studyExchange # 表示要使用的Exchange名称定义
            content-type: application/json # 设置消息类型，本次为对象json，如果是文本则设置“text/plain”
            binder: defaultRabbit # 设置要绑定的消息服务的具体设置
  
  
  
  eureka:
    client: # 客户端进行Eureka注册的配置
      service-url:
        defaultZone: http://localhost:7001/eureka
    instance:
      lease-renewal-interval-in-seconds: 2 # 设置心跳的时间间隔（默认是30秒）
      lease-expiration-duration-in-seconds: 5 # 如果现在超过了5秒的间隔（默认是90秒）
      instance-id: receive-8802.com  # 在信息列表时显示主机名称
      prefer-ip-address: true     # 访问的路径变为IP地址
  
  ```

- controller

  ```java
  package com.atguigu.springcloud.controller;
  
  import org.springframework.beans.factory.annotation.Value;
  import org.springframework.cloud.stream.annotation.EnableBinding;
  import org.springframework.cloud.stream.annotation.StreamListener;
  import org.springframework.cloud.stream.messaging.Sink;
  import org.springframework.messaging.Message;
  import org.springframework.stereotype.Component;
  
  import javax.annotation.Resource;
  
  /**
   * @auther zzyy
   * @create 2020-02-22 11:57
   */
  @Component
  @EnableBinding(Sink.class)
  public class ReceiveMessageListenerController
  {
      @Value("${server.port}")
      private String serverPort;
  
  
      @StreamListener(Sink.INPUT)
      public void input(Message<String> message)
      {
          System.out.println("消费者1号,----->接受到的消息: "+message.getPayload()+"\t  port: "+serverPort);
      }
  }
  
  ```

- 启动 eureka

- 启动生产者

- 启动Rabbint

- 启动消费者

- 测试 运行http://localhost:8801/sendMessage

### 解决重复消费

```yml
 bindings: # 服务的整合处理
        input: # 这个名字是一个通道的名称
          destination: studyExchange # 表示要使用的Exchange名称定义
          content-type: application/json # 设置消息类型，本次为对象json，如果是文本则设置“text/plain”
          binder: defaultRabbit # 设置要绑定的消息服务的具体设置
          group: atguiguA #自定义分组   加这个就可以
```

## Sleuth分布式请求链路跟踪

### zipkin的安装

- https://dl.bintray.com/openzipkin/maven/io/zipkin/java/zipkin-server/
- 下载  zipkin-server-2.12.9-exec 
- 运行 cmd  java - jar 下载的zipkin
- 访问http://localhost:9411/zipkin/

### 使用

- pom

  ```xml
     <!--包含了sleuth+zipkin-->
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-zipkin</artifactId>
          </dependency>
  ```

- yml

  ```yml
  spring:
    application:
      name: cloud-provider-service
    zipkin:
      base-url: http://localhost:9411
    sleuth:
      sampler:
        probability: 1 #采样率值介于 0 到 1 之间，1 则表示全部采集
  ```

- 运行 jar 

- 测试地址 http://localhost:9411/zipkin/

## Spring Cloud Alibaba Nacos

一个更易于构建云原生应用的动态服务发现、配置管理和服务管理平台

### 搭建服务提供者

- pom

  ```xml
      <dependencies>
          <!--SpringCloud ailibaba nacos -->
          <dependency>
              <groupId>com.alibaba.cloud</groupId>
              <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
          </dependency>
          <!-- SpringBoot整合Web组件 -->
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-web</artifactId>
          </dependency>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-actuator</artifactId>
          </dependency>
          <!--日常通用jar包配置-->
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-devtools</artifactId>
              <scope>runtime</scope>
              <optional>true</optional>
          </dependency>
          <dependency>
              <groupId>org.projectlombok</groupId>
              <artifactId>lombok</artifactId>
              <optional>true</optional>
          </dependency>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-test</artifactId>
              <scope>test</scope>
          </dependency>
      </dependencies>
  ```

- yml

  ```yml
  server:
    port: 9001
  
  spring:
    application:
      name: nacos-payment-provider
    cloud:
      nacos:
        discovery:
          server-addr: localhost:8848 #配置Nacos地址
  
  management:
    endpoints:
      web:
        exposure:
          include: '*'
  ```

- 主启动类加@EnableDiscoveryClient

### 搭建服务消费者

- pom

  ```xml
      <dependencies>
          <!--SpringCloud ailibaba nacos -->
          <dependency>
              <groupId>com.alibaba.cloud</groupId>
              <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
          </dependency>
          <!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
          <dependency>
              <groupId>com.atguigu.springcloud</groupId>
              <artifactId>cloud-api-commons</artifactId>
              <version>${project.version}</version>
          </dependency>
          <!-- SpringBoot整合Web组件 -->
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-web</artifactId>
          </dependency>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-actuator</artifactId>
          </dependency>
          <!--日常通用jar包配置-->
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-devtools</artifactId>
              <scope>runtime</scope>
              <optional>true</optional>
          </dependency>
          <dependency>
              <groupId>org.projectlombok</groupId>
              <artifactId>lombok</artifactId>
              <optional>true</optional>
          </dependency>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-test</artifactId>
              <scope>test</scope>
          </dependency>
      </dependencies>
  ```

- yml

  ```yml
  server:
    port: 83
  
  
  spring:
    application:
      name: nacos-order-consumer
    cloud:
      nacos:
        discovery:
          server-addr: localhost:8848
  
  
  #消费者将要去访问的微服务名称(注册成功进nacos的微服务提供者)
  service-url:
    nacos-user-service: http://nacos-payment-provider
  
  
  
  ```

- 配置类

  ```java
  package com.atguigu.springcloud.alibaba.config;
  
  import org.springframework.cloud.client.loadbalancer.LoadBalanced;
  import org.springframework.context.annotation.Bean;
  import org.springframework.context.annotation.Configuration;
  import org.springframework.web.client.RestTemplate;
  
  /**
   * @auther zzyy
   * @create 2020-02-23 14:45
   */
  @Configuration
  public class ApplicationContextConfig
  {
      @Bean
      @LoadBalanced
      public RestTemplate getRestTemplate()
      {
          return new RestTemplate();
      }
  }
  
  ```

- controller

  ```java
  package com.atguigu.springcloud.alibaba.controller;
  
  import lombok.extern.slf4j.Slf4j;
  import org.springframework.beans.factory.annotation.Value;
  import org.springframework.web.bind.annotation.GetMapping;
  import org.springframework.web.bind.annotation.PathVariable;
  import org.springframework.web.bind.annotation.RestController;
  import org.springframework.web.client.RestTemplate;
  
  import javax.annotation.Resource;
  
  /**
   * @auther zzyy
   * @create 2020-02-23 15:01
   */
  @RestController
  @Slf4j
  public class OrderNacosController
  {
      @Resource
      private RestTemplate restTemplate;
  
      @Value("${service-url.nacos-user-service}")
      private String serverURL;
  
      @GetMapping(value = "/consumer/payment/nacos/{id}")
      public String paymentInfo(@PathVariable("id") Long id)
      {
          return restTemplate.getForObject(serverURL+"/payment/nacos/"+id,String.class);
      }
  
  }
  
  ```

- 启动类 @EnableDiscoveryClient

> Nacos自带集群 多创建提供者就可以

### 配置中心配置

- pom

```xml
<!--nacos-config-->
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-config</artifactId>
</dependency>
<!--nacos-discovery-->
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
</dependency>
```

- bootstrap.yml

```
# nacos配置
server:
  port: 3377

spring:
  application:
    name: nacos-config-client
  cloud:
    nacos:
      discovery:
        server-addr: localhost:8848 #Nacos服务注册中心地址
      config:
        server-addr: localhost:8848 #Nacos作为配置中心地址
        file-extension: yaml #指定yaml格式的配置
        #group: DEV_GROUP
        #namespace: 7d8f0f5a-6a53-4785-9686-dd460158e5d4


# ${spring.application.name}-${spring.profile.active}.${spring.cloud.nacos.config.file-extension}
# nacos-config-client-dev.yaml

# nacos-config-client-test.yal   ----> config.info
```

- application.yml

  ```yml
  spring:
    profiles:
      active: dev # 表示开发环境
      #active: test # 表示测试环境
      #active: info
  ```

- 启动类注解 @EnableDiscoveryClient
- 打开网址 新建配置 测试 运行

### DataId配置

- 在nacos中新建一个 设置为test环境

- 修改application文件中的

  ```yml
  spring:
    profiles:
      #active: dev # 表示开发环境
      active: test # 表示测试环境
      #active: info
  ```

- bootstrap.yml

  ```yml
  # nacos配置
  server:
    port: 3377
  
  spring:
    application:
      name: nacos-config-client
    cloud:
      nacos:
        discovery:
          server-addr: localhost:8848 #Nacos服务注册中心地址
        config:
          server-addr: localhost:8848 #Nacos作为配置中心地址
          file-extension: yaml #指定yaml格式的配置
          #group: TEST_GROUP
          #namespace: 7d8f0f5a-6a53-4785-9686-dd460158e5d4
  
  
  # ${spring.application.name}-${spring.profile.active}.${spring.cloud.nacos.config.file-extension}
  # nacos-config-client-dev.yaml
  
  # nacos-config-client-test.yaml   ----> config.info
  ```

### Group配置

- 在nacos新建一个组设置为名称

- 修改bootstrap.yml文件

  ```yml
  # nacos配置
  server:
    port: 3377
  
  spring:
    application:
      name: nacos-config-client
    cloud:
      nacos:
        discovery:
          server-addr: localhost:8848 #Nacos服务注册中心地址
        config:
          server-addr: localhost:8848 #Nacos作为配置中心地址
          file-extension: yaml #指定yaml格式的配置
          group: TEST_GROUP #分组
          #namespace: 7d8f0f5a-6a53-4785-9686-dd460158e5d4
  
  
  # ${spring.application.name}-${spring.profile.active}.${spring.cloud.nacos.config.file-extension}
  # nacos-config-client-dev.yaml
  
  # nacos-config-client-test.yaml   ----> config.info
  ```

- application.yml

  ```yml
  spring:
    profiles:
      #active: dev # 表示开发环境
      #active: test # 表示测试环境
      active: info
  ```

### NameSpace

- 在nacos 创建命名空间

- 修改bootstrap.yml文件

  ```yml
  # nacos配置
  server:
    port: 3377
  
  spring:
    application:
      name: nacos-config-client
    cloud:
      nacos:
        discovery:
          server-addr: localhost:8848 #Nacos服务注册中心地址
        config:
          server-addr: localhost:8848 #Nacos作为配置中心地址
          file-extension: yaml #指定yaml格式的配置
          group: DEV_GROUP
          namespace: 7001c47f-7036-4293-a362-3e699eaa4bb0
  
  # ${spring.application.name}-${spring.profile.active}.${spring.cloud.nacos.config.file-extension}
  # nacos-config-client-dev.yaml
  
  # nacos-config-client-test.yaml   ----> config.info
  ```

- application文件

  ```yml
  spring:
    profiles:
      active: dev # 表示开发环境
      #active: test # 表示测试环境
      #active: info
  ```

### Nacos集群 <重要>

https://blog.csdn.net/qq_37345604/article/details/90034424

> 查看mysql启动

```
service mysqld status 


upstream cluster{
         server 127.0.0.1:3333;
         server 127.0.0.1:4444;
         server 127.0.0.1:5555;
     }
```

> 查看启动几个

```
 ps -ef|grep nacos|grep -v grep|wc -l
```



#### Nginx安装

> 创建目录

```
mkdir /usr/local/nginx
```

> 下载

```
wget http://nginx.org/download/nginx-1.5.9.tar.gz
```

> 解压

```
 tar -zxvf nginx-1.5.9.tar.gz 
```

> 解压好后移至目录

```
cd nginx-1.5.9/
```

> 设置Nginx安装路径，如果没有指定，默认为/usr/local/nginx

```
./configure --prefix=/usr/local/nginx
```

> 如果出现红色字体错误，需要执行下

```
yum -y install gcc gcc-c++ autoconf automake make
```

```
./configure --prefix=/usr/local/nginx
```

> 可能会出现这个错误

```
./configure: error: the HTTP rewrite module requires the PCRE library.
You can either disable the module by using --without-http_rewrite_module
option, or install the PCRE library into the system, or build the PCRE library
statically from the source with nginx by using --with-pcre=<path> option.
```

> 如果出现了，就执行下这个

```
yum -y install openssl openssl-devel
```

> 再次执行

```
 ./configure --prefix=/usr/local/nginx
```

> 编译

```
make
```

> 安装

```
make install
```

> 启动

```
/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
```

> 停止

**查询nginx主进程号**

```
ps -ef | grep nginx
```

在进程列表里 面找master进程，它的编号就是主进程号了。

发送信号

从容停止Nginx

```
kill -QUIT 主进程号
```

快速停止Nginx

```
kill -TERM 主进程号
```

强制停止Nginx

```
pkill -9 nginx
```

另外， 若在nginx.conf配置了pid文件存放路径则该文件存放的就是Nginx主进程号，如果没指定则放在nginx的logs目录下。有了pid文 件，我们就不用先查询Nginx的主进程号，而直接向Nginx发送信号了，命令如下：
kill -信号类型 '/usr/nginx/logs/nginx.pid'

> 平滑重启

如果更改了配置就要重启Nginx，要先关闭Nginx再打开？不是的，可以向Nginx 发送信号，平滑重启。
平滑重启命令：
kill -HUP 主进程号或进程号文件路径

或者使用

```
/usr/nginx/sbin/nginx -s reload
```

注意，修改了配置文件后最好先检查一下修改过的配置文件是否正 确，以免重启后Nginx出现错误影响服务器稳定运行。

判断Nginx配置是否正确命令

```
nginx -t -c /usr/nginx/conf/nginx.conf
```

或者

/usr/nginx/sbin/nginx -t

> 访问 测试 默认端口号80

> **加了中文注解的nginx.conf**‘



```
user www www;
# 工作进程个数，可配置多个
worker_processes auto;

error_log /data/wwwlogs/error_nginx.log crit;
pid /var/run/nginx.pid;
worker_rlimit_nofile 51200;

events {
  use epoll;
  # 单个进程最大连接数
  worker_connections 51200;
  multi_accept on;
}

http {
  include mime.types;
  default_type application/octet-stream;
  server_names_hash_bucket_size 128;
  client_header_buffer_size 32k;
  large_client_header_buffers 4 32k;
  client_max_body_size 1024m;
  client_body_buffer_size 10m;
  sendfile on;
  tcp_nopush on;
  keepalive_timeout 120;
  server_tokens off;
  tcp_nodelay on;

  fastcgi_connect_timeout 300;
  fastcgi_send_timeout 300;
  fastcgi_read_timeout 300;
  fastcgi_buffer_size 64k;
  fastcgi_buffers 4 64k;
  fastcgi_busy_buffers_size 128k;
  fastcgi_temp_file_write_size 128k;
  fastcgi_intercept_errors on;

  #Gzip Compression
  gzip on;
  gzip_buffers 16 8k;
  gzip_comp_level 6;
  gzip_http_version 1.1;
  gzip_min_length 256;
  gzip_proxied any;
  gzip_vary on;
  gzip_types
    text/xml application/xml application/atom+xml application/rss+xml application/xhtml+xml image/svg+xml
    text/javascript application/javascript application/x-javascript
    text/x-json application/json application/x-web-app-manifest+json
    text/css text/plain text/x-component
    font/opentype application/x-font-ttf application/vnd.ms-fontobject
    image/x-icon;
  gzip_disable "MSIE [1-6]\.(?!.*SV1)";

  #If you have a lot of static files to serve through Nginx then caching of the files' metadata (not the actual files' contents) can save some latency.
  open_file_cache max=1000 inactive=20s;
  open_file_cache_valid 30s;
  open_file_cache_min_uses 2;
  open_file_cache_errors on;

######################## default ############################
  # 服务器集群名称  和下面的location地址对应
  upstream myServer {
    # weigth参数表示权值，权值越高被分配到的几率越大
    # server 127.0.0.1:8080 weight=1;
    # server 127.0.0.1:8060 weight=1;
    server 47.93.10.184:8080;
    server 47.93.10.184:8081;

  }

  # 每一个server相当于一个代理服务器
  server {
  # 监听端口，默认80
  listen 8848;
  # 当前服务的域名，可以有多个，用空格分隔(我们是本地所以是localhost)  www.kolbe.cn
  server_name localhost;
  #server_name _;
  access_log /data/wwwlogs/access_nginx.log combined;
  root /data/wwwroot/default;
  # 当没有指定主页时，默认会选择这个指定的文件，可多个，空格分隔
  index index.html index.htm index.php;
  # 表示匹配的路径，这时配置了/表示所有请求都被匹配到这里
  location / {
      # 请求转向自定义的服务器列表
      proxy_pass http://myServer;
  }
  location /nginx_status {
    stub_status on;
    access_log off;
    allow 127.0.0.1;
    deny all;
    }
  location ~ [^/]\.php(/|$) {
    #fastcgi_pass remote_php_ip:9000;
    fastcgi_pass unix:/dev/shm/php-cgi.sock;
    fastcgi_index index.php;
    include fastcgi.conf;
    }
  location ~ .*\.(gif|jpg|jpeg|png|bmp|swf|flv|mp4|ico)$ {
    expires 30d;
    access_log off;
    }
  location ~ .*\.(js|css)?$ {
    expires 7d;
    access_log off;
    }
  location ~ /\.ht {
    deny all;
    }
  }

########################## vhost #############################
  include vhost/*.conf;
}
```

> 开放端口

```
firewall-cmd --zone=public --add-port=3333/tcp --permanent
```

> 保存设置

```
firewall-cmd --reload
```

> 强制停止

```
pkill -9 nginx
```

> 看几个启动

```
ps -ef|grep nacos|grep -v grep|wc -l
```



### Nacos集群

- 提前准备 安装1个Nginx、安装3个Nacos(3个或3个以上的Nacos节点才能成为集群)、安装1个mysql。
- Nacos持久化切换配置

```
# 官网：https://nacos.io/zh-cn/docs/deployment.html

# Nacos默认自带的是嵌入式数据库Derby。


# Derby到mysql切换步骤配置：（mysql version 5.6.5+）

# 1、再 nacos/conf/ 目录下找到sql脚本 nacos-mysql.sql。

# 2、创建数据库，数据库名字为 nacos_config。

# 3、在 nacos_config 数据库中执行sql脚本到数据库创建表。

# 4、修改conf/application.properties文件，增加支持mysql数据源配置（目前只支持mysql），添加mysql数据源的url、用户名和密码。
spring.datasource.platform=mysql

db.num=1
db.url.0=jdbc:mysql://39.97.3.60:3306/nacos_config?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true
db.user=root
db.password=333

# 5、再以单机模式启动nacos，nacos所有写嵌入式数据库的数据都写到了mysql
```

- 集群搭建

```
# 1、提前准备
安装1个Nginx、安装3个Nacos(3个或3个以上的Nacos节点才能成为集群)、安装1个mysql。

# 2、Linux服务器上mysql数据库持久化配置(具体步骤建2.8.2)

# 3、复制cluster.conf.example 为cluster.conf
[root@mingyu conf]# cp cluster.conf.example cluster.conf
[root@mingyu conf]# ll
total 56
-rw-r--r-- 1  502 games  1769 Jun 19 17:34 application.properties
-rw-r--r-- 1  502 games   408 Oct 11  2019 application.properties.example
-rw-r--r-- 1 root root     58 Jun 20 13:53 cluster.conf
-rw-r--r-- 1  502 games    58 Oct 11  2019 cluster.conf.example
-rw-r--r-- 1  502 games 20210 Nov  4  2019 nacos-logback.xml
-rw-r--r-- 1  502 games  9788 Oct 11  2019 nacos-mysql.sql
-rw-r--r-- 1  502 games  7196 Oct 11  2019 schema.sql

# 4、修改cluster.conf内容
39.97.3.60:3333
39.97.3.60:4444
39.97.3.60:5555

# 5、编辑Nacos的启动脚本startup.sh，使它能够接受不同的端口。

# 修改前
  while getopts ":m:f:s:" opt
  do
      case $opt in
          m)
              MODE=$OPTARG;;
          f)
              FUNCTION_MODE=$OPTARG;;
          s)
              SERVER=$OPTARG;;
          ?)
          echo "Unknown parameter"
          exit 1;;
      esac
  done
 
133 echo "$JAVA ${JAVA_OPT}" > ${BASE_DIR}/logs/start.out 2>&1 &
134 nohup $JAVA ${JAVA_OPT} nacos.nacos >> ${BASE_DIR}/logs/start.out 2>&1 &
135 echo "nacos is starting，you can check the ${BASE_DIR}/logs/start.out"
 

# 修改后
 57 while getopts ":m:f:s:p:" opt
 58 do
 59     case $opt in
 60         m)
 61             MODE=$OPTARG;;
 62         f)
 63             FUNCTION_MODE=$OPTARG;;
 64         s)
 65             SERVER=$OPTARG;;
 66         p)
 67             PORT=$OPTARG;;
 68         ?)
 69         echo "Unknown parameter"
 70         exit 1;;
 71     esac
 72 done

133 echo "$JAVA ${JAVA_OPT}" > ${BASE_DIR}/logs/start.out 2>&1 &
134 nohup $JAVA -Dserver.port=${PORT} ${JAVA_OPT} nacos.nacos >> ${BASE_DIR}/logs/start.out 2>&1 &
135 echo "nacos is starting，you can check the ${BASE_DIR}/logs/start.out"

# 6、Nginx的配置文件，反向代理 + 负载均衡
 
      upstream cluster{
         server 127.0.0.1:3333;
         server 127.0.0.1:4444;
         server 127.0.0.1:5555;
      }
 40 
 41     server {
 42         listen       1111;
 43         server_name  localhost;
 44 
 45         #charset koi8-r;
 46 
 47         #access_log  logs/host.access.log  main;
 48 
 49         location / {
 50            # root   html;
 51            # index  index.html index.htm;
 52            proxy_pass http://cluster;
 53         }

# 7、启动mysql5.7、Nacos集群、nginx
./startup.sh -p 3333
./startup.sh -p 4444
./startup.sh -p 5555

# 8、测试 http://39.97.3.60:1111/nacos 通过nginx访问nacos集群
```



```
win启动 startup.cmd -m cluster
```



## Spring Cloud Alibaba Sentinel 处理分布式事务

面对云原生微服务的流量控制,熔断降级组件

Hystrix

1. 需要我们自己搭建监控平台
2. 没有一套web界面可以更加好的配置流控,速率控制,服务熔断,服务降级

Seatinel

1. 单独一个组件,可以独立出来
2. 直接界面化的细粒度统一配置

预定>配置>编码 



### 安装

- 下载sentinel-dashboard-1.7.0.jar
- 打开cmd 运行 java -jar sentinel-dashboard-1.7.0.jar
- 浏览器访问 127.0.0.1:8080 账号 密码都是 Seatinel

### 初始化演示工程

- pom

  ```xml
      <!--SpringCloud ailibaba nacos -->
          <dependency>
              <groupId>com.alibaba.cloud</groupId>
              <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
          </dependency>
          <!--SpringCloud ailibaba sentinel-datasource-nacos 后续做持久化用到-->
          <dependency>
              <groupId>com.alibaba.csp</groupId>
              <artifactId>sentinel-datasource-nacos</artifactId>
          </dependency>
          <!--SpringCloud ailibaba sentinel -->
          <dependency>
              <groupId>com.alibaba.cloud</groupId>
              <artifactId>spring-cloud-starter-alibaba-sentinel</artifactId>
          </dependency>
  ```

- yml

  ```yml
  server:
    port: 8401
  
  spring:
    application:
      name: cloudalibaba-sentinel-service
    cloud:
      nacos:
        discovery:
          server-addr: localhost:8848 #Nacos服务注册中心地址
      sentinel:
        transport:
          dashboard: localhost:8080 #配置Sentinel dashboard地址
          port: 8719
  
  management:
    endpoints:
      web:
        exposure:
          include: '*'
  
  feign:
    sentinel:
      enabled: true # 激活Sentinel对Feign的支持
  ```

- 进行controller访问

- 进到127.0.0.1:8080 进行查看监控信息

### 流控规则 

- 直接失败 QPS 配置

![流控规则-QPS-直接失败](D:\MD文档笔记\img\spring cloud\流控规则-QPS-直接失败.png)

- 线程 直接失败 配置

![流控规则-线程-直接失败](D:\MD文档笔记\img\spring cloud\流控规则-线程-直接失败.png)

- 关联 QPS 配置

`使用模拟发送B的请求,在自己访问A发现已经挂了`

![流控规则-QPS-关联](D:\MD文档笔记\img\spring cloud\流控规则-QPS-关联.png)

- 链路

![链路1](D:\MD文档笔记\img\spring cloud\链路1.png)

![链路1](D:\MD文档笔记\img\spring cloud\链路1.png)

`/testA 和 /testB 都是从 sentinel_web_servlet_context（从Sentinel—Dashboard可以看到） 的节点，添加链路的时候，入口资源填写【sentinel_web_servlet_context】，就可以实现链路的限流。`

### 流控效果

- 直接报错

  ```
  Blocked by Sentinel (flow limiting)
  ```

- Warm Up  预热

  ```
  预热计算 QPS / 3 就是每秒的并发
  
  预热时长是郭几秒开发真正的承受并发
  ```

![预热](D:\MD文档笔记\img\spring cloud\预热.png)

- 排队等待  就是一个一个的来

### 降级规则

- RT

```
# 1、是什么？
1秒持续进入5个请求 ---> 触发降级(断路器打开) ---> 时间窗口结束 ---> 关闭降级

# 2、配置
降级策略【RT】，RT写【200】(单位：毫秒)，时间窗口写【1】(单位：秒)

我们希望资源的处理速度在200ms内正常，当平均处理时长超过200ms，开启断路器，且该资源在【时间窗口】时间范围内不可用。
```

![RT-](D:\MD文档笔记\img\spring cloud\RT-.png)

- 异常比例

```
QPS >= 5 && 异常比例(秒级统计)超过阈值 ---> 触发降级(断路器打开) ---> 时间窗口结束 ---> 关闭降级
```

```
降级策略【异常比例】，异常比例写【0.2】(代表20%)，时间窗口写【1】(单位：秒)
```

![异常比例](D:\MD文档笔记\img\spring cloud\异常比例.png)

- 异常数

```
# 1、是什么
异常数(分钟统计)超过阈值 ---> 触发降级(断路器打开) ---> 时间窗口结束 ---> 关闭降级
```

![异常数](D:\MD文档笔记\img\spring cloud\异常数.png)



### 热点规则

何为热点？热点即经常访问的数据。很多时候我们希望统计某个热点数据中访问频次最高的 Top K 数据，并对其访问进行限制。比如：

- 商品 ID 为参数，统计一段时间内最常购买的商品 ID 并进行限制
- 用户 ID 为参数，针对一段时间内频繁访问的用户 ID 进行限制

**热点参数限流会统计传入参数中的热点参数，并根据配置的限流阈值与模式，对包含热点参数的资源调用进行限流。热点参数限流可以看做是一种特殊的流量控制****，仅对包含热点参数的资源调用生效。**



- 在controller创建方法

```java
    @GetMapping("/testHotKey")
    @SentinelResource(value = "testHotKey", blockHandler = "deal_testHotKey")
    public String testHotKey(@RequestParam(value = "p1", required = false) String p1,
                             @RequestParam(value = "p2", required = false) String p2) {
        //int age = 10/0;
        return "------testHotKey";
    }

    public String deal_testHotKey(String p1, String p2, BlockException exception) {
        return "------deal_testHotKey,o(╥﹏╥)o";  //sentinel系统默认的提示：Blocked by Sentinel (flow limiting)
    }
```

- 在控制台指定![RT-](D:\MD文档笔记\img\spring cloud\RT-.png)

- 高级热点规则

```
普通 超过1秒钟一个后,达到阈值1后马上被限流
我们期望参数p1当他是某个特殊值时,他的限流值和平时不一样
特例 假如当p1的值等于5时,他的阈值可以达到200
```

![高级](D:\MD文档笔记\img\spring cloud\高级.png)

- 自定义限流

```java
//自定义限流处理逻辑
//写一个全局兜底类

package com.ymy.spring.cloud.alibaba.handler;

import com.alibaba.csp.sentinel.slots.block.BlockException;
import com.ymy.spring.cloud.entity.SimpleResponse;

public class CustomerBlockHandler {
    /**
     * 全局兜底方案
     * 这里一定要static
     */
    public static SimpleResponse handlerException(BlockException e) {
        return new SimpleResponse(444, "按用户自定义,全局兜底方案");
    }
}
//测试代码

/**
* 用户自定义限流处理逻辑
* 限流的时候会去全局兜底的类找指定的方法
*/
@GetMapping("/rateLimit/customerBlockHandler")
@SentinelResource(value = "customerBlockHandler",
                  blockHandlerClass = CustomerBlockHandler.class,
                  blockHandler = "handlerException")
public SimpleResponse customerBlockHandler() {
    return new SimpleResponse(200, "按用户自定义限流OK！", new Payment("3", "serial03"));
}
```



### 系统规则

了解即可

### @SentinelSource注解属性说明

```
@SentinelSource注解属性说明
@SentinelResource 用于定义资源，并提供可选的异常处理和 fallback 配置项。 @SentinelResource 注解包含以下属性：

value：资源名称，必需项（不能为空）。
entryType：entry 类型，可选项（默认为 EntryType.OUT）。
blockHandler / blockHandlerClass: blockHandler 对应处理 BlockException 的函数名称，可选项。blockHandler 函数访问范围需要是 public，返回类型需要与原方法相匹配，参数类型需要和原方法相匹配并且最后加一个额外的参数，类型为 BlockException。blockHandler 函数默认需要和原方法在同一个类中。若希望使用其他类的函数，则可以指定 blockHandlerClass 为对应的类的 Class 对象，注意对应的函数必需为 static 函数，否则无法解析。
fallback/fallbackClass：fallback 函数名称，可选项，用于在抛出异常的时候提供 fallback 处理逻辑。fallback 函数可以针对所有类型的异常（除了exceptionsToIgnore里面排除掉的异常类型）进行处理。fallback 函数签名和位置要求：
返回值类型必须与原函数返回值类型一致；
方法参数列表需要和原函数一致，或者可以额外多一个 Throwable 类型的参数用于接收对应的异常。
fallback 函数默认需要和原方法在同一个类中。若希望使用其他类的函数，则可以指定 fallbackClass 为对应的类的 Class 对象，注意对应的函数必需为 static 函数，否则无法解析。
defaultFallback（since 1.6.0）：默认的 fallback 函数名称，可选项，通常用于通用的 fallback 逻辑（即可以用于很多服务或方法）。默认 fallback 函数可以针对所有类型的异常（除了exceptionsToIgnore里面排除掉的异常类型）进行处理。若同时配置了 fallback 和 defaultFallback，则只有 fallback 会生效。defaultFallback 函数签名要求：
返回值类型必须与原函数返回值类型一致；
方法参数列表需要为空，或者可以额外多一个 Throwable 类型的参数用于接收对应的异常。
defaultFallback 函数默认需要和原方法在同一个类中。若希望使用其他类的函数，则可以指定 fallbackClass 为对应的类的 Class 对象，注意对应的函数必需为 static 函数，否则无法解析。
exceptionsToIgnore（since 1.6.0）：用于指定哪些异常被排除掉，不会计入异常统计中，也不会进入 fallback 逻辑中，而是会原样抛出。
```



### 按资源名称限流

- 方法

```java
@GetMapping("/byResouce")
    @SentinelResource(value = "byResouce", blockHandler = "handleException")
    public CommonResult byResouce() {
        return new CommonResult(200, "按资源名称限流测试OK", new Payment(2020L, "serial001"));
    }

    public CommonResult handleException(BlockException exception) {
        return new CommonResult(444, exception.getClass().getCanonicalName() + "\t服务不可用");
    }
```

- ![按资源名称限流](D:\MD文档笔记\img\spring cloud\按资源名称限流.png)

- 节点是临时的 只要把服务关闭,节点消失

### URl限流处理

- 方法

```java
 @GetMapping("/reteLimit/byUrl")
    @SentinelResource(value = "byUrl")
    public CommonResult byUrl() {
        return new CommonResult(200, "按Url限流测试OK", new Payment(2020L, "serial002"));
    }
```

![按Url限流](D:\MD文档笔记\img\spring cloud\按Url限流.png)



### 自定义限流

- controller

```java
@GetMapping("/reteLimit/customerBlockHandler")
    @SentinelResource(value = "customerBlockHandler", blockHandlerClass = CustomerBlockHandler.class,//类的class文件
            blockHandler = "handlerException"//具体的方法)
    public CommonResult customerBlockHandler() {
        return new CommonResult(200, "按客户自定义限流测试OK", new Payment(2020L, "serial003"));
    }
```

- 自定义处理

```java
package com.atguigu.springcloud.alibaba.myheandler;

import com.alibaba.csp.sentinel.slots.block.BlockException;
import com.atguigu.springcloud.alibaba.entities.CommonResult;
import com.atguigu.springcloud.alibaba.entities.Payment;

/**
 * Create By 王嘉浩
 * Time 2020/07/ 22:22
 */

public class CustomerBlockHandler {
    //必须加static 否则不可以用
    public static CommonResult handlerException(BlockException exception) {
        return new CommonResult(4444, "按客户自定义限流测试失败返回信息");
    }
    public static CommonResult handlerException2(BlockException exception) {
        return new CommonResult(4444, "按客户自定义限流测试失败返回信息====2");
    }
}

```

- 到控制台进行限流

## Sentinel整合Ribbon

pom

```xml
       <!--seata-->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-seata</artifactId>
            <exclusions>
                <exclusion>
                    <artifactId>seata-all</artifactId>
                    <groupId>io.seata</groupId>
                </exclusion>
            </exclusions>
        </dependency>
```

### Java异常处理

```java
 @SentinelResource(value = "fallback"//可以自定义的名字 和getMapping保持一致
 , fallback = "handlerFallback") //fallback只负责业务异常  类的名字
```

```java
 @RequestMapping("/consumer/fallback/{id}")
 @SentinelResource(value = "fallback", fallback = "handlerFallback") //fallback只负责业务异常
public CommonResult<Payment> fallback(@PathVariable Long id) {
        CommonResult<Payment> result = restTemplate.getForObject(SERVICE_URL + "/paymentSQL/" + id, CommonResult.class, id);

        if (id == 4) {
            throw new IllegalArgumentException("IllegalArgumentException,非法参数异常....");
        } else if (result.getData() == null) {
            throw new NullPointerException("NullPointerException,该ID没有对应记录,空指针异常");
        }

        return result;
    }

    //本例是fallback
    public CommonResult handlerFallback(@PathVariable Long id, Throwable e) {
        Payment payment = new Payment(id, "null");
        return new CommonResult<>(444, "兜底异常handlerFallback,exception内容  " + e.getMessage(), payment);
    }
```

### sentinel配置异常处理

```java
 @SentinelResource(value = "fallback", blockHandler = "blockHandler"//类的名字) //blockHandler只负责sentinel控制台配置违规
```

```java
 //本例是blockHandler
    public CommonResult blockHandler(@PathVariable Long id, BlockException blockException) {
        Payment payment = new Payment(id, "null");
        return new CommonResult<>(445, "blockHandler-sentinel限流,无此流水: blockException  " + blockException.getMessage(), payment);
    }
```

### 配置-Java异常统一处理

```java
 @SentinelResource(value = "fallback", fallback = "handlerFallback", blockHandler = "blockHandler")
```

```java
 //本例是fallback
    public CommonResult handlerFallback(@PathVariable Long id, Throwable e) {
        Payment payment = new Payment(id, "null");
        return new CommonResult<>(444, "兜底异常handlerFallback,exception内容  " + e.getMessage(), payment);
    }

    //本例是blockHandler
    public CommonResult blockHandler(@PathVariable Long id, BlockException blockException) {
        Payment payment = new Payment(id, "null");
        return new CommonResult<>(445, "blockHandler-sentinel限流,无此流水: blockException  " + blockException.getMessage(), payment);
    }
```

### 异常忽略

```java
 @SentinelResource(value = "fallback", fallback = "handlerFallback", blockHandler = "blockHandler",
            exceptionsToIgnore = {IllegalArgumentException.class})//异常类class文件
```

## Sentinel整合Feign

- pom

```xml
 <!--SpringCloud openfeign -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-openfeign</artifactId>
        </dependency>
```

- yml

```yml
# 激活Sentinel对Feign的支持
feign:
  sentinel:
    enabled: true
```

- 主启动类注解

```
@EnableFeignClients
```

- service-serviceimpl

```java
//service
@FeignClient(value = "nacos-payment-provider",fallback = PaymentFallbackService.class)
public interface PaymentService
{
    @GetMapping(value = "/paymentSQL/{id}")
    public CommonResult<Payment> paymentSQL(@PathVariable("id") Long id);
}
//serviceimpl
@Component
public class PaymentFallbackService implements PaymentService
{
    @Override
    public CommonResult<Payment> paymentSQL(Long id)
    {
        return new CommonResult<>(44444,"服务降级返回,---PaymentFallbackService",new Payment(id,"errorSerial"));
    }
}

```

- 启动后测试  故意关闭服务提供者 会自动降级


## sentinel持久化规则

- 一旦我们重启应用,sentinel规则将消失,生产环境需要将配置规则进行持久化

- xml

```xml
 <!--SpringCloud ailibaba sentinel-datasource-nacos 后续做持久化用到-->
        <dependency>
            <groupId>com.alibaba.csp</groupId>
            <artifactId>sentinel-datasource-nacos</artifactId>
        </dependency>
```

- yml

```yml
server:
  port: 8401

spring:
  application:
    name: cloudalibaba-sentinel-service
  cloud:
    nacos:
      discovery:
        server-addr: localhost:8848 #Nacos服务注册中心地址
    sentinel:
      transport:
        dashboard: localhost:8080 #配置Sentinel dashboard地址
        port: 8719
      datasource:
        ds1:
          nacos:
            server-addr: localhost:8848
            dataId: cloudalibaba-sentinel-service
            groupId: DEFAULT_GROUP
            data-type: json
            rule-type: flow

management:
  endpoints:
    web:
      exposure:
        include: '*'

feign:
  sentinel:
    enabled: true # 激活Sentinel对Feign的支持



```

- 在nacos配置 data id 是服务名字

```json
[
    {
        "resource": "资源名称",
        "limitApp": "来源应用",  
        "grade": 阈值类型,0表示线程数,1表示QPS,
        "count": 单机阈值,
        "strategy": 流控模式,0表示直接,1表示关联,2表示链路,
        "controlBehavior": 流控效果,0表示快速失败.1表示Warm Up, 2表示排队等待,
        "clusterMode": 是否集群 true false
    }
]
```

- 刷新服务测试


## Seata处理分布式事务

### 分布式事务的由来

- 分布式之前：单机单库没有这个问题，o(╥﹏╥)o。
- 分布式之后：单体应用被拆分成微服务应用，原来的三个模块被拆分成三个独立的应用，分别使用三个独立的数据源，业务操作需要调用三个服务来完成。此时每个服务内部的数据一致性由本地事务来保证，但是全局的数据一致性问题没办法保证。
- **一句话：一次业务操作需要跨多个数据源或需要跨多个系统进行远程调用，就产生分布式事务。**

### seata术语

**TC - 事务协调者**

维护全局和分支事务的状态，驱动全局事务提交或回滚。

**TM - 事务管理器**

定义全局事务的范围：开始全局事务、提交或回滚全局事务。

**RM - 资源管理器**

管理分支事务处理的资源，与TC交谈以注册分支事务和报告分支事务的状态，并驱动分支事务提交或回滚。

### 安装

- 下载jar包  seata-server-0.9.0.zip
- 修改配置文件 file.conf
- service模块 修改前

```
service {
  #vgroup->rgroup
  vgroup_mapping.my_test_tx_group = "default"
  #only support single node
  default.grouplist = "127.0.0.1:8091"
  #degrade current not support
  enableDegrade = false
  #disable
  disable = false
  #unit ms,s,m,h,d represents milliseconds, seconds, minutes, hours, days, default permanent
  max.commit.retry.timeout = "-1"
  max.rollback.retry.timeout = "-1"
}
```

- service 修改后

```
service {
  #vgroup->rgroup
  vgroup_mapping.my_test_tx_group = "fsp-tx-group"#主要修改它
  #only support single node
  default.grouplist = "127.0.0.1:8091"
  #degrade current not support
  enableDegrade = false
  #disable
  disable = false
  #unit ms,s,m,h,d represents milliseconds, seconds, minutes, hours, days, default permanent
  max.commit.retry.timeout = "-1"
  max.rollback.retry.timeout = "-1"
}
```

- store修改前

```
## transaction log store
store {
  ## store mode: file、db
  mode = "file"
```

- store修改后

```
## transaction log store
store {
  ## store mode: file、db
  mode = "db"
```

```

  ## database store
  db {
    ## the implement of javax.sql.DataSource, such as DruidDataSource(druid)/BasicDataSource(dbcp) etc.
    datasource = "dbcp"
    ## mysql/oracle/h2/oceanbase etc.
    db-type = "mysql"
    driver-class-name = "com.mysql.jdbc.Driver"
    url = "jdbc:mysql://127.0.0.1:3306/seata"
    user = "root"
    password = "0009"
    min-conn = 1
    max-conn = 3
    global.table = "global_table"
    branch.table = "branch_table"
    lock-table = "lock_table"
    query-limit = 100
  }
}
```

- 创建数据库seata
- 创建表

```sql
-- the table to store GlobalSession data
DROP TABLE IF EXISTS `global_table`;
CREATE TABLE `global_table` (
  `xid` VARCHAR(128)  NOT NULL,
  `transaction_id` BIGINT,
  `status` TINYINT NOT NULL,
  `application_id` VARCHAR(32),
  `transaction_service_group` VARCHAR(32),
  `transaction_name` VARCHAR(128),
  `timeout` INT,
  `begin_time` BIGINT,
  `application_data` VARCHAR(2000),
  `gmt_create` DATETIME,
  `gmt_modified` DATETIME,
  PRIMARY KEY (`xid`),
  KEY `idx_gmt_modified_status` (`gmt_modified`, `status`),
  KEY `idx_transaction_id` (`transaction_id`)
);

-- the table to store BranchSession data
drop table if exists `branch_table`;
create table `branch_table` (
  `branch_id` bigint not null,
  `xid` varchar(128) not null,
  `transaction_id` bigint ,
  `resource_group_id` varchar(32),
  `resource_id` varchar(256) ,
  `lock_key` varchar(128) ,
  `branch_type` varchar(8) ,
  `status` tinyint,
  `client_id` varchar(64),
  `application_data` varchar(2000),
  `gmt_create` datetime,
  `gmt_modified` datetime,
  primary key (`branch_id`),
  key `idx_xid` (`xid`)
);

-- the table to store lock data
drop table if exists `lock_table`;
create table `lock_table` (
  `row_key` varchar(128) not null,
  `xid` varchar(96),
  `transaction_id` long ,
  `branch_id` long,
  `resource_id` varchar(256) ,
  `table_name` varchar(32) ,
  `pk` varchar(36) ,
  `gmt_create` datetime ,
  `gmt_modified` datetime,
  primary key(`row_key`)
);

```

- 修改registry.conf文件 根据自己的情况修改
- 启动nacos
- 启动 seata-server

# 面试题

- 什么是微服务?

  ```
  通常而言,微服务架构师一种架构模式或者说是一种架构风格,他提倡将单一的应用程序划分为一组小的服务,每个服务运行在其独立的自己的进程中
  ```

- 微服务之间是如何通信的?

  ```
  同步：RPC ,REST等。
  异步：消息队列，要考虑消息的可靠传输、高性能，以及编程模型的变化等。
  ```

- Spring Cloud 和 Dubbo有哪些区别?

  ```
  Dubbo是RPC通信机制,Spring cloud是基于HTTP的RESTFUL API 
  ```

- SpringBoot 和SpringCloud,请你谈谈您对他们的理解

  ```
  SpringBoot专注于快速方便的开发单个个体微服务
  SpringBoot可以单独使用可不依赖于SpringCLoud,SpringCloud必须依赖于SpringBoot
  属于依赖关系
  SpringBoot专注于快速,方便的开发单个微服务个体SpringCloud关注全局的服务治理框架
  ```

- 什么是服务熔断?什么是服务降级?

  ```
  服务熔断的作用类似于我们家用的保险丝，当某服务出现不可用或响应超时的情况时，为了防止整个系统出现雪崩，
  暂时停止对该服务的调用。
  　　服务降级是从整个系统的负荷情况出发和考虑的，对某些负荷会比较高的情况，为了预防某些功能（业务场景）出现
  负荷过载或者响应慢的情况，在其内部暂时舍弃对一些非核心的接口和数据的请求，而直接返回一个提前准备好的fallback
  （退路）错误处理信息。这样，虽然提供的是一个有损的服务，但却保证了整个系统的稳定性和可用性。
  ```

- 微服务的优缺点分别是什么?说下你在项目开发中遇到的坑?

  ```
  优点：
  
  松耦合，聚焦单一业务功能，无关开发语言，团队规模降低。在开发中，不需要了解多有业务，
  只专注于当前功能，便利集中，功能小而精。微服务一个功能受损，对其他功能影响并不是太大，可以快速定位问题。
  微服务只专注于当前业务逻辑代码，不会和 html、css 或其他界面进行混合。可以灵活搭配技术，独立性比较舒服。
  
  缺点：
  
  随着服务数量增加，管理复杂，部署复杂，服务器需要增多，服务通信和调用压力增大，运维工程师压力增大，
  人力资源增多，系统依赖增强，数据一致性，性能监控。
  ```

- 你所知道的微服务技术栈有哪些,请列举一二?

  ```
  维度(springcloud)
  服务开发：springboot spring springmvc
  服务配置与管理:Netfix公司的Archaiusm ,阿里的Diamond
  服务注册与发现:Eureka,Zookeeper
  服务调用:Rest RPC gRpc
  服务熔断器:Hystrix
  服务负载均衡:Ribbon Nginx
  服务接口调用:Fegin
  消息队列:Kafka Rabbitmq activemq
  服务配置中心管理:SpringCloudConfig
  服务路由（API网关）Zuul
  事件消息总线:SpringCloud Bus
  ```
  
- eureka 和 zookeeper都可以提供服务注册和发现的功能,请说说两个的区别?

  ```
  1）、Zookeeper保证了CP（C：一致性，P：分区容错性），Eureka保证了AP（A：高可用）
  （1）、当向注册中心查询服务列表时，我们可以容忍注册中心返回的是几分钟以前的信息，但不能容忍直接down掉不可用。也就是说，服务注册功能对高可用性要求比较高，但zk会出现这样一种情况，当master节点因为网络故障与其他节点失去联系时，剩余节点会重新选leader。问题在于，选取leader时间过长，30 ~ 120s，且选取期间zk集群都不可用，这样就会导致选取期间注册服务瘫痪。在云部署的环境下，因网络问题使得zk集群失去master节点是较大概率会发生的事，虽然服务能够恢复，但是漫长的选取时间导致的注册长期不可用是不能容忍的。
  （2）、Eureka保证了可用性，Eureka各个节点是平等的，几个节点挂掉不会影响正常节点的工作，剩余的节点仍然可以提供注册和查询服务。而Eureka的客户端向某个Eureka注册或发现是发生连接失败，则会自动切换到其他节点，只要有一台Eureka还在，就能保证注册服务可用，只是查到的信息可能不是最新的。除此之外，Eureka还有自我保护机制，如果在15分钟内超过85%的节点没有正常的心跳，那么Eureka就认为客户端与注册中心发生了网络故障，此时会出现以下几种情况：
  ①、Eureka不在从注册列表中移除因为长时间没有收到心跳而应该过期的服务。
  ②、Eureka仍然能够接受新服务的注册和查询请求，但是不会被同步到其他节点上（即保证当前节点仍然可用）
  ③、当网络稳定时，当前实例新的注册信息会被同步到其他节点。
  
  因此，Eureka可以很好的应对因网络故障导致部分节点失去联系的情况，而不会像Zookeeper那样使整个微服务瘫痪。
  ```

- ID生成规则部分硬性要求

  - 全局唯一

    ```
    不能出现重复的ID号,既然是唯一标识,这是最基本的要求
    ```

  - 趋势递增

  - 单调递增

    ```
    保证下一个ID一定大于上一个ID,例如事务版本号,IM增量信息,排序等特殊需求
    ```

  - 信息安全

  - 含时间戳

  ID生成规则部分可用性要求

  ```
  高可用
  低延迟
  高QPS
  ```

  解决方案

  ```
  UUID
  数据库自增
  基于Ridis生成全局Id策略
  ```

  雪花算法

  

