# SpringDataJPA

### orm的思想

- 主要目的:操作实体类就相当于操作数据库表
- 建立两个映射关系:
  - 实体类和表的映射关系
  - 实体类中属性和表中字段的映射关系
- 不在重点关注:sql语句

**实现了ORm实现的框架:Mybatis hibernate**

### hidernate框架介绍

是一个开放源代码的对象关系映射框架

​	他对JDBC进行了非常轻量级的对象封装

​	他将POJO于数据库表建立映射关系,是一个全自动的orm框架

### JPA规范

​	jpa规范,实现jpa规范,实现jpa规范.内部接口有抽象类组成 

### JPA搭建

- 加载配置文件创建实体类管理器工厂
- 根据实体类管理器工厂,创建实体管理器
- 创建事务对象,开启事务
- 增删改查的操作
- 提交事务
- 释放资源

- 在resources创建文件夹

  - 新建META-INF

    - persisistence.xml

    - 约束

      ```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <persistence xmlns="http://java.sun.com/xml/ns/persistence" version="2.0">
      ```

      配置

      ```xml
          <persistence-unit name="myJpa" transaction-type="RESOURCE_LOCAL">
              <!--jpa的实现方式-->
              <provider>org.hibernate.jpa.HibernatePersistenceProvider</provider>
              <!--数据库信息-->
              <properties>
                  <property name="javax.persistence.jdbc.user" value="root"/>
                  <property name="javax.persistence.jdbc.password" value="0009"/>
                  <property name="javax.persistence.jdbc.driver" value="com.mysql.jdbc.Driver"/>
                  <property name="javax.persistence.jdbc.url" value="jdbc:mysql://localhost:3306/acc"/>
                  <!--可选配置 配置jpa实现方的实现信息-->
                  <!--显示sql-->
                  <property name="hibernate.show_sql" value="true"/>
                  <!--自动创建数据库表
                  create  程序运行时创建表
                  update  程序运行时创建表
                  none    不会创建表
                  -->
                  <property name="hibernate.hbm2ddl.auto" value="update"/>
              </properties>
      
          </persistence-unit>
      ```

    - 配置文件属性

      ```xml
      persistence-unit
      	属性:
      
      name:自定义 和方法名字差不多
      		transaction-type:事务管理方式
      			JTA: 分布式事务管理
                  RESOURCE_LOCAL  本地事务管理
      
      jpa的实现方式
      
      <provider>org.hibernate.jpa.HibernatePersistenceProvider</provider>
      
      配置数据库信息
        <properties>
                  <property name="javax.persistence.jdbc.user" value="root"/>
                  <property name="javax.persistence.jdbc.password" value="0009"/>
                  <property name="javax.persistence.jdbc.driver" value="com.mysql.jdbc.Driver"/>
                  <property name="javax.persistence.jdbc.url" value="jdbc:mysql://localhost:3306/acc"/>
                  <!--可选配置 配置jpa实现方的实现信息-->
                  <!--显示sql-->
                  <property name="hibernate.show_sql" value="true"/>
                  <!--自动创建数据库表
                  create  程序运行时创建表
                  update  程序运行时创建表
                  none    不会创建表
                  -->
                  <property name="hibernate.hbm2ddl.auto" value="update"/>
              </properties>
      
      显现打印sql语句
      
      <property name="hibernate.show_sql" value="true"/>
      属性是 false true
      
      自动创建数据库表
      
        <property name="hibernate.hbm2ddl.auto" value="update"/>
      属性value 
      	create:运行时创建数据库表<如果有表删除在创建>
          update:运行时创建数据库表<如有有表不在创建>
          none:什么都不干
      ```

### 测试

```java
 @Test
    public void run1() {
        EntityManagerFactory factory = Persistence.createEntityManagerFactory("myJpa");
        EntityManager entityManager = factory.createEntityManager();
        EntityTransaction transaction = entityManager.getTransaction();
        transaction.begin()
        entityManager.persist(c);
        transaction.commit();
        entityManager.close();
        factory.close();
    }
```



### 注解

