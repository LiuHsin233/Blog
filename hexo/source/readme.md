# 关于目录

1. `_posts`文件夹存放网站的文章,`assets`用于存放网站的资源

2. 网站中某些图片资源主要存放在`assets`文件夹中,比如配置文件`_config.icarus.yml`中的支付宝二维码就存放在这里,使用方式`/assets/img/alipay.jpg`,从`assets`开始写

3. 对于`_posts`文件夹中的内容,`md`格式文件后面会渲染成单独的文章,与`md`文件同名的文件夹中存放的文章中所使用的图片,直接写文件名就是在这个文件夹下图片

   ```yml
   -- 以上需要修改设置
   -- _config.yml
   post_asset_folder: true
   marked:
     prependRoot: true
     postAsset: true
   ```

   参考内容:[hexo资源文件夹](https://hexo.io/zh-cn/docs/asset-folders.html)

