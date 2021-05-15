---
title: HowToComment
date: 2021-03-31 23:42:41
tags: ['前端','hexo','gitalk']
categories: ['前端','hexo','gitalk']
---
# ISSUE
diaspora的主题自带gitalk，可是先前一直没有办法显示.
会提示:
>"未找到相关的Issues进行评论 请联系@**** 初始化创建
> ",点击"使用GitHub"登录的时候,跳回网站首页。
    
# 解决
这个问题困扰了我很久，在<a herf="https://blog.csdn.net/Cirzearchenille/article/details/88802534">这个博客</a>里的实例给了解决方法.
问题在于github oauth app的一个选项
Authorization callback URL里应该是填cname的域名

> C A L L B A C K！
> ![callback](/callback.png)

# 实现效果    
总而言之，实现后效果是这样：
![CommentExample](/CommentExample.png)
效果很好，孩子很开心(｡･∀･)ﾉﾞ