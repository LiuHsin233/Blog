---
title: 使用Hexo搭建博客
date: 2022-01-17 20:27:31
tags: [Blog]
toc: true
---

# 准备

# 安装Hexo


# Blog搭建

# 主题应用

## 主题

## icarus

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




## 其他主题

> Hexo主题网站:<https://hexo.io/themes/>



1. Meadow:<https://garybear.cn/hexo-theme-meadow/#/>