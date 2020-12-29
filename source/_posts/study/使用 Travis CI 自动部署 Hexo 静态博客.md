---
title: 使用-Travis-CI-自动部署-Hexo-静态博客
tag:
 - hexo
---



我们搭建个人网站的初衷，不就是为了能好好地写博客吗？一切重复且枯燥的工作都应该交给程序去自动完成，尤其是静态博客，**我们只需要专注文字**。



## 什么是 CI

**CI(Continuous Integration)** 翻译为**持续集成**。[Travis CI](https://travis-ci.com/) 是一个提供持续集成功能的平台，Github 可关联 Travis CI，当 GitHub 仓库有代码 push 时，会推送通知到 Travis CI，根据设置的脚本运行指定任务。

## 使用 CI 自动部署的好处

- 可以直接在线编辑 md 文件，立即生效。假设你已发布一篇文章，过几天你在别的电脑上浏览发现有几个明显的错别字，这是完全不能容忍的。但此时你电脑上又没有 hexo + node.js + git 等完整的开发环境，重新配置开发环境明显不现实。如果使用 CI，你可以直接用浏览器访问 GitHub 上的项目仓库，直接编辑带错别字的 md 文章，改完，在线提交，稍等片刻，你的网站就自动更新了。
- 手动部署需要推送 public 整个文件夹到 GitHub 上，当后期网站文章、图片较多时候，很多时候连接 GitHub 不是那么顺畅，经常要傻等很长的上传时间。有了 CI，你可以只提交 post 文件里单独的 md 文件即可，很快很爽，谁用谁知道。
- 使用 CI，你可以一次性将这些静态博客页面部署到多个服务器上，例如：GitHub Pages、七牛云、阿里云等。
- …

## 搭建流程

**本文以 Hexo + [Keep](https://github.com/XPoet/hexo-theme-keep) 搭建的静态网站为例，教你如何使用 Travis CI 自动部署到 GitHub Pages 服务器。**

### 新建 GitHub 仓库

创建一个用来存储 Hexo 项目源代码和静态页面的[GitHub 仓库](https://github.com/new)

![img](https://cdn.jsdelivr.net/gh/XPoet/image-hosting@master/使用Travis-CI自动部署Hexo静态博客/create-repos.1evjlz6fnchs.png)

备注：选公有仓库和私有仓库都可以，但 Travis CI 只对 GitHub 的 public 仓库免费。

例如：本文案例仓库 `keep-demo`。

- 用 `main 分支` 来存储 hexo 博客项目源代码。
- 用 `gh-pages 分支` 存储来编译生成后静态页面。

当 `main 分支`的源代码（主题文件，文章 md 文件、图片等）有变动时，CI 会自动编译并部署到 `gh-pages 分支`。

### 新建 GitHub Token

创建一个有 repo 权限的 [GitHub Token](https://github.com/settings/tokens/new) 。

![img](https://cdn.jsdelivr.net/gh/XPoet/image-hosting@master/使用Travis-CI自动部署Hexo静态博客/image.8ew2trw9if4.png)

新生成的 Token 只会显示一次，如有遗失，重新生成即可。

![img](https://cdn.jsdelivr.net/gh/XPoet/xpoet-image-hosting/PicX/image.krns6rvn9l.png)

### 添加 `.travis.yml`

在你的 Hexo 博客项目文件夹下添加 Travis CI 的配置文件 `.travis.yml`。

![img](https://cdn.jsdelivr.net/gh/XPoet/image-hosting@master/使用Travis-CI自动部署Hexo静态博客/image.4fgd9xj4kl20.png)

`.travis.yml` 文件的内容如下：

```
# 编译环境、语言
dist: xenial
os: linux
language: node_js

# Node.js 版本
node_js:
  - 12

branches:
  only:
    - main                      # 只有 main 分支检出更改才触发 CI

before_install:
  - export TZ='Asia/Shanghai'   # 配置时区为东八区 UTC+8
  - npm install hexo-cli        # 安装 hexo

install:
  - npm install                 # 安装 hexo 项目相关的依赖

# 执行脚本 
script:                         
  - hexo clean                  # 清除 hexo 缓存
  - hexo generate               # 生成静态文件

deploy:
  on:
    branch: main                # 工作分支
  strategy: git
  provider: pages
  skip_cleanup: true            # 跳过清理
  token: $GH_TOKEN              # GitHub Token 变量
  keep_history: true            # 保持推送记录，以增量提交的方式
  local_dir: public             # 需要推送到 gh-pages 分支的静态文件目录
  target_branch: gh-pages       # 推送的目标文件夹 local_dir(public) -> gh-pages 分支
```

### Travis CI 关联项目仓库

- 使用 GitHub 账号登录 [Travis CI 官网](https://travis-ci.com/)，关联你的 hexo 博客项目仓库，并绑定前面生成的 GitHub Token。
  ![img](https://cdn.jsdelivr.net/gh/XPoet/image-hosting@master/使用Travis-CI自动部署Hexo静态博客/image.29mrt40ry85c.png)
- 点击右上角头像，选择 “Settings”。
  ![img](https://cdn.jsdelivr.net/gh/XPoet/image-hosting@master/使用Travis-CI自动部署Hexo静态博客/image.61r86to55dk0.png)
- 在所列出来的仓库里找到你的 `hexo 项目仓库`，点击 “Settings” 。如果仓库过多，可以直接搜索。
  ![img](https://cdn.jsdelivr.net/gh/XPoet/image-hosting@master/使用Travis-CI自动部署Hexo静态博客/image.2h7f3eetn9g0.png)
- 增加环境变量，`GH_TOKEN` 的值填你在前面生成的 `GitHub Token`，最后点击 “Add” 添加。
  ![img](https://cdn.jsdelivr.net/gh/XPoet/image-hosting@master/使用Travis-CI自动部署Hexo静态博客/image.i5puxt6ef7c.png)

## 使用流程

### 修改源代码文件

在你的 hexo 项目文件夹下，修改你的文章、图片、主题等。

### push 到仓库

将你的 hexo 项目代码 push 到 GitHub 仓库的 main 分支，Travis CI 检测到 main 分支代码有变动，会自动执行脚本命令，将 hexo 项目编译生成静态页面，部署到 `gh-pages` 分支。

备注：`gh-pages` 分支是 GitHub Pages 服务的固定分支，你只需在 `.travis.yml` 文件正确填写，会自动创建。

### 使用自定义域名访问

你可以使用自己的域名来访问 GitHub Pages 服务，只需在 hexo 项目的 `source` 目录下添加 `CNANE` 文件。

`CNANE` 文件内容参考如下：

```
keep.xpoet.cn
```

![img](https://cdn.jsdelivr.net/gh/XPoet/image-hosting@master/使用Travis-CI自动部署Hexo静态博客/image.40wfwkzns480.png)

### 开启 https

下图是 Travis CI 自动部署到 `gh-pages` 分支 成功的效果。

![img](https://cdn.jsdelivr.net/gh/XPoet/image-hosting@master/使用Travis-CI自动部署Hexo静态博客/image.3slemzli8ai0.png)

我们可在仓库 `Settings` 开启域名 https 协议。

![img](https://cdn.jsdelivr.net/gh/XPoet/image-hosting@master/使用Travis-CI自动部署Hexo静态博客/image.3d1cd0bwi5i0.png)

至此，使用 Travis CI 自动部署 Hexo 静态博客到 GitHub Pages 教程完毕，有任何问题，欢迎在评论区留言。

- 本文链接：https://keep.xpoet.cn/2020/11/使用-Travis-CI-自动部署-Hexo-静态博客/