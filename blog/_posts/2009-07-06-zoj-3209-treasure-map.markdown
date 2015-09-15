---
layout: post
status: publish
published: true
title: ZOJ 3209 Treasure Map
author:
  display_name: twcai
  login: admin
  email: clumsywyvern@gmail.com
  url: http://www.caitengwei.com
author_login: admin
author_email: clumsywyvern@gmail.com
author_url: http://www.caitengwei.com
wordpress_id: 507
wordpress_url: http://child.kilu.de/blog/?p=507
date: '2009-07-06 12:39:40 +0800'
date_gmt: '2009-07-06 04:39:40 +0800'
categories:
- ACM&#47;ICPC
tags:
- Dancing Link
- zoj
comments:
- id: 583
  author: primemusic
  author_email: ecjtuprimemusic@gmail.com
  author_url: http://123
  date: '2010-08-21 06:36:29 +0800'
  date_gmt: '2010-08-21 14:36:29 +0800'
  content: "为什么这行代码\r\nfor(i = r[0]; i; i = r[i]) { \r\n        if(s[i] < mi) { \r\n
    \           mi = s[i]; \r\n            c = i; \r\n        } \r\n    } \r\n改成for(i=l[0];i;i=l[i])就会TLE呢？"
---
<p>精确覆盖问题，看着DLX算法的伪码打的。<br />
以格子为行，矩形为列，构造一个描述覆盖情况的矩形，用DLX算法求解。</p>
<p>其他可以用dancing links求解的题目还有<br />
<a href="http:&#47;&#47;acm.nuaa.edu.cn&#47;acmhome&#47;problemdetail.do?&method=showdetail&id=1267" target="_blank">nuaa 1267 N皇后问题<&#47;a><br&#47;><br />
<a href="http:&#47;&#47;acm.hust.edu.cn&#47;thx&#47;problem.php?id=1017" target="_blank">hust 1017 Exact Cover<&#47;a><br />
23849	clumsydragon	1017	Accepted	1872 kb	256 ms	C++	2253 B	2009-07-10 13:37:56<br&#47;><br />
<a href="http:&#47;&#47;www.spoj.pl&#47;problems&#47;NQUEEN&#47;" target="_blank">spoj 1771 Yet Another N-Queen Problem<&#47;a><br />
2559174	 2009-07-12 07:19:00	CD	Yet Another N-Queen Problem	 accepted	0.36	 2.6M	 C++<br&#47;><br />
<a href="http:&#47;&#47;acm.tju.edu.cn&#47;acm&#47;showp3219.html" target="_blank">tju 3219 Radar<&#47;a><br&#47;><br />
<a href="http:&#47;&#47;acm.fzu.edu.cn&#47;problem.php?pid=1686" target="_blank">fzu 1686 神龙的难题<&#47;a><br&#47;><br />
神龙的难题允许overlap的覆盖，写了3遍还是TLE，先放一放</p>
<p>贴下3209的代码</p>
<pre class="prettyprint" download="3209.cpp">#include <iostream><br />
#include <cstring><br />
using namespace std;</p>
<p>#define sz 451451</p>
<p>int l[sz], r[sz], u[sz], d[sz], y[sz];<br />
int s[961];</p>
<p>int n, m, ret;</p>
<p>inline void remove(const int &c) {<br />
	int i, j;<br />
	r[l[c]] = r[c];<br />
	l[r[c]] = l[c];<br />
	for(i = d[c]; i != c; i = d[i]) {<br />
		for(j = r[i]; j != i; j = r[j]) {<br />
			d[u[j]] = d[j];<br />
			u[d[j]] = u[j];<br />
			s[y[j]] --;<br />
		}<br />
	}<br />
}</p>
<p>inline void resume(const int &c) {<br />
	int i, j;<br />
	for(i = u[c]; i != c; i = u[i]) {<br />
		for(j = l[i]; j != i; j = l[j]) {<br />
			d[u[j]] = j;<br />
			u[d[j]] = j;<br />
			s[y[j]] ++;<br />
		}<br />
	}<br />
	r[l[c]] = c;<br />
	l[r[c]] = c;<br />
}</p>
<p>inline int dfs(int k) {<br />
	if(ret <= k)<br />
		return 0;</p>
<p>	int i, j, c;<br />
	if(r[0] == 0) {<br />
		if(k < ret)<br />
			ret = k;<br />
		return 1;<br />
	}<br />
	int mi = 0x7FFFFFFF;<br />
	for(i = r[0]; i; i = r[i]) {<br />
		if(s[i] < mi) {<br />
			mi = s[i];<br />
			c = i;<br />
		}<br />
	}</p>
<p>	remove(c);<br />
	for(i = d[c]; i != c; i = d[i]) {<br />
		for(j = r[i]; j != i; j = r[j]) {<br />
			remove(y[j]);<br />
		}</p>
<p>		dfs(k + 1);</p>
<p>		for(j = l[i]; j != i; j = l[j]) {<br />
			resume(y[j]);<br />
		}<br />
	}<br />
	resume(c);</p>
<p>	return 0;<br />
}</p>
<p>int main()<br />
{<br />
	int t, tn, tm, t1, t2, pos;<br />
	int i, j, k;<br />
	int x1, y1, x2, y2;<br />
	scanf("%d", &t);</p>
<p>	while(t --) {<br />
		scanf("%d %d %d", &tn, &tm, &n);<br />
		m = tn * tm;<br />
		for(i = 0; i <= m; i++) {<br />
			if(i + 1 > m)<br />
				t1 = 0;<br />
			else<br />
				t1 = i + 1;<br />
			r[i] = t1, l[t1] = i;<br />
			u[i] = i;<br />
			s[i] = 0;<br />
		}</p>
<p>		int hd;<br />
		t2 = m + 1;</p>
<p>		for(i = 1; i <= n; i++) {<br />
			scanf("%d %d %d %d", &x1, &y1, &x2, &y2);<br />
			hd = t2;<br />
			x2 --, y2 --;<br />
			for(j = y1; j <= y2; j++) {<br />
				pos = j * tn + x1 + 1;<br />
				for(k = x1; k <= x2; k++) {<br />
					t1 = t2;<br />
					if(j == y2 && k == x2)<br />
						t2 = hd;<br />
					else<br />
						t2 ++;<br />
					u[t1] = u[pos], d[u[t1]] = t1;<br />
					u[pos] = t1, s[pos] ++;<br />
					r[t1] = t2, l[t2] = t1;<br />
					y[t1] = pos;<br />
					pos++;<br />
				}<br />
			}<br />
			t2 = t1 + 1;<br />
		}</p>
<p>		bool fg = 1;</p>
<p>		for(j = 1; j <= m; j++) {<br />
			if(!s[j]) {<br />
				fg = 0;<br />
				break;<br />
			}<br />
			d[u[j]] = j;<br />
		}</p>
<p>		if(!fg)<br />
			printf("-1\n");<br />
		else {<br />
			ret = 0x7FFFFFFF;<br />
			dfs(0);<br />
			if(ret == 0x7FFFFFFF)<br />
				printf("-1\n");<br />
			else<br />
				printf("%d\n", ret);<br />
		}<br />
	}<br />
	return 0;<br />
}</p>
<p>&#47;*<br />
2</p>
<p>5 10 9<br />
0 0 5 1<br />
0 1 5 2<br />
0 2 5 3<br />
0 3 5 4<br />
0 4 5 5<br />
0 5 5 10<br />
2 3 5 10<br />
0 5 2 10<br />
0 3 2 5</p>
<p>30 30 8<br />
0 0 11 30<br />
11 0 30 11<br />
11 11 20 20<br />
11 20 20 30<br />
20 11 30 30<br />
0 0 11 11<br />
0 11 11 30<br />
0 0 30 20<br />
*&#47;<&#47;pre></p>
