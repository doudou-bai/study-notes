# AWT课程

## AWT简介

```
AWT(Abstract Window Toolkit)，中文译为抽象窗口工具包，该包提供了一套与本地图形界面进行交互的接口，是Java提供的用来建立和设置Java的图形用户界面的基本工具。AWT中的图形函数与操作系统所提供的图形函数之间有着一一对应的关系，称之为peers，当利用AWT编写图形用户界面时，实际上是在利用本地操作系统所提供的图形库。由于不同操作系统的图形库所提供的样式和功能是不一样的，在一个平台上存在的功能在另一个平台上则可能不存在。为了实现Java语言所宣称的“一次编写，到处运行(write once, run anywhere)”的概念，AWT不得不通过牺牲功能来实现平台无关性，也即AWT所提供的图形功能是各种操作系统所提供的图形功能的交集。
```

## Container容器

### 常见API

- setLocation(int x,int y) 设置组件的位置
- setSize(int width,int heigth) 设置组件的大小
- setBounds(int x,int y,int width,int heigth) 同时设置组件的位置大小
- setVisible(Boolean b) 设置该组件的可见性



