---
title: Css 打字机效果，文字循环 逐个出现，逐个删除
tag: 
  - css
  - 特效
  - html
categories:
  - study
---
看见一个不错的特效：

**效果如下：**
![在这里插入图片描述](https://raw.githubusercontent.com/markruan/cloudimg/master/img/20200521164422488.gif)
html 文本

```html
<h1 id="box"></h1>
```

css 样式

```css
// keyframes 可根据展示的文本长度，自行添加，我的格式为： @keyframes  ‘type’+'文本长度'
@keyframes typing10 {
  from {
    width: 0;
  }
  50% {
    width: 10ch;
  }
  100% {
    width: 0
  }
}
@keyframes typing4 {
  from {
    width: 0;
  }
  50% {
    width: 4ch;
  }
  100% {
    width: 0
  }
}
@keyframes typing6 {
  from {
    width: 0;
  }
  50% {
    width: 6ch;
  }
  100% {
    width: 0
  }
}
@keyframes caret { 50% { border-color: transparent; } }
h1 {
  width: 0;
  animation: typing 6s steps(15) infinite,caret 1s steps(1) infinite;
  white-space: nowrap;
  overflow:hidden;
  border-right: .05em solid;
  font-family: Consolas, Monaco, monospace;//注意这儿，要设置字体为等宽字体,ch才会充分发挥效果
}
 
```

js文件

```javascript
const arr = ['TypeScript','JavaScript','小程序','less','sass' ];//显示的文本
const dom = document.getElementById('box')
let j = 0; //从数组第一个开始展示
// 递归函数
const func =(j) => {
  if(j < arr.length){ // 当达到数组长度时，就从头开始继续
    const item = arr[j]
    const itemLen = item === '小程序' ? 6 : item.length; // 汉字是占两个ch
    dom.innerHTML = item; // 显示文字
    for (var i = 0, len = itemLen; i < len; i++) { // 添加文本效果
      var textLen = dom.textContent.length, s = dom.style;
      s.animationTimingFunction = "steps(" + textLen + "),steps(1)";; //动态设置steps
      s.animationName = `typing${itemLen}`; //文本长度不同，展示的宽度就不同，所以需要动态设置
      s.animationDuration = `${itemLen/2}s,0.5s`; //这儿设置速度
    }
    setTimeout(() => {
      func(j + 1)
    },itemLen*500) //这儿和上面的animationDuration速度一致，只不过这儿是毫秒，所以要乘以1000
    
  }else{
    func(0); //就从头开始继续
  }
}
func(j); 
```

参考文章： https://www.w3cplus.com/css3/css-secrets/typing-animation.html