# ElasticSearch

https://www.bilibili.com/video/BV17a4y1x7zq?p=11   30:00

## 核心概念

- 索引 index
- 类型 type
- 字段 Field
- 映射 maapping
- 文档 document 
- 接近实时 NRT
- 集群 cluster
- 节点 node
- 分片和复制 shards&replicas

## 安装

解压

```
elasticsearch-7.6.2
```

熟悉目录

```
bin 启动目录
config 配置文件
	log4j2.properties 配置文件
	jvm Java参数
	elasticsearch 配置文件  默认9200端口
lin 相关jar包
modules 模块
plugins 插件
log 日志
```

启动后访问地址http://localhost:9200/

**安装可视化界面**

https://github.com/mobz/elasticsearch-head/

- `git clone git://github.com/mobz/elasticsearch-head.git`
- `cd elasticsearch-head`
- `cnpm install`
- `npm run start`

- `open` http://localhost:9100/

**elasticsearch**

**配置文件**

```
http.cors.enabled: true
http.cors.allow-origin: "*"
```

解压kibana-7.6.2-windows-x86_64

修改配置文件

```
i18n.locale: "zh-CN"
```

## IK分词器插件

下载https://github.com/medcl/elasticsearch-analysis-ik

在es插件文件夹中新建文件夹es 解压文件

可以创建一个任意名字的文件后缀文`.dic`添加自己的词语然后在IKAnalyzer.cfg.xml中进行配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE properties SYSTEM "http://java.sun.com/dtd/properties.dtd">
<properties>
	<comment>IK Analyzer 扩展配置</comment>
	<!--用户可以在这里配置自己的扩展字典 -->
	<entry key="ext_dict">my.dic</entry>
	 <!--用户可以在这里配置自己的扩展停止词字典-->
	<entry key="ext_stopwords"></entry>
	<!--用户可以在这里配置远程扩展字典 -->
	<!-- <entry key="remote_ext_dict">words_location</entry> -->
	<!--用户可以在这里配置远程扩展停止词字典-->
	<!-- <entry key="remote_ext_stopwords">words_location</entry> -->
</properties>

```

## Rest风格

| 请求   | 地址                                            |                      |
| ------ | ----------------------------------------------- | -------------------- |
| PUT    | localhost:9200/索引地址/类型名称/文档id         | 创建文档(指定文档id) |
| POST   | localhost:9200/索引地址/类型名称                | 创建文档(随机文档id) |
| POST   | localhost:9200/索引地址/类型名称/文档id/_update | 修改文档             |
| DELETE | localhost:9200/索引地址/类型名称/文档id         | 删除文档             |
| GET    | localhost:9200/索引地址/类型名称/文档id         | 查询通过文档id       |
| POST   | localhost:9200/索引地址/类型名称/_search        | 查询所有数据         |

| 数据类型   |                                                         |
| ---------- | ------------------------------------------------------- |
| 字符串类型 | text keyword                                            |
| 数值类型   | long integet short byte double float half ,scaled float |
| 日期类型   | date                                                    |
| 布尔值类型 | boolean                                                 |
| 二进制类型 | binary                                                  |

## 关于索引的基本操作

> 基础测试 创建一个索引

```
PUT /test1/type1/1
{
  "name":"王嘉浩",
  "age":3
}
```

> 指定字段的类型

```
PUT /test2
{
  "mappings": {
    "properties": {
      "name":{
        "type": "text"
      },
      "age":{
        "type": "text"
      }
    }
  }
}
```

> 获得这个规则

```
GET test2
```

> 查看默认信息

```
如果自己的文档没有指定类型那么es会给我们默认配置类型
```

> 扩展命令

```
GET _cat/health
```

```
GET _cat/indices?v
```

> 修改索引 直接使用put进行覆盖就可以

```java
PUT /test1/type1/1
{
  "name":"王嘉浩",
  "age":4
}

```

```java
POST /test1/type1/1/_update
{
  "doc":{
    "name":"zahnsgan"
  }
}
```

> 删除索引

```
DELETE test1
```

## 关于文档的基本操作

> 基本操作

> 添加数据

```java
#创建数据
PUT /doudou/user/3
{
  "name":"李四",
  "age":58,
  "desc":"没有具体信息",
  "tages":["漂亮","旅游","唱歌"]
}

