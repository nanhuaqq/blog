---
title: "Createblog"
date: 2018-08-29T17:36:32+08:00
draft: true
---

## 免费搭建自己的博客

### 搭建的方式

使用github和hugo搭建。

### hugo的安装

- 在mac上使用brew方式安装

```shell
brew install hugo
```

- 查看hogo版本

```shell
hugo version
```

- 生成静态站点

```shell
hugo new site blog
```

- 为站点添加一个主题

```shell
cd blog;
git init;
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke;

vim config.toml
```

- 在config中配置主题，添加配置如下

```shell
theme = "ananke"
```

- 发布一篇文章

```
hugo new posts/article.md
```

然后可以使用typora程序编辑刚刚新建的文件.

- 启动服务器看一下

```
hugo server -D
```

在浏览器输入  **http://localhost:1313/**



[hugo 快速开始](https://gohugo.io/getting-started/quick-start/)



## 创建github.io页面

[创建文档](https://pages.github.com/)

我创建的是个人和组织站点

## 关联github和本地hugo站点

[hugo文档](https://gohugo.io/hosting-and-deployment/hosting-on-github/)

其中有一步需要注意，在输入命令 

```shell
git submodule add -b master git@github.com <USERNAME>/<USERNAME>.github.io.git public
```

时，github提示Permission denied (publickey)。这很大概率是因为github账号没有设置你的ssh公钥。

### 设置github公钥

前往account settings - > setting - > ssh keys -> new ssh key

Title处填写“id_rsa.pub”或其他任意信息。 key处原样拷贝下面命令的打印 `~/.ssh/id_rsa.pub` 文件的内容：

``` cat ~/.ssh/id_rsa.pub ```



然后继续按照[hugo文档](https://gohugo.io/hosting-and-deployment/hosting-on-github/)

大功告成
