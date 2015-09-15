---
layout: post
status: publish
published: true
title: HDOJ  2428  Stars
author:
  display_name: twcai
  login: admin
  email: clumsywyvern@gmail.com
  url: http://www.caitengwei.com
author_login: admin
author_email: clumsywyvern@gmail.com
author_url: http://www.caitengwei.com
wordpress_id: 100
wordpress_url: http://child.kilu.de/blog/?p=100
date: '2008-10-22 23:54:30 +0800'
date_gmt: '2008-10-22 15:54:30 +0800'
categories:
- ACM&#47;ICPC
tags:
- HDOJ
- "成都网络赛"
comments: []
---
<p>成都网络赛第一题，比赛中是Teddy和 WYB一起A掉了。<br />
比赛中觉得对这题挺有想法，现在拿回来做WA了20次&hellip;&hellip;不过好歹是过掉了，离散化用的不多是主要原因，层出不穷的小错误也让我改到崩溃，看来我今天脑子被撞坏了。<br />
我的做法是，先把出现的坐标值全部插入到数组中，排序后离散化，并替代原来的点的坐标，用hash标记，但是这儿有一个要注意的地方(就是我WA这么多次的原因)，原来的值一定不能丢掉，这在后面差值的比较中会用到。接着按坐标轴上从上往下，从左到右的顺序排序，然后枚举不同的两个点，看是否能够作为一个正方形的对角线，如果可以，那么看看另外两个点有没有被hash过&hellip;&hellip;<br />
贴下代码:</p>
<pre class="prettyprint">#include <iostream><br />
#include <algorithm><br />
using namespace std;<br />
struct node{<br />
	int i;<br />
	int j;<br />
};<br />
node d[1011];<br />
int n;<br />
int ls[2012];<br />
int tt[20100];<br />
int hash[2011][2011];</p>
<p>inline bool cmp(node x, node y)<br />
{<br />
	if(x.i == y.i)<br />
		return x.j < y.j;<br />
	else<br />
		return x.i > y.i;<br />
}</p>
<p>int main()<br />
{<br />
	int t, i, j, k, ret, cas = 0;<br />
	scanf("%d", &t);<br />
	while(t--)<br />
	{<br />
		scanf("%d", &n);<br />
		cas ++;<br />
		if(n < 4) {<br />
			for(i = 0; i < n; i++)<br />
				scanf("%d %d", &d[i].j, &d[i].i);<br />
			printf("0n");<br />
			continue;<br />
		}<br />
		j = 0;<br />
		for(i = 0; i < n; i++)<br />
		{<br />
			scanf("%d %d", &d[i].j, &d[i].i);<br />
			ls[j++] = d[i].i;<br />
			ls[j++] = d[i].j;<br />
		}<br />
		sort(ls, ls + j);<br />
		k = 0;<br />
		memset(tt, -1, sizeof(tt));<br />
		for(i = 0; i < j; i++)<br />
		{<br />
			if(tt[ls[i] + 10000] >= 0)<br />
				continue;<br />
			else<br />
			{<br />
				tt[ls[i] + 10000] = k;<br />
				ls[k] = ls[i];<br />
				k++;<br />
			}<br />
		}<br />
		for(i = 0; i < n; i++)<br />
		{<br />
			d[i].i = tt[d[i].i + 10000];<br />
			d[i].j = tt[d[i].j + 10000];<br />
			hash[d[i].i][d[i].j] = cas;<br />
		}<br />
		sort(d, d+n, cmp);<br />
		ret = 0;<br />
		for(i = 0; i < n; i++)<br />
			for(j = i + 1; j < n; j++)<br />
			{<br />
				if(d[i].i == d[j].i || d[i].j >= d[j].j)<br />
					continue;<br />
				if((ls[d[i].i] - ls[d[j].i]) != (ls[d[j].j] - ls[d[i].j]))<br />
					continue;<br />
				if(hash[d[i].i][d[j].j] == cas && hash[d[j].i][d[i].j] == cas)<br />
					ret++;<br />
			}<br />
		printf("%dn", ret);<br />
	}<br />
	return 0;<br />
}<&#47;pre></p>
