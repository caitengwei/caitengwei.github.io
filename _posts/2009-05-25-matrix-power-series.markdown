---
layout: post
status: publish
published: true
title: Matrix Power Series
author:
  display_name: twcai
  login: admin
  email: clumsywyvern@gmail.com
  url: http://www.caitengwei.com
author_login: admin
author_email: clumsywyvern@gmail.com
author_url: http://www.caitengwei.com
wordpress_id: 466
wordpress_url: http://child.kilu.de/blog/?p=466
date: '2009-05-25 14:53:23 +0800'
date_gmt: '2009-05-25 06:53:23 +0800'
categories:
- Geek Stuff
tags: []
comments:
- id: 61
  author: JaneRadriges
  author_email: janer@ds4ns1ns2.cn
  author_url: http://www.google.com
  date: '2009-06-14 11:55:03 +0800'
  date_gmt: '2009-06-14 03:55:03 +0800'
  content: Great post! I'll subscribe right now wth my feedreader software!
- id: 62
  author: Tengwei Cai
  author_email: clumsywyvern@gmail.com
  author_url: http://child.kilu.de/blog
  date: '2009-06-15 18:38:36 +0800'
  date_gmt: '2009-06-15 10:38:36 +0800'
  content: 'Thank you. Why don''t you leave your blog website? : )'
---
<p>经小HH大牛指点，重新过了一遍POJ 3233，效率有很大的提高<br />
题目给出一个矩阵A, 要求求出A^1 + A^2 + ... + A^k<br />
这里的做法是构造一个两倍于A的矩阵B[math]matrix{2}{2}{e A 0 A}[&#47;math]<br />
然后求B^K次即可，所要的矩阵位于B的右上角</p>
<pre class="prettyprint">#include <iostream><br />
using namespace std;<br />
&#47;&#47;A^1 + A^2 + ... + A^k<br />
int modnum;</p>
<p>class matrix{<br />
public :<br />
	int rw, cn, ma[65][65];</p>
<p>	matrix() {<br />
		rw = 0, cn = 0;<br />
	}</p>
<p>	matrix(int x, int y) {<br />
		int i, j;<br />
		rw = x;<br />
		cn = y;<br />
		for(i = 0; i < rw; i++) {<br />
			for(j = 0; j < cn; j++) { ma[i][j] = 0; }<br />
		}<br />
	}</p>
<p>	matrix(const matrix &x) {<br />
		int i, j;<br />
		rw = x.rw, cn = x.cn;<br />
		for(i = 0; i < rw; i++){<br />
			for(j = 0; j < cn; j++) { ma[i][j] = x.ma[i][j]; }<br />
		}<br />
	}</p>
<p>	matrix operator*(matrix &x)<br />
	{<br />
		int i, j, k;<br />
		matrix ret(cn, x.rw);<br />
		for(i = 0; i < rw ; i++) {<br />
			for(j = 0; j < x.cn ; j++) {<br />
				for(k = 0; k < cn; k++) {<br />
					ret.ma[i][j] += ma[i][k] * x.ma[k][j];<br />
					if(ret.ma[i][j] >= modnum)<br />
						ret.ma[i][j] %= modnum;<br />
				}<br />
			}<br />
		}<br />
		return ret;<br />
	}</p>
<p>	matrix power(int x) {<br />
		matrix ret(rw, cn);<br />
		if(x == 1) return *this;<br />
		if(x == 2) {<br />
			int i, j ,k;<br />
			for(i = 0; i < rw; i++) {<br />
				for(j = 0; j < cn; j++) {<br />
					for(k = 0; k < cn; k++) {<br />
						ret.ma[i][j] += ma[i][k] * ma[k][j];<br />
						if(ret.ma[i][j] >= modnum)<br />
							ret.ma[i][j] %= modnum;<br />
					}<br />
				}<br />
			}<br />
		}<br />
		else if(!(x & 1)) {<br />
			ret = this->power(x >> 1);<br />
			ret = ret.power(2);<br />
		}<br />
		else {<br />
			ret = this->power(x >> 1);<br />
			ret = ret.power(2);<br />
			ret = ret * (*this);<br />
		}<br />
		return ret;<br />
	}</p>
<p>	inline matrix operator+= (const matrix &x) {<br />
		int i, j;<br />
		for(i = 0; i < rw; i++) {<br />
			for(j = 0; j < cn; j++)<br />
			{<br />
				ma[i][j] += x.ma[i][j];<br />
				if(ma[i][j] >= modnum)<br />
					ma[i][j] %= modnum;<br />
			}<br />
		}<br />
		return *this;<br />
	}</p>
<p>	inline matrix operator = (const matrix &x) {<br />
		int i, j;<br />
		rw = x.rw, cn = x.cn;<br />
		for(i = 0; i < rw; i++) {<br />
			for(j = 0; j < cn; j++) { ma[i][j] = x.ma[i][j]; }<br />
		}<br />
		return *this;<br />
	}<br />
};</p>
<p>int main()<br />
{<br />
	int n, m, k;<br />
	int i, j;<br />
	while(scanf("%d %d %d", &n, &k, &m) != EOF) {<br />
		matrix org(2 * n, 2 * n), ret(2 * n, 2 * n);<br />
		for(i = 0; i < n; i++) {<br />
			org.ma[i][i] = 1;<br />
			for(j = 0; j < n; j++) {<br />
				scanf("%d", &org.ma[i][n + j]);<br />
				org.ma[n + i][n + j] = org.ma[i][n + j];<br />
			}<br />
		}<br />
		modnum = m;<br />
		ret = org.power(k);<br />
		for(i = 0; i < n; i++) {<br />
			for(j = 0; j < n; j++) {<br />
				if(j) printf(" ");<br />
				printf("%d", ret.ma[i][n + j]);<br />
			}<br />
			printf("\n");<br />
		}<br />
	}<br />
	return 0;<br />
}<&#47;pre></p>
