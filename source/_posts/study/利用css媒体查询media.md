---
title: 利用css媒体查询media
tags:
  - html
  - css
categories:
  - study
---



为了实现手机与电脑网页宽度自适应，在css3中新增了 media query属性用于增强media type属性。因此当css3问世后，使media type可以进行条件判断输出对应的css。

核心代码：

```css
 <style>
 .wap{display: none;}
 @media screen and (max-width:768px){
    .wrap{display: none;}
    .wap{display: block;}
 }
 </style>
```

wap是手机端的的css最外的盒子；wrap是pc端对外的盒子；@media screen and (max-width:768px)的意思是当屏幕的分辨率低于768px的时候css生效，这个媒体外部的全部css不生效；

因此，当设备分辨率为手机，媒体里面的手机端的css自动生效，当分辨率大于768px时，css就自动渲染外部的css。

**@media具体语法：**

```css
@media screen and (min-width: 769px) {
    /* CSS样式定义部分 */
}
@media screen and (min-device-width: 481px) and (max-device-width: 768px) {
    /* CSS样式定义部分 */
}
@media only screen and (max-device-width: 480px) {
    /* CSS样式定义部分 */
}
```

**一、判断不同的显示设备，跳转到不同的网页。**

```css
<link rel="alternate" media="only screen and (max-width: 640px)" href="https://x.iqimeng.com/">
```



**二、判断媒体类型，引用不同的样式表**

```css
<link rel=”stylesheet” media=”screen and (判断条件)” herf=”需要调用的样式表文件” />
```

通过设定屏幕的判断条件，调用对应的css文件。该实例多用于整页面不同风格的css调用与选取，使用该方法可能需要为一个页面制作多份个css文件。

**三、判断媒体横向与纵向，引用不同的样式**

```css
@media screen and (orientation:portrait){横向样式}
@media screen and (orientation:landscape){纵向样式}
```

**四、判断媒体类型，执行不同的css样式属性**

```css
@media screen and (max-width:240px){
.box{width:200px;}
.title{color:red;}
}
```

Bootstrap响应式设计中几个临界点的分辨率，运用这几个分辨率，我们就可以轻松的用CSS3来写自己的自适应代码了

```css
@media (min-width: 768px){ //>=768的设备 }
@media (min-width: 992px){ //>=992的设备 }
@media (min-width: 1200px){//>=1200的设备}
```

注意下顺序，如果你把@media (min-width: 768px)写在了下面那么就会出错，因为如果是1440,由于1440>768那么你的1200就会失效。

所以我们用min-width时，小的放上面大的在下面，同理如果是用max-width那么就是大的在上面，小的在下面

```css
@media (max-width: 1199px){//<=1199的设备}
@media (max-width: 991px){ //<=991的设备 }
@media (max-width: 767px){ //<=768的设备 }
```



重要的内容重复3次：顺序是min-width从小到大，max-width从大到小。

