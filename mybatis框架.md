# Mybatis

https://www.bilibili.com/video/BV1NE411Q7Nx?p=25

三层架构

- 表现层
  - 用于展示数据
- 业务层
  - 处理业务需求
- 持久层
  - 适合数据库交互

## mybatis的概述

​	mybatis是一个持久层框框架,用java编写的

​	它封装了jdbc操作的很多细节,使开发者只需要关注sql语句本身,不需要注册驱动,创建连接等复杂的过程,他使用了ORM思想实现了结果集的封装

## Mybatis 的特性

1. Mybatis是支持定制化SQL,存储过程以及高级映射的优秀的持久层框架
2. Mybatis 避免了几乎所有的JDBC代码和手动设置参数以及获取结果集
3. Mybatis可以使用简单的XML或注解用于配置和原始映射,将接口和Java的POJO映射成数据库中的记录
4. Mybatis是一个半自动的ORM框架

## 和其他持久化层技术对比

- JDBC
  - SQL夹杂在Java代码中耦合度高,导致硬编码内伤
  - 维护不易实际开发需求中SQL有变化,修改的情况多见
  - 开发效率低
- Hibernate和JPA
  - 操作简单,开发效率高
  - 程序中的长难复杂SQL需要绕过框架
  - 内部自动生产的的SQL,不容易做特优化
  - 基于全映射的全自动框架,大量字段的POJO进行部分映射时比较困难
  - 反射操作太多,导致数据库性能下降
- Mybatis
  - 轻量级,性能出色
  - Sql和Java编码分开,功能边界清晰.Java代码专注业务,Sql语句专注数据
  - 开发效率稍逊与Hibernate但是完全可以接受

## mybatis的入 门

​	环境搭建

​	入门案例

mybatis的环境搭建

- 创建maven工程并且导入坐标

- 创建实体类和dao的接口

- 创建Mybatis的主配置

  SqlMapConfig.xml

- 创建映射配置文件

  IUserDao.xml

- **注意事项:**创建IUserDao.xml和IUserDao.java名称是为了和自谦的保持一致

- 在mybatis中他把持久层的操作接口名称和映射文件也叫做Mapper

- 所以IUserDao和IUserMapper是一样的

- 在idea中创建目录的时候,他和包是不一样的

- mybatis的映射配置文件位置必须和dao接口的包结构相同

- 映射配置文件的mapper标签namespace属性的取值必须是到接口的全限定类名

- 映射配置文件的操作配置,id属性的取值必须是dao接口的方法名字
  当我们遵从了第三,四,五点之后,我们在开发中就无须在写dao的实现类



### 配置文件

```xml
<dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
    <!--mybatis-->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>3.4.5</version>
    </dependency>
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>5.1.45</version>
    </dependency>
    <dependency>
      <groupId>log4j</groupId>
      <artifactId>log4j</artifactId>
      <version>1.2.12</version>
    </dependency>
          <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.16.20</version>
        </dependency>
  </dependencies>

    <build>
        <resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>
            <resource>
                <directory>src/main/resource</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>
        </resources>
    </build>
```

SqlMapConfig.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!-- mybatis的主配置文件 -->
<configuration>
    <!-- 配置环境 -->
    <environments default="mysql">
        <!-- 配置mysql的环境-->
        <environment id="mysql">
            <!-- 配置事务的类型-->
            <transactionManager type="JDBC"></transactionManager>
            <!-- 配置数据源（连接池） -->
            <dataSource type="POOLED">
                <!-- 配置连接数据库的4个基本信息 -->
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/java"/>
                <property name="username" value="root"/>
                <property name="password" value="0009"/>
            </dataSource>
        </environment>
    </environments>

    <!-- 指定映射配置文件的位置，映射配置文件指的是每个dao独立的配置文件 -->
    <mappers>
         <mapper resource="cn/doudou/dao/userDao.xml"></mapper>
    </mappers>
</configuration>
```

userDao.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="cn.doudou.dao.userDao">
    <select id="findAll" resultType="cn.doudou.domain.User">
select * from user
    </select>
    <insert id="saveUser" parameterType="cn.doudou.domain.User">
        <selectKey keyProperty="id" keyColumn="id" resultType="int" order="AFTER">
            select last_insert_id();
        </selectKey>
        insert  into user username = #{username},birthday = #{birthday},sex = #{sex},address = #{address};
    </insert>
    <update id="" parameterType="cn.doudou.domain.User">
        update user  set username = #{username},address = #{address},sex = #{sex},birthday = #{birthday} where id = #{id};
    </update>
    <delete id="deleteuser" parameterType="java.lang.Integer">
        delete from user where id = #{value}
    </delete>
    <select id="findById" parameterType="java.lang.Integer" resultType="cn.doudou.domain.User">
        select * from user where id = #{vlaue}
    </select>
    <select id="findByName" parameterType="String" resultType="cn.doudou.domain.User">
        <!-- select * from user where username like #{name}-->
        select * from user where username like '%${value}%';
    </select>
    <select id="findtotal" resultType="int">
        select count(id) from user;
    </select>
</mapper>
```

