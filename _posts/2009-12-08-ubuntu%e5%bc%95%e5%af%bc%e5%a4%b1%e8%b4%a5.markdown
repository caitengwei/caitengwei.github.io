---
status: publish
published: true
title: ubuntu引导失败
author:
  display_name: twcai
  login: admin
  email: clumsywyvern@gmail.com
  url: http://www.caitengwei.com
author_login: admin
author_email: clumsywyvern@gmail.com
author_url: http://www.caitengwei.com
wordpress_id: 624
wordpress_url: http://child.kilu.de/blog/?p=624
date: '2009-12-08 15:05:03 +0800'
date_gmt: '2009-12-08 07:05:03 +0800'
categories:
- Ubuntu Notes
tags:
- Busybox
- Grub
- Menu.lst
- Ubuntu
- "引导"
comments: []
---
<p>　　昨天面试前想进ubuntu复习一下自己写的shell脚本，却发现引导ubuntu失败了。ubuntu的图标出现后就黑屏，按任意键，屏幕上就出现提示:</p>
<pre>Gave up waiting for root device.<br />
.<br />
.<br />
.<br />
Alert &#47;dev&#47;disk&#47;by-uuid&#47;... doesn't exist ...</p>
<p>BusyBox ....<br />
.<br />
(initramfs)_<&#47;pre></p>
<p>　　这个问题上学期曾经碰到过的，当时在网上搜索无果，于是重装了系统。但问题是现在我的ubuntu下已经存了很多代码，就算无法修复，我至少也得把代码给备份回来。<br&#47;><br />
　　于是就开始在网上瞎逛，关于这个问题众说纷纭，有说内核损坏的，有说系统来不及加载驱动程序的，但是感觉都不靠谱。我用实验室电脑上的ubuntu9.10制作了个启动盘，用Palimpsest磁盘实用工具查看硬盘，发现安装ubuntu那一块分区被标注为&ldquo;未知、无法辨识&rdquo;了。这种问题我从没碰到过，上网找了个磁盘修复的命令fsck，检查了一遍这个分区 "&#47;dev&#47;sda6"，接着mount到&#47;foo，发现访问没问题，于是赶紧先备份了代码。<br&#47;><br />
　　重新启动以后，ubuntu仍然启动失败，郁闷的是"&#47;dev&#47;sda6"明明可以访问啊&hellip;&hellip;我重新用启动盘挂载了该分区，查看&#47;boot&#47;grub&#47;menu.lst文件，发现有件奇怪的事情，menu.lst中的example的kernel，有一句关于root的信息 "root=&#47;dev&#47;hda2"。而实际启动时，kernel项则把一个很奇怪的叫uuid的字符串给了root。<br&#47;><br />
　　我觉得直接用分区路径来启动是肯定可行的，于是把原来的kernel行注释，加了一行
<pre>kernel		&#47;boot&#47;vmlinuz-2.6.31-14-generic root=&#47;dev&#47;sda6 ro locale=zh_CN quiet single<&#47;pre><br />
　　重启后，终于进入了9.10的登录界面！<br &#47;><br />
　　重新用磁盘实用工具检查，ubuntu所在分区还是未知，用命令
<pre>ls -al &#47;dev&#47;disk&#47;by-uuid<&#47;pre>查看所有分区的uuid,却发现没有"&#47;dev&#47;sda6"。使用失效的uuid，这就是引导失败的原因所在啊。稍微google了下，据介绍uuid可以不受硬盘中其他分区的变化影响，因此比直接用分区路径安全，但前提是分区大小不能改变。至于怎么把ubuntu所在分区恢复为出问题以前的状态我也不是很清楚，希望能在论坛中尽快找到答案吧。</p>
<p>Update: 在Ubuntu中文社区上找到了答案，用fsck命令扫描并修复文件系统后，ubuntu所在分区就恢复正常了。</p>
