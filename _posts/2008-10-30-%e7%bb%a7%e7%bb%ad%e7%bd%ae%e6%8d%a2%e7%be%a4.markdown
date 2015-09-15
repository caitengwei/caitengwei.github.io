---
layout: post
status: publish
published: true
title: "继续置换群"
author:
  display_name: twcai
  login: admin
  email: clumsywyvern@gmail.com
  url: http://www.caitengwei.com
author_login: admin
author_email: clumsywyvern@gmail.com
author_url: http://www.caitengwei.com
wordpress_id: 140
wordpress_url: http://child.kilu.de/blog/?p=140
date: '2008-10-30 15:46:10 +0800'
date_gmt: '2008-10-30 07:46:10 +0800'
categories:
- ACM&#47;ICPC
tags:
- POJ
- "置换群"
comments:
- id: 36
  author: Mark
  author_email: gan-676@163.com
  author_url: http://www.december.kilu.de/blog/
  date: '2008-11-03 23:45:27 +0800'
  date_gmt: '2008-11-03 15:45:27 +0800'
  content: "待续...你倒是贴点东西出来我看下啊.....-_-.."
- id: 37
  author: "灰色橙子"
  author_email: chenghui2050@qq.com
  author_url: http://hi.baidu.com/chenghui2050
  date: '2008-10-31 14:06:51 +0800'
  date_gmt: '2008-10-31 06:06:51 +0800'
  content: |-
    我知道你是谁了，二班的高杰！
    My December: Partner
    WYB1989: Partner ^^

    --------一个甘露，一个云斌，既然是搭档那就是高杰
    没猜错吧
---
<p>奉Teddy大牛暨队长之命，我这个离散白痴重新开始置换群专题。</p>
<p>先链接一下以前的关于这个专题的日志：<a href="http:&#47;&#47;child.kilu.de&#47;blog&#47;?p=25" target="_blank">置换群及P&oacute;lya定理<&#47;a></p>
<p>pku1721 CARDS : 这道题我用模拟置换群的平方运算，找出循环次数n，再顺推 n - s(mod n) 次这样的笨办法过的。最好的方法是用置换群的分数幂运算(这个还在学习中，看得相当头大)，在效率上会有很大的差别，不过POJ数据偏弱了。<br />
贴下代码：</p>
<pre class="prettyprint">#include <iostream><br />
using namespace std;</p>
<p>int dor[1010];<br />
int d[2][1010];</p>
<p>int main()<br />
{<br />
	int n, s, i, j;<br />
	int f, nf, np, count;</p>
<p>	while(scanf("%d %d", &n, &s) != EOF)<br />
	{<br />
		for(i = 1; i <= n; i++)<br />
		{<br />
			scanf("%d", &dor[i]);<br />
			d[0][i] = dor[i];<br />
		}<br />
		f = 0;<br />
		np = 0;<br />
		count = 0;<br />
		while(1)<br />
		{<br />
			nf = 1 - f;<br />
			np = 1;<br />
			for(i = 1; i <= n; i++)<br />
				if(d[f][i] != dor[i])<br />
				{<br />
					np = 0;<br />
					break;<br />
				}<br />
			if(np == 1 && count) break;<br />
			for(i = 1; i <= n; i++)<br />
				d[nf][i] = d[f][d[f][i]];<br />
			f = nf;<br />
			count++;<br />
		}</p>
<p>		s = count - s % count;<br />
		f = 0;<br />
		for(i = 1; i <= n; i++)<br />
			d[0][i] = dor[i];</p>
<p>		for(i = 0 ; i < s; i++)<br />
		{<br />
			nf = 1 - f;<br />
			for(j = 1; j <= n; j++)<br />
				d[nf][j] = d[f][d[f][j]];<br />
			f = nf;<br />
		}</p>
<p>		for(i = 1; i <= n; i++)<br />
			printf("%dn", d[nf][i]);<br />
	}<br />
	return 0;<br />
}<&#47;pre></p>
