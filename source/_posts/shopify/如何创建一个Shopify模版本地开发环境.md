---
title: 如何创建一个Shopify模版本地开发环境.
categories:
  - shopify
---
### 安装主题套件

首先，转到[themekit](https://link.zhihu.com/?target=https%3A//www.shopifyfans.com/wp-content/themes/begin/go.php%3Furl%3DaHR0cHM6Ly9zaG9waWZ5LmdpdGh1Yi5pby90aGVtZWtpdC8%3D)下载主题套件。

### macOS安装

使用[homebrew](https://link.zhihu.com/?target=https%3A//www.shopifyfans.com/wp-content/themes/begin/go.php%3Furl%3DaHR0cDovL2JyZXcuc2gv)安装themekiit.

```text
brew tap shopify/shopify
brew install themekit
```

### Windows Chocolatey安装

首先安装[Chocolatey](https://link.zhihu.com/?target=https%3A//www.shopifyfans.com/wp-content/themes/begin/go.php%3Furl%3DaHR0cHM6Ly9jaG9jb2xhdGV5Lm9yZy8%3D)，然后通过以下命令安装themekit。

```as3
choco install themekit
```

### Linux安装

如果是Linux系统，则可以使用以下脚本安装themekit。

```text
curl -s https://shopify.github.io/themekit/scripts/install.py | sudo python
```

安装完毕之后运行**theme**，如果显示下图信息则安装成功。

![img](https://pic3.zhimg.com/80/v2-8cce0690f64d6c6a02ef0c91aedf59a6_720w.jpg)



### 链接到商店

要想连接到商店拥有主题的读写权限，首先得建立私人应用将API秘钥添加到我们的配置中。

请登录Shopify后台，然后创建一个私人应用程序。

> Shopify管理员 > Apps > 单击Manage private apps > 单击Create a new private app创建应用

然后填写信息，并将**Theme templates and theme assets**权限设置为读写访问权限并保存，页面刷新之后复制密码，后面步骤用得到。



![img](https://pic4.zhimg.com/v2-c5672b6847b0eb3768ab31ae2772ecc7_b.jpg)



### 下载需要修改的模板

接下来，我们需要将主题下载到本地环境中。要下载模板，首先需要知道模板的ID。获取ID的最简单方法是使用get命令，如下所示：

1. theme get --list -p=上一步复制的密码 -s=[http://you-store.myshopify.com](https://link.zhihu.com/?target=http%3A//you-store.myshopify.com)





![img](https://pic1.zhimg.com/80/v2-4db25c89310144da8a0178b52516dfe8_720w.png)


然后，记下模板ID，运行以下命令从shopify下载主题：

1. theme get -p=上一步复制的密码 -s=[http://you-store.myshopify.com](https://link.zhihu.com/?target=http%3A//you-store.myshopify.com) -t=your-theme-id





![img](https://pic4.zhimg.com/80/v2-f35f2d0497884ca2054caa92d7f3b0b3_720w.png)



### 编辑模板

我们可以编辑这些本地文件，然后运行**theme watch**。这将监视模板文件中的更改，当检测到文件被修改时，Theme Kit将自动将新版本上载到Shopify，因此您可以立即查看编辑后的模板样式。



![img](https://pic1.zhimg.com/80/v2-d05bbd9df19f9ebab7b5f48fd157a790_720w.jpg)



当我们对theme.scss.liquid文件进行了一些更改，您将在终端上看到此输出



![img](https://pic3.zhimg.com/80/v2-503c4fedd4f708bb2c7472247cc4af1e_720w.jpg)



> 要上传特定文件，请运行theme upload <file>。要删除特定文件，请运行theme remove <file>。您可以通过运行查找所有命令的列表theme help。您可以通过运行获取有关命令的更多信息theme help <command>

### 实时预览

没有人喜欢编辑一次然后手动刷新一次页面。下面我们将使用Prepros来达到实时预览的功能。

首先下载[Prepros](https://link.zhihu.com/?target=https%3A//www.shopifyfans.com/wp-content/themes/begin/go.php%3Furl%3DaHR0cHM6Ly9wcmVwcm9zLmlvLw%3D%3D)并安装



![img](https://pic3.zhimg.com/80/v2-81a904f9da10308140a2387dcd37b74a_720w.jpg)



### 将主题添加为项目



![img](https://pic1.zhimg.com/v2-c100f31eacdfb0f033c87de8dc6e9c34_b.jpg)



只需将整个目录拖到Prepros中，即可将主题作为项目添加到Prepros。

### 监视.liquid文件

应将.liquid文件添加到Prepros将要监视的文件类型列表中。默认情况下是不会监视它们的，因为Prepros不会编译Liquid。

要将.liquid文件添加到监视列表，请右键任意.liquid文件，然后选择“ **Watch .liquid files**”。

![img](https://pic2.zhimg.com/80/v2-feb48e382f61af3f0709e211727c5cd9_720w.jpg)



### 将实时预览链接到店铺

下一步是设置实时预览的URL。也就是将Prepros与Shopify商店链接起来并实现实时重载的功能。

具体设置如下图：

![img](https://pic1.zhimg.com/v2-c69eef525d534cd9784f643dbf3017a4_b.jpg)



### 设置重新加载的延迟

最后，您需要在Prepros中设置延迟。延迟的原因是让Theme Kit有时间观察到更改，并将更改与Shopify的服务器同步。

具体设置如下图：

![img](https://pic2.zhimg.com/v2-8912efba9332fff5ecc0251c1e1f7e1d_b.jpg)



### 进行修改并实时预览

现在，您已经设置了实时预览，按**Ctrl+L**在浏览器中打开就能看到。	