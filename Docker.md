# Docker

https://www.bilibili.com/video/BV1og4y1q7M4?p=20



## 容器化技术

**容器化技术不是模拟的一个完整的操作系统**

## 安装

卸载旧的版本

```
yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

基本环境

```
 yum install -y yum-utils
```

设置镜像的仓库

```
 yum-config-manager \
 --add-repo \
 http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

更新索引

```
yum makecache fast
```

安装docker引擎

```
 yum install docker-ce docker-ce-cli containerd.io
```

启动docker

```
systemctl start docker
```

是否安装成功

```
docker version
```

测试HelloWorld

```
 docker run hello-world
```

如果运行helloworld报错设置

```
vi daemon.json



# 增加内容
{
  "registry-mirrors": ["https://registry.docker-cn.com"，“http://hub-mirror.c.163.com"]
}
#重启docker服务
service docker restart
#再次进行运行
docker run hello-world
#######################################方法2
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://bbsvsfl5.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

卸载docker

```
 yum remove docker-ce docker-ce-cli containerd.io
 rm -rf /var/lib/docker
```

命令:

查看docker信息

```
docker info
```

启动docker：

```
systemctl start docker
```

停止docker：

```
systemctl stop docker
```

重启docker：

```
systemctl restart docker
```

查看docker状态：

```
systemctl status docker
```

开机启动：

```
systemctl enable docker
```

查看docker概要信息

```
docker info
```

查看docker帮助文档

```
docker --help
```

## 设置ustc的镜像

编辑该文件：

```
vi /etc/docker/daemon.json  
```

在该文件中输入如下内容：

```json
{
  "registry-mirrors":
        ["http://f1361db2.m.daocloud.io",
        "http://hub-mirror.c.163.com",
        "https://registry.docker-cn.com"]
}

```

## 镜像

查看镜像

```
docker images
```

REPOSITORY：镜像名称

TAG：镜像标签

IMAGE ID：镜像ID

CREATED：镜像的创建日期（不是获取该镜像的日期）

SIZE：镜像大小

这些镜像都是存储在Docker宿主机的/var/lib/docker目录下

搜索镜像

```
docker search 镜像名称
```

拉取镜像

```
docker pull 镜像名称
```

删除镜像

```
docker rmi -f 镜像ID
```

删除所有镜像

```&quot;
docker rmi `docker images -q`
```

## 容器命令

查看正在运行的容器

```
docker ps
```

查看所里有容器

```
docker ps -a
```

查看最后一次运行的容器

```
docker ps -1
```

查看停止的容器

```
docker ps -f status=exited /bin/bash
```

创建容器

```
docker run

	-i表示运行容器
	-t表示容器启动后进入命令行
	--name指定名字
	-v表示目录映射关系
	-d创建一个守护容器在后台运行
	-p表示端口映射
```

退出容器

```
exit
```

守护创建

```
 docker run -di --name=名字 镜像
```

登录

```
docker exec -it 名字 /bin/bash
```

停止容器

```
docker stop 容器名称(或者容器ID)
```

启动容器

```
docker start 容器名称(或者容器ID)
```

文件拷贝

```
docker cp 文件的目录或者文件 容器名称:容器目录
```

从容器中拷贝出来文件

```
docker cp 容器名称:容器目录 需要拷贝的文件或目录
```

目录挂载

```
docker run -di --name=名字 -v /usr/local/myhtml:/usr/local/myhtml 镜像
```

​	异常解决

```
-privileged=true 
```

查看容器ip地址

```
docker inspect 容器名称
```

只查看ip

```
docker inspect --format='{{.NetworkSettings.IPAddress}}' 容器名称
```

删除容器

```
docker rm 容器名称
```

## MySQL部署

拉取mysql 镜像

```
docker pull centos/mysql-57-centos7
```

创建容器

```
docker run -d  -p 3310:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 --name mysql01 mysql:5.7


-d 后台运行
-v 目录挂载
-e 环境配置
-p 端口映射
--name 起个名字
```

## Tomcat部署

拉取镜像

```
docker pull tomcat
```

创建容器

```
docker run -di --name=local_tomcat -p 9000:8080 -v /usr/local/webapps://usr/local/webapps tomcat
```

进入容器

```
docker exec -it tomcat01 /bin/bash
```



## Nginx部署

搜索镜像

```
docker search nginx
```

拉取镜像

```
docker pull nginx
```

启动nginx

```
docker run -d --name nginx01 -p 3344:80 nginx

-d表示后台运行
--name表示起个名字
-p端口映射
```

进入容器

```
docker exec -it nginx01 /bin/bash
```

查看目录

```
whereis nginx
```



## 迁移与备份

容器保存为镜像

```
docker commit 打包的名字 现在的名字
```

镜像备份

```
doxker save -o 镜像名称 名字
```

恢复与迁移

```
docker load -i 打包的镜像名字
```

## Portainer可视化

```
docker run -d -p 8088:9000 \
--restart=always \
-v /var/run/docker.sock:/var/run/docker.sock \
--name prtainer-test \
docker.io/portainer/portainer
```

## Commit镜像

```
docker commit -m="描述" -a="作者" 容器id 目标镜像名
```

## 容器数据卷

**数据如果在容器中,那么一删除数据就会消失 需求:数据可以持久化**

```shell
docker run -it -v 主机目录:容器目录 -p 主机端口:容器端口 tomcat /bin/bash
```

## 具名和匿名挂载

```
匿名挂载
-v 容器内路径!
docker run -d -p --name nginx01 -v /etc/nginx nginx
具名挂载
docker run -d -p --name nginx01 -v nginx:/etc/nginx nginx
```

## Dockerfile 

```shell

FROM centos

VOLUME ["volume01","volume02"]

CMD echo "-----end-----"
CMD /bin/bash




#############################
docker build -f /home/docker-test-volume/dockerfile  -t doudou/centos:1.0 .
```

