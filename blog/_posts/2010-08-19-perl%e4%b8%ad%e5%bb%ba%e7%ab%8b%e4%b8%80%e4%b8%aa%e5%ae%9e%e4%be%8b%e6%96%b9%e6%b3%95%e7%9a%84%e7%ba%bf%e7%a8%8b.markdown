---
layout: post
status: publish
published: true
title: Perl中建立一个实例方法的线程
author:
  display_name: twcai
  login: admin
  email: clumsywyvern@gmail.com
  url: http://www.caitengwei.com
author_login: admin
author_email: clumsywyvern@gmail.com
author_url: http://www.caitengwei.com
wordpress_id: 857
wordpress_url: http://caitengwei.com/blog/?p=857
date: '2010-08-19 09:42:17 +0800'
date_gmt: '2010-08-19 17:42:17 +0800'
categories:
- Perl
tags:
- "多线程"
- Perl
- OO
- "引用"
comments: []
---
<p>标题有点复杂吧？其实就是新建一个线程，来运行某个对象实例中的特定函数。</p>
<p>一般在Perl中新建一个线程的方法很简单：</p>
<pre class="prettyprint">use threads;<br />
my $th = threads->create( function_ref, parameters );<&#47;pre></p>
<p>但是启动一个实例中的函数就不太一样了，因为不能用 \&$object->method 来取得该函数的引用。</p>
<p>因为自己写脚本的时候有用到，于是花了一个下午探索实验。然后发现一个确实可以work的办法：在一个匿名函数中调用该方法。</p>
<p>不过这个做法实在是丑陋，Perl这样灵活的语言，一定可以有更好的办法来解决这种问题。</p>
<p>实验加翻阅Intermediate perl一个下午还是无果，突然Perl帝出现，看了一眼代码后瞬间给出一个非常正规的解决方法。</p>
<p>具体请直接看示例代码：</p>
<pre class="prettyprint" download="cat.pm">package Cat;</p>
<p>use strict;<br />
use warnings;</p>
<p>sub new {<br />
    my $class = shift;<br />
    my $self = {<br />
        hello => 'Miao',<br />
        @_<br />
    };<br />
    return bless $self, $class;<br />
}</p>
<p>sub sayhi {<br />
    my $self = shift;<br />
    my $times = shift || 3;</p>
<p>    foreach ( 1 .. $times ) {<br />
        print "$self->{hello}\n";<br />
        sleep 1;<br />
    }<br />
}</p>
<p>1;<&#47;pre></p>
<pre class="prettyprint" download="sayhi.pl">#!&#47;usr&#47;bin&#47;perl</p>
<p>use strict;<br />
use warnings;<br />
use threads;<br />
use FindBin qw($Bin);<br />
use lib "$Bin";<br />
use Cat;</p>
<p>my $cat = Cat->new( hello => 'meow' );</p>
<p># solution 1: works but ugly<br />
print "\n+++++++ solution 1 +++++++\n";<br />
my $th1 = threads->create( sub { $cat->sayhi(4); } );</p>
<p>foreach ( 1 .. 4 ) {<br />
    print "This is main function.\n";<br />
    sleep 1;<br />
}<br />
$th1->join;</p>
<p># solution 2: more professional<br />
print "\n+++++++ solution 2 +++++++\n";<br />
my $th2 = threads->create( \&Cat::sayhi, $cat, 4 );</p>
<p>foreach ( 1 .. 4 ) {<br />
    print "This is main function.\n";<br />
    sleep 1;<br />
}<br />
$th2->join;</p>
<p>print "\nDemo ends.\n";<&#47;pre></p>