#获取数据
GET /doudou/user/2
```

> 更新数据

```java
#更新数据
PUT /doudou/user/3
{
  "name":"李四2355",
  "age":58,
  "desc":"没有具体信息",
  "tages":["漂亮","旅游","唱歌"]
}
```

> 推荐使用post

```java
#更新数据
POST /doudou/user/1/_update
{
  "doc":{
    "name":"111111"
  }
  
}
```

> 简单搜索

```
#获取数据
GET /doudou/user/2
```

```
#获取数据
GET /doudou/user/_search?q=name:张三
请求方式 /索引/文档/id/_search?q=字段:值
```

> 复杂操作

> 复杂搜索

```java
#获取数据
GET /doudou/user/_search
{
  "query":{
    "match": {
    "name":"张三"
    }
  }
}
```

> 限制输出字段

```java
#获取数据
GET /doudou/user/_search
{
  "query":{
    "match": {
    "name":"张三"
    }
  },
  #限制输入字段
  "_source": ["name","desc"]
}

```

> 排序

```java
#获取数据
GET /doudou/user/_search
{
  "query":{
    "match": {
    "name":"张三"
    }
  },
    #排序
 "sort": [
   {
       #对什么字段进行排序
     "age": {
         #进行升序或者降序 取值 desc asc
       "order": "desc"
     }
   }
 ]
}
```

> 分页查询

```java
#获取数据
GET /doudou/user/_search
{
  "query":{
    "match": {
    "name":"张三"
    }
  },
 "sort": [
   {
     "age": {
       "order": "asc"
     }
   }
 ],
    #分页查询  从哪里开始
 "from": 0 ,
    #查询几个
 "size": 1
}
```

> 布尔值查询

`mush mysql里面的And  条件 where id = 1 and name = xxx`

```java
#获取数据
GET /doudou/user/_search
{
  "query":{
   "bool": {
     "must": [
       {
         "match": {
           "name": "张"
         }
       },
       {
         "match": {
           "age": "8"
         }
       }
     ]
   }
  }
}
```

`shoule 满足其一`

```java
#获取数据
GET /doudou/user/_search
{
  "query":{
   "bool": {
     "should": [
       {
         "match": {
           "name": "张"
         }
       },
       {
         "match": {
           "age": "8"
         }
       }
     ]
   }
  }
}
```

`not`

```java
#获取数据
GET /doudou/user/_search
{
  "query":{
   "bool": {
     "must_not": [
       {
         "match": {
           "name": "张"
         }
       },
       {
         "match": {
           "age": "8"
         }
       }
     ]
   }
  }
}
```

> 过滤器

```java
#获取数据
GET /doudou/user/_search
{
  "query":{
   "bool": {
     "must": [
       {
         "match": {
           "name": "张"
         }
       }
     ],
       #过滤器
     "filter": [
       {
         "range": {
             #字段
           "age": {
               #大于  gte  大于等于
             "gt": 5,
               #小于  lte  小于等于
             "lt": 20
           }
         }
       }
     ]
   }
  }
}
```

> 匹配多个条件

```java
#获取数据
GET /doudou/user/_search
{
  "query":{
    "match": {
        #字段名称
      "desc": "没有 法"
    }
  }
}
```

> 精准查询

```java
#获取数据
GET /doudou/user/_search
{
  "query":{
    "term": {
      "desc": "没有具体信息"
    }
  }
}
```

> 多个值匹配的精确查询

```java
#获取数据
GET /doudou/user/_search
{
  "query":{
    "bool": {
      "should": [
        {
          "term": {
              "name": "张"
          }
        },
        {
          "term": {
              "age": 8
        }
       }
      ]
    }
  }
}

```

> 高亮查询

```java
#获取数据
GET /doudou/user/_search
{
  "query": {
    "match": {
      "name": "张"
    }
  },
  "highlight": {
    "fields": {
      "name":{}
    }
  }
}

