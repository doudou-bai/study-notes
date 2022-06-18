## Mongodb入门<非关系型数据库>

注册服务

**管理员打开cmd**

```
./mongod.exe --config "D:\MongoDB\mongo.conf" --install
```

启动服务

```
net start MongoDB
```

停止服务

```
net stop MongoDB
```

移除服务

```
"D:\MongoDB\bin\mongod.exe" --remove
```

### 基础概念

| SQL术语/概念 | MongoDB术语/概念 | 解释/说明                                 |
| ------------ | ---------------- | ----------------------------------------- |
| database     | database         | 数据库                                    |
| tabel        | collection       | 数据库表/集合                             |
| row          | document         | 数据记录行/文档                           |
| column       | field            | 数据字段/域                               |
| index        | index            | 索引                                      |
| table joins  |                  | 未连接/<MongoDB不支持>                    |
| primary key  | primary key      | 注解,MongoDB自动在每个集合中添加_id的主键 |

### 数据库操作

查询数据库

```
show dbs;
```

创建数据库 

```
use DATABASE_NAME
```

删除数据库

```
db.dropDatabase()
```

### 集合

创建集合

```
db.createCollection(name,options)
name:创建集合的名字
optioes:参数
```

删除集合

```
db.集合名称.drop()
```

### 文档

插入

```
db.COLLECTION_NAME.insert({document})
```

更新文档

```
db.集合名字.update({
	<query>,
	<update>,
	<options>
})
query:查询条件
update:更新内容
options:选项
```

$.set修改器

```
db.集合名字.update({条件},{$set:{修改的内容}},{multi:true})
multi false更新第一个匹配的文档
true 更新所有匹配的文档
```

删除文档

```
db.集合名字.remove({query})
query:删除条件
删除所有文档:db.集合.remove({})
删除符合条件的集合:db.集合.remove({"集合名字":值})
```

查询文档

```
db.结合名字.find(query,projection)
query:条件
projection:投影查询
查询全部:db.集合.find()
查询符合条件:db.集合.find({"集合名字":值})
投影查询:db.集合.find({"集合名字":值},{name:1,age:1,_id:0})只显示name和age id不显示
```

### 用户管理

```
db.createUser(
	{user:"name",
	 pwd:"password",
	 customData:{自定义数据},
	 roles:[
	 		{role:"",db:"}
	 ]
	
	}
)
```

| 数据库用户角色 | 数据库管理角色 | 集群管理角色   | 备份恢复角色 | 所有数据库角色       |
| -------------- | -------------- | -------------- | ------------ | -------------------- |
| read           | dbAdmin        | clusterAdmin   | backup       | readAnydatabase      |
| readWrite      | dbOwner        | clusterManager | restore      | readWriteAnyDatabase |
|                | userAdmin      | clusterMonitor |              | userAdminAnyDatabase |
|                |                | hostManager    |              | dbAdminAnyDatabase   |

示例:

```
db.createUser(
	{user:"root",
	pwd:"123456",
	roles:[{role:"root",db:"admin"}]
	}) 
```

认证登录:

- 在mono.conf中设置auth=true
- 重启
- 使用账号密码连接数据库

查询用户

```
show users
```

删除用户

```
db.dropUser("用户名")
```

修改用户

```
db.updateUser("用户名",{roles:[{"权限",db:"用户名"}]})
```

修改密码

```
db.changeUserPassword("username","passwprd")
```