测试方法

可以定义一个utils类进行简化操作

```java
package cn.doudou.utils;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.jdbc.SQL;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;

/**
 * Create By 王嘉浩
 * Time 2020/7/11 15:35
 */
public class MybatisUtils {
    private static SqlSessionFactory sqlSessionFactory;

    //加载配置文件xml
    static {
        try {
            InputStream inputStream;
            String resource = "mybatis-config.xml";
            inputStream = Resources.getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    //创建并且返回一个可以执行sql语句的对象
    public static SqlSession getSqlSession() {
        return sqlSessionFactory.openSession();
    }

}

```

```java
//读取配置文件
        InputStream in = Resources.getResourceAsStream("SqlMapConfig.xml");
        //创建SqlSessionFactory工厂
        SqlSessionFactoryBuilder builder = new SqlSessionFactoryBuilder();
        SqlSessionFactory factory = builder.build(in);
        //使用工厂生产SqlSession对象
        SqlSession sqlSession = factory.openSession();
        //使用SqlSession创建Dao接口的代理对象
        AccountDao mapper = sqlSession.getMapper(AccountDao.class);
        //5.使用代理对象执行方法
        for (Account account : mapper.findAll()) {
            if (account.getId() == 1001 || account.getId() == 1003 || account.getId() == 1004)
                System.out.println(account);
        }
        //6.释放资源
        sqlSession.close();
        in.close();
```

```java
  InputStream in = null;
    SqlSessionFactory factory = null;
    SqlSession sqlSession = null;
    userDao dao = null;

    @Before//用于加载文件
    public void init() throws IOException {
        in = Resources.getResourceAsStream("SqlMapConfig.xml");
        factory = new SqlSessionFactoryBuilder().build(in);
        sqlSession = factory.openSession();
        dao = sqlSession.getMapper(userDao.class);
    }

    @After//用于最后执行
    public void destroy() throws IOException {
        sqlSession.commit();//提交事务
        sqlSession.close();
        in.close();
    }

```

## mybatis配置

```xml
<properties resource="org/mybatis/example/config.properties">
</properties>
<dataSource type="POOLED">
  <property name="driver" value="${driver}"/>
  <property name="url" value="${url}"/>
  <property name="username" value="${username}"/>
  <property name="password" value="${password}"/>
</dataSource>
```

## 类型别名

```xml
    <typeAliases>
        <package name="cn.doudou.pojo"/>
    </typeAliases>
```

## mappers

配置xml对应的文件

```xml
 <mappers>
        <package name="cn.doudou.mapper" />
    </mappers>
```



## 引入外部配置文件

### 新建配置文件**jdbc.properties**

```properties
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/test
jdbc.username=root
jdbc.password=0009
```

在mybatis中加载文件

```xml
 <properties resource="jdbc.properties"/>
```

然后使用${}读取文件内容

## Mybatis获取参数值的两种方式



## 设置

| 设置名             | 描述                                                         | 有效值        | 默认值 |
| :----------------- | :----------------------------------------------------------- | :------------ | :----- |
| cacheEnabled       | 全局性地开启或关闭所有映射器配置文件中已配置的任何缓存。     | true \| false | true   |
| lazyLoadingEnabled | 延迟加载的全局开关。当开启时，所有关联对象都会延迟加载。 特定关联关系中可通过设置 `fetchType` 属性来覆盖该项的开关状态。 | true \| false | false  |

## 其他配置

映射器

```xml
<!-- 使用相对于类路径的资源引用 -->
<mappers>
  <mapper resource="org/mybatis/builder/AuthorMapper.xml"/>
  <mapper resource="org/mybatis/builder/BlogMapper.xml"/>
  <mapper resource="org/mybatis/builder/PostMapper.xml"/>
</mappers>
<!-- 使用完全限定资源定位符（URL） -->
<mappers>
  <mapper url="file:///var/mappers/AuthorMapper.xml"/>
  <mapper url="file:///var/mappers/BlogMapper.xml"/>
  <mapper url="file:///var/mappers/PostMapper.xml"/>
</mappers>
<!-- 使用映射器接口实现类的完全限定类名 -->
<mappers>
  <mapper class="org.mybatis.builder.AuthorMapper"/>
  <mapper class="org.mybatis.builder.BlogMapper"/>
  <mapper class="org.mybatis.builder.PostMapper"/>
</mappers>
<!-- 将包内的映射器接口实现全部注册为映射器 -->
<mappers>
  <package name="org.mybatis.builder"/>
</mappers>
```

