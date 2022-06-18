# Spring Boot 整合篇

https://www.bilibili.com/video/BV1KW411F7oX?p=20

## Spring Boot 与缓存

> JSR107

 **Java Caching定义了5个核心接口，分别是CachingProvider, CacheManager, Cache, Entry 和 Expiry。**

1. CachingProvider定义了创建、配置、获取、管理和控制多个CacheManager。一个应用可以在运行期访问多个CachingProvider。
2. CacheManager定义了创建、配置、获取、管理和控制多个唯一命名的Cache，这些Cache存在于CacheManager的上下文中。一个CacheManager仅被一个CachingProvider所拥有。
3. Cache是一个类似Map的数据结构并临时存储以Key为索引的值。一个Cache仅被一个CacheManager所拥有。
4. Entry是一个存储在Cache中的key-value对。
5. Expiry 每一个存储在Cache中的条目有一个定义的有效期。一旦超过这个时间，条目为过期的状态。一旦过期，条目将不可访问、更新和删除。缓存有效期可以通过ExpiryPolicy设置

> 重要概念&缓存注解



| Cache          | 缓存接口,自定缓存操作.实现RedisCache,EhCacheCache,CoucurrentMapCache等 |
| -------------- | ------------------------------------------------------------ |
| CacheManager   | 缓存管理器,管理各种缓存cache组件                             |
| @Cacheable     | 主要针对方法配置,能够根据方法的请求对其结果进行缓存          |
| @CacheEvict    | 清空缓存                                                     |
| @CachePut      | 保证方法被调用,希望结果被缓存                                |
| @EnableCaching | 开启基于注解的缓存                                           |
| keyGenerator   | 缓存数据的key生成策略                                        |
| serialize      | 缓存数据的value序列化的策略                                  |

## 缓存的使用

> 开启缓存

```
@EnableCaching//开启基于注解的缓存
```

> 配置

```yml
#开启驼峰
mybatis.configuration.map-underscore-to-camel-case=true

logging.level.cn.doudou.springboor01cache.mapper=debug
```

> service

```
 @Cacheable
 
 属性
 	cacheNames/values;指定缓存组件的名字
 	key;缓存数据使用key,可以用它来指定,默认是使用方法参数的值 1-方法的返回值
 	keyGenerator;key的生成器,可以自己指定key的生成器的组件id,key/keyGenerator二选一
 	cacheManager;指定缓存的管理器,或者cacheResolver指定解析器
 	condition;符合条件才缓存
 	unless;否定缓存 返回条件为true才会缓存  unless = "#result==null"
 	sync;是否使用异步模式
```

```
@CacheEvict
	属性 
		key指定要清楚的数据
		beforeInvocation = false是否在方法执行前执行
```

```
@Caching  指定多个规则
```

## Spring Boot整合Redis

> 安装

```
docker pull redis
```

> 运行

```
docker run -d  -p 3344:6379 --name myredis redis
```

> pom

```xml
<dependency>
 	<groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

> 自动注入对象

```
	//操作字符串
    @Autowired
    private StringRedisTemplate stringRedisTemplate;

    //操作对象
    @Autowired
    private RedisTemplate redisTemplate;

```

> 操作字符串

```java
//写入操作
	@Test
    public void test01() {
        stringRedisTemplate.opsForValue().append("1873629279", "6666");
    }
```

```java
//获取数据
    @Test
    public void test01() {
        System.out.println(stringRedisTemplate.opsForValue().get("1873629279"));
    }

```

> 操作list

```java
//写入数据
	@Test
    public void test01() {
        stringRedisTemplate.opsForList().leftPush("mylist", "1");
        stringRedisTemplate.opsForList().leftPush("mylist", "2");
        stringRedisTemplate.opsForList().leftPush("mylist", "3");
        stringRedisTemplate.opsForList().leftPush("mylist", "4");
    }
```

```java
//获取数据
  @Test
    public void test01() {
        //获取哪个数据库 下标是什么
        for (String mylist : stringRedisTemplate.opsForList().range("mylist", 1, 2)) {
            System.out.println(mylist);
        }
    }
```

> 序列化

```java
package cn.doudou.springboor01cache.config;

import cn.doudou.springboor01cache.bean.Employee;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.redis.connection.RedisConnectionFactory;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.data.redis.serializer.Jackson2JsonRedisSerializer;
import org.springframework.http.codec.cbor.Jackson2CborDecoder;

