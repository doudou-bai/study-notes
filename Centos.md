## *Centos

### 配置JDK

- 上传jdk安装包  或下载

  ```
  wget https://download.oracle.com/java/18/latest/jdk-18_linux-x64_bin.tar.gz
  ```

- 配置环境变量

  ```
  vi  /etc/profile
  ```

  ```
  #JDK全局环境变量配置
  export JAVA_HOME=/java/jdk-18.0.1
  export CLASSPATH=$:CLASSPATH:$JAVA_HOME/lib/
  export PATH=$PATH:$JAVA_HOME/bin
  ```

- 让环境变量生效

  ```
  source /etc/profile
  ```

- 测试输入java

### 配置tomcat

- 上传tomcat安装包

- 解压

  ```
  tar -zxvf 安装包
  ```

- 修改conf中server.xml中端口

- 开启

- 开放端口

  ```
  firewall-cmd --zone=public --add-port=80/tcp --permanent   # 开放5672端口
  ```

- 配置生效

  ```
  firewall-cmd --reload   # 配置立即生效
  ```

- 访问测试

### 配置nginx

- 下载gcc环境

  ```
  yum install gcc-c++
  ```

- pcre

  ```
  yum install -y pcre pcre-devel
  ```

- zilb

  ```
  yum install -y zlib zlib-devel
  ```

- OpenSSl

  ```
  yum install -y openssl openssl-devel
  ```

- 上传源码

- 解压

  ```
  tar -zxvf
  ```

- 进入nginx-1.8.0目录  使用 configure 命令创建一 makeFile 文件

  ```
  ./configure \
  --prefix=/usr/local/nginx \
  --pid-path=/var/run/nginx/nginx.pid \
  --lock-path=/var/lock/nginx.lock \
  --error-log-path=/var/log/nginx/error.log \
  --http-log-path=/var/log/nginx/access.log \
  --with-http_gzip_static_module \
  --http-client-body-temp-path=/var/temp/nginx/client \
  --http-proxy-temp-path=/var/temp/nginx/proxy \
  --http-fastcgi-temp-path=/var/temp/nginx/fastcgi \
  --http-uwsgi-temp-path=/var/temp/nginx/uwsgi \
  --http-scgi-temp-path=/var/temp/nginx/scgi
  
  ```

- 编译

  ```
  make
  ```

- 安装

  ```
  make install
  ```

- 启动

  ```
  mkdir /var/temp/nginx/client -p
  ```

  ```
  cd /usr/local/nginx/sbin
  ```

  ```
  ./nginx
  ```

- 查看进程

  ```
  ps aux|grep nginx
  ```

- 关闭

  ```
  ./nginx -s stop
  ```

  ```
  ./nginx -s quitll
  ```

- 刷新配置文件

  ```
  ./nginx -s reload
  ```

  

### 配置Mysql

#### 安装

- 下载并安装MySQL官方的 Yum Repository

```
wget -i -c http://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm
```

-  使用上面的命令就直接下载了安装用的Yum Repository，大概25KB的样子，然后就可以直接yum安装了。

```
yum -y install mysql57-community-release-el7-10.noarch.rpm
```

- 安装MySQL服务器。

```
yum -y install mysql-community-server
```

#### MySQL数据库设置

- 首先启动MySQL

```
systemctl start  mysqld.service
```

- 查看MySQL运行状态，运行状态如图：

```
systemctl status mysqld.service
```

- 通过如下命令可以在日志文件中找出密码：

```
grep "password" /var/log/mysqld.log
```

- 进入数据库：

```
mysql -uroot -p
```

- 改密码之后才能操作数据库：

```
ALTER USER 'root'@'localhost' IDENTIFIED BY '18736292279';
```

##### mysql的远程访问

```
 GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '18736292279';
```

```
flush privileges; 
```

```
exit
```

#### 开放端口

```
firewall-cmd --zone=public --add-port=3306/tcp --permanent
```

#### 刷新

```
firewall-cmd --reload
```

### 配置Redis

安装gcc依赖

```
yum install -y gcc 
```

下载并解压安装包

```
wget http://download.redis.io/releases/redis-5.0.3.tar.gz
```

```
tar -zxvf redis-5.0.3.tar.gz
```

```
cd redis
```

编译

```
make
```

安装

```
make install PREFIX=/usr/local/redis
```

启动服务

```
cp /usr/local/redis/redis.conf /usr/local/redis/bin/
```

修改 redis.conf 文件，把 daemonize no 改为 daemonize yes

[root@localhost bin]# vi redis.conf

后台启动

[root@localhost bin]# ./redis-server redis.conf


六、设置开机启动

添加开机启动服务

[root@localhost bin]# vi /etc/systemd/system/redis.service

复制粘贴以下内容：

复制代码
[Unit]
Description=redis-server
After=network.target

[Service]
Type=forking
ExecStart=/usr/local/redis/bin/redis-server /usr/local/redis/bin/redis.conf
PrivateTmp=true

[Install]
WantedBy=multi-user.target

复制代码
注意：ExecStart配置成自己的路径 


设置开机启动

[root@localhost bin]# systemctl daemon-reload

[root@localhost bin]# systemctl start redis.service

[root@localhost bin]# systemctl enable redis.service

创建 redis 命令软链接

[root@localhost ~]# ln -s /usr/local/redis/bin/redis-cli /usr/bin/redis

测试 redis


服务操作命令

systemctl start redis.service   #启动redis服务

systemctl stop redis.service   #停止redis服务

systemctl restart redis.service   #重新启动服务

systemctl status redis.service   #查看服务当前状态

systemctl enable redis.service   #设置开机自启动

systemctl disable redis.service   #停止开机自启动
