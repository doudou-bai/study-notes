# MongoDB

## 为什么使用No SQL

1. 对数据高并发读写
2. 对海量数据的高效率存储和访问
3. 对数据库的高可扩展性和高可用性

## 弱点

1. 数据事务一致性
2. 数据库的写实时性和读实时性需求
3. 对复杂的SQL查询,特别是多表关联查询的需求

## SpringBoot 整合 MongoDB

```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-mongodb</artifactId>
        </dependency>
```

配置文件

```properties
spring.data.mongodb.uri=mongodb://127.0.0.1:27017/test

```

测试类

```jAVA
package com.atguigu.mongodb;

import com.atguigu.mongodb.entity.User;
import com.mongodb.client.result.DeleteResult;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.data.mongodb.core.MongoTemplate;
import org.springframework.data.mongodb.core.query.Criteria;
import org.springframework.data.mongodb.core.query.Query;

import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.regex.Pattern;

@SpringBootTest
class MongodbApplicationTests {
    @Autowired
    private MongoTemplate mongoTemplate;

    //添加
    @Test
    void contextLoads() {
        User user = new User();
        user.setAge(1);
        user.setName("test");
        user.setEmail("88@88.com");
        User insert = mongoTemplate.insert(user);
        System.out.println(insert);
    }

    //查询所有
    @Test
    public void findAll() {
        List<User> all = mongoTemplate.findAll(User.class);
        System.out.println(all);
    }

    //根据Id查询
    @Test
    void findById() {
        System.out.println(mongoTemplate.findById("60bf71aa716d5a5569c24f01", User.class));
    }

    //条件查询
    @Test
    void findUserList() {
        //name = admin and age = 20
        Query query = new Query(Criteria.where("name").is("admin").and("age").is(0));
        System.out.println(mongoTemplate.find(query, User.class));
    }

    //模糊查询
    @Test
    void findLikeUserList() {
        //name = admin and age = 20
        String name = "min";
        String regex = String.format("%s%s%s", "^.*", name, ".*$");
        Pattern pattern = Pattern.compile(regex, Pattern.CASE_INSENSITIVE);
        Query query = new Query(Criteria.where("name").regex(pattern));
        System.out.println(mongoTemplate.find(query, User.class));
    }

    //分页查询
    @Test
    public void findUsersPage() {
        String name = "est";
        int pageNo = 1;
        int pageSize = 10;

        Query query = new Query();
        String regex = String.format("%s%s%s", "^.*", name, ".*$");
        Pattern pattern = Pattern.compile(regex, Pattern.CASE_INSENSITIVE);
        query.addCriteria(Criteria.where("name").regex(pattern));
        int totalCount = (int) mongoTemplate.count(query, User.class);
        List<User> userList = mongoTemplate.find(query.skip((pageNo - 1) * pageSize).limit(pageSize), User.class);

        Map<String, Object> pageMap = new HashMap<>();
        pageMap.put("list", userList);
        pageMap.put("totalCount", totalCount);
        System.out.println(pageMap);
    }

    //修改
    @Test
    public void updateUser() {
        User user = mongoTemplate.findById("60bf71cc971c361cc626b846", User.class);
        user.setName("张三_1");
        user.setAge(25);
        user.setEmail("883220990@qq.com");
        User save = mongoTemplate.save(user);
        System.out.println(save);
    }

    //删除
    @Test
    public void delete() {
        Query query = new Query(Criteria.where("_id").is("60bf71cc971c361cc626b846"));
        DeleteResult remove = mongoTemplate.remove(query, User.class);
        long deletedCount = remove.getDeletedCount();
        System.out.println(deletedCount);
    }

}

```

增加UserRepository进行测试

```JAVA
package com.atguigu.mongodb.repository;

import com.atguigu.mongodb.entity.User;
import org.springframework.data.mongodb.repository.MongoRepository;

/**
 * Create By 王嘉浩
 * Time 2021/6/10 20:41
 */
public interface UserRepository extends MongoRepository<User,String> {
}

```

测试类

```java
package com.atguigu.mongodb;


import com.atguigu.mongodb.entity.User;
import com.atguigu.mongodb.repository.UserRepository;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.data.domain.Example;
import org.springframework.data.domain.ExampleMatcher;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.PageRequest;

import java.util.List;

/**
 * Create By 王嘉浩
 * Time 2021/6/10 20:43
 */
@SpringBootTest
public class Test1 {
    @Autowired
    private UserRepository userRepository;

    //查询全部
    @Test
    public void t1() {
        List<User> all = userRepository.findAll();
        System.out.println(all);
    }

    //根据ID进行查询
    @Test
    public void t2() {
        System.out.println(userRepository.findById("60bf71aa716d5a5569c24f01").get());
    }

    //添加操作
    @Test
    public void t3() {
        User user = new User();
        user.setAge(30);
        user.setName("wnag");
        user.setEmail("88999@.com");
        User save = userRepository.save(user);
        System.out.println(save);
    }

    //添加查询
    @Test
    public void t4() {
        User user = new User();
        user.setName("wnag");
        Example example = Example.of(user);
        List all = userRepository.findAll(example);
        System.out.println(all);
    }

    //模糊查询
    @Test
    public void t5() {
        //设置模糊查询
        ExampleMatcher matcher = ExampleMatcher.matching().withStringMatcher(ExampleMatcher.StringMatcher.CONTAINING).withIgnoreCase(true);

        User user = new User();
        user.setName("w");
        Example example = Example.of(user,matcher);
        List all = userRepository.findAll(example);
        System.out.println(all);
    }
    //分页查询
    @Test
    public void t6() {
        //设置分页
        PageRequest page = PageRequest.of(0, 1);
        User user = new User();
        user.setName("w");
        Example example = Example.of(user);
        Page<User> all = userRepository.findAll(example, page);
        System.out.println(all);
    }

    //修改
    @Test
    void t7(){
        User user = userRepository.findById("60c20a3eb1762b0cde7c2234").get();
        user.setAge(1100);
        user.setName("doudou");
        User save = userRepository.save(user);
        System.out.println(save);

    }

    //删除
    @Test
    void t8(){
        userRepository.deleteById("60c20a3eb1762b0cde7c2234");
    }
}

```

