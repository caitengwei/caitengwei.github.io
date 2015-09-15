---
layout: post
status: publish
published: true
title: TopCoder Competetion Arena无法启动
author:
  display_name: twcai
  login: admin
  email: clumsywyvern@gmail.com
  url: http://www.caitengwei.com
author_login: admin
author_email: clumsywyvern@gmail.com
author_url: http://www.caitengwei.com
wordpress_id: 529
wordpress_url: http://child.kilu.de/blog/?p=529
date: '2009-07-24 16:26:30 +0800'
date_gmt: '2009-07-24 08:26:30 +0800'
categories:
- TopCoder
tags:
- Arena
- TopCoder
comments:
- id: 2730
  author: acBool
  author_email: wmengn@gmail.com
  author_url: ''
  date: '2012-07-08 23:42:02 +0800'
  date_gmt: '2012-07-09 07:42:02 +0800'
  content: "如何删除那些东西？烦请详细告之。"
- id: 2734
  author: twcai
  author_email: clumsywyvern@gmail.com
  author_url: http://www.caitengwei.com
  date: '2012-07-14 23:20:16 +0800'
  date_gmt: '2012-07-15 07:20:16 +0800'
  content: '@<a href="#comment-2730" rel="nofollow">acBool <&#47;a>直接用文本编辑器打开那个jnlp文件，把jnlp标签中的属性删掉就可以了啊'
---
<p>上午CH大牛安装了win7以后，发现TC的Arena启动不了了。<br />
每次打开Arena，java就会弹出一个无法启动的对话框，说是缺少必需的<jnlp>标签。我搜了一下，找到了高杰的博客，原来他也碰到过这个问题.(我在好多台不同的机器上用过tc, 从没碰到过，看来是人品好啊，哈哈)<br />
据高大牛说，这个问题只要用
<pre>javaws -wait xxx.jnlp<&#47;pre>就可以搞定了。我试了一下，仍旧不行。<br />
继续找，看到有人在csdn上说删掉xxx.jnlp文件中第一行xml的声明&hellip;&hellip;感觉不搭界，还是试了一下，问题依旧。<br />
接着我看到第二行就是<jnlp> 标签，明明在么，干嘛说缺少这个标签 -_-!<br />
呃，下一秒我没有原因的猜了一下：&ldquo;会不会是标签中长长的参数有问题？&rdquo; 于是删之，arena顺利启动。</p>
<p>本人对java没什么浓厚的兴趣，随便在网上搜了一下原因但无果，于是不再深究。不过还是把过程挂到博客上，给碰到相同问题的coder参考。</p>
