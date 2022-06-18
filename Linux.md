# Linux

## 命令:

进入root目录

```
pwd
```

切换目录名录

```
cd
```

列出文件列表

```
ls
```

列出隐藏目录

```
ls -a
```

列出目录的详细信息

```
ls -l  可以简写为  ll
```

切换目录

```
cd  
```

退回上一级目录

```
cd ..
```

放回上一次访问的目录

```
cd -
```

创建目录

```
 mkdir 目录名称
```

删除目录

```
rmdir 目录名称
```

创建多级目录

```
mkdir mkdir -p 目录名称
```

查看文件内容

```
cat 文件名字
```

查看文件内容显示一个屏幕

```
more 文件 按q退出 按回车显示下一一行 按空格显示下一屏幕
```

```
less 和more一样 多一个上下键查看
```

动态查看

```
tail 文件  最后10行  tail -f 动态查看
```

复制文件

```
cp 文件名字 文件夹
```

剪切文件 

```
mv 文件 目录
```

删除文件

```
rm 文件
```

删除文件夹

```
rm -r 文件夹
```

不提示删除

```
rm -rf 文件夹 文件
```

打包解压
-c:创建一个新的tar文件

-v:显示运行过程的信息

-f:指定文件名

-z:调用gzip压缩命令进行压缩

-t:查看压缩文件的内容

-x:解开tar文件

查找

```
find /-name 文件名称 
```

查找文件中的内容

```
grep 内容 -color 高亮显示
```

创建一个空文件

```
touch 文件
```

清屏

```
clear
```

重定向输出

```
cat 文件 > 文件名 读取并且写入到新的文件
```

```
cat 文件 >> 文件 读取并且追加到文件中
```

查看进程

```
ps -ef
```

查找某一个进程

```
ps -ef | grep ssh 
```

杀死111进程

```
kill 111 
```

强制杀死进程

```
kill -9 111
```

管道命令

```
|
```

-表示文件

d表示文件夹

l表示链接

r读

w写

x执行

查看主机名

```
hostname
```
