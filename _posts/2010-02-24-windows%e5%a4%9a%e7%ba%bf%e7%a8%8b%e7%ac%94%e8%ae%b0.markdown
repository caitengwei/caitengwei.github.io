---
layout: post
status: publish
published: true
title: Windows多线程笔记
author:
  display_name: twcai
  login: admin
  email: clumsywyvern@gmail.com
  url: http://www.caitengwei.com
author_login: admin
author_email: clumsywyvern@gmail.com
author_url: http://www.caitengwei.com
wordpress_id: 665
wordpress_url: http://caitengwei.com/blog/?p=665
date: '2010-02-24 06:02:16 +0800'
date_gmt: '2010-02-24 14:02:16 +0800'
categories:
- Windows
tags:
- Windows API
- "多线程"
comments: []
---
<p>　　最近手头上的东西终于有了一点小突破，这段时间代码上遇到一些问题，有些困了我蛮久。因为之前根本没接触过Windows下面的SDK，Windows核心编程和MSDN都翻了不少，也没少向集训队的学长请教。把这段时间遇到的几个问题整理下，如果能帮到别人就更好了。</p>
<p><strong>子进程的标准输入输出重定向问题：<&#47;strong><br />
　　没有仔细看MSDN的例子和注释，代码写好后，子进程的标准输入输出还是在父进程的命令行下进行。<br />
　　主要原因是 CreateProcess 之前， STARTUPINFO 这个结构不仅仅是指定一下hStdInput, hStdOutput这几个句柄就行了，dwFlags 这个变量需要设置为 STARTF_USESTDHANDLES 才能使以上几个句柄有效。CreateProcess 时，bInheritHandles 需要设置为 TRUE。不仅如此，还有一个容易遗忘的细节，就是 CreateFile 时的 LPSECURITY_ATTRIBUTES 也需要设置为TRUE（同样，CreatePipe 的 SECURITY_ATTRIBUTES 结构的 bInheritHandle 也要设置为TRUE）。</p>
<p><strong>ReadFile堵塞问题：<&#47;strong><br />
　　如果父进程和子进程通过匿名管道来通信，且把子进程的标准输入输出重定向到了管道，那么会碰到下面这个问题。当子进程的输出被存在缓冲区内，没有刷新的话，管道中就一直没有数据，这时候如果用ReadFile读取管道中的数据则ReadFile被堵塞，于是父进程也被堵塞。目前我还没找到在不修改子进程代码的情况下解决这个问题的办法。只能用不使用缓冲区的输出函数来解决。<br />
　　但是如果子进程确实没有输出，那么还是有办法防止父进程被堵塞的，就是事先用 GetFileSize 来检查管道文件容量是否为0。还有一个办法是使用异步I&#47;O来完成通信。</p>
<p><strong>ReadFile读取控制：<&#47;strong><br />
　　如果父进程在一个工作流程中，只需要从子进程发回的信息中读取一行的话，则只让ReadFile读取一个字符的数据，直到碰到换行符为止，Windows下文件的换行符为"\r\n"。</p>