- 声明此类事务类

  ```
  @Entity
  ```

- 配置实体类和表的关系 name代表数据库表名

  ```
  @Table(name = "数据库表")
  ```

  ```
  @MappedSuperclass
  ```

- 对应数据库主键的配置

  ```
  @Id
  ```

- 添加事务的支持

  ```
  @Transactional
  ```

- 把默认的回滚改为false

  ```
  @Rollback
  ```

- 加载另外一个表的class文件

  ```
   @OneToMany(targetEntity = LinkMan.class) 一对多得到注解
   	属性:
   		mappedBy:对象
   		cascade：配置级联
   			CascadeType.ALL：所有
   						MERGE:更新
   						PERSIST:保存
   						REMOVE:删除
  ```

- 一对多 多的注解

  ```
  @ManyToOne
  ```

  

- 放弃外键维护

  ```
  /*@JoinColumn(name = "lkm_cust_id",referencedColumnName = "cust_id")//放弃外进维护权*/进行注释就可以
  ```

- 外键

  ```
  @JoinColumn(name = "lkm_cust_id",referencedColumnName = "cust_id")//放弃外进维护权
  ```

  

- 更新操作

  ```
  @Query
  @Modifying
  测试类必须要加事务的支持
  必须把Rollback改为false
  ```

- sql语句的查询

  ```
  @Query(value"",nativeQuery = "取值")
  	ps nativeQuery 取值是 true 使用的是sql查询 false 为 jpql语句查询
  ```

  

- 配置主键的生成策略  自增

  ```
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  
  GeneratedValue属性
  	strategy
  		GenerationType.IDENTITY:自增 Mysql
  			底层数据库必须支持自动增长(底层数据库支持的自动增长方式,对id自增)
  		GenerationType.SEQUENCE序列 oracle
  			底层数据库必须支持序列
  		GenerationType.TABLE jpa提供的机制
          GenerationType.AUTO 由程序自己控制
  		
  ```

- 数据库表中的字段名称

  ```
  @Column(name = "数据库表中字段映射的名字")
  ```

- Entitymanager对象:实体类管理器

  - beginTransaction:创建事务对象
  - presist:保存操作
  - merge:更新
  - remove:删除
  - find/getRefrence:根据id进行查询

- Transaction对象:事务

  - begin:开启事务
  - commit:提交事务
  - rollback:回滚 

- 排序

  ```
  @OrderBy
  ```

  



### Jpql查询

Sql:查询的是表和表中的字段

jpql:查询的是实体类的属性

- 查询所有

  ```jpql
  from 实体类名
  ```

- 分页查询

  ```
  from 实体类名
   query.setFirstResult(0);//起始索引
   query.setMaxResults(20);//每次查询的条数
  ```

- 统计查询

  ```
  select count(字段名字) from 实体类名
  ```

- 条件查询

  ```
  from 实体类名字 where 字段名 like ?
  query.setParameter(1,"豆%");//进行赋值
  ```

- 排序查询

  ```
  from 实体类名 order by 实体类的排序id  desc
  ```


### JPA环境搭建

