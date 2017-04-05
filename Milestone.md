---
layout: page
title: "Milestone"
description: "建站日志 "
header-img: "img/about-bg.jpg"
---


## To do （Features want to change）

### 添加功能
####  标签
- [ ] 添加：标签到文章摘要
- [ ] 添加：标签计数显示
- [ ] 添加：点击标签跳转到该标签下文章列表
- [ ] 添加：夜间模式
- [ ] 添加：Back-to-Top
- [ ] 添加：[in-site-search](http://jekyll.tips)
- [ ] 添加站内文章搜索：
	参考http://chenjun.com/
	https://github.com/Zhu8/zhu8.github.io
- [ ] 添加最近更新文章：
	参考http://9leg.com/

	1.打赏功能（打赏文案根据消费者心理调整）
	4.阅读进度显示

6.上一篇，下一篇文章标题显示
7.阅读人数显示
8.百度谷歌统计
9.多说评论
10.豆瓣书籍页面添加。


### 美化界面
- [ ] 修复：FEATURED TAGS不能显示
- [ ] 更改：显示字体
- [ ] 更改：博客小图标Icon
- [ ] 更改：文章详细阅读页面标签位置
- [ ] 更改：文章发布时间靠右对齐，取消斜体
- [ ] 更改：footer的SNS图标的hover颜色和文案。参考http://chenjun.com/
- [ ] 更改：去除文章摘要的链接

## ChangeLog
1.1.2(2017-03-28)
- [x] 添加<span class="love" style="color:red">❤</span>在 `footer.html` 83 行添加如下代码实现
```html
<span class="love" style="color:red">❤</span>
```

1.1.1(2017-03-24)
- [x] 更改：标签位置到最后（移动post添加：继续阅读/全文
方法：在`index.html` 21行加入
```html
 <a href="{{ post.url | prepend: site.baseurl }}" class="post-read-more">[Read&nbsp;More]</a>
```

1.1.0 (2017-03-23)
- [x] 更改：标签位置到最后（移动post.html 中相应代码）
- [x] 更改：RSS图标位置到最后（移动footer.html 中相应代码）
- [x] 修复：标签不能显示（原因：需要将_post里的文档设置为utf-8格式，自己的SublimeText默认新建的是utf- with-bom格式，故导致解析失败）。
- [x] 更改：文章摘要字体为非斜体(通过(https://voleking.github.io)[https://voleking.github.io]复制替换CSS文件实现)
- [x] 添加：License
- [x] 修改footer显示
- [x] Code Syntax Highlighting
- [x] ~~<del>删除线<del>~~