---
title: "Hugo 建站指南"
description: 这篇文章主要是介绍如何使用 hugo 搭建自己的个人博客网站。
date: 2024-03-06T15:48:37+08:00
draft: false
tags: ["Areas/Blog"]
---

这篇文章主要是介绍如何使用 hugo 搭建自己的个人博客网站，这是我个人的博客: [https://chinjo.top/](https://chinjo.top/)。

### 前提条件

这里的前提条件我就不再多讲了，无非就两样，我就简单介绍一下就行了，大家多去搜索一下就行。

- 域名
- 服务器

域名很简单，网上搜索会有很多购买的网站，这里就推荐[NameSilo](https://www.namesilo.com/?rid=d27fa32do)，默认就有 WHOIS 的隐私保护服务，挺好的，也不贵。需要注意的是，购买的时候多留意一下，续费是不是同价，有的域名购买的第一年会很便宜，第二年开始价格会不一样，这点需要多留意下就可以了。

服务器接触的最多的是虚拟主机和 VPS，虚拟机价格便宜，性能弱（也就一般需求不高的企业可以用），可定制化低。VPS 性能更好，安全性更高，可定制性高，价格稍贵。至于去哪个服务商购买，这里就推荐一个「Cloud Cone 」，其他服务商，我也没购买过，不敢随便下定论。

### 建站

在此之前，需要先下载 hugo 的命令行执行文件。

所有的版本下载[地址](https://github.com/gohugoio/hugo/releases/)。

下载及安装完成后，就可以开始入门 Hugo 了。这部分建议多去官网看看详细的教程，参考官方的[快速文档](https://gohugo.io/getting-started/quick-start/)基本都可以实现出来.

以下是官方的教程，需要有一定的代码基础

```
hugo new site quickstart

cd quickstart

git init

git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke

echo "theme = 'ananke'" >> hugo.toml

hugo server
```

### 新建文章

官方建议是通过命令创建内容的

```
hugo new posts/my-first-post.md
```

Hugo 会创建一个新的文件在`content/posts`的目录里面，只需要在编辑器上打开这个文件就可以了。

```
+++
title = 'My First Post'
date = 2024-01-14T07:07:07+01:00
draft = true
+++
```

只需要在`+++`下面添加你的文章内容就可以了。需要注意的是，默认生成的文件上面，`draft`属性是为`true`的，在预览的时候，需要将其修改成`false`或者删除这一行都可以，不然会预览不到新建的这篇文章。

### 主题选择

默认的主题基本都不好看，可以自己去[主题中心](https://themes.gohugo.io/)找找看。我选择的是[Archie](https://athul.github.io/archie/)，其中我把里面的字体替换了，改成自己想要的字体[「霞鹜文楷」](https://github.com/lxgw/LxgwWenKai)，有兴趣的可以去看看，一款不错的楷体，还是开源的。

### 预览

本地预览的操作其实很简单，直接在编辑器的命令行中，输入`hugo server`命令即可生成本地预览地址。

### 编译

编译也就是把你添加的`.md`文件转换成`HTML`文件，命令也很简单，直接输入`hugo`即可。
编译完成后，你会发现`public`的文件目录下多了一些文件和其他目录，这些就是静态的`HTML`文件，之后只需要把这里的文件放到服务器上就可以了。

### 服务器

考虑到有的人是尝新的，直接购买服务器可能会有点不划算，所以我这里说的直接用`GitHub Pages`来实现博客展示。

其实就是把当前的代码，更新到自己的库里面去，然后用`GitHub`自带的`Workflow` 功能实现自动把文件复制到 `GitHub` 提供的服务器上 。

整体的 `Workflow`可以直接使用 `GitHub` 推荐的静态文件部署的流程，然后针对复制部分，把`public`目录下的所有文件复制到一个临时的文件中，上传的时候把临时的文件上传就可以了，具体代码如下：

```
- name: Copy files

# 把 public 下的文件复制到一个临时文件夹

run: |

mkdir temp &&

cp -r public/* temp/

- name: Upload artifact

uses: actions/upload-pages-artifact@v2

with:

# Upload files from hardy-blog/output

path: temp/

# Set the name for the uploaded artifact

name: hardy-blog

- name: Deploy to GitHub Pages

id: deployment

uses: actions/deploy-pages@v3

with:

# 注意：这里的 artifact 参数应该与你上传时的名称一致

artifact_name: hardy-blog
```

最后就是使用`GitHub Pages`的域名访问网址就可以看到效果了。

### 另外提醒

因为这个是用`GitHub`发布的博客，所以就有可能出现在另外一台电脑继续添加文章的操作。本身这方案是支持这个操作的，只是当把项目 clone 下来之后，需要把主题的库也得 fetch 到本地才行，不然修改 hugo 的配置文件，某些参数不会生效的，具体命令是：

```
git submodule foreach git fetch --all
git submodule update --init --recursive
```

### 最后推荐

现在「GPT」这么好用，大家一定要多多去用这个工具，遇到问题可以优先使用这工具去寻找答案，有条件的可以用上「4.5」的话，就可以拼命地用，没有条件用着免费的其实都很好用，虽然数据模型有点低，但是不妨碍使用的。可以结合搜索一起使用，准确率会好很多。
