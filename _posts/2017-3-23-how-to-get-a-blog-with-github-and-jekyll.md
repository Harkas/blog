---
layout:     post
title:      "如何用Github和Jekyll建立一个个人博客"
subtitle:   "个人博客建立方法"
date:       2017-03-23
author:     "Harkas"
tags:
    - 个人博客
    - Github
    - Jekyll
    - Blog
---

# Github注册
# 新建仓库
# 重命名仓库
# Fork
# 认识Jekyll
## jekyll是什么？
```
Jekyll是一个简洁的、特别针对博客平台的静态网站生成器。它使用一个模板目录作为网站布局的基础框架，并在其上运行Textile、Markdown或Liquid标记语言的转换器，最终生成一个完整的静态Web站点，可以被放置在Apache或者你喜欢的其他任何Web服务器上。它同时也是GitHub Pages、一个由GitHub提供的用于托管项目主页或博客的服务，在后台所运行的引擎。
```
## Jekyll的主要结构及功能
一个典型的Jekyll站点通常具有如下结构：
```
  _config.yml
  _layouts
  _posts
  _index.html
```
*  _config.yml
jekyll配置文件
*  _layouts
文件夹内存放默认可引用的模板
*  _posts
文件夹内存放发布的文章
*  _index.html
文章首页




# 改造
添加文章统计功能
参考页面：[http://wyh.life/archive]http://wyh.life/archive
# 其他
## 文章内页添加音乐并自动播放
<audio autoplay="autoplay" controls="controls">
<source src="http://link.hhtjim.com/163/413812448.mp3" type="audio/mpeg">
</audio>
代码如下：
```html
<audio autoplay="autoplay" controls="controls">
<source src="http://link.hhtjim.com/163/413812448.mp3" type="audio/mpeg">
</audio>
```

# 写作
