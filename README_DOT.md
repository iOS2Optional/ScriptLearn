# DOT 语言绘图学习

DOT 是程序员应该了解的一种代码绘图语言。

## 一、整体格式
```
digraph G {
      // 核心代码
}
```

如：
```
digraph G {
  A -> B1 -> C1;
  A -> B2 -> C2;
}
```

其效果是：  
![Study.dot.png](https://upload-images.jianshu.io/upload_images/1198135-c8014385a55509fc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 二、定义样式
### 2.1 标签样式
```
digraph G {
  # 定义样式
  A  [shape=box,label = "文本-A"];

  A -> B1 -> C1;
  A -> B2 -> C2;
}
```

效果如下：  
![study.dot.png](https://upload-images.jianshu.io/upload_images/1198135-1df43363b72fc22c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

A 标签由之前的的椭圆变成矩形，同时显示文本更改。


### 2.2  箭头样式

```
digraph G {
  # 定义样式
  A  [shape=box,label = "文本-A"];
  # 箭头样式
  A -> B1 -> C1 [label=指令, color=red];
  A -> B2 -> C2;
}
```

效果如下：  
![study.dot.png](https://upload-images.jianshu.io/upload_images/1198135-fe0b7575e24a4c3a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


箭头变成红色，添加文本 **指令**。


如果需要那种么有箭头的样式，那么是将 **->** 换成 **--**, 其次还需要将关键字 **digraph** 换成 **graph**，代码如下：
```
graph G {
  # 定义样式
  A  [shape=box,label = "文本-A"];
  # 箭头样式
  A -- B1 -- C1 [label=指令, color=red];
  A -- B2 -- C2;
}
```

效果如下：  
![Study.dot.png](https://upload-images.jianshu.io/upload_images/1198135-f854a81203bd4736.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

没有小箭头、就是一条线。

### 2.3 板块设计
代码如下：
```
digraph G {
  # 定义样式
  A  [shape=box,label = "文本-A"];
  # 箭头样式
  A -> B1 -> C1 [label=指令, color=red];
  A -> B2 -> C2;

  subgraph cluster_B3  {
  	node [style=filled];
  	B3 [shape=box, label="板块设计"]
  	B3 -> C31 [label = 第一条子线];
  	B3 -> C32 [label = 第二条子线, color = green];

  	label = "B3板块";
  	color=red;
  }

  A ->  B3;
  # A ->  cluster_B3; 无效
}
```

效果如下：  
![Study.dot.png](https://upload-images.jianshu.io/upload_images/1198135-369e279775b90d24.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这是一个怪异的语法，**subgraph** 的名称一定要以 **cluster** 开头。


### 2.4 Tab设计
```
digraph G {
  # 定义样式
  A  [shape=box,label = "文本-A"];
  # 箭头样式
  A -> B1 -> C1 [label=指令, color=red];
  A -> B2 -> C2;

  subgraph cluster_B3 {
  	node [style=filled];
  	B3 [shape=box, label="板块设计"]
  	B3 -> C31 [label = 第一条子线];
  	B3 -> C32 [label = 第二条子线, color = green];

  	label = "B3板块";
  	color=red;
  }

  A ->  B3;


  subgraph cluster_B4 {
  	B4 [shape=record, label="tab1|tab2|tab3|tab4"];
  	B41 [shape=record, label="Home|Center"];
  	b42 [shape=record, label="我是\nCoderHG|{A1|{A21|A22}|{A31|A32|A33}|A4|{A51|A52|A53|A54|A55}}|帅|美"]

  	B4 -> B41;
  	B4 -> b42

  	label="Tab结构表";
  	color = blue;
  }

  A -> B4
}
```

效果如下：  
![Study.dot.png](https://upload-images.jianshu.io/upload_images/1198135-4947e8642ea14f9d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 2.5 其它常用的属性
```
digraph G {
	fontColor [fontcolor=red, label="字体颜色"]

	fontSize  [fontsize=30, label="字体大小"]

	fillColor [style=filled, fillcolor=green, label="填充色"]

	fontColor -> fontSize;
	fontSize  ->  fillColor;
}
```

效果如下：  
![other.dot.png](https://upload-images.jianshu.io/upload_images/1198135-07a0dd6eaa8cb59f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)






###### 以上应该就是比较常用的功能了

###### 参考：
[使用 dot 来绘图](http://www.360doc.com/content/16/0717/23/12572656_576393368.shtml)
