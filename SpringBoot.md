# Spring Boot

### 环境搭建

- 创建一个maven工程

- 导入起步依赖

  ```xml
  <!--所有的springboot都要继承下面这个-->
  <parent>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-parent</artifactId>
          <version>2.0.1.RELEASE</version>
      </parent>
  ```

  ```xml
  <!--web起步的坐标--> 
  <dependencies>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-web</artifactId>
          </dependency>
      </dependencies>
  ```

- 随便创建一个类

  ```
  注解:@SpringBootApplication 表示该类是SpringBoot的引导类
  ```

  **示例:**

  ```java
  @SpringBootApplication
  public class MySpringBootApplication {
      public static void main(String[] args) {
          SpringApplication.run(MySpringBootApplication.class);
      }
  }
  ```

- 创建一个controller类

  ```
  启动项目直接访问
  ```


### yml文件格式

语法:key : value

```yaml
name:lisi
```

对象格式:

```yaml
person:
  name: lisi
  age: 12
```

行内对象格式

```yaml
person:{name: lisi,age: 12}
```

数组，集合

```yaml
key:
 - value1
 - value2
```

```yaml
key:[value1,value2]
```

配置数据,集合(对象数据)

```yaml
key:
	-name : lisi
	age: 14
	-name : lisi
	age: 14
	-name : lisi
	age: 14
	....
```

```yaml
key:[{name: lisi,age:12},{name: lisi,age:12},{name: lisi,age:12}]
```

map配置

```yaml
map:
	key1: values1
	key1: values1
	key1: values1
```

获取配置的值

```
@Value("${name}")
```

映射值

```
@ConfigurationProperties(prefix = "")
需要提供set get方法
```

### SpringBoot集成Mybatis

- 导入mybatis'的环境

  ```
  <!--mybatis起步依赖-->
          <dependency>
              <groupId>org.mybatis.spring.boot</groupId>
              <artifactId>mybatis-spring-boot-starter</artifactId>
              <version>1.1.1</version>
          </dependency>
  ```

- 导入mysql的jar

  ```
   <!-- MySQL连接驱动 -->
          <dependency>
              <groupId>mysql</groupId>
              <artifactId>mysql-connector-java</artifactId>
          </dependency>
  ```

- 在application的配置文件配置

  ```
  #数据库连接信息
  #DB Configuration:
  spring.datasource.driverClassName=com.mysql.jdbc.Driver
  spring.datasource.url=jdbc:mysql://localhost:3306/acc?useUnicode=true&characterEncoding=utf8
  spring.datasource.username=root
  spring.datasource.password=0009
  #spring集成Mybatis环境
  #pojo别名扫描包
  mybatis.type-aliases-package=cn.doudou.domain
  #加载Mybatis映射文件
  mybatis.mapper-locations=classpath:mapper/*Dao.xml
  
  ```

- 创建dao接口

  ```
  加注解@Mapper注解
  ```

  编写接口

  ```
     List<Account> findAll();
  ```

- 在controller类测试

  ```java
  
  @Controller
  public class Mybatis {
      @Autowired
      private AccountDao dao;
  
      @ResponseBody
      @RequestMapping("/l")
      public List<Account> run() {
          List<Account> all = dao.findAll();
          return all;
      }
  }
  
  ```

### SpringBoo集成junit

- 导入junit的jar坐标

  ```
  <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-test</artifactId>
              <scope>test</scope>
              <exclusions>
                  <exclusion>
                      <groupId>org.junit.vintage</groupId>
                      <artifactId>junit-vintage-engine</artifactId>
                  </exclusion>
              </exclusions>
          </dependency>
  ```

- 在test包创建测试类

  ```
  @RunWith(SpringRunner.class)
  @SpringBootTest(classes = SpringbootMybatisApplication.class)
  public class demo {
      @Autowired
      private AccountDao dao;
  
      @Test
      public void run() {
          List<Account> all = dao.findAll();
          for (Account account : all) {
              System.out.println(account);
          }
  
      }
  }
  ```

### SpringBoot集成SpringDataJPA

- 导入jar

  ```
    <!-- springBoot JPA的起步依赖 -->
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-data-jpa</artifactId>
          </dependency>
          <!-- MySQL连接驱动 -->
          <dependency>
              <groupId>mysql</groupId>
              <artifactId>mysql-connector-java</artifactId>
          </dependency>
  ```

- 在dao创建一个接口

  ```java
  package cn.doudou.dao;
  
  import cn.doudou.domain.Account;
  import org.springframework.data.jpa.repository.JpaRepository;
  import org.springframework.data.jpa.repository.JpaSpecificationExecutor;
  
  public interface AccountDao extends JpaRepository<Account, Integer>, JpaSpecificationExecutor<Account> {
  }
  
  ```

- 在创建实体类

  ```java
  package cn.doudou.domain;
  
  import javax.persistence.Entity;
  import javax.persistence.GeneratedValue;
  import javax.persistence.GenerationType;
  import javax.persistence.Id;
  import java.io.Serializable;
  
  @Entity
  public class Account implements Serializable {
      @Id
      @GeneratedValue(strategy = GenerationType.IDENTITY)
      private Integer id;
      private String name;
      private Double money;
  
      public Integer getId() {
          return id;
      }
  
      public void setId(Integer id) {
          this.id = id;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public Double getMoney() {
          return money;
      }
  
      public void setMoney(Double money) {
          this.money = money;
      }
  
      @Override
      public String toString() {
          return "Account{" +
                  "id=" + id +
                  ", name='" + name + '\'' +
                  ", money=" + money +
                  '}';
      }
  }
  
  ```

- jdk9可以报错,在pom.xml导入

  ```
  <!--jdk9需要导入如下坐标-->
  <dependency>
      <groupId>javax.xml.bind</groupId>
      <artifactId>jaxb-api</artifactId>
      <version>2.3.0</version>
  </dependency>
  ```


### SpringBoot常用的配置

| 配置名称                    | 默认值 | 描述              |
| --------------------------- | ------ | ----------------- |
| server.port                 | 8080   | 端口号            |
| server.servlet.context-path | /      | 设置应用上下文    |
| logging.file                | 无     | 日志文件输出路径  |
| logging.level               | info   | 最低日志输出级别  |
| debug                       | false  | 开启/关闭调试模式 |
| spring.datasource.*         |        | 数据库相关的设置  |

### banner

在resources创建banner.txt

```
${AnsiColor.BRIGHT_RED}
                          _ooOoo_
                         o8888888o
                         88" . "88
                         (| ^_^ |)
                         O\  =  /O
                      ____/`---'\____
                    .'  \\|     |//  `.
                   /  \\|||  :  |||//  \
                  /  _||||| -:- |||||-  \
                  |   | \\\  -  /// |   |
                  | \_|  ''\---/''  |   |
                  \  .-\__  `-`  ___/-. /
                ___`. .'  /--.--\  `. . ___
              ."" '<  `.___\_<|>_/___.'  >'"".
            | | :  `- \`.;`\ _ /`;.`/ - ` : | |
            \  \ `-.   \_ __\ /__ _/   .-` /  /
      ========`-.____`-.___\_____/___.-`____.-'========
                           `=---='
      ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
            佛祖保佑       永不宕机     永无BUG
      --------------------------------------------------
```



