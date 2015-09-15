---
layout: post
status: publish
published: true
title: HDOJ 2360 Word Ladder
author:
  display_name: twcai
  login: admin
  email: clumsywyvern@gmail.com
  url: http://www.caitengwei.com
author_login: admin
author_email: clumsywyvern@gmail.com
author_url: http://www.caitengwei.com
wordpress_id: 19
wordpress_url: http://child.kilu.de/blog/?p=19
date: '2008-08-28 21:55:28 +0800'
date_gmt: '2008-08-28 13:55:28 +0800'
categories:
- ACM&#47;ICPC
tags:
- BFS
- "路径保存"
comments: []
---
<p>BFS+路径保存即可。枚举所有单词作为&ldquo;第一阶&rdquo;，找只差一个字母的单词扩展节点，记录该单词前驱，当扩展的单词和第一个单词完全不同时结束BFS。枚举N次，每次碰到比原有情况更短的&ldquo;阶梯&rdquo;，就把路径保存下来。题目要求多结果时按字典序输出，只要在读入单词后，对所有单词按字典序排序就可以啦。<br />
有一个比较重要的优化就是对所有单词进行预处理，把只相差一个字母的一对单词和完全不同的一对单词记录下来(我用邻接矩阵保存)，然后在进行bfs。在枚举过程中，碰到有阶梯数刚好为l+1的情况，就可以直接结束枚举的过程了(不可能有比l+1更短的情况)，由于数据量不大，手打快排和qsort()没太大区别。</p>
<pre class="prettyprint">#include <iostream><br />
#include <cstdlib><br />
#include <cstring><br />
using namespace std;<br />
#define OVER 70000<br />
int t,n,l;<br />
char word[101][MAX];<br />
int path[101],root[101];<br />
bool one[110][110],tol[110][110];<br />
bool hash[101],h[27];<br />
struct node{<br />
	int num;<br />
	int cost;<br />
};<br />
node now,next;<br />
node que[70001];<br />
int ql,qh;</p>
<p>inline void QuickSort(int low, int high)<br />
{<br />
	char key[MAX];<br />
	int LOW,HIGH;</p>
<p>	if(low>high) return ;<br />
	strcpy(key,word[low]);<br />
	LOW=low;HIGH=high;<br />
	while(low<high)<br />
	{<br />
		while(high>low)<br />
		{<br />
			if(strcmp(key,word[high])>0)<br />
			{<br />
				strcpy(word[low],word[high]);<br />
				low++;break;<br />
			}<br />
			high--;<br />
		}<br />
		while(low<high)<br />
		{<br />
			if(strcmp(key,word[low])<0)<br />
			{<br />
				strcpy(word[high],word[low]);<br />
				high--;break;<br />
			}<br />
			low++;<br />
		}<br />
	}<br />
	strcpy(word[low],key);<br />
	QuickSort(LOW,low-1);<br />
	QuickSort(low+1,HIGH);<br />
}</p>
<p>&#47;&#47;inline int cmp(const void *a,const void *b)<br />
&#47;&#47;{<br />
&#47;&#47;	char* c=(char *)a;<br />
&#47;&#47;	char* d=(char *)b;<br />
&#47;&#47;	return strcmp(c,d);<br />
&#47;&#47;}</p>
<p>inline int comp(const int &x,const int &y)<br />
{<br />
	int c,flag;<br />
	memset(h,0,sizeof(h));c=0;<br />
	for(int i=0;i<l;i++)<br />
	{<br />
		flag=0;<br />
		for(int j=0;j<l;j++)<br />
			if(!h[j] && word[x][i]==word[y][j])<br />
			{c++;h[j]=1;break;}<br />
	}<br />
	return c;<br />
}</p>
<p>inline int bfs(const int &x)<br />
{<br />
	ql=0;qh=0;<br />
	now.num=x;now.cost=1;hash[x]=1;<br />
	que[qh++]=now;if(qh>OVER) qh%=OVER;<br />
	while(ql<qh)<br />
	{<br />
		now=que[ql++];if(ql>OVER) ql%=OVER;<br />
		if(tol[now.num][x]==1) return now.cost;<br />
		for(int i=0;i<n;i++)<br />
		{<br />
			if(hash[i]) continue;<br />
			if(one[now.num][i]==1)<br />
			{<br />
				next.num=i;next.cost=now.cost+1;<br />
				que[qh++]=next;if(qh>OVER) qh%=OVER;<br />
				hash[i]=1;root[i]=now.num;<br />
			}<br />
		}<br />
	}<br />
	return 0;<br />
}</p>
<p>int main()<br />
{<br />
	int minpath,tem;</p>
<p>	scanf("%d",&t);<br />
	while(t--)<br />
	{<br />
		scanf("%d %d",&n,&l);<br />
		for(int i=0;i<n;i++)<br />
			scanf("%s",word[i]);<br />
		&#47;&#47;qsort(word,n,sizeof(word[0]),cmp);<br />
		QuickSort(0,n-1);<br />
		memset(tol,0,sizeof(tol));<br />
		memset(one,0,sizeof(one));<br />
		for(int i=0;i<n-1;i++)<br />
			for(int j=i+1;j<n;j++)<br />
			{<br />
				tem=comp(i,j);<br />
				if(tem==l-1) {one[i][j]=1;one[j][i]=1;}<br />
				if(tem==0) {tol[i][j]=1;tol[j][i]=1;}<br />
			}<br />
		minpath=200;<br />
		for(int i=0;i<n && minpath!=l+1;i++)<br />
		{<br />
			memset(hash,0,sizeof(hash));<br />
			memset(root,-1,sizeof(root));<br />
			path[0]=bfs(i);<br />
			if(path[0]>l && path[0]<minpath)<br />
			{<br />
				minpath=path[0];<br />
				for(int j=1;j<=minpath;j++)<br />
				{path[j]=now.num;now.num=root[now.num];}<br />
			}<br />
		}<br />
		for(int i=minpath;i>0;i--)<br />
		{<br />
			if(i==1) printf("%sn",word[path[i]]);<br />
			else printf("%s ",word[path[i]]);<br />
		}<br />
	}<br />
	return 0;<br />
}<&#47;pre></p>
