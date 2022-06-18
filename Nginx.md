# Nginx

## 基本概念

> nginx是什么,做什么事情

是一个高性能的HTTP和反向代理服务器,特点是占有内存少,并发能力强,事实上nginx的并发能力确实在同类型的网页服务器中表现较好

nginx转为性能优化而开发,性你那个是其最重要的考量,事实上非常注重效率,能经受高负载的考验,有报告表明能支持高达50000个并发连接数

> 反向代理

- 正向代理
  - 在客户端(浏览器)配置代理服务器,通过代理服务器进行互联网
- 反向代理
  - 不暴露原有的服务器,隐藏了服务器,对外只提供一个服务器

> 负载均衡

请求集中到单个服务器上的情况改为将请求分发到多个服务器上,将负载均衡分发到不同的服务器.页就是我们所说的负载均衡

> 动静分离



## nginx 安装,常用命令和配置文件

> 在liunx系统中安装nginx



> nginx常用命令

- nginx启动默认侦听80端口
- 查看进程端口信息（有没有启动）：
  - netstat -ntpl | grep 端口(web80|redis6379|mysql3306)
  - ps aux |grep nginx
- 停止：nginx -s stop
- 启动：sudo nginx
- 重启：sudo nginx -s reload
- 测试配置文件，看配置文件夹有没有错误：sudo nginx -t
- 使用指定的配置文件启动nginx：sudo nginx -c /etc/nginx/nginx.conf
- 显示版本信息：sudo nginx -v



> nginx配置文件



## nginx配置实例-反向代理

>  在host文件中添加域名地址

> 修改nginx配置文件  单独配置

```js
 # HTTPS server
    #
    server {
           listen       80;
           server_name  127.0.0.1;
           location / {
                proxy_pass http://127.0.0.1:8080;
           }
        }
    }
```

> 多个配置

```js
 # HTTPS server
    #
    server {
           listen       80;
           server_name  127.0.0.1;
               location ~ /edu/ {
                    proxy_pass http://127.0.0.1:8080;
               }
          location ~ /vod/ {
                proxy_pass http://127.0.0.1:8081;
           }
        }
    }
```

## nginx配置实例-负载均衡

- **默认是轮询**

- **weight 权重 默认值是1  server 127.0.0.1:8080 weight=5;**

- **ip_hash  指定某一个ip固定访问一个服务**

- **fair  按照访问的相应的时间分配**

```js
http {
    ip_hash
	upstream myserver {
		server 127.0.0.1:8080;
		server 127.0.0.1:8081;
 }
}
server {
           listen       80;
           server_name  127.0.0.1;
           location / {
                proxy_pass http://myserver;
                index index.html index.htm;
           }
        }
    }
```

## nginx配置实例-动静分离

简单理解就是动态请求一个服务器,静态请求一个服务器

```js
		location /www/ {
                root 动态资源的地址
                index index.html index.htm;
           }
           
          location /image/ {
                root 静态资源的地址
                autoindex on;#列出访问的资源
           }
```

## nginx配置高可用集群

> **什么是高可用?**

**就是Nginx的集群 配置多个Nginx的机器**

> 配置高可用的准备工作

- 需要两台服务器

- 安装Nginx

- 在两台服务器安装Keepalived

- 安装Keepalived后会在etc中自动生成目录Keepalived,文件Keepalived.conf

- ```conf
  #全局定义
  global_defs {
  	notification_email {
  	  acassen@firewall.loc
  	  failover@firewall.loc
  	  sysadmin@firewall.loc
  	}
  	notification_email_from Alexandre.Cassen@firewall.loc
  	smtp_ server 192.168.17.129
  	smtp_connect_timeout 30
  	router_id LVS_DEVEL	# LVS_DEVEL这字段在/etc/hosts文件中看；通过它访问到主机
  }
  
  vrrp_script chk_http_ port {
  	script "/usr/local/src/nginx_check.sh"
  	interval 2   # (检测脚本执行的间隔)2s
  	weight 2  #权重，如果这个脚本检测为真，服务器权重+2
  }
  
  vrrp_instance VI_1 {
  	state BACKUP   # 备份服务器上将MASTER 改为BACKUP
  	interface ens33 //网卡名称
  	virtual_router_id 51 # 主、备机的virtual_router_id必须相同
  	priority 100   #主、备机取不同的优先级，主机值较大，备份机值较小
  	advert_int 1	#每隔1s发送一次心跳
  	authentication {	# 校验方式， 类型是密码，密码1111
          auth type PASS
          auth pass 1111
      }
  	virtual_ipaddress { # 虛拟ip
  		192.168.17.50 // VRRP H虛拟ip地址
  	}
  }
  ```

