# Spring全家桶

### Spring Framework的历史

- 诞生于2002年,成型与2003年,最早的作者为Rod Johnson
- 用于构建企业级应用的轻量级一站式解决方案

### 设计理念

- 力争让选择无处不在
- 体现海纳百川的精神
- 保持向后的兼容性
- 专注API设计
- 追求严苛的代码质量

### 导包

Boot-监控导包

```xml
  <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
  </dependency>
```

### Sprig Data JPA

常用JPA注解

实体

- @Entity
- @MappedSuperclass
- @Table(name)

注解

- @Id
- @GeneratedValue(strategy,generator)
- @SequenceGenerator(name,sequenceName)

映射

- @Column(name,nullable,length,insertable,updatable)
- @JoinTable(name)
- @JoinColumn(name)

关系

- @ONeToOne
- @OneToMany
- @ManyToOne
- @ManyToMany
- @OrderBy

### Project  Lombok

- @Getter
- @Setter
- @ToString
- @NoArgsConstructor
- @RequiredArgsConstructor
- @AllArgsConstructor
- @Data
- @Builder
- @Slf4j
- @CommonsLog
- @Log4j2

spring 的jdbc操作

spring-jdbc

- core jdbctemplate等相关核心接口和类
- datasource.数据源相关的辅助类
- object,将基本的jdbc操作封装为对象
- support,错误码等其他辅助工具

通过注解定义bean

@component

@repository

@service

@controller

@restcontroller

jdbctemplate操作

query

queryforobject

queryforlist

update

execute

### Spring MVC

DispatcherServlet

- Controller
- xxxResolver
  - ViewResolver
  - HandlerExceptionResolver
  - MultipartResolver
- HandlerMapping

**常用注解**

- @Controller
  - @RestController
- RequestMapping
  - GetMapping / @PostMapping
  - @PutMapping / @DeleteMapping
- @RequestBody / @ResponseBody / @ResponseStatus