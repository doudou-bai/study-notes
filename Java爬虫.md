## 爬虫

**入门案例**

```java
package cn.doudou.test;

import org.apache.http.HttpEntity;
import org.apache.http.client.methods.CloseableHttpResponse;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.util.EntityUtils;

import java.io.IOException;

public class demo1 {
    public static void main(String[] args) throws IOException {
        //打开浏览器
        CloseableHttpClient aDefault = HttpClients.createDefault();
        //输入网址
        HttpGet httpGet = new HttpGet("https://www.iqiyi.com/");
        //回车 发起请求
            CloseableHttpResponse execute = aDefault.execute(httpGet);

        //解析数据
        if(execute.getStatusLine().getStatusCode() == 200)
        {
            HttpEntity entity = execute.getEntity();
            String s = EntityUtils.toString(entity, "UTF-8");
            System.out.println(s);
        }
    }
}

```

### HttpCilent

#### Get

**HttpGet请求把HttpCilent替换就可以**
**带参数Get**

```java
package cn.doudou.test;

import org.apache.http.client.methods.CloseableHttpResponse;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.client.utils.URIBuilder;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.util.EntityUtils;

import java.io.IOException;
import java.net.URISyntaxException;

public class demo03 {
    public static void main(String[] args) throws URISyntaxException {
        CloseableHttpClient httpClient = HttpClients.createDefault();
        URIBuilder uriBuilder = new URIBuilder("https://www.dashengpan.com/search");
        uriBuilder.setParameter("keyword","慕课");
        HttpGet httpGet = new HttpGet(uriBuilder.build());
        CloseableHttpResponse re = null;
        try {
            re = httpClient.execute(httpGet);
            if (re.getStatusLine().getStatusCode() == 200) {
                String s = EntityUtils.toString(re.getEntity(), "UTf-8");
                System.out.println(s);
                System.out.println(s.length());
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                re.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
            try {
                httpClient.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}

```

#### HttpPost

**替换HttpaClient**

Post带参数

```java
package cn.doudou.test;

import org.apache.http.NameValuePair;
import org.apache.http.client.entity.UrlEncodedFormEntity;
import org.apache.http.client.methods.CloseableHttpResponse;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.message.BasicNameValuePair;
import org.apache.http.util.EntityUtils;

import java.io.IOException;
import java.util.ArrayList;
import java.util.List;

public class demo05 {
    public static void main(String[] args) throws IOException {
        CloseableHttpClient httpClient = HttpClients.createDefault();
        HttpPost httpPost = new HttpPost("https://www.dashengpan.com/");
        List<NameValuePair> parms = new ArrayList<NameValuePair>();
        parms.add(new BasicNameValuePair("keyword", "Java"));
        UrlEncodedFormEntity formEntity = new UrlEncodedFormEntity(parms, "utf8");
        httpPost.setEntity(formEntity);
        CloseableHttpResponse execute = httpClient.execute(httpPost);
        if (execute.getStatusLine().getStatusCode() == 200) {
            String s = EntityUtils.toString(execute.getEntity(), "UTF8");
            System.out.println(s);
        }
    }
}

```

#### 连接池

**不带参数**

```java
package cn.doudou.test;

import org.apache.http.HttpEntity;
import org.apache.http.client.methods.CloseableHttpResponse;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.impl.conn.PoolingHttpClientConnectionManager;
import org.apache.http.util.EntityUtils;

import java.io.IOException;

public class demo06 {
    public static void main(String[] args) {
        //创建连接池管理器
        PoolingHttpClientConnectionManager cm = new PoolingHttpClientConnectionManager();
        //设置最大连接数
        cm.setMaxTotal(100);
        //设置主机的最大连接数
        cm.setDefaultMaxPerRoute(10);
        //使用连接管理器发起请求
        doGet(cm);
        doGet(cm);
        doGet(cm);
    }

    private static void doGet(PoolingHttpClientConnectionManager cm) {
        //从连接池获取
        CloseableHttpClient httpCilent = HttpClients.custom().setConnectionManager(cm).build();
        HttpGet httpGet = new HttpGet("https://www.dashengpan.com/");
        CloseableHttpResponse execute = null;
        try {
          execute = httpCilent.execute(httpGet);
          if (execute.getStatusLine().getStatusCode() == 200)
          {
              String utf8 = EntityUtils.toString( execute.getEntity(), "utf8");
              System.out.println(utf8.length());
          }
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if (execute != null)
            {
                try {
                    execute.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }


    }
}

```

**设置参数**

```java
package cn.doudou.test;

import org.apache.http.client.config.RequestConfig;
import org.apache.http.client.methods.CloseableHttpResponse;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.client.utils.URIBuilder;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.util.EntityUtils;

import java.io.IOException;
import java.net.URISyntaxException;

public class demo07 {
    public static void main(String[] args) throws URISyntaxException {
        CloseableHttpClient httpClient = HttpClients.createDefault();
        HttpGet httpGet = new HttpGet("https://www.dashengpan.com/search");

        //配置请求信息                                     创建连接的最长时间          设置连接的最长时间               设置数据传输的最长时间
        RequestConfig config = RequestConfig.custom().setConnectTimeout(1000).setConnectionRequestTimeout(500).setSocketTimeout(10 * 1000).build();
        httpGet.setConfig(config);

        CloseableHttpResponse re = null;
        try {
            re = httpClient.execute(httpGet);
            if (re.getStatusLine().getStatusCode() == 200) {
                String s = EntityUtils.toString(re.getEntity(), "UTf-8");
                System.out.println(s);
                System.out.println(s.length());
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                re.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
            try {
                httpClient.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}

```

#### jsoup

```java
package jsoup;


import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.select.Elements;
import org.junit.Test;

import java.net.URL;

public class demo1 {
    @Test
    public void run1() throws Exception {
        //解析url
        Document doc = Jsoup.parse(new URL("https://www.dashengpan.com/search?keyword=lll"), 10000);
        //使用标签选择器
        Elements elementsByClass = doc.getElementsByClass("resource-item-wrap valid");
        Elements a = elementsByClass.select("a");
        String href = a.attr("href");
        System.out.println(href);
    }
}

```

### WebMagic

方法

```
.regex() 选择内容爬取
```

```
.get()   获取一条数据
```

```
.toString()	获取一条数据
```

```
.all()	获取全部数据
```

```
page.addTargetRequests(page.getHtml().css("ul.JS_navCtn li a").links().all());	获取连接
```

```
.thread(5) 设置多线程
```

```
.addPipeline(new FilePipeline("C:\\jd")) 设置输出文件
```

```

    private Site site = Site.me()
            .setCharset("utf-8")//编码
            .setTimeOut(3000)//设置超时时间
            .setRetrySleepTime(10000)//设置重试时间
            .setSleepTime(3);//设置重试次数
```

