---
title: 使用Hexo搭建博客
date: 2022-01-17 20:27:31
tags: [Blog]
toc: true
---

# 准备工作

1. 需要安装的软件 node.js和git

2. 使用npm安装hexo和一些插件,参考文档https://hexo.io/zh-cn/docs/

   > 安装方式:在安装node.js之后在控制台直接输入npm install [packname])
   >
   > 需要安装的内容:
   >
   > * hexo
   > * hexo-deployer-git
   > * hexo-toc
   >
   > 比如说需要安装hexo就`npm install hexo`,其余以此类推
   >
   > hexo-deployer-git 用于生成文件直接同步到你的库中   
   >
   > hexo-toc 是提供toc支持markdown文本的toc支持(可以不装)

3. 准备两个库,一个存放对应的blog文件,另外一个存放生成好的网页文件

   > 注意:存放网页文件的库命名固定为<你的 GitHub 用户名>.github.io
   >
   > 后续你的博客打开链接为https://<你的 GitHub 用户名>.github.io/
   >
   > 比如说你用户名是`tom`,那么库名就是`tom.github.io`,最后的博客链接就是`https://tom.github.io/`

   <!--more-->

# 安装Hexo

1. 将blog那个库和本地同步并且绑定,然后在blog文件夹中用控制台执行`hexo init <文件夹名>` 初始化

   > 打开cmd,然后用cd命令切换到对应的目录,然后再hexo init啥的,后续一样的

2. 初始化之后会有一堆配置文件,找到其中的`_config.yml`并且打开(vscode啥都行),然后更改其中的内容

   > 具体参考:https://hexo.io/zh-cn/docs/configuration
   >
   > 像Site那块就是网页的配置,title,author什么的随便改就行,具体要说明的是下面这个deploy
   >
   > deploy是关于网页部署的配置,为了方便说明假设你用户名是tom,那么修改后配置如下
   >
   > ```
   > deploy:
   > type: git
   > repo: https://github.com/tom/tom.github.io.git
   > branch: main
   > ```
   >
   > > 关于deploy的几点说明
   > >
   > > type 现在使用git,之前使用的github,
   > >
   > > repo 就是之前提到的那个固定格式的库的完整地址(也就是后面记得加.git)
   > >
   > > branch 表示那个库的分支,之前默认分支是master,现在默认是main(也可以自己调整)

3. 增加新的博客(如果不想加直接跳转到4)

   > 使用控制台直接hexo new 新文件名,然后到目录下的`source\_post`中找到对应的md文件编辑即可,使用markdown语法编辑
   >
   > 具体markdown语法可参考http://www.markdown.cn/
   >
   > 不使用hexo new直接去对应目录创建文件夹和文件也是可以的

4. 生成网页

   > 编辑好设置和博客后,使用`hexo g`和`hexo s`来生成可供本地预览的版本
   >
   > ![hexo s效果](hexo_build.png)
   >
   >  成功后会给出一个链接`http://localhost:4000/`直接复制到浏览器中打开即可看到
   >
   > 如果有出现问题根据具体问题修改.
   
5. 提交到github

   > 这里需要安装`hexo-deployer-git`
   >
   > 使用`hexo clean` 和`hexo deploy`命令,成功了就可以尝试打开之前提到的链接`https://tom.github.io/`
   >
   > 至于本地的库另外同步到github就可以了(不影响链接的打开)

# blog更新

## hexo命令

详细介绍参考 https://hexo.io/zh-cn/docs/commands.html

> hexo new <文件名> 新增一篇文章(默认在source\\_post文件夹中)
>
> hexo g  生成静态文件
>
> hexo s 启动服务器(搭配上面的使用,使用`http://localhost:4000/`预览效果)
>
> hexo clean 清理缓存和静态文件(搭配下面的hexo deploy一起用)
>
> hexo deploy 生成对应的网页文件并且推送到github

## git命令

> git clone <github链接>  将一个库克隆到本地

## 参考教程

* https://erik-ly.blog.csdn.net/article/details/102925267
* https://zhuanlan.zhihu.com/p/26625249

## 工具

1. VScode(管理git项目)
2. Typore(markdown编辑器)

# 博客美化


## icarus主题

> 链接:[icarus](https://ppoffice.github.io/hexo-theme-icarus/)

### 安装方式

1. 使用git bash,输入如下命令`git clone https://github.com/ppoffice/hexo-theme-icarus.git themes/icarus`,将下载的源码放到`themes`目录下
2. 在hexo文件夹下使用npm安装` npm install -S hexo-theme-icarus`
3. 直接从github仓库中下载源码并且解压放入到hexo的`themes`目录下

### 配置修改

1. 设置主题(以下几种方案任选其一)
   1. 直接修改hexo目录下的`_config.yml`文件,将其中的theme设置为`icarus`
   2. 使用hexo命令修改`hexo config theme icarus`
2. 设置icarus皮肤, 当前支持`default`或者`cyberpunk`两种

```_config.icarus.yml
# 注意了,这个文件需要第一次生成网页的时候才会有,请设置好主题之后重新生成下网页,再到hexo目录寻找这个文件

# 主题,可以使用`default`或者'cyberpunk`
variant: default

# 网站log,后面是网站的图标目录地址,如果不想使用图片,可以使用后面的第二种方式
log: /img/logo.svg
# 方式2
# log:
#    text: 学习笔记

# 导航栏设置
navbar:
    # 导航栏菜单项
    menu:
        主页: /
        存档: /archives
        分类: /categories
        标签: /tags
        关于: /about
        # 上面左边的文字对应的是页面上方菜单栏中的文本,右边的/archivers是hexo/public目录下的文件夹
    # 导航栏右侧的链接
    links:
        GitHub: 'https://github.com'
        Download on GitHub:
            icon: fab fa-github
            url: 'https://github.com/ppoffice/hexo-theme-icarus'
```

3. 其他插件什么的主要参考icarus文档为主


## 其他主题

> Hexo主题网站:<https://hexo.io/themes/>



1. Meadow:<https://garybear.cn/hexo-theme-meadow/#/>