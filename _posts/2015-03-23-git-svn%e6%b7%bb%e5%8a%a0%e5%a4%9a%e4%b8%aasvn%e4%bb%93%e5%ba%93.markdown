---
status: publish
published: true
title: Git svn添加多个svn仓库
author:
  display_name: twcai
  login: admin
  email: clumsywyvern@gmail.com
  url: http://www.caitengwei.com
author_login: admin
author_email: clumsywyvern@gmail.com
author_url: http://www.caitengwei.com
wordpress_id: 1265
wordpress_url: http://caitengwei.com/blog/?p=1265
date: '2015-03-23 07:20:28 +0800'
date_gmt: '2015-03-23 15:20:28 +0800'
categories:
- Geek Stuff
- Programming
tags: []
comments: []
---
<p>很早以前刚学会 Git 的时候就觉得 Subversion 相比 Git 不只是落后，而是落后了一个时代，还在豆瓣上写了篇<a href="http:&#47;&#47;www.douban.com&#47;note&#47;321006700&#47;">日志<&#47;a>吐槽。</p>
<p>虽然公司目前还是以 Subversion 为主流，但幸好有 git-svn 插件，目前日常开发中的 SCM 工作已经可以完全使用 Git 来满足。</p>
<p>Git-svn也非常强大，在项目的一份本地代码中中随手切换任意一个 Subversion branch 也是直接看懵了一起干活的同学。要做到这样只需在用 git-svn clone 代码时加上 -T trunk -b branches 就能自动添加 Subversion 分支到 Git 的远程 branch 中，一般来说用 --stdlayout 可以直接搞定大部分情况。</p>
<p>不过这里要说的另外一种比较奇葩又相对少见的情况，就是 trunk 和 dev branch 并不按照常规分布（常规是指 trunk 在 svn:&#47;&#47;root&#47;project&#47;trunk，branch 在 svn:&#47;&#47;root&#47;project&#47;branches&#47;x_branch）。</p>
<p>最极端的情况是这两个代码库分别位于完全不同的Subversion 代码库，例如 svn:&#47;&#47;root&#47;projectA&#47; 和 svn:&#47;&#47;root&#47;projectB 。</p>
<p>以下就是对应的解决步骤：</p>
<ol>
<li>首先 clone trunk 代码：git svn clone svn:&#47;&#47;root&#47;projectA&#47; project<&#47;li>
<li> 修改 project 目录下的 .git&#47;config ，增加如下内容：
<pre class='prettyprint'>
[svn-remote "dev-branch"]<br />
url = svn:&#47;&#47;root&#47;projectB<br />
fetch = :refs&#47;remotes&#47;git-svn-dev-branch<br />
<&#47;pre><&#47;li></p>
<li>在 project 目录下执行
<pre class="prettyprint">git svn fetch --all<&#47;pre>执行这一步后 git-svn 应会增加一个 remotes&#47;git-svn-dev-branch，并且fetch 了相应的代码<&#47;li></p>
<li>用 git checkout -b dev-branch remotes&#47;git-svn-dev-branch 在本地创建开发分支<&#47;li><br />
<&#47;ol></p>
