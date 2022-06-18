Vue3 + TS

## TS

### Type Script的特点

- **始于JavaScript 归于JavaScript**
- **强大的类型系统**
- **先进的JavaScript**

### **安装Type Script**

命令行运行如下命令，全局安装 TypeScript：

```bash
npm install -g typescript
```

安装完成后，在控制台运行如下命令，检查安装是否成功(3.x)：

```命令行运行如下命令，全局安装 TypeScript：
tsc -V 
```

### 第一个Type Script

```typescript
(() => {
    //str这个参数是string类型的
    function sayHi(str:string) {
        return '你好啊' + str
    }
    let text = '小甜甜'
    console.log(sayHi(text))
})()
```

### 手动编译代码 

```
tes ts文件
```

### TS在VsCode自动编译

```
1). 生成配置文件tsconfig.json
    tsc --init
2). 修改tsconfig.json配置
    "outDir": "./js",
    "strict": false,    
3). 启动监视任务: 
    终端 -> 运行任务 -> 监视tsconfig.json
```

### 类型注解

```typescript
//类型注解:是一种轻量级的为函数或者变量添加的约束
(() => {
    //绑定string类型
    function showMsg(str: string) {
        return '床前明月光,' + str
    }
    let msg = '疑是地上霜'
    console.log(showMsg(msg))
})()
```

### 接口

```typescript
//接口:是一种能力,一种约束而已
(() => {
    //定义一个接口
    interface IPerson {
        firstName: string
        lastName: string
    }
    //输入姓名
    function showFullName(person: IPerson) {
        return person.firstName + '_' + person.lastName
    }
    //定义一个对象
    const person = {
        firstName: '东方',
        lastName: '不败'
    }
    console.log(showFullName(person))
})()
```