## 核心文件配置文件层级关系

-  configuration配置
  - properties设置
  - settings设置
  - typeAliases类型别名
  - typeHandrers类型处理器
  - objectFactory对象工厂
  - plugins插件
  - environments环境
    - environment环境变量
      - transactionManager事务管理器
      - dataDource数据源
    - databaseldProvider数据库厂商标识
    - mappers映射器 

## 结果集映射 

```xml
    <resultMap id="可以随意" type="pojo的类路径">
        <result property="实体类属性" column="数据库属性"/>
    </resultMap>
```

## 日志

| logImpl | 指定 MyBatis 所用日志的具体实现，未指定时将自动查找。 | SLF4J \| LOG4J \| LOG4J2 \| JDK_LOGGING \| COMMONS_LOGGING \| STDOUT_LOGGING \| NO_LOGGING | 未设置 |
| ------- | ----------------------------------------------------- | ------------------------------------------------------------ | ------ |
|         |                                                       |                                                              |        |

```xml
    <settings>
        <setting name="logImpl" value="LOG4J"/>
    </settings>
```

## Log4j

配置文件

```properties
#将等级为DEBUG的日志信息输出到console和file两个目的地
log4j.rootLogger=DEBUG,console,file

#控制台输出的相关设置
log4j.appender.console=org.apache.log4j.ConsoleAppender
log4j.appender.console.Target=System.out
log4j.appender.console.Threshold=DEBUG
log4j.appender.console.layout=org.apache.log4j.PatternLayout
log4j.appender.console.layout.ConversionPattern=【%c】-%m%n

#文件输出的相关配置
log4j.appender.file=org.apache.log4j.RollingFileAppender
log4j.appender.file.File=./log/kuang.log
log4j.appender.file.MaxFileSize=10mb
log4j.appender.file.Threshold=DEBUG
log4j.appender.file.layout=org.apache.log4j.PatternLayout
log4j.appender.file.layout.ConversionPattern=【%p】[%d{yy-MM-dd}【%c】%m%n

#日志输出级别
log4j.logger.org.mybatis=DEBUG
log4j.logger.java.sql=DEBUG
log4j.logger.java.sql.Statement=DEBUG
log4j.logger.java.sql.ResultSet=DEBUG
log4j.logger.java.sql.PreparedStatement=DEBUG
```

## 分页

```xml
   <select id="getLimitAccount" parameterType="map" resultType="cn.doudou.pojo.Account">
        select * from account limit #{startIndex},#{pageSize}
    </select>
```

## 注解开发

查询

```
@Select("select * from account")
```

删除

```
@Delete("sql语句")
```

修改

```
@Update("sql语句")
```

新增

```
@insert("sql语句")
```

## 多对一

```xml
针对于查询映射   
<resultMap id="studentteacher" type="student">
        <result column="id" property="id"/>
        <result column="name" property="name"/>
        <association property="teacher" javaType="Teacher" column="tid" select="getTeacher"/>
    </resultMap>

    <select id="getStudentListForTeacher" resultMap="studentteacher">
      SELECT * FROM student
    </select>
    <select id="getTeacher" resultType="teacher">
        select * from teacher where id = #{id}
    </select>
```

```xml
针对于结果映射    集合用collection 对象用 association javaType java的类型 ofType 泛型的类型


<resultMap id="studentteacher" type="student">
        <result column="sid" property="id"/>
        <result column="sname" property="name"/>
        <association property="teacher" javaType="Teacher">
            <result column="tname" property="name"/>
            <result column="tid" property="id"/>
        </association>
    </resultMap>

    <select id="getStudentListForTeacher" resultMap="studentteacher">
    SELECT s.id AS sid,s.`name` AS sname ,
t.`name` AS tname,t.`id` AS tid FROM student AS s,teacher AS t WHERE s.`tid`= t.`id`
    </select>
```

## 动态SQL

