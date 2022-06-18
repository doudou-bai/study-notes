# xml

### 概述

  Extensible Markup Language  可扩展标记语言

  可扩展:标签都是自定义的

##### 功能

  存储数据

​		配置文件

​		在网络中传输

##### 与html区别

​	xml的标签都是自定义的,html是预定的

​	xml语法严格,html语法松散

​	xml是存储数据的,html是展示数据的

### 语法

​	基本语法

​		xml文档的后缀名 .xml

​		xml第一行必须定义为文档声明

​		xml文档中有且仅有一个根标签

​		属性值必须使用引号引起来

​		标签必须正确关闭

​		xml标签区分大小写

### 解析

​	文档声明

​		格式:

```xml
<?xml 属性列表 ?>
```

​	属性列表

​	version : 版本号

​	encoding : 编码格式 默认 ISO-8859-1

​	styandalone : 是否独立 yes no

​	指令

​		结合css的	

​	标签

​		规则

​			名称可以包含字母.数字以及其他的字符

​			名称不能以数字或者标点符号开始

​			名称不能以字符xml获取XML Xml等等开始

​			名称不能以空格开始

​	属性

​		id属性值唯一

​	文本

约束:

​	编写xml?-- 用户 软件的使用者

​	解析xml?-- 软件 

分类

1. DTD:一种简单的约束技术
2. Schema:一种复杂的约束技术

DTD引入

​	本地	<!DOCTYPE 根标签名 STSYEM "dtd文件的位置">

​	网络	<!DOCTYPE 根标签名 PUBLIC	"dtd文件的名字 dad文件的URL">

解析:操作xml文档,将文档的数据读取到内存中

​	操作xml文档

​		解析(读取) 将文档的数据读取到内存中

​		写入 将内存中的数据保存到xml文档中.持久化存储

​	解析xml的方式

​		DOM:将标记语言文档一次性加载进内存,在内存中形成一颗dom树

​		优点:操作比较方便,可以对文档进行CRUD的所有操作

​		缺点:消耗内存 

SAX:逐行读取,基于事件驱动

​		优点:不占内存

​		缺点:只能读取,不能修改

xml常见的解析器:

- JAXP:sun公司提供的,支持dom和sax
- DOM4J:
- soup:
- PULL:安卓内置的解析器

对象的使用:

​	**Jsoup工具类,可以解析html或者xml文档,返回Document**

​		Parse解析html获xml文档,返回Document

​		parse(File in,String charsetName)解析xml获html文件的

​		parse(String html):解析xml获取html字符串的

​		parse(URL url,int timeoutMills )通过网络路径获取指定的xml 获html文件

**Document:文档对象**

​	获取Element对象

​		getElementByTag(String Name) 通过标签名称获取元素对象集合

​		getElementByAttribute(String key)根据属性名称获取元素对象集合

​		getElementByAttributeValue(String key,String value)根据对应的属性名和属性值获取元素的对象集合

​		getElementById(String id)根据id属性值获取唯一的id元素属性值   	

**Elements:**元素对象的集合.可以当做Arraylist<Element>来使用

**Element**元素对象

获取子元素标签

方法和上面一样

​	**获取属性值**

​		String arrt(String key) 根据属性名称获取属性值

​	**获取文本内容**

​		String text()获取文本内容

​		String html()获取标签体的所有内容



**Node**:节点对象

​	是Document和Element的父类

快捷查询方式

​	selector:选择器

​	XPath:

`		使用Jsoup的Xpath需要额外导入jar包

