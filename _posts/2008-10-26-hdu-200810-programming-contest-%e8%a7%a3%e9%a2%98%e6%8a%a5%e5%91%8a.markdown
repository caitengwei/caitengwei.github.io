---
layout: post
status: publish
published: true
title: HDU 2008&#039;10 Programming Contest 解题报告
author:
  display_name: twcai
  login: admin
  email: clumsywyvern@gmail.com
  url: http://www.caitengwei.com
author_login: admin
author_email: clumsywyvern@gmail.com
author_url: http://www.caitengwei.com
excerpt: |
  暑假集训后第一场月赛，可惜我没的参加。那天晚上把所有题（2519-2527）A完了，估计了一下，即使参加也来不及做完吧。
  贴下我的解题报告，大牛不要笑偶：
  新生晚会：题目比较直白，排列组合问题，求 Cn取m ，这个一般推荐利用杨辉三角来求解，如果用公式求，中间要注意约分，否则64位整数也不够用。

  我是菜鸟：等差公式求和，结果为 N^2。

  反素数：预处理，用筛法求因子数，然后在a -> b之间扫描一遍，记录最小值。

  A Simple Problem : 模拟题+hash。模拟手算除法的过程，即每次把被除数乘十，输出除以除数所得的商(整数除法)，然后把余数hash，并作为被除数继续计算，直到出现重复的被除数为止(说明第一个循环结结束)。注意n不一定是一个正数。
wordpress_id: 131
wordpress_url: http://child.kilu.de/blog/?p=131
date: '2008-10-26 23:55:01 +0800'
date_gmt: '2008-10-26 15:55:01 +0800'
categories:
- ACM&#47;ICPC
tags:
- HDOJ
- "月赛"
comments:
- id: 30
  author: Mark
  author_email: gan-676@163.com
  author_url: http://www.december.kilu.de/blog/
  date: '2008-10-30 23:29:46 +0800'
  date_gmt: '2008-10-30 15:29:46 +0800'
  content: "我是真的来膜拜的,代表广大菜鸟~"
- id: 31
  author: "已经换域名->http:&#47;&#47;www.december.kilu.de&#47;blog&#47; at My December"
  author_email: ''
  author_url: http://www.rookieway.kilu.de/blog/?p=201
  date: '2008-11-04 20:41:59 +0800'
  date_gmt: '2008-11-04 12:41:59 +0800'
  content: "[...] baichi [...]"
---
<p>暑假集训后第一场月赛，可惜我没的参加。那天晚上把所有题（2519-2527）A完了，估计了一下，即使参加也来不及做完吧。<br />
贴下我的解题报告，大牛不要笑偶：<br />
新生晚会：题目比较直白，排列组合问题，求 Cn取m ，这个一般推荐利用杨辉三角来求解，如果用公式求，中间要注意约分，否则64位整数也不够用。</p>
<p>我是菜鸟：等差公式求和，结果为 N^2。</p>
<p>反素数：预处理，用筛法求因子数，然后在a -> b之间扫描一遍，记录最小值。</p>
<p>A Simple Problem : 模拟题+hash。模拟手算除法的过程，即每次把被除数乘十，输出除以除数所得的商(整数除法)，然后把余数hash，并作为被除数继续计算，直到出现重复的被除数为止(说明第一个循环结结束)。注意n不一定是一个正数。<br />
<a id="more"></a><a id="more-131"></a><br />
Sort Again : O(n^2)求出所有组合数，并在数组中hash掉，然后从小到大一直扫描一直到找到第K个大的组合数为止。</p>
<p>矩形A+B : 容易推出 高为n，宽为m时的矩形数为 (n*(n+1)&#47;2 ) * (m * (m+1) &#47; 2)。</p>
<p>Clone Wars : 递推题，我出的哈哈。不过大家都说题目描述太挫，第一名更是A完8题，提前二十分钟走人，直接无视我啦&hellip;&hellip;我的做法是从第0天开始，把当天(第i天)诞生的克隆人的伤害和繁殖效果加到接下来的(i+1)到(i+d)天上，递推至第x天，需要64位整型。</p>
<p>浪漫手机：模拟题。第i行j列的格子可以通过第i - 1行 j &ndash; 1到 j +1列的格子情况来推出。题目给出的模式串把上面一排转化为二进制hash比较方便。</p>
<p>Safe or Unsafe : 一道比较直白的求哈夫曼树权值问题，求出整棵树的权值，与给定值比较。</p>
