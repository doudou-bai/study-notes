### Git

### 主流的版本控制器有那那些

- Git
- SVN
- CVS
- VSS
- TFS

### 版本控制分类

- 本地版本控制
- 集中版本控制
- 分布式版本控制

> 初始化仓库

```
git init
```

> 查看仓库状态

```
git status
```

> 从工作区上传到暂存区

```
git add .
```

> 提交

```
git commit -m "相当于注释"
```

> 关联远程仓库

```
git remote add origin https://github.com/doudou-bai/cloud-config.git
				在本地的名字		地址

```

> 查看远程仓库

```
git remote -v
```

> 把本地仓库的内容提交到远程

```
git push origin master
			名字
```

> 从远程拉取

```
git pull origin master
```

> 查看分支

```
git branch
```

> 创建分支

```
git branch dev 名字
```

> 切换分支

```
git checkout 分支名字
```

> 日志

```
git log --oneline
```

> 详细日志

```
git log
```

> 合并分支

```
git merge dev
```