- 在resources文件夹创建applicltionContext.xml文件

  头部文件

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:aop="http://www.springframework.org/schema/aop"
         xmlns:context="http://www.springframework.org/schema/context"
         xmlns:jdbc="http://www.springframework.org/schema/jdbc" xmlns:tx="http://www.springframework.org/schema/tx"
         xmlns:jpa="http://www.springframework.org/schema/data/jpa"
         xmlns:task="http://www.springframework.org/schema/task"
         xsi:schemaLocation="
  		http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
  		http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd
  		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
  		http://www.springframework.org/schema/jdbc http://www.springframework.org/schema/jdbc/spring-jdbc.xsd
  		http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd
  		http://www.springframework.org/schema/data/jpa
  		http://www.springframework.org/schema/data/jpa/spring-jpa.xsd">
  
  ```

  **spring 和 Spring Data  JPA的配置**

  ```xml
  <!--spring和spring data jpa的配置-->
  
      <!---->
      <bean id="entityManagerFactory" class="org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean">
          <property name="dataSource" ref="dataSource"/>
          <!--配置扫描的包 实体类所在的包-->
          <property name="packagesToScan" value="cn.doudou.domain"/>
          <!--jpa的实现厂家 实现方式-->
          <property name="persistenceProvider">
              <bean class="org.hibernate.jpa.HibernatePersistenceProvider"/>
          </property>
          <!--jpa的供应商设配器-->
          <property name="jpaVendorAdapter">
              <bean class="org.springframework.orm.jpa.vendor.HibernateJpaVendorAdapter">
                  <!--配置是否自动创建数据库表-->
                  <property name="generateDdl" value="false"/>
                  <!--数据库类型-->
                  <property name="database" value="MYSQL"/>
                  <!--数据库方言-->
                  <property name="databasePlatform" value="org.hibernate.dialect.MySQLDialect"/>
                  <!--显示sql语句-->
                  <property name="showSql" value="true"/>
              </bean>
          </property>
          <!--jpa的方言 高级特性-->
          <property name="jpaDialect">
              <bean class="org.springframework.orm.jpa.vendor.HibernateJpaDialect"/>
          </property>
      </bean>
  
      <!--创建数据库连接池-->
  
      <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
          <property name="driverClass" value="com.mysql.jdbc.Driver"/>
          <property name="jdbcUrl" value="jdbc:mysql://localhost:3306/acc"/>
          <property name="user" value="root"/>
          <property name="password" value="0009"/>
      </bean>
  
      <!--整合Spring data jpa-->
      <jpa:repositories base-package="cn.doudou.dao" transaction-manager-ref="transactionManager"
                        entity-manager-factory-ref="entityManagerFactory"/>
      <!--配置事务管理器-->
      <bean id="transactionManager" class="org.springframework.orm.jpa.JpaTransactionManager">
          <property name="entityManagerFactory" ref="entityManagerFactory"/>
      </bean>
      <!--声明式事务-->
      <tx:advice id="txAdvice" transaction-manager="transactionManager">
          <tx:attributes>
              <tx:method name="save*" propagation="REQUIRED"/>
              <tx:method name="insert*" propagation="REQUIRED"/>
              <tx:method name="update*" propagation="REQUIRED"/>
              <tx:method name="delete*" propagation="REQUIRED"/>
              <tx:method name="get*" read-only="true"/>
              <tx:method name="find*" read-only="true"/>
              <tx:method name="*" propagation="REQUIRED"/>
          </tx:attributes>
      </tx:advice>
  
      <!-- 5.aop-->
      <aop:config>
          <aop:pointcut id="pointcut" expression="execution(* cn.doudou.service.*.*(..))" />
          <aop:advisor advice-ref="txAdvice" pointcut-ref="pointcut" />
      </aop:config>
  
      <!--配置包扫描-->
      <context:component-scan base-package="cn.doudou"/>
  ```

- 在dao中创建接口

  ```
  在dao接口中继承JpaRepository<Customer, Long>, JpaSpecificationExecutor<Customer>
  	ps:
    		JpaRepository
    		第一个类型 操作实体类的类型
   		第二个类型 实体类主键的类型
    		JpaSpecificationExecutor
    		操作实体类的类型
  ```

- 测试类的方法介绍

  - 根据id进行查询

    ```
    findOne()
    ```

  - 添加

    ```
    save()
    ```

  - 更新

    ```
    save()
    必须要有id属性
    ```

  - 删除

    ```
    delete()
    必须要有id属性
    ```

  - 查询所有

    ```
    findAll()
    ```

  - 查询多少条

    ```
    count()
    ```

  - 判断id为?数据是否存在

    ```
    exists()
    ```

  - 根据id进行查询

    ```
    getOne()
    ```

### 方法名称规则查询

**方法名字的约定**

- findBy*:查询

  对象中的属性名<首字母大写>查询的条件

- findBy+属性名称+"查询方式"<like | isnull>

-  多条件的查询 

  findBy+属性名字+"查询方式"+"多条件的连接符<and | or>"+其他属性名字+其他属性的查询方式

### Specifications动态查询

- 方法列表

  - 查询单个对象

    ```
    T findOne(Specification<T> spec);
    ```

  - 查询列表

    ```
    List<T> findAll(Specification<T> spec);
    ```

  - 查询列表,分页 pageable参数

    ```
    Page<T> findAll(Specification<T> spec,pageable pageable);
    ```

  - 查询列表 Sort:排序列表

    ```
    List<T> findAll(Specification<T> spec, Sort sort);
    ```

  - 统计查询

    ```
    long count(Specification<T> spec);
    ```

- **Specification:查询条件**

  自定义我们自己的Specification实现?类

  实现方法

  ```
   Predicte toPredicte(Root <T> root, CriteriaQuery<?> query,CriteriaBuilder cd);
   ps:
   参数介绍
  	root:查询的根对象(查询的任何属性都可以从根对象中获取)
  	CriteriaQuery:顶层查询对象,自定义查询方式(了解:一般不使用)
  	CriteriaBuilder :查询的构造器,封装了很多的查询条件
  ```

- 根据名字进行查询

  ```java
   @Test
      public void run1() {
          Specification<Customer> sc = new Specification<Customer>() {
              public Predicate toPredicate(Root<Customer> root, CriteriaQuery<?> criteriaQuery, CriteriaBuilder criteriaBuilder) {
                  Path<Object> custName = root.get("custName");
                  Predicate equal = criteriaBuilder.equal(custName, "111");
                  return equal;
              }
          };
          Customer one = dao.findOne(sc);
          System.out.println(one);
  
      }
  ```

- 根据名字和地址进行模糊查询

  ```java
    @Test
      public void run2() {
          Specification<Customer> sc = new Specification<Customer>() {
              public Predicate toPredicate(Root<Customer> root, CriteriaQuery<?> criteriaQuery, CriteriaBuilder criteriaBuilder) {
                  Path<Object> custName = root.get("custName");
                  Path<Object> custAddress = root.get("custAddress");
                  Predicate e1 = criteriaBuilder.equal(custName, "111");
                  Predicate e2 = criteriaBuilder.equal(custAddress, "嵩");
                  Predicate and = criteriaBuilder.and(e1, e2);
                  return and;
              }
          };
          Customer one = dao.findOne(sc);
          System.out.println(one);
  
      }
  ```

- 根据地址进行模糊查询并且倒叙

  ```java
  @Test
      public void run3() {
          Specification<Customer> sc = new Specification<Customer>() {
              public Predicate toPredicate(Root<Customer> root, CriteriaQuery<?> criteriaQuery, CriteriaBuilder criteriaBuilder) {
                  Path<Object> custAddress = root.get("custAddress");
                  Predicate like = criteriaBuilder.like(custAddress.as(String.class), "%县%");
                  return like;
              }
          };/*
          List<Customer> one = dao.findAll(sc);
          for (Customer customer : one) {
              System.out.println(customer);
          }*/
          //排序
          Sort sort = new Sort(Sort.Direction.DESC, "custId");//DESC就是倒叙  ASC就是正序
          List<Customer> all = dao.findAll(sc, sort);
          for (Customer customer : all) {
              System.out.println(customer);
          }
      }
  ```

- 分页查询

  ```java
    //分页查询
      @Test
      public void run4() {
          Specification spec = null;
          PageRequest pageRequest = new PageRequest(0,3);
          Page all = dao.findAll(spec, pageRequest);
          System.out.println(all.getTotalElements());
          System.out.println(all.getContent());
          System.out.println(all.getTotalPages());
      }
  ```




### 多表查询

- 一对一

- 一对多:外键 

- 多对多

  **分析步骤**

- 明确表与表的关系

- 明确表关系(描述 外键|中间表)

- 编写实体列,在实体类中描述表关系(包含关系)

- 配置映射关系 

**一对多案例**

**对象导航查询**

```
getLikMans
```

从一方查询多方

​	默认:使用延迟加载

从多方加载一方

​	默认:使用立即加载