---
title: X3 photo gallery 授权破解
categories:
  - study
tag:
  - 采坑
---
## X3 photo gallery 另类破解

这个软件用了很久，之前也用过破解版，但升级后接失效了，今天闲来无事，试着破解，搜索关键字，查看源码，自以为很简单，直接注销代码，看了下，底部链接是消失了，但是后来，点击上面的目录时才发现，会跳出授权经过....

后来又试了另外的方法，终于成功了。就是把授权的文字直接把字体颜色改成背景色。具体方法如下：

1.zai 源文件 templates 下76文件夹（因为通过搜索发现授权这行代码的class"x3-footer-link"在这个文件）

![image-20201129184535600](https://raw.githubusercontent.com/markruan/cloudimg/master/img/image-20201129184535600.png)

2.随便找一行代码，我是在131行 加入如下代码：

```js
echo "<style>.footer .x3-footer-link,.footer .x3-footer-link a {color:#e2d6d2;pointer-events: none;} </style>";
```

 完成。

方法很笨，但效果达到 

 