```

> 自定义高亮

```java
#获取数据
GET /doudou/user/_search
{
  "query": {
    "match": {
      "name": "张"
    }
  },
  "highlight": {
    "pre_tags": "<span style='color:red'>", 
    "post_tags": "</sapn>", 
    "fields": {
      "name":{}
    }
  }
}

```

## 集成SpringBoot

> es依赖

```xml
<properties>
        <java.version>1.8</java.version>
        <elasticsearch.version>7.6.1</elasticsearch.version>
    </properties>

    <dependencies>
        <!--解析网页jsoup-->
        <dependency>
            <groupId>org.jsoup</groupId>
            <artifactId>jsoup</artifactId>
            <version>1.11.3</version>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
            <version>1.2.50</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-elasticsearch</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-thymeleaf</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-configuration-processor</artifactId>
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
            <exclusions>
                <exclusion>
                    <groupId>org.junit.vintage</groupId>
                    <artifactId>junit-vintage-engine</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
    </dependencies>
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>
```

> 配置类

```java
package cn.doudou.config;

import org.apache.http.HttpHost;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

/**
 * Create By 王嘉浩
 * Time 2020/7/24 14:58
 */
@Configuration
public class ESClientConfig {
    @Bean
    public RestHighLevelClient restHighLevelClient() {
        return new RestHighLevelClient(
                RestClient.builder(
                        //可以写ip地址
                        new HttpHost("localhost", 9200, "http")
                )
        );
    }

}

```

> 测试 索引

```java
package cn.doudou.test;

import cn.doudou.config.ESClientConfig;
import org.elasticsearch.action.admin.indices.delete.DeleteIndexRequest;
import org.elasticsearch.action.support.master.AcknowledgedResponse;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.client.indices.CreateIndexRequest;
import org.elasticsearch.client.indices.CreateIndexResponse;
import org.elasticsearch.client.indices.GetIndexRequest;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import sun.font.CreatedFontTracker;

import java.io.IOException;

/**
 * Create By 王嘉浩
 * Time 2020/7/24 15:03
 */
@SpringBootTest
public class Test {
    //注入对象
    @Autowired
    private ESClientConfig esClientConfig;

    /**
     * 测试索引的创建
     */
    @org.junit.jupiter.api.Test
    public void testCreateIndex() throws IOException {
        //创建索引请求
        CreateIndexRequest request = new CreateIndexRequest("kaung-index");
        //加载自定义的class 方法
        RestHighLevelClient restHighLevelClient = esClientConfig.restHighLevelClient();
        //执行创建索引请求
        CreateIndexResponse createIndexResponse = restHighLevelClient.indices().create(request, RequestOptions.DEFAULT);

        System.out.println(createIndexResponse);
    }

    /**
     * 测试获取索引
     */
    @org.junit.jupiter.api.Test
    public void getIndex() throws IOException {
        //加载自定义的class 方法
        RestHighLevelClient restHighLevelClient = esClientConfig.restHighLevelClient();
        //创建get请求
        GetIndexRequest request = new GetIndexRequest("kaung-index");
        //发送请求
        boolean exists = restHighLevelClient.indices().exists(request, RequestOptions.DEFAULT);
        //输出
        System.out.println(exists);
    }

    /**
     * 删除索引
     */
    @org.junit.jupiter.api.Test
    public void deleteIndex() throws IOException {
        //加载自定义的class 方法
        RestHighLevelClient restHighLevelClient = esClientConfig.restHighLevelClient();
        //创建delete请求
        DeleteIndexRequest request = new DeleteIndexRequest("kaung-index");
        //发送请求
        AcknowledgedResponse delete = restHighLevelClient.indices().delete(request, RequestOptions.DEFAULT);
        //输出
        System.out.println(delete.isAcknowledged());
    }

}

```

> 测试 文档

```java
package cn.doudou.test;

