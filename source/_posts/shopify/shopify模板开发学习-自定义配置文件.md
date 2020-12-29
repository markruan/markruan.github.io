---
title: shopify模板开发学习-自定义配置文件
categories:
  - shopify
---



在创建主题时，可以为客户预留一些自定义的配置，是Shopify主题模板常用的做法。Shopify使用settings_schema.json文件提供了这个自定义配置的方式。

在Shopify主题的config目录中，在此文件中定义一些对象属性，就可以实现自定义的配置选项。当你选择在线商店 》 模板 》自定义按钮，就可以看到控制面板中这些选项。

## 配置文件的文件格式

settings_schema.json文件，本身是个JSON文件，那么他需要遵守JSON文件规范，这里所有的数据都用[]括起来。在此范围内，你可以将相关选项组合在一起。每个分组都有一个名称，然后是定义这个组的配置。比如：

```javascript
[
    {
        "name" : "颜色",
        "settings" : [ ]
    }
]
123456
```

然后，每个选项都是设置数组中的一个对象。 像这样的东西：

```json
[
  {
    "name": "Shopify119",
    "theme_name": "Shopify119 theme",
    "theme_version": "1.0.0",
    "theme_author": "Leo",
    "theme_documentation_url": "https://shopify119.blog.csdn.net",
    "theme_support_url": "https://shopify119.blog.csdn.net"
  },
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
  },
  {
    "name": "Logo",
    "settings": [
      {
        "type": "image",
        "id": "logo.png",
        "label": "Logo",
        "info": "这里可以改变店铺的Logo"
      }
    ]
  }
]
 
```

上面的例子中，在自定义设置的侧栏上，你可以看到标签“颜色”，当你单击他时，可以选择设置背景颜色和内容文字颜色；选择Logo可以更改店铺的Logo。
![在这里插入图片描述](https://raw.githubusercontent.com/markruan/cloudimg/master/img/20200305144403759.gif)

## 配置文件的属性

每个设置都有5个属性：type、id、label、default、info



| 类型 | 是否必填 | 描述                   |
| ---- | -------- | ---------------------- |
| type | 必填     | 定义选项所需的输入类型 |
|id |必填| id必须唯一，这将在主题中引用它|
| label | 必填 | 向用户描述了该选项的用途，可以用中文 |
|placeholder| 可选| 输入的占位符文本的值。这仅适用于基于文本的设置类型。|
|default| 可选| 该选项的默认值|
|info| 可选| 为用户提供该选项的详细使用信息|



## 常规设置类型

下表描述了允许的常规输入类型，每个值在type属性中设置。

| 值   | 说明 |
| ---- | ---- |
| text | 允许用户输入单行文本字段 |
|textarea| 允许用户输入多行文本字段|
|image| 允许用户上传图片|
|radio |允许用户使用单选按钮|
|select| 允许用户从下拉列表中进行选择|
|checkbox| 允许用户选中一个框，返回true或false值|

image type
需要注意的是，用这种方式上传的图片将保存在模板的assets文件夹中。该文件使用id中定义的名称和格式进行保存。所以，即使上传的是.jpg文件，但是id定义的是logo.png，图片也将会保存为.png文件。

radio和select type
由于radio和select有多个值可提供选择，因此还需要设置额外的属性。比如：

```json
{
		  "type":      "radio",
		  "id":        "id",
		  "label":     "Text",
		  "options": [
		    { "value": "one", "label": "Radio One" },
		    { "value": "two", "label": "Radio Two" }
		  ],
		  "default":   "one",
		  "info":      "Text"
} 
```

## 特殊设置类型

特殊设置类型的定义访问和常规设置类型相似，不同之处在于这些设置，将为用户提供内置或特定的选择信息。比如：产品类型是下拉列表，但只允许用户从已经在商店中定义的产品类型中进行选择。

| 值   | 说明 |
| ---- | ---- |
|color| 允许用户使用颜色选择器窗口小部件选择颜色|
| font | 允许用户从可用字体列表中进行选择 |
| collection | 允许用户选择商店中可用的产品系列 |
|product| 允许用户选择商店中可用的产品|
|blog| 允许用户从商店中设置的博客列表中进行选择|
|link_list| 允许用户从可用菜单中进行选择|
|page |允许用户选择商店中定义的特定页面|
|snippets| 允许用户选择主题中可用的特定代码段|

## Blog Type

Shopify内置了博客，你可以添加博客文章。还可以把这些博客文章添加到不同的博客中。blog type设置下拉列表允许你选择要用于改设置的博客。

## Snippet Type

代码片段在模板中的snippets目录里面定义。

### 信息设置



Shopify还允许将创建主题的作者信息放入侧边栏中，它们只有3个属性：type, content, info

| 类型 | 是否必填 | 描述 |
| ---- | -------- | ---- |
| type | 必填 | 定义选项所需的输入类型。 对于侧边栏设置，这只能是标题或段落 |
| content | 必填 | 文本内容 |
| info | 可选 | 向用户提供有关该选项的其他信息。 |


在模板中调用配置信息
现在已经可以创建设置信息了，但是如何在实际的模板中调用并使用它们？这将是下篇文章的内容。