import java.net.UnknownHostException;

/**
 * Create By 王嘉浩
 * Time 2020/7/26 12:50
 */
@Configuration
public class MyRedisConfig {
    @Bean
    public RedisTemplate<Object, Employee> redisTemplate(
            RedisConnectionFactory redisConnectionFactory) throws UnknownHostException {
        RedisTemplate<Object, Employee> template = new RedisTemplate<Object, Employee>();
        template.setConnectionFactory(redisConnectionFactory);
        //序列化器
        Jackson2JsonRedisSerializer<Employee> ser = new Jackson2JsonRedisSerializer<Employee>();
        template.setDefaultSerializer(ser);
        return template;
    }
}

```

> 保存对象 必须序列化

```java
    @Autowired
    private RedisTemplate<Object, Employee> redisTemplate2; //注入自己的redis
    
    
     @Test
    public void test01() {
        Employee employeeById = employeeMapper.getEmployeeById(1);//从数据拿到数据
        redisTemplate2.opsForValue().set("emp-02", employeeById);
    }
```

## JMS & AMQP消息

- JMS(Java Message Service) Java消息服务-基于JVM消息代理的规范.ActiveMQ HornetMQ是JMS实现
- AMQP(Advanced Message Queuing Protocol)-高级消息队列协议,也是消息代理的规范,兼容JMSRabbintMQ是AMQP的实现

> 安装RabbitMQ

```
docker pull rabbitmq:3-management
```

> 启动

```
docker run -d -p 5672:5672 -p 15672:15672 --name myrabbitmq  rabbitmq的镜像id
```

> 查看镜像

```
docker images
```

> 访问地址

```
ip+:15672/
```

> 账号 密码

```
guest : guest
```

direct 只有完全匹配的可以收到

fanout 都可以收到

topic 根据匹配规则发送

## Spring Boot整合RabbitMQ

> pom

```xml
 		<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-amqp</artifactId>
        </dependency>
         <dependency>
            <groupId>org.springframework.amqp</groupId>
            <artifactId>spring-rabbit-test</artifactId>
            <scope>test</scope>
        </dependency>
```

> 配置文件

```properties
spring.rabbitmq.host=192.168.0.101
spring.rabbitmq.port=5672
spring.rabbitmq.username=guest
spring.rabbitmq.password=guest
```

> 发送消息

```java
   @Test
    public void contextLoads() {
        Map<String, String> map = new HashMap<>();
        map.put("测试消息1", "Java测试消息");
        map.put("测试消息2", "Rabbit测试消息");
        rabbitTemplate.convertAndSend("exchange.direct", "atguigu.news", map);
    }
```

> 获取消息

```java
 @Test
    public void get() {
        Object receive = rabbitTemplate.receiveAndConvert("atguigu.news");
        System.out.println(receive);
        System.out.println(receive.getClass());
    }
```

> 序列化为Json发送

```java
package cn.doudou.springboot01amqp.config;

import org.springframework.amqp.support.converter.Jackson2JsonMessageConverter;
import org.springframework.amqp.support.converter.MessageConverter;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

/**
 * Create By 王嘉浩
 * Time 2020/7/26 17:21
 */
@Configuration
public class MyAMQPConfig {
    @Bean
    public MessageConverter messageConverter() {
        return new Jackson2JsonMessageConverter();
    }
}

```

> 监听消息队列

```
@EnableRabbit //开启基于注解的RabbitMQ
```

```java
package cn.doudou.springboot01amqp.service;

import cn.doudou.springboot01amqp.bean.Book;
import cn.doudou.springboot01amqp.bean.Email;
import cn.doudou.springboot01amqp.utils.SendMail;
import org.springframework.amqp.rabbit.annotation.RabbitListener;
import org.springframework.stereotype.Service;

/**
 * Create By 王嘉浩
 * Time 2020/7/26 17:34
 */
@Service
public class BookService {
    //监听Rabbit
    @RabbitListener(queues = "atguigu.news")
    public void receive(Email email) {
        SendMail sm = new SendMail();
        sm.sendMail(email.getEmailname(), email.getTitle(), email.getTxt());
        System.out.println("邮件地址:" + email.getEmailname());
        System.out.println("邮件标题:" + email.getTitle());
        System.out.println("邮件内容:" + email.getTxt());

    }
}

```

> AMQP Admin

```
    @Autowired
    private AmqpAdmin amqpAdmin//自动注入 