- 在路径/usr/local/src/ 下新建检测脚本 nginx_check.sh

- ```
  #! /bin/bash
  A=`ps -C nginx -no-header | wc - 1`
  if [ $A -eq 0];then
  	/usr/local/nginx/sbin/nginx
  	sleep 2
  	if [`ps -C nginx --no-header| wc -1` -eq 0 ];then
  		killall keepalived
  	fi
  fi
  ```

- 把两台服务器上nginx和keepalived启动

- ```
  $ systemctl start keepalived.service		#keepalived启动
  $ ps -ef I grep keepalived	
  ```

- ```
  $ systemctl stop keepalived.service  #keepalived停止
  ```

  

## nginx原理

**1、master和worker**

![master和worker](D:\MD文档笔记\img\nginx\master和worker.png)

**2、worker如何进行工作的**

![](D:\MD文档笔记\img\nginx\worker如何进行工作的.png)

**3、一个master和多个woker的好处**
(1) 可以使用nginx -s reload热部署。

```
首先，对于每个worker进程来说，独立的进程，不需要加锁，所以省掉了锁带来的开销，
同时在编程以及问题查找时，也会方便很多。其次,采用独立的进程，可以让互相之间不会
影响，一个进程退出后，其它进程还在工作，服务不会中断，master进程则很快启动新的
worker进程。当然，worker进程的异常退出，肯定是程序有bug了，异常退出，会导致当
前worker.上的所有请求失败，不过不会影响到所有请求，所以降低了风险。
```

**4、设置多少个woker合适**

```
Nginx同redis类似都采用了io多路复用机制，每个worker都是一个独立的进程， 但每个进
程里只有一个主线程，通过异步非阻塞的方式来处理请求，即使是 千上万个请求也不在话
下。每个worker的线程可以把一个cpu的性能发挥到极致。所以worker数和服务器的cpu
数相等是最为适宜的。设少了会浪费cpu,设多了会造成cpu频繁切换上下文带来的损耗。
# 设置worker数量
worker.processes 4 

# work绑定cpu(4work绑定4cpu)
worker_cpu_affinity 0001 0010 0100 1000

# work绑定cpu (4work绑定8cpu中的4个)
worker_cpu_affinity 0000001 00000010 00000100 00001000
```

**5、连接数worker_ connection**

```
这个值是表示每个worker进程所能建立连接的最大值，所以，一个nginx 能建立的最大连接数，应该是worker.connections * worker processes。当然，这里说的是最大连接数，对于HTTP 请求本地资源来说，能够支持的最大并发数量是worker.connections * worker processes,如果是支持http1.1的浏览器每次访问要占两个连接，所以普通的静态访问最大并发数是: worker.connections * worker.processes / 2, 而如果是HTTP作为反向代理来说，最大并发数量应该是worker.connections * worker_proceses/4. 因为作为反向代理服务器，每个并发会建立与客户端的连接和与后端服务的连接，会占用两个连接.
```

> 第一个: 发送请求，占用了woker的几个连接数?
> 答案: 2或者4个。
>
> 第二个: nginx有一个master,有四个woker,每个woker支持最大的连接数1024,支持的最大并发数是多少?
> 答案：普通的静态访问最大并发数是: worker connections * worker processes /2，
> 而如果是HTTP作为反向代理来说，最大并发数量应该是worker connections * worker processes/4