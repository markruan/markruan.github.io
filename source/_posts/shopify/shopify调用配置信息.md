---
title: shopify调用配置信息
categories:
  - shopify
---

### 调用配置

```javascript
要调用模板中的配置信息，需要使用 liquid 语言。可以使用{%%}逻辑标签和{{}}显示标签。在这两种标签里，都可以使用settings.id，其中id就是配置中定义的属性。比如配置文件里是这样写的：

[
{
    "name" : "颜色",
    "settings" : [
      {
        "type": "color",
        "id": "color_background",
        "label": "背景颜色",
        "default": "#e5e5e5",
        "info" : "这个将调整背景颜色"
      },
      {
        "type": "color",
        "id": "color_body_text",
        "label": "内容文字颜色",
        "default": "#2980b9",
        "info" : "这个将调整内容文字颜色"
      }
    ]
  }
]
```

你可以这样调用背景颜色：

```jade
{{ settings.color_background }}
```

#### 常规配置类型

常规配置类型包括：text, textarea, image, radio, select, checkbox。每种类型都允许用户选择来修改模板。这些配置用一组liquid标签来调用。 

```
{{}}  //将会把信息显示在页面上
{{ settings.your_id }}

{%%}可以把配置信息用于逻辑处理上。

    {% if settings.product_order == true %}
      <p>可以下单!</p>
    {% else %}
      <p>不能下单 :(</p>
    {% endif %}
```



## 特殊设置类型

特殊设置类型包括：`color`, `font`, `collection`, `product`, `blog`, `page`, `link_list`,  `snippet。要调用他们，比常规配置稍微复杂一些。`

### `Color和Font`

```
color和font和上面的调用方式相同，如果你在页面上直接调用，那么它将在页面上显示16进制，然而对于我们来说并没有什么卵用，我们需要在样式表中调用这个才有意义，比如将我们的sass文件保存成application.scss.liquid，就可以使用liquid语法来调用它。
body{



    background-color: #{'{{ settings.color_background }}'} 



}
```

**注意：这里用#{''}包裹。**

同样，字体也可以用这种方式调用：

```
body {
  font-family: #{'{{ settings.header_font }}'};
 }
```

## Collections

collections的调用方式会更复杂一些，首先要注意的是，当你将设置的类型为Collections是，选择面板中将显示用户的collections下拉列表，其中包括已经在商店中定义的所有Collections。这意味着必须至少已经定义了2个集合。其次，需要知道shopify都有哪些特殊配置的标签，这里有个表 http://cheat.markdunkley.com/，可以方便查看。

比如，我们在这里找到了collection.liquid部分，上面有用什么标签全局访问。

```
collections['the-handle'].variable
```

这里，the-handle是集合的名称，或者说是集合的slug。在settings_schema.json配置文件中，id的名称将定于这个属性。比如：

```javascript
 [
     {
      "name": "Collection",
      "settings" : [
      {
     "type": "collection",
     "id": "feature_collection",
      "label": "Feature collection"
      }
    ]
  }
 ]
```

那么就这样调用：

```
{{ collections[settings.feature_collection] }}
```

但是，上面的代码只会显示为CollectionDrop。 为了获得有意义的东西，需要选择集合的属性（可在http://cheat.markdunkley.com/上获得），例如标题或产品。

```
{{ collections[settings.feature_collection].title }}
```

您可能还想访问该集合中每个产品的信息。 这可以通过引用集合上的products属性然后循环遍历这些来轻松实现。

```html
{% for product in collections[settings.feature_collection].products %}
  <p>{{ product.title }} | {{ product.price }}</p>
 {% endfor %}
```

通过liquid循环语句，可以把集合中的每个产品遍历出来，并显示产品的标题和价格。

## Products

产品和集合的使用方式类似，查一下表，看看如何调用这个products。

```
all_products['the-handle'].variable
```

注意这里是all_products，而不是products。 所以，这样调用产品的标题和价格：

```
{{ all_products[settings.feature_product].title }} | {{ all_products[settings.feature_product].price }}
```

如果要调用产品的头图，这样来。

```
<img src="{{ all_products[settings.feature_product].featured_image | img_url: 'small' }}" alt="{{ a
```

