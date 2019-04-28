---
title: 使用Hexo与GitHub搭建简易博客
date: 2018-07-03 15:06:19
tags: 
  - 心路历程
  - 技术沉淀
---

>说了很久想自己写一个个人博客，但是无奈就是患有拖延症，现在才想到逐渐补上。那好，就直接从怎样搭建现在这个简易博客说起。

能够快速地搭建起这一个博客，非常感谢的是前辈们给出的相关文档。更多的，是依赖于 Hexo 这个开源框架，以及 GitHub 这个为广大程序员所熟知的平台。下面先简单介绍下他们的作用（其实更多的是记录给自己看）

---

### GitHub Pages

[GitHub Pages](https://pages.github.com/) 是 GitHub 所提供的免费博客托管平台，并且有 GitHub 免费提供的域名，例如 https://username.github.io/，
很大程度上减少了维护一个个人博客的成本。其本质上来说，就是静态网站的托管服务器。


### Hexo

[Hexo](https://hexo.io/) 是一个快速搭建博客的框架，依赖于 Node.js，拥有丰富多彩的[主题](https://hexo.io/themes/)，能够直接将撰写好的 MarkDown 文件编译成为静态文件，嵌入到网站整体当中。

同时，Hexo 还能方便的与 GitHub Pages 结合，使用其封装好的 `hexo-cli` 命令行工具，一键部署更新后的代码到各个平台。

---

### 开始使用

>事先声明，以下内容针对 Mac 用户，如果你不是 Mac 用户，那么欢迎[摇身一变](https://osx.cx/2016-clover-macos-sierra10-12-1-jiaocheng.html)成为 Mac 用户。

首先，先完成 GitHub Pages 的配置。根据官方文档，其实步骤很简单。

  - 在 GitHub 创建名为 `username.github.io` 的仓库，这里的 `username` 使用自己 GitHub 的用户名进行替换
  - 然后在心里默念仓库地址 10 遍，等下要用到，`https://github.com/username/username.github.io`

关于 GitHub Pages 所需要做的，其实就是这么多。接下来，就是要使用 Hexo，创建博客网站，并提交到 `username.github.io` 这个仓库就可以了。

接下来，我们开始关键的步骤（这里假定我们已经是 GitHub 的熟手，早已完成了 SSH key 以及其他繁杂的配置）。

  - 安装 hexo

    如果你已经安装了 `npm`，那么恭喜你，一行命令解千愁。

    `npm install -g hexo`

    如果还没有，而且你是苹果用户，希望你已经装了 [Homebrew](https://brew.sh/)，如果还是没有的话，就点进去看看，安装 5 分钟，排错 2 小时，然后就能用 `brew` 指令安装 `npm` 了。编译可能有点久，耐心等等。

    `brew install npm`

  - 创建 hexo 项目

    执行下面指令，项目名称自由发挥，我比较低调，就叫了 blog。

    `hexo init blog`

    然后到项目目录下，安装依赖

    `npm install`

    这时候，其实你也同样可以为 hexo 项目的源码创建一个独立的 git 仓库（不是刚刚的 `username.github.io`），方便对 hexo 的源码进行管理，包括你引入、修改主题，以及你创建的 MarkDown 文档。

  - 配置 hexo 项目

    初始化完成后，会在项目目录下发现名为 `_config.yml` 的文件，用你喜欢的任何编辑器打开它，修改其中的内容。

    找到下面这一段配置，然后回忆一下刚刚默念过 10 遍的 GitHub Pages 的项目地址，大胆的填进去。当然，你也可以定制化分支，通常情况下没这个必要。

    ```
    # Deployment
    ## Docs: https://hexo.io/docs/deployment.html
    deploy:
      type: git
      repository: https://github.com/username/username.github.io
      branch: master
    ```

    这段配置就是告诉 hexo，它到时候编译出来的静态文件应该推送到哪里。最关键的配置其实就是这里，这里记得配置好 git 所用的 SSH key，不然是不能自动推送上去的。

    至于主题，也是在配置文件中指定。例如我使用的就是 [vexo](https://github.com/yanm1ng/hexo-theme-vexo)，在主题自己的官网，能根据文档快速的将其引入到你自己的 hexo 项目中。

---

### 大功告成

好了，该装的已经装了，该配的已经配了。那我们就开始撰写自己的博客，并推送到服务器上吧。

  - 创建博文

    使用指令 `hexo new article_name`，创建一篇博文，你会在 `source/_posts` 目录下，找到对应的 MarkDown 文件。

    打开该文件，默认会生成以下内容：

    ```
    ---
    title: article_name
    date: 2018-07-03 15:06:19
    tags: 
    ---
    ```

    `tags` 中你可以随意的加入自己的分类标签。

  - 生成和部署

    写完博文之后，运行下面的快捷命令，hexo 框架就会生成静态文件，并且部署到你指定的 GitHub Pages 仓库。

    ```
    hexo d -g # generate and deploy
    ```

  - 静静等待

    现在你就可以访问 `https://username.github.io/` 查看自己的博客网站了。根据实测，将静态文件推送到仓库，到真正显示更新后的内容，大约需要半分钟到一分钟，所以，喝口茶、检查下错别字，确认下自己提交的内容准确无误吧。