import cn.doudou.config.ESClientConfig;
import cn.doudou.pojo.User;
import com.alibaba.fastjson.JSON;
import org.elasticsearch.action.admin.indices.delete.DeleteIndexRequest;
import org.elasticsearch.action.bulk.BulkRequest;
import org.elasticsearch.action.bulk.BulkResponse;
import org.elasticsearch.action.delete.DeleteRequest;
import org.elasticsearch.action.delete.DeleteResponse;
import org.elasticsearch.action.get.GetRequest;
import org.elasticsearch.action.get.GetResponse;
import org.elasticsearch.action.index.IndexRequest;
import org.elasticsearch.action.index.IndexResponse;
import org.elasticsearch.action.search.SearchRequest;
import org.elasticsearch.action.search.SearchResponse;
import org.elasticsearch.action.support.master.AcknowledgedResponse;
import org.elasticsearch.action.update.UpdateRequest;
import org.elasticsearch.action.update.UpdateResponse;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.client.indices.CreateIndexRequest;
import org.elasticsearch.client.indices.CreateIndexResponse;
import org.elasticsearch.client.indices.GetIndexRequest;
import org.elasticsearch.common.unit.TimeValue;
import org.elasticsearch.common.xcontent.XContentType;
import org.elasticsearch.index.query.MatchAllQueryBuilder;
import org.elasticsearch.index.query.QueryBuilder;
import org.elasticsearch.index.query.QueryBuilders;
import org.elasticsearch.index.query.TermQueryBuilder;
import org.elasticsearch.search.SearchHit;
import org.elasticsearch.search.builder.SearchSourceBuilder;
import org.elasticsearch.search.fetch.subphase.FetchSourceContext;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import sun.font.CreatedFontTracker;

import java.io.IOException;
import java.util.ArrayList;
import java.util.concurrent.TimeUnit;

/**
 * Create By 王嘉浩
 * Time 2020/7/24 15:03
 */
@SpringBootTest
public class Test {
    //注入对象
    @Autowired
    private ESClientConfig esClientConfig;

    /**
     * 测试添加文档
     */
    @org.junit.jupiter.api.Test
    public void addDocument() throws IOException {
        //创建对象
        User user = new User("王嘉浩", 18);
        //创建请求
        IndexRequest request = new IndexRequest("doudou");
        //规则
        request.id("1");
        request.timeout(TimeValue.timeValueSeconds(1));
        request.timeout("1s");
        //数据放入请求
        request.source(JSON.toJSONString(user), XContentType.JSON);
        //发送请求
        IndexResponse indexResponse = esClientConfig.restHighLevelClient().index(request, RequestOptions.DEFAULT);
        //输出状态
        System.out.println(indexResponse.status());
        System.out.println(indexResponse.toString());
    }

    /**
     * 判断是否存在文档
     */
    @org.junit.jupiter.api.Test
    public void getDocumentBoo() throws IOException {
        GetRequest request = new GetRequest("doudou", "1");
        //不获取返回的_source的上下文
        request.fetchSourceContext(new FetchSourceContext(false));
        request.storedFields("_none_");
        boolean exists = esClientConfig.restHighLevelClient().exists(request, RequestOptions.DEFAULT);
        System.out.println(exists);
    }

    /**
     * 获取文档的信息
     */
    @org.junit.jupiter.api.Test
    public void getDocument() throws IOException {
        //创建get请求
        GetRequest request = new GetRequest("doudou", "1");
        //发送请求
        GetResponse exists = esClientConfig.restHighLevelClient().get(request, RequestOptions.DEFAULT);
        //获取内容,自动转换为map集合
        System.out.println(exists.getSourceAsString());
        //获取全部的内容
        System.out.println(exists);
    }

    /**
     * 更新文档
     */
    @org.junit.jupiter.api.Test
    public void update() throws IOException {
        //创建get请求
        UpdateRequest request = new UpdateRequest("doudou", "1");
        //设置超时时间
        request.timeout("1s");
        //创建对象
        User user = new User("逗逗测试Java", 45);
        //对象转换为json
        request.doc(JSON.toJSONString(user), XContentType.JSON);
        //发送请求
        UpdateResponse update = esClientConfig.restHighLevelClient().update(request, RequestOptions.DEFAULT);
        //输入
        System.out.println(update);
    }