```

> 创建Exchanges

```java
  /**
     * 创建Exchange
     */
    @Test
    public void createExchange() {
        amqpAdmin.declareExchange(new DirectExchange("Java_amqp_exchange"));
    }
```

> 创建队列   Queues

```java
   /**
     * 创建 Queues
     */
    @Test
    public void createExchange() {
        amqpAdmin.declareQueue(new Queue("amqpadmin.queue", true));
    }
```

> 创建绑定

```java
/**
     * 创建 绑定规则
     */
    @Test
    public void createExchange() {
        amqpAdmin.declareBinding(new Binding("amqpadmin.queue", Binding.DestinationType.QUEUE,
                "Java_amqp_exchange",
                "amqphaha", null));
    }
```

## Spring Boot 与任务

> 异步任务

```java
 //告诉Spring这是一个异步的
    @Async
    public void hello() {
        try {
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("处理数据中");
    }
```

```java\
@EnableAsync//开启异步注解
```

> 定时任务

网站  https://www.bejson.com/othertools/cron/

```
@EnableScheduling//开启定时任务
```

```java
 @Scheduled(cron = "1 * * * * ? ")//每天下午3点14分1秒执行
    public void hello() {
        System.out.println("Hello.....");
    }
```

> 邮件任务

```xml
		<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-mail</artifactId>
        </dependency>
```

```properties
spring.mail.username=douoai@163.com
spring.mail.password=XNRQERACSMIGCBDU
spring.mail.host=smtp.163.com

#QQ邮箱要开启
spring.mail.properties.mail.smtp.ssl.enable=true
```

`简单邮件的发送`

```java
    @Test
    void contextLoads() {
        SimpleMailMessage simpleMailMessage = new SimpleMailMessage();
        simpleMailMessage.setSubject("通知-今晚加班");//设置title
        simpleMailMessage.setText("今晚20:30加班");//设置内容
        simpleMailMessage.setTo("2484003268@qq.com");//设置发送人
        simpleMailMessage.setFrom("douoai@163.com");//设置谁发的
        javaMailSender.send(simpleMailMessage);
    }

```

`html邮件发送`

```java
    @Test
    void test2() throws MessagingException {
        MimeMessage mimeMessage = javaMailSender.createMimeMessage();

        MimeMessageHelper helper = new MimeMessageHelper(mimeMessage, true);
        //邮件设置
        helper.setSubject("通知-今晚加班");//设置title
        helper.setText("<h1 style='color:red'>测试</h1>", true);//设置内容
        helper.addAttachment("1.jpg", new File("C:\\Users\\Mi\\Desktop\\18中职软件03班\\1.jpg"));//上传文件
        helper.setTo("2484003268@qq.com");//设置发送人
        helper.setFrom("douoai@163.com");//设置谁发的

        javaMailSender.send(mimeMessage);
    }
```

## Spring Boot与安全

> xml

```
   <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-security</artifactId>
        </dependency>
```

> 配置

```java
package cn.doudou.springboot05security.config;

import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;

/**
 * Create By 王嘉浩
 * Time 2020/7/27 15:53
 */
@EnableWebSecurity
public class MySecurityConfig extends WebSecurityConfigurerAdapter {

    /**
     * 配置 资源的路径的控制 还有登录 注销
     *
     * @param http
     * @throws Exception
     */
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        //授权规则
        http.authorizeRequests().antMatchers("/").permitAll()
                .antMatchers("/level1/*").hasAnyRole("VIP1")
                .antMatchers("/level2/*").hasAnyRole("VIP2")
                .antMatchers("/level3/*").hasAnyRole("VIP3");
        //super.configure(http);
        //开启登录
        http.formLogin().loginPage("/userlogin"); 

        //用户注销
        http.logout().logoutSuccessUrl("/");
        
        
        //记住我
        http.rememberMe();
    }

    /**
     * 配置用使用内存的用户进行认证
     *
     * @param auth
     * @throws Exception
     */
    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        //定义认证规则
        auth.inMemoryAuthentication().passwordEncoder(new BCryptPasswordEncoder())
                .withUser("user1").password(new BCryptPasswordEncoder().encode("123456")).roles("VIP1")
                .and()
                .withUser("user2").password(new BCryptPasswordEncoder().encode("123456")).roles("VIP2")
                .and()
                .withUser("user3").password(new BCryptPasswordEncoder().encode("123456")).roles("VIP3");
        //super.configure(auth);
    }
}

```