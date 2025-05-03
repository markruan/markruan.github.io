---
title: Vue中使用H5的audio
tags: Vue
---

## H5audio标签有许多事件

![20190127152315247](https://cdn.jsdelivr.net/gh/markruan/cloudimg@master/img/20190127152315247.png)

在应用到vue中后的使用如下：

比如在使用onplay时，要去掉on，用@play派发时间，在methods中定义方法执行体

```vue
<template>
    <div>
        <audio src="../../static/1.mp3" @play="ready" @pause="pause" controls></audio>
    </div>
</template>
 
<script>
    export default {
        name: 'musci',
        data() {
            return {
            }
        },
        methods:{
            ready(){
                console.log("play click");
            },
            pause(){
                console.log("pause click");
            }
        }
    }
</script>
```