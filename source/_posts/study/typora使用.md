---
title: typora使用
categories:
  - study
---
## Typora介绍

Typora是一款免费的轻量级Markdown编辑器，它没有[Mou](https://link.zhihu.com/?target=http%3A//25.io/mou/)，[Haroopad](https://link.zhihu.com/?target=http%3A//pad.haroopress.com/)等Markdown编辑器那么大名鼎鼎，但算是较为小众的一款产品。

Typora作为一款离线Markdown无疑是非常棒的， 如果作为笔记工具的话，推荐你使用 cmd Markdown，因人而异。



下载地址：**[Typora](https://link.zhihu.com/?target=https%3A//typora.io/)**

@[TOC](https://link.zhihu.com/?target=https%3A//my.openwrite.cn/user/article/%E7%9B%AE%E5%BD%95%EF%BC%88Contens%EF%BC%89)

## 标题

\#一阶标题 （快捷键Ctrl+1）

\##二阶标题 （快捷键Ctrl+2）

\###三阶标题 （快捷键Ctrl+3）

\####四阶标题 （快捷键Ctrl+4）

\#####五阶标题 （快捷键Ctrl+5）

\######六阶标题 （快捷键Ctrl+6）

## 如何生成目录

```text
@[TOC]目录

在文章开始地方输入[toc]，即可在对应位置插入目录
@[TOC]目录

以下不用写，直接写@[TOC](目录)即可自动获到目录中
#一阶标题 （快捷键Ctrl+1）
##二阶标题 （快捷键Ctrl+2）
###三阶标题 （快捷键Ctrl+3）
####四阶标题 （快捷键Ctrl+4）
#####五阶标题 （快捷键Ctrl+5）
######六阶标题 （快捷键Ctrl+6）
注：凡是文章标题带有#（1-n个）的都会被捕获到目录中。
```

## 文本居中

这是要居中的文本内容\

**注**：Typora目前并不会直接预览居中效果——相应的效果只有输出文本的时候才会显现。

## 下划线

下划线使用格式 下划线的内容<\u> 或者快捷键Ctrl+U

下划线在Typora显示形式是 这就是我亲测的下划线

## 删除线

删除线使用格式：~~ 删除线的内容

## 字体加粗

前面某个字段使用两个*，\*加粗字体* 或者快捷键Ctrl+B

## 字体倾斜

使用一个”星“，*字体倾斜了* 或者快捷键Ctrl+I

## 图片的插入

直接拖你想要图片进来即可

## 超链接

- 使用快捷键Ctrl+K
- 使用2个反斜杠""，
  [百度][[https://www.baidu.com/](https://link.zhihu.com/?target=https%3A//www.baidu.com/)]

[百度一下](https://link.zhihu.com/?target=https%3A//www.baidu.com/)

**注**：按住Ctrl键+点击上面链接就可以直接访问该链接

## 代码区域

三个反引号个（```）+编程语言即可

```text
//设置线程名字
thread.setName("线程1"); 
thread1.setName("线程2");
```

## 表格的使用

第一种：快捷键**Ctrl+T**

第二种：|ID|name|age|回车即可

学号姓名年龄20200506MarkerHunJava35

## 任务列表

\- [ ] 文字 （**注**：注意用空格隔开）

- [x] Java
- [x] 大数据
- [ ] 人工智能
- [ ] 机器学习

## 有序无序列表

**创建无序列** :+ 、- 、* （后面加空格）

**多行无序列表**:

- Java

- - 容器

  - - HashMap

**有序列表**:(1.)空格

1. Java
2. Biodata

**多行有序列表：**

```text
1. Java
2. Biodata
    1. Java
    2. Biodata
```

## 水平分割线

```text
***或者- - -
```

## 引用的使用格式

```text
>+空格
```

## 表情

```text
:单词
```

## 数学表达式

Typora支持加入用LaTeX写成的数学公式，并且在软件界面下用MathJax直接渲染，数学公式分为两种参考**[Mathpix Snip](https://link.zhihu.com/?target=https%3A//mathpix.com/)**

- 行内公式 `$ ... $`
- 行间公式 `$$ ... $$`,（或者$$+回车）
  **注**：行间公式形式是将数学式插在文本行之间（多行公式、公式组和微积分方程等复杂的数学式都是采用行间） **注**：行内公式形式是将数学式插入文本行之内（适合编写简 短的数学式） **如**：将公式插入到本行内，符号：`$公式内容$`，$xyz$或“$$”+回车即可

\#### 1、上标、下标、求和、括号、分式、根号

**语法**：行内公式输入在两个`$$`之间，行外公公式`$$内容公式$$`或`$$`+回车即可输入。

![img](https://raw.githubusercontent.com/markruan/cloudimg/master/img/v2-fc1eb7e3e05ef1b0bbb7a47975db5de2_720w-20201107100422676.jpg)

### 2、基本运算符

![img](https://raw.githubusercontent.com/markruan/cloudimg/master/img/v2-c3703593a2e990069e3834247b437206_720w-20201107100449798.jpg)

### 3、三角函数、指数、对数

![img](https://raw.githubusercontent.com/markruan/cloudimg/master/img/v2-f525471ca6da7be4fe0cfb25717b7411_720w-20201107100303444.jpg)

### 4、高等数学相关运算符

![img](https://raw.githubusercontent.com/markruan/cloudimg/master/img/v2-a3e3be0b70dc25c0d09a22544136174f_720w-20201107100312691.jpg)

### 6、希腊字母

![img](https://raw.githubusercontent.com/markruan/cloudimg/master/img/v2-f8cf4f5d21042f66e5ecc0c4f1c415cb_720w-20201107100321024.jpg)

### 甘特图

~~~text
```mermaid
	gantt
	        dateFormat  YYYY-MM-DD
	        title Adding GANTT diagram functionality to mermaid
	        section 现有任务
	        已完成               :done,    des1, 2019-09-02,220-01-20
	        进行中               :active,  des2, 2020-05-06, 3d
	        计划一               :         des3, after des2, 5d
	        计划二               :         des4, after des3, 5d
　```
~~~

![img](https://raw.githubusercontent.com/markruan/cloudimg/master/img/v2-01b334770f043d6ae251f12e7fc5947b_720w-20201107100331425.jpg)

### Mermaid流程图

~~~text
```mermaid
	graph LR
	graph LR
	A[老鹰] -- 吃 --> B((小鸡))
	A -- 吃 --> C(蛇)
	B -- 吃--> D{虫}
	C --> D
	```
~~~

![img](https://raw.githubusercontent.com/markruan/cloudimg/master/img/v2-10220c614d3474fbea35b656187271e9_720w-20201107100342942.jpg)

[更多参考文档](https://link.zhihu.com/?target=https%3A//mermaid-js.github.io/mermaid/%23/)

### Flowchart流程图

![](https://raw.githubusercontent.com/markruan/cloudimg/master/img/v2-01b334770f043d6ae251f12e7fc5947b_720w-20201107100331425.jpg)