---
title: shopify 图片CDN 详解
categories:
  - shopify
---
对于刚入手shopify 的小白来说，shopify 图片是一个急需了解的点。
对于大企业来说资源管理是必须优化到极致的，目前对于资源管理比较有效的方式是 CDN 资源管理。shopify 自然也会为它的资源搭建CDN服务，而对图片则做图片CDN，图片CDN与传统CDN的区别在于，它是专门为图片做优化的，通常包含缩放、格式转换等。你可以把它看成是一个API，通过传入尺寸、质量、格式等参数，获取到对应的图片内容。这也使得我们在使用上非常方便，适用于多种不同的场景。

下面我们则针对 shopify 图片CDN的使用做讲解

## Shopify 图片的参数使用

下面花括号里面使用的 [image 是指 shopify 的图片对象](https://shopify.dev/docs/themes/liquid/reference/objects/image）

### 图片尺寸参数

您可以为图像的宽度和高度指定精确的像素尺寸，最大5760 x 5760 px。除非[裁剪](https://shopify.dev/docs/themes/liquid/reference/filters/url-filters/#crop)图像，否则图像的原始长宽比将保留。（无论您指定什么尺寸，都不能将图像的大小调整为大于其原始尺寸。如果大于原始尺寸则返回原始尺寸大下的图片）

#### 固定尺寸

根据设置的 宽高 返回对应尺寸的图片

**格式**

```
{{ image | img_url: '<宽>x<高>' }} 
```

**输入**

```html
{{ image | img_url: '720x720' }} 
```

**CDN**

```html
https://cdn.shopify.com/s/files/1/1183/1048/products/boat-shoes_720x720.jpeg
```

#### 英文名称尺寸

与固定尺寸一样的意义，只不过，值使用英文名称替代

| 英文名称 | 示例                                                 | 返回尺寸 |
| -------- | ---------------------------------------------------- | -------- |
| <空>     | &#123;&#123; image \| img_url &#125;&#125;           | 100x100  |
| small    | &#123;&#123;image \| img_url : ‘small’ &#125;&#125;  | 100x100  |
| medium   | &#123;&#123; image \| img_url: ‘medium’ &#125;&#125; | 240x240  |
| large    | &#123;&#123; image \| img_url: ‘large’ &#125;&#125;  | 480x480  |
| master   | &#123;&#123; image \| img_url: ‘master’ &#125;&#125; | 原始尺寸 |

#### 仅宽或高尺寸

您只能指定宽度或高度，Shopify会根据原始图像的尺寸计算其他尺寸，并**保持原始图像的长宽比**：

例子 图片尺寸为 400x300

**仅宽度**

```json
{{ image | img_url: '200x' }} //返回 图片尺寸为 200x150
```

**仅高度**

```json
{{ image | img_url: 'x150' }} //返回 图片尺寸为 200x150
```

### 图片剪切参数 crop

您可以指定`crop`参数以确保生成的图像的尺寸与请求的尺寸匹配。如果整个图像都不适合您要求的尺寸，则该`crop`参数指定要显示图像的哪一部分。有效选项包括：`top`、`centent`、`bottom`、`left`、`right`

列子 图片 宽高 为 100x300，（按竖直方式平分为三个，分别为 上中下）

```json
{{ image | img_url: '100x100', crop: 'bottom' }} // 显示部分 为 下
```

#### 示例

##### **原图** - 九宫格

尺寸：900x900

![img](https://cdn.shopify.com/s/files/1/0449/5491/0874/files/sudoku_300x300.jpg)

##### **1、不带 crop，则根据固定尺寸原则，返回原始尺寸**

**输入**

```json
{{ image | img_url: '900x300' }} 
```

**CDN**

```
//cdn.shopify.com/s/files/1/0449/5491/0874/files/sudoku_900x300.jpg
```

**效果图**

![img](https://cdn.shopify.com/s/files/1/0449/5491/0874/files/sudoku_900x300.jpg)

##### 2、带 crop， 图片不符合尺寸时，则根据crop指定的位置，截取要显示的部分

**输入**

```json
{{ image | img_url: '300x100', crop: 'top' }} 
{{ image | img_url: '300x100', crop: 'center'}} 
{{ image | img_url: '300x100', crop: 'bottom'}} 
{{ image | img_url: '100x300', crop: 'left' }} 
{{ image | img_url: '100x300', crop: 'center'}} 
{{ image | img_url: '100x300', crop: 'right'}} 
```

**CDN**

```
//cdn.shopify.com/s/files/1/0449/5491/0874/files/sudoku_300x100_crop_top.jpg
//cdn.shopify.com/s/files/1/0449/5491/0874/files/sudoku_300x100_crop_center.jpg
//cdn.shopify.com/s/files/1/0449/5491/0874/files/sudoku_300x100_crop_bottom.jpg
//cdn.shopify.com/s/files/1/0449/5491/0874/files/sudoku_100x300_crop_left.jpg
//cdn.shopify.com/s/files/1/0449/5491/0874/files/sudoku_100x300_crop_cen300x150
//cdn.shopify.com/s/files/1/0449/5491/0874/files/sudoku_100x300_crop_right.jpg
```

**图片**

| 300x100 top                                                  | 300x100 center                                               | 300x100 right                                                |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![img](https://cdn.shopify.com/s/files/1/0449/5491/0874/files/sudoku_300x100_crop_top.jpg) | ![img](https://cdn.shopify.com/s/files/1/0449/5491/0874/files/sudoku_300x100_crop_center.jpg) | ![img](https://cdn.shopify.com/s/files/1/0449/5491/0874/files/sudoku_300x100_crop_bottom.jpg) |

| 100x300 left                                                 | 100x300 center                                               | 100x300 right                                                |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![img](https://cdn.shopify.com/s/files/1/0449/5491/0874/files/sudoku_100x300_crop_left.jpg) | ![img](https://cdn.shopify.com/s/files/1/0449/5491/0874/files/sudoku_100x300_crop_center.jpg) | ![img](https://cdn.shopify.com/s/files/1/0449/5491/0874/files/sudoku_100x300_crop_right.jpg) |

### 图片比例（倍数）参数 scale

*谷歌翻译 为 亲密度，但是从效果来看我觉得翻译为比例或者倍数更加恰当*

该`scale`参数使您可以指定图像的像素密度。（返回img_url设置的尺寸的scale倍数的图片尺寸，这里我可能解释的不是很清楚，我们还是直接看示例）

##### 示例

**输入**

```json
{{ image | img_url: '150x150' }}
{{ image | img_url: '150x150', scale: 2 }}
```

**CDN**

```html
//cdn.shopify.com/s/files/1/0449/5491/0874/files/sudoku_150x150.jpg
//cdn.shopify.com/s/files/1/0449/5491/0874/files/sudoku_150x150@2x.jpg
```

**效果图**

| &#123;&#123; image \| img_url: ‘150x150’ &#125;&#125;        | &#123;&#123; image \| img_url: ‘150x150’, scale: 2 &#125;&#125; |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![img](https://cdn.shopify.com/s/files/1/0449/5491/0874/files/sudoku_150x150.jpg) | ![img](https://cdn.shopify.com/s/files/1/0449/5491/0874/files/sudoku_150x150@2x.jpg) |
| 图片尺寸：150x150                                            | 图片尺寸：300x300                                            |

根据上述例子，相信你应该能明白 **scale** 的作用了

### 图片格式参数 format

该`format`参数使您可以指定要用于显示图像的文件格式。有效选项包括：`jpg`、`pjpg`([渐进式JPEG](https://en.wikipedia.org/wiki/JPEG#JPEG_compression)。浏览器以逐渐提高的质量加载全尺寸的渐进式JPEG，而不是像传统JPEG那样从上到下加载完整质量的图像。)

Shopify可以为您执行以下格式转换：PNG 转 JPG、PNG 转 PJPG、JPG 转 PJPG

#### 示例

**输入**

```json
{{ image | img_url, format: 'jpg'  }} 
{{ image | img_url, format: 'pjpg' }}
{{ image | img_url, format: 'pjpg'  }}
```

**CDN**

```json
/* PNG 转 JPG */
https://cdn.shopify.com/s/files/1/0449/5491/0874/files/baymax_100x100.png.jpg 
/* PNG 转 PJPG */
https://cdn.shopify.com/s/files/1/0449/5491/0874/files/baymax_100x100.progressive.png.jpg
/* JPG 转 PJPG */
https://cdn.shopify.com/s/files/1/0449/5491/0874/files/baymax_100x100.progressive.jpg
```

**效果图**

| PNG 转 JPG                                                   | PNG 转 PJPG                                                  | JPG 转 PJPG                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| &#123;&#123; image \| img_url, format: ‘jpg’ &#125;&#125;&#125; | &#123;&#123;image \| img_url, format: ‘pjpg’ &#125;&#125;    | &#123;&#123;image \| img_url, format: ‘pjpg’ &#125;&#125;    |
| ![img](https://img-blog.csdnimg.cn/img_convert/9e71f5c9dfdc27044f53d3600b702398.png) | ![img](https://img-blog.csdnimg.cn/img_convert/9e71f5c9dfdc27044f53d3600b702398.png) | ![img](https://img-blog.csdnimg.cn/img_convert/af27185e6344fa9e237d57f87d48f858.png) |
| ![img](https://img-blog.csdnimg.cn/img_convert/70c761fd11c6c783542b745340ba4b0a.png) | ![img](https://img-blog.csdnimg.cn/img_convert/0369ae7f97d6b7011609e8d4ec8ec295.png) | ![img](https://img-blog.csdnimg.cn/img_convert/6c9061c123da783eeabd183d1db2ba45.png) |