> 记录创建blog的笔记

[toc]

# 1. 准备工作

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

# 2. 创建过程

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
   >   type: git
   >   repo: https://github.com/tom/tom.github.io.git
   >   branch: main
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

4. 生成网页

   > 编辑好设置和博客后,使用`hexo g`和`hexo s`来生成可供本地预览的版本
   >
   > ![image-20210221174147069](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210221174147069.png)
   >
   > 成功后会给出一个链接`http://localhost:4000/`直接复制到浏览器中打开即可看到
   >
   > 如果有出现问题根据具体问题修改.

5. 提交到github

   > 这里需要安装`hexo-deployer-git`
   >
   > 使用`hexo clean` 和`hexo deploy`命令,成功了就可以尝试打开之前提到的链接`https://tom.github.io/`
   >
   > 至于本地的库另外同步到github就可以了(不影响链接的打开)

# 3. 博客美化

> 暂时略过,以后补充

# 4. 一些命令整理

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



# 参考教程

* https://erik-ly.blog.csdn.net/article/details/102925267
* https://zhuanlan.zhihu.com/p/26625249

# 使用到的工具

1. VScode(管理git项目)
2. Typora(markdown编辑器)