```xml
#####if
SELECT * FROM books
        <where>
            <if test="id != null">
                 id = #{id}
            </if>
            <if test="name != null">
                and name = #{name}
            </if>
            <if test="number != null">
                and number >= #{number}
            </if>
        </where>
#####choose
 SELECT * FROM books
        <where>
            <choose>
                <when test="id != null">
                    id = #{id}
                </when>
                <when test="name != null">
                    and name = #{name}
                </when>
                <otherwise>
                   and number = #{number}
                </otherwise>
            </choose>
        </where>
#####set
<update id="undateBooks" parameterType="map">
        update books
        <set>
            <if test="name != null">
                name = #{name},
            </if>
        </set>
        <set>
            <if test="number != null">
                number = #{number},
            </if>
        </set>
        where id = #{id}
    </update>
#####sql引用
   <sql id="name-number">
        <set>
            <if test="name != null">
                name = #{name},
            </if>
        </set>
        <set>
            <if test="number != null">
                number = #{number},
            </if>
        </set>
    </sql>

    <update id="undateBooks" parameterType="map">
        update books
        <include refid="name-number"/>
        where id = #{id}
    </update>
#####foreach
  <select id="getOneTwo" parameterType="map" resultType="books">
        select * from books
        <where>
            <foreach collection="ids" item="id" open="and (" separator="or" close=")">
                id = #{id}
            </foreach>
        </where>
    </select>
#测试
  @Test
    public void test3() {
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        BooksMapper mapper = sqlSession.getMapper(BooksMapper.class);
        HashMap map = new HashMap();
        ArrayList<Integer> list = new ArrayList<Integer>();
        list.add(1001);
        list.add(1002);
        list.add(1003);
        map.put("ids", list);
        List<Books> oneTwo = mapper.getOneTwo(map);
        for (Books books : oneTwo) {
            System.out.println(books);
        }
        sqlSession.commit();
        sqlSession.close();
    }
```

常用标签

```
if
choose when  otherwise 相当于java的switch语句
where 相当于sql语句的where 条件查询
```



## Lombok

```
@Data
@Setter
@ToString
@Getter
@AllArgsConstructor
@NoArgsConstructor
```

## Mybatis的参数

parameterType(输入类型)

传递简单类型

传递pojo对象

​	OGNL表达式:Object Graphic Navigation Language

​								对象	图			导航				语言

他是通过对象的取值方法来获取数据,在写法上把get给省略了

传递pojo包装对象

## Mybatis中的连接池

Mybatis中连接池使用及分析

Mybatis事务控制的分析

Mybatis基于xml配置的动态SQL语句使用

- if
- where 
- foreach
- sql

Mybatis中的多表操作

- 一对一
- 一对多
- 多对多

连接池

​	提供了3中方式的配置

​	主配置文件<dateSource标签> type就是表示采用哪种连接池方式

**type 属性**

POOLED 采用传统的DataSource实现

UNPOOLED 采用传统的获取连接的方式并没有使用池的思想

 JNDI  采用服务器提供的技术,实现来获取DataSource,不同的服务器,所能拿到的资源是不一样的

​		注意:如果不是web获取maven war工程是不能使用的

Mybatis事务

- 什么是事务

- 事务的四大特性ACID

- 不考虑隔离性会产生的3个问题

- 解决办法:四种隔离级别

  他是通过sqlSession对象的commit

REsultMap结果映射

## Mybatis多表查询

表之间的关系

- ​	一对多
- ​	多对多
- ​	一对一
- ​	多对多

步骤:

1. 建立两张表:用户表和账号表

   让用户和账号之间具备一对多的关系:需要使用外键在账户表中添加

2. 建立两个实体类:用户实体类和账户实体类

   让用户和账户的实体类能体现出一对多的关系

3. 建立两个配置文件

   用户的配置文件

   账户的配置文件

4. 实现配置

   当我们查询用户时,可以同时得到用户下所包含的账户信息

   当我们查询账户时,可以同时得到账户的所属用户信息

## JNDI

Java Naming and Directory Interface

## 延迟加载

​	在真正使用数据时才发起查询,不用的时候不查询,懒加载

## 立刻加载

不管用不用,调用方法,开始查询

## 缓存

​	存在于内存中的临时数据

​	减少和数据库的交互次数,提高执行效率

一级缓存

​	它指的是Mybatis中SQLsession对象的缓存.当我们执行查询之后,查询的结果会同时存在sqlsession的内存中

**一级缓存的分析**

一级缓存是SQLsession范围的缓存,当调用sqlsession的修改,添加,删除,commit(),cloce()等方法的时候就会清空一级缓存

二级缓存

在主配置文件中开启缓存

```xml
<settings>
    <setting name="logImpl" value="LOG4J"/>
    <setting name="cacheEnabled" value="true"/>//开启缓存
</settings>
```

在mapper.xml文件中加`<cache/>`

属性

```
<cache eviction="FIFO" 引擎
flushInterval="60000" 60秒刷新一次
size="512" 最大为512
readOnly="true"
/>
```

配置查询

```xml
<select id="getOneTwo" parameterType="map" resultType="books" useCache="true"//开启缓存 true 开启 false 关闭></select>
```

## 自定义缓存ehcache

导包

```xml
<!-- https://mvnrepository.com/artifact/org.mybatis.caches/mybatis-ehcache -->
<dependency>
    <groupId>org.mybatis.caches</groupId>
    <artifactId>mybatis-ehcache</artifactId>
    <version>1.2.1</version>
</dependency>

```

mapper接口

```xml
<cache eviction="FIFO" flushInterval="60000" size="512" readOnly="true" type="org.mybatis.caches.ehcache.EhcacheCache"/>
```