    /**
     * 删除文档记录
     */
    @org.junit.jupiter.api.Test
    public void delete() throws IOException {
        //创建get请求
        DeleteRequest request = new DeleteRequest("doudou", "1");
        //设置超时时间
        request.timeout("1s");
        //发送请求
        DeleteResponse update = esClientConfig.restHighLevelClient().delete(request, RequestOptions.DEFAULT);
        //输入
        System.out.println(update.status());
    }

    /**
     * 批量插入数据
     */
    @org.junit.jupiter.api.Test
    public void testBulkRequest() throws IOException {
        //创建一个批量插入的请求
        BulkRequest bulkRequest = new BulkRequest();
        //设置超时是阿金
        bulkRequest.timeout("10s");
        //创建list集合
        ArrayList<User> userList = new ArrayList<>();
        //添加集合
        userList.add(new User("张三", 1));
        userList.add(new User("李四", 2));
        userList.add(new User("王五", 3));
        userList.add(new User("李丹", 4));
        userList.add(new User("王狗蛋", 5));
        userList.add(new User("李鸡蛋", 6));
        userList.add(new User("彭万里", 7));
        userList.add(new User("孙韬", 8));
        userList.add(new User("孙棣", 9));
        userList.add(new User("孙炜程", 10));
        userList.add(new User("王海", 11));
        //对list集合进行遍历
        for (int i = 0; i < userList.size(); i++) {
            //把list的内容遍历后加入请求中
            bulkRequest.add(new IndexRequest("doudou")
                    //设置id
                    .id("" + (i + 1))
                    //设置数据和格式
                    .source(JSON.toJSONString(userList.get(i)), XContentType.JSON)
            );
        }
        //发送请求
        BulkResponse bulk = esClientConfig.restHighLevelClient().bulk(bulkRequest, RequestOptions.DEFAULT);
        //输出状态
        System.out.println(bulk.hasFailures());
    }

    /**
     * 查询
     */
    @org.junit.jupiter.api.Test
    public void testSearch() throws IOException {
        //创建请求
        SearchRequest searchRequest = new SearchRequest("doudou");
        //构建搜索的条件
        SearchSourceBuilder sourceBuilder = new SearchSourceBuilder();
        //构建查询器
        TermQueryBuilder termQueryBuilder = QueryBuilders.termQuery("name", "张三");
        //MatchAllQueryBuilder ma = QueryBuilders.matchAllQuery("name","王");
        sourceBuilder.query(termQueryBuilder);
        //sourceBuilder.from();
        //sourceBuilder.size();
        //设置超时时间
        sourceBuilder.timeout(new TimeValue(20, TimeUnit.SECONDS));
        //发送请求
        SearchResponse search = esClientConfig.restHighLevelClient().search(searchRequest, RequestOptions.DEFAULT);
        //json>=对象 输出
        System.out.println(JSON.toJSONString(search));
        System.out.println("===================");
        //遍历输出
        for (SearchHit hit : search.getHits().getHits()) {
            System.out.println(hit.getSourceAsMap());
        }
    }
}

```

## 实战

> pom

```xml
    <groupId>org.example</groupId>
    <artifactId>es-jd</artifactId>
    <version>1.0-SNAPSHOT</version>


    <properties>
        <java.version>1.8</java.version>
        <elasticsearch.version>7.6.1</elasticsearch.version>
    </properties>

    <dependencies>
        <!--解析网页jsoup-->
        <dependency>
            <groupId>org.jsoup</groupId>
            <artifactId>jsoup</artifactId>
            <version>1.11.3</version>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
            <version>1.2.50</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-elasticsearch</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-thymeleaf</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-configuration-processor</artifactId>
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
            <exclusions>
                <exclusion>
                    <groupId>org.junit.vintage</groupId>
                    <artifactId>junit-vintage-engine</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
    </dependencies>
```

> Application

```properties
server.port=8080
# 关闭 thymeleaf的缓存
spring.thymeleaf.cache=false

```

> controller

```java
package cn.doudou.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

/**
 * Create By 王嘉浩
 * Time 2020/7/24 18:01
 */
@Controller
public class IndexController {
    @GetMapping("/")
    public String index() {
        return "index";
    }
}

```



## 爬虫

## 前后端分离

## 搜索高亮