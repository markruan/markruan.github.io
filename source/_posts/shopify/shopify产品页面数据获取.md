---
title: shopify产品页面数据获取
categories:
  - shopify
---
### 获取产品数据



#### 获取标题

```
{{ product.title }}
```

#### 获取最低价和最高价

```
{{ product.price_min | money }} - {{ product.price_max | money }}
```

#### 获取 variant （后面我将叫它为变体），并获取关联数据

这里我先讲一下 我的选购逻辑，因为这里的代码数据应该如何获取与我的选购逻辑有关系。我的选购逻辑与速卖通的有点像，速卖通是有个选项可以绑定图片，这样用户可以更直观的知道他的选择。而为我的逻辑是通过选择图片进行选购，不一样的是我的图片可以通过选择属性进行筛选，而不是不同属性的图片是一样的，下面是速卖通的截图

![速卖通图片选项](https://img-blog.csdnimg.cn/20200330124554589.gif)

####  **获取 variant 和关联数据，图片，标题，ID**

这里我规定 多重属性 的 第一个option 是 image 第二个是 size，因为我的项目选项是固定的，可以这样做，当然你也可以写成灵活的，只是这样你需要做的工作量比较多而已

~~~
{% for variant in product.variants %}
  {% assign id = variant.id %}
  {% assign title = variant.title %}
  {% assign image = variant.image %}
  {% assign size = variant.option2 %}
{% endfor%}
~~~

#### 获取选项数据

这里可以根据我根据我的项目需求进行获取，我的项目需求可以简单的认为只有 图片 和 尺寸
图片上面已经有了，所以这里我只需要得到 size。这里是有条件，要求你在上传产品的时候设置多重属性的时候就要对应名称，我这里是 image 和 color。

```
// 获取 size
{% for value in product.options_by_name['size'].values %}
  <li>{{ value }}</li>
{% endfor %}

```

#### 数据绑定

数据绑定还是比较简单的，讲获取到的数据通过 data- 绑定在dom上就好了，后面我们通过js来读取即可，可根据自己需要进行绑定

对于大部分人来说可能更加喜欢通过 js 渲染数据。这里给大家提供以下如何在js中获取产品数据的代码，如果你需要考虑SEO,那你就的主意一下，因为爬虫是无法读取js渲染的数据

````
// 记得必须是在产品页面下才有效 需要访问得到 {{ product }}
<script>
  // 获取 product 的json数据
  let product = {};
  product.data = {{ product | json }};
</script>
````

