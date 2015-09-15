---
layout: post
status: publish
published: true
title: TOJ 2919 Alphanumeric Expression
author:
  display_name: twcai
  login: admin
  email: clumsywyvern@gmail.com
  url: http://www.caitengwei.com
author_login: admin
author_email: clumsywyvern@gmail.com
author_url: http://www.caitengwei.com
wordpress_id: 65
wordpress_url: http://child.kilu.de/blog/?p=65
date: '2008-09-11 02:16:54 +0800'
date_gmt: '2008-09-10 18:16:54 +0800'
categories:
- ACM&#47;ICPC
tags:
- "栈"
- "表达式"
comments:
- id: 8
  author: Mark
  author_email: gan-676@163.com
  author_url: http://www.december.kilu.de/blog
  date: '2008-09-11 09:19:39 +0800'
  date_gmt: '2008-09-11 01:19:39 +0800'
  content: YM YM...
---
<p>用栈模拟下，数据结构课上王立波老师讲过思想，就是把一个可以计算的表达式 a (op) b ,拆成操作数和操作符分别入栈，如果表达式中的下一个操作符的优先级比栈顶的操作符高，则继续入栈，否则计算栈顶的两个操作数和操作符，再把结果压入操作数的栈中，碰到括号，我就用dfs来求括号中的子表达式。<br />
第一次写，还是在比赛中写，居然就过了，还是蛮高兴的。由于题目说在中间过程中不会出现负数的情况，因此这个代码并没有对负数的处理。^ ^</p>
<pre class="prettyprint">#include<iostream><br />
#include<cstring><br />
using namespace std;<br />
#define MAX 200<br />
int ops[MAX];<br />
int nos[MAX];<br />
char fom[MAX];<br />
int top,tno,ind,len;</p>
<p>inline void dfs(int &index)<br />
{<br />
	bool enflag=0;<br />
	bool nflag;<br />
	int ortop,ortno;<br />
	int nop,op;<br />
	int no1,no2;<br />
	int t1;<br />
	ortop=top;ortno=tno;ind++;<br />
	while(!enflag)<br />
	{<br />
		if(fom[index]==')') {nflag=1;enflag=1;ind++;}<br />
		else if(fom[ind]>='0' && fom[ind]<='9')<br />
		{<br />
			t1=fom[ind++]-'0';<br />
			while(fom[ind]>='0' && fom[ind]<='9')<br />
			{<br />
				t1*=10;<br />
				t1+=fom[ind++]-'0';<br />
			}<br />
			if(t1>26) t1%=26;<br />
			nos[tno++]=t1;nflag=1;<br />
		}<br />
		else if(fom[ind]>='A' && fom[ind]<='Z')<br />
		{nos[tno++]=fom[ind++]-'A'+1;nflag=1;}<br />
		else if(fom[ind]=='(')<br />
		{dfs(ind);nflag=1;}<br />
		else if(fom[ind]=='+')<br />
		{ops[top++]=0;ind++;nflag=0;}<br />
		else if(fom[ind]=='-')<br />
		{ops[top++]=1;ind++;nflag=0;}<br />
		else if(fom[ind]=='*')<br />
		{ops[top++]=2;ind++;nflag=0;}<br />
		else if(fom[ind]=='&#47;')<br />
		{ops[top++]=3;ind++;nflag=0;}<br />
		else {ind++;continue;}<br />
		while(tno>=ortno+2 && top>=ortop+1)<br />
		{<br />
			if(!nflag) break;<br />
			switch(fom[ind])<br />
			{<br />
			case '+':nop=0;break;<br />
			case '-':nop=1;break;<br />
			case '*':nop=2;break;<br />
			case '&#47;':nop=3;break;<br />
			default:nop=0;break;<br />
			}<br />
			op=ops[top-1];<br />
			if((op&#47;2)>=(nop&#47;2))<br />
			{<br />
				top--;<br />
				no2=nos[--tno];<br />
				no1=nos[--tno];<br />
				switch(op)<br />
				{<br />
				case 0:no1=no1+no2;break;<br />
				case 1:no1=no1-no2;break;<br />
				case 2:no1=no1*no2;break;<br />
				case 3:no1=no1&#47;no2;break;<br />
				}<br />
				if(no1>26) no1%=26;<br />
				nos[tno++]=no1;<br />
			}<br />
			else nflag=0;<br />
		}<br />
	}<br />
}</p>
<p>int main()<br />
{<br />
	int nop,op;<br />
	int no1,no2;<br />
	int t1,ret;<br />
	bool nflag;<br />
	while(gets(fom))<br />
	{<br />
		len=strlen(fom);<br />
		ind=0;top=0;tno=0;<br />
		while(ind<=len)<br />
		{<br />
			if(ind==len) {nflag=1;ind++;}<br />
			else if(fom[ind]>='0' && fom[ind]<='9')<br />
			{<br />
				t1=fom[ind++]-'0';<br />
				while(fom[ind]>='0' && fom[ind]<='9')<br />
				{<br />
					t1*=10;<br />
					t1+=fom[ind++]-'0';<br />
				}<br />
				nos[tno++]=t1;nflag=1;<br />
			}<br />
			else if(fom[ind]>='A' && fom[ind]<='Z')<br />
			{nos[tno++]=fom[ind++]-'A'+1;nflag=1;}<br />
			else if(fom[ind]=='(')<br />
			{dfs(ind);nflag=1;}<br />
			else if(fom[ind]=='+')<br />
			{ops[top++]=0;ind++;nflag=0;}<br />
			else if(fom[ind]=='-')<br />
			{ops[top++]=1;ind++;nflag=0;}<br />
			else if(fom[ind]=='*')<br />
			{ops[top++]=2;ind++;nflag=0;}<br />
			else if(fom[ind]=='&#47;')<br />
			{ops[top++]=3;ind++;nflag=0;}<br />
			else {ind++;continue;}<br />
			while(tno>=2 && top>=1)<br />
			{<br />
				if(!nflag) break;<br />
				switch(fom[ind])<br />
				{<br />
				case '+':nop=0;break;<br />
				case '-':nop=1;break;<br />
				case '*':nop=2;break;<br />
				case '&#47;':nop=3;break;<br />
				default:nop=0;break;<br />
				}<br />
				op=ops[top-1];<br />
				if((op&#47;2)>=(nop&#47;2))<br />
				{<br />
					top--;<br />
					no2=nos[--tno];<br />
					no1=nos[--tno];<br />
					switch(op)<br />
					{<br />
					case 0:no1=no1+no2;break;<br />
					case 1:no1=no1-no2;break;<br />
					case 2:no1=no1*no2;break;<br />
					case 3:no1=no1&#47;no2;break;<br />
					}<br />
					if(no1>25) no1%=26;<br />
					nos[tno++]=no1;<br />
				}<br />
				else nflag=0;<br />
			}<br />
		}<br />
		ret=nos[tno-1];<br />
		if(ret>26) ret%=26;<br />
		if(ret==0) ret=26;<br />
		printf("%s",fom);<br />
		printf("=%cn",'A'+ret-1);<br />
	}<br />
	return 0;<br />
}<br />
&#47;*<br />
(A+1)+(A+2)*(D&#47;2)<br />
(A+B*(C+D)-E+9)<br />
*&#47;<&#47;pre></p>
