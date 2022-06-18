# Maven

### 仓库

- 本地仓库
- 远程仓库
- 中央仓库

**标椎目录结构**

- 核心代码部分
- 配置文件部分
- 测试代码部分
- 测试配置文件

**maven项目标椎目录结构**

- src/main/java目录 核心代码部分
- src/main/resources 配置文件部分
- src/test/java目录 测试代码目录
- src/test/resources 测试配置文件
- src/main/webapp 页面资源 js css 图片

### 命令

- mvn clean 删除target目录
- mvn compile 编译项目
- mvn test 测试编译
- mvn packagr 打包
- mvn install 安装
- mvn deploy  发布

### 仓库的种类

- 本地仓库
- 私服
- 中央仓库

仓库之间的关系:当我们启动maven项目的时候,maven会通过文件中的坐标去找对应的jar包