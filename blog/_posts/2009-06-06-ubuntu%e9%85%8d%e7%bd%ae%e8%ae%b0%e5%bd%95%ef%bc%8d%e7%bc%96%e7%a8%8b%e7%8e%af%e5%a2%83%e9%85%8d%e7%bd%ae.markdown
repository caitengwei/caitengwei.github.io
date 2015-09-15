---
layout: post
status: publish
published: true
title: Ubuntu配置记录－编程环境配置
author:
  display_name: twcai
  login: admin
  email: clumsywyvern@gmail.com
  url: http://www.caitengwei.com
author_login: admin
author_email: clumsywyvern@gmail.com
author_url: http://www.caitengwei.com
excerpt: "GVIM在今天早上算是做好了最基本的配置，可以拿来写代码做算法题了。上次说到不知道配色文件在哪里配置=,=, 其实这是个小白问题，就在 &#47;usr&#47;share&#47;vim&#47;vim71&#47;colors下面(vim71需要对你安装的gvim版本)。\r\nNetbeans的中文显示问题，也算解决了，具体见下帖
  ： <a href=\"http:&#47;&#47;forum.ubuntu.org.cn&#47;viewtopic.php?f=70&t=179713&p=1169093&hilit=netbeans+%E4%B9%B1%E7%A0%81#p1169093\">安装日文支持以后NetBeans界面的字符乱码<&#47;a>。当然，实际上跟日文支持是没有关系的。Netbeans的中文显示问题有很多解决方案，而且并非全部都很有效，所以碰到的话，还是需要都尝试一下。\r\n尽管搞定了中文显示问题，但是netbeans下面的字体显示仍然非常难看，google了下ubuntu中文社区，据说可以通过修改配置文件完成。目前对linux的文件配置机制还不是很熟悉，而且主要还是用gvim来编码，因此把这个问题先暂且搁下。留下一个链接，方便以后解决：<a
  href=\"http:&#47;&#47;forum.ubuntu.org.cn&#47;viewtopic.php?f=8&t=75690\">[问题]［Netbeans］
  JRE［英文］字体配置问题<&#47;a>\r\n继续转强帖：\r\n<a href=\"http:&#47;&#47;wiki.ubuntu.org.cn&#47;index.php?title=%E8%B7%9F%E6%88%91%E4%B8%80%E8%B5%B7%E5%86%99Makefile:MakeFile%E4%BB%8B%E7%BB%8D&variant=zh-cn\">makefile编写<&#47;a>；\r\n<a
  href=\"http:&#47;&#47;forum.ubuntu.org.cn&#47;viewtopic.php?t=90260\">两篇很牛的vim使用技巧（1）<&#47;a>；\r\n<a
  href=\"http:&#47;&#47;forum.ubuntu.org.cn&#47;viewtopic.php?f=68&t=90261\">两篇很牛的vim使用技巧（2）<&#47;a>。\r\n\r\n最后分享一下我的gvim配置文件和配色文件代码。\r\nUpdate
  at 2010.Apr.13: 这两个文件因为会经常修改，我自己使用的最新版本将会放在DropBox上，随时供需要的人下载。也请路过的大牛多多指教。Download
  via <a href=\"http:&#47;&#47;dl.dropbox.com&#47;u&#47;4531990&#47;ConfigFile&#47;.vimrc\">.vimrc<&#47;a>
  <a href=\"http:&#47;&#47;dl.dropbox.com&#47;u&#47;4531990&#47;ConfigFile&#47;ctw.vim\">ctw.vim<&#47;a>\r\n\r\nps.
  如果下载后的配置文件中有^M字符，可以在gvim的命令模式下用下面这个命令来清除\r\n<pre>:%s&#47;[Ctrl-v][Enter]&#47;&#47;g<&#47;pre>\r\n\r\n<pre
  class=\"prettyprint\" download=\".vimrc\">\" $HOME&#47;.vimrc\r\n\" Collected and
  modified by CTW\r\n \r\n\" Basics {\r\n    \" 关闭兼容模式\r\n    set nocompatible\r\n
  \   \r\n    \" 设定文件浏览器目录为当前目录\r\n    set bsdir=buffer\r\n    set autochdir\r\n    \r\n
  \   \" 设置编码\r\n    set enc=utf-8\r\n    \r\n    \" 设置文件编码检测类型及支持格式\r\n    set fencs=utf-8,ucs-bom,gb18030,gbk,gb2312,cp936\r\n
  \   \r\n    \" 指定菜单语言\r\n    set langmenu=zh_CN.UTF-8\r\n    source $VIMRUNTIME&#47;delmenu.vim\r\n
  \   source $VIMRUNTIME&#47;menu.vim\r\n    \r\n    \" 与windows共享剪切板\r\n    set clipboard+=unnamed\r\n
  \   \r\n    \" 键盘操作\r\n    map <up> gk\r\n    map <down> gj\r\n \r\n    \" 开放光标移动\r\n
  \   set whichwrap=b,s,<,>,[,]\r\n \r\n    \" 命令行高度\r\n    set cmdheight=1\r\n    \r\n
  \   \" 中文帮助\r\n    if version > 603\r\n    set helplang=cn\r\n    endif\r\n \r\n
  \   \" 增强检索功能\r\n    set tags=.&#47;tags,.&#47;..&#47;tags,.&#47;**&#47;tags\r\n
  \   \r\n    \" 保存文件格式\r\n    set fileformats=unix\r\n\" }\r\n \r\n \r\n\" Visual
  {\r\n    \" 设置配色文件\r\n    colo ctw\r\n \r\n    \" 设置开启语法高亮\r\n    syntax on\r\n
  \r\n    \" 设置初始窗体行数列数\r\n    set lines=36\r\n    set columns=124\r\n \r\n    \"
  font\r\n    set guifont=Monaco\r\n \r\n    \" 查找结果高亮度显示\r\n    set hlsearch\r\n
  \   \r\n    \" tab宽度\r\n    set tabstop=4\r\n    set cindent shiftwidth=4\r\n    set
  autoindent shiftwidth=4\r\n    \" }\r\n \r\n    \" Autocommands {\r\n    \" Enable
  load plugin files\r\n    filetype plugin on\r\n\r\n    \" 自动补全\r\n    filetype plugin
  indent on\r\n\r\n    \" 只在下列文件类型被侦测到的时候显示行号，普通文本文件不显示\r\n    if has(\"autocmd\")\r\n
  \      autocmd FileType xml,html,c,cs,java,perl,shell,sh,bash,cpp,python,vim,php,ruby
  set number\r\n       autocmd FileType xml,html vmap <c -o> <esc>'<i <!--<ESC>o<esc>'>o-->\r\n
  \      autocmd FileType java,c,cpp,cs vmap <c -o> <esc>'<o &#47;*<ESC>'>o*&#47;\r\n
  \      autocmd FileType html,text,php,vim,c,java,xml,bash,shell,perl,python setlocal
  textwidth=100\r\n       autocmd Filetype html,xml,xsl source $VIMRUNTIME&#47;plugin&#47;closetag.vim\r\n
  \    \" Error happend, repair needed\r\n     \" autocmd BufReadPost *\r\n     \"
  \   \\ if line(\"'\\\"\") > 0 && line(\"'\\\"\") < = line(\"$\") |\r\n     \"    \\
  \  exe \"normal g`\\\"\" |\r\n     \"    \\ endif\r\n    endif \" has(\"autocmd\")\r\n
  \   \r\n    \" 自动完成\r\n    autocmd FileType python set omnifunc=pythoncomplete#Complete\r\n
  \   autocmd FileType javascrīpt set omnifunc=javascrīptcomplete#CompleteJS\r\n    autocmd
  FileType html set omnifunc=htmlcomplete#CompleteTags\r\n    autocmd FileType css
  set omnifunc=csscomplete#CompleteCSS\r\n    autocmd FileType xml set omnifunc=xmlcomplete#CompleteTags\r\n
  \   autocmd FileType php set omnifunc=phpcomplete#CompletePHP\r\n    autocmd FileType
  c set omnifunc=ccomplete#Complete\r\n \tautocmd FileType java set omnifunc=javacomplete#Complete\r\n
  \   \" auto complete\r\n    \" inoremap } }<esc>: <cr>O\r\n\" }\r\n \r\n\" C&#47;C++
  Programming {\r\n    \" C&#47;C++注释\r\n    set comments=:&#47;&#47;\r\n    \r\n
  \   \" Enable OmniCppComplete\r\n    set nocp\r\n    set completeopt=menu\r\n\r\n\t\"
  Config OmniCppComplete\r\n\t\" autocomplete with .\r\n    let OmniCpp_MayCompleteDot
  = 1 \r\n\t\" autocomplete with ->\r\n    let OmniCpp_MayCompleteArrow = 1 \r\n\t\"
  autocomplete with ::\r\n    let OmniCpp_MayCompleteScope = 1 \r\n    \" select first
  item (but don't insert)\r\n\tlet OmniCpp_SelectFirstItem = 2 \r\n    \" search namespaces
  in this and included files\r\n\tlet OmniCpp_NamespaceSearch = 2 \r\n    \" show
  function prototype (i.e. parameters) in popup window\r\n    let OmniCpp_ShowPrototypeInAbbr
  = 1 \r\n\r\n\t\" Add STL tags\r\n\tset tags+=~&#47;.myTags&#47;stl.tags\r\n\r\n
  \   \" 修正自动C式样注释功能 <2005&#47;07&#47;16>\r\n    set comments=s1:&#47;*,mb:*,ex0:&#47;\r\n
  \r\n\t\" 临时：使用pthread的C源代码的编译\r\n\tmap <F4> :call PTHCompileRunGPP()<cr>\r\n\tfunc!
  PTHCompileRunGPP()\r\n\texec \"w\"\r\n\texec \"!gcc -D_REENTRANT % -o %< -g -lpthread\"\r\n\tendfunc\r\n\r\n
  \   \" C的编译和运行\r\n    map <f5> :call CCompileRunGpp()<cr>\r\n    func! CCompileRunGpp()\r\n
  \   exec \"w\"\r\n    exec \"!gcc % -o %< -ansi -g -Wall \"\r\n    endfunc\r\n    \r\n
  \   \" C++的编译和运行\r\n    map <f6> :call CPPCompileRunGpp()<cr>\r\n    func! CPPCompileRunGpp()\r\n
  \   exec \"w\"\r\n    exec \"!g++ % -o %< -ansi -g -Wall \"\r\n    endfunc\r\n\r\n
  \   \" CTags\r\n\tset completeopt=longest,menu \r\n\r\n\t\" TagList\r\n    \" 按照名称排序\r\n
  \   let Tlist_Sort_type = \"name\"\r\n    \r\n    \" 如果只有一个Buffer，kill窗口时也kill掉buffer\r\n
  \   let Tlist_Exit_OnlyWindow = 1\r\n\r\n\t\" 只显示一个文件的Tag\r\n\tlet Tlist_Show_One_File=1\r\n
  \   \r\n\t\" Tlist Auto Open\r\n\tlet Tlist_Auto_Open=1\r\n\r\n\" }<&#47;pre>\r\n"
wordpress_id: 400
wordpress_url: http://child.kilu.de/blog/?p=400
date: '2009-06-06 16:46:57 +0800'
date_gmt: '2009-06-06 08:46:57 +0800'
categories:
- Ubuntu Notes
tags:
- gvim
- netbeans
- Ubuntu
- DropBox
- vimrc
comments:
- id: 63
  author: AndrewBoldman
  author_email: andrewb@cndnsfive.cn
  author_url: http://www.google.com
  date: '2009-06-05 05:55:55 +0800'
  date_gmt: '2009-06-04 21:55:55 +0800'
  content: I really liked this post. Can I copy it to my site? Thank you in advance.
---
<p>GVIM在今天早上算是做好了最基本的配置，可以拿来写代码做算法题了。上次说到不知道配色文件在哪里配置=,=, 其实这是个小白问题，就在 &#47;usr&#47;share&#47;vim&#47;vim71&#47;colors下面(vim71需要对你安装的gvim版本)。<br />
Netbeans的中文显示问题，也算解决了，具体见下帖 ： <a href="http:&#47;&#47;forum.ubuntu.org.cn&#47;viewtopic.php?f=70&t=179713&p=1169093&hilit=netbeans+%E4%B9%B1%E7%A0%81#p1169093">安装日文支持以后NetBeans界面的字符乱码<&#47;a>。当然，实际上跟日文支持是没有关系的。Netbeans的中文显示问题有很多解决方案，而且并非全部都很有效，所以碰到的话，还是需要都尝试一下。<br />
尽管搞定了中文显示问题，但是netbeans下面的字体显示仍然非常难看，google了下ubuntu中文社区，据说可以通过修改配置文件完成。目前对linux的文件配置机制还不是很熟悉，而且主要还是用gvim来编码，因此把这个问题先暂且搁下。留下一个链接，方便以后解决：<a href="http:&#47;&#47;forum.ubuntu.org.cn&#47;viewtopic.php?f=8&t=75690">[问题]［Netbeans］ JRE［英文］字体配置问题<&#47;a><br />
继续转强帖：<br />
<a href="http:&#47;&#47;wiki.ubuntu.org.cn&#47;index.php?title=%E8%B7%9F%E6%88%91%E4%B8%80%E8%B5%B7%E5%86%99Makefile:MakeFile%E4%BB%8B%E7%BB%8D&variant=zh-cn">makefile编写<&#47;a>；<br />
<a href="http:&#47;&#47;forum.ubuntu.org.cn&#47;viewtopic.php?t=90260">两篇很牛的vim使用技巧（1）<&#47;a>；<br />
<a href="http:&#47;&#47;forum.ubuntu.org.cn&#47;viewtopic.php?f=68&t=90261">两篇很牛的vim使用技巧（2）<&#47;a>。</p>
<p>最后分享一下我的gvim配置文件和配色文件代码。<br />
Update at 2010.Apr.13: 这两个文件因为会经常修改，我自己使用的最新版本将会放在DropBox上，随时供需要的人下载。也请路过的大牛多多指教。Download via <a href="http:&#47;&#47;dl.dropbox.com&#47;u&#47;4531990&#47;ConfigFile&#47;.vimrc">.vimrc<&#47;a> <a href="http:&#47;&#47;dl.dropbox.com&#47;u&#47;4531990&#47;ConfigFile&#47;ctw.vim">ctw.vim<&#47;a></p>
<p>ps. 如果下载后的配置文件中有^M字符，可以在gvim的命令模式下用下面这个命令来清除</p>
<pre>:%s&#47;[Ctrl-v][Enter]&#47;&#47;g<&#47;pre></p>
<pre class="prettyprint" download=".vimrc">" $HOME&#47;.vimrc<br />
" Collected and modified by CTW</p>
<p>" Basics {<br />
    " 关闭兼容模式<br />
    set nocompatible</p>
<p>    " 设定文件浏览器目录为当前目录<br />
    set bsdir=buffer<br />
    set autochdir</p>
<p>    " 设置编码<br />
    set enc=utf-8</p>
<p>    " 设置文件编码检测类型及支持格式<br />
    set fencs=utf-8,ucs-bom,gb18030,gbk,gb2312,cp936</p>
<p>    " 指定菜单语言<br />
    set langmenu=zh_CN.UTF-8<br />
    source $VIMRUNTIME&#47;delmenu.vim<br />
    source $VIMRUNTIME&#47;menu.vim</p>
<p>    " 与windows共享剪切板<br />
    set clipboard+=unnamed</p>
<p>    " 键盘操作<br />
    map <up> gk<br />
    map <down> gj</p>
<p>    " 开放光标移动<br />
    set whichwrap=b,s,<,>,[,]</p>
<p>    " 命令行高度<br />
    set cmdheight=1</p>
<p>    " 中文帮助<br />
    if version > 603<br />
    set helplang=cn<br />
    endif</p>
<p>    " 增强检索功能<br />
    set tags=.&#47;tags,.&#47;..&#47;tags,.&#47;**&#47;tags</p>
<p>    " 保存文件格式<br />
    set fileformats=unix<br />
" }</p>
<p>" Visual {<br />
    " 设置配色文件<br />
    colo ctw</p>
<p>    " 设置开启语法高亮<br />
    syntax on</p>
<p>    " 设置初始窗体行数列数<br />
    set lines=36<br />
    set columns=124</p>
<p>    " font<br />
    set guifont=Monaco</p>
<p>    " 查找结果高亮度显示<br />
    set hlsearch</p>
<p>    " tab宽度<br />
    set tabstop=4<br />
    set cindent shiftwidth=4<br />
    set autoindent shiftwidth=4<br />
    " }</p>
<p>    " Autocommands {<br />
    " Enable load plugin files<br />
    filetype plugin on</p>
<p>    " 自动补全<br />
    filetype plugin indent on</p>
<p>    " 只在下列文件类型被侦测到的时候显示行号，普通文本文件不显示<br />
    if has("autocmd")<br />
       autocmd FileType xml,html,c,cs,java,perl,shell,sh,bash,cpp,python,vim,php,ruby set number<br />
       autocmd FileType xml,html vmap <c -o> <esc>'<i <!--<ESC>o<esc>'>o--><br />
       autocmd FileType java,c,cpp,cs vmap <c -o> <esc>'<o &#47;*<ESC>'>o*&#47;<br />
       autocmd FileType html,text,php,vim,c,java,xml,bash,shell,perl,python setlocal textwidth=100<br />
       autocmd Filetype html,xml,xsl source $VIMRUNTIME&#47;plugin&#47;closetag.vim<br />
     " Error happend, repair needed<br />
     " autocmd BufReadPost *<br />
     "    \ if line("'\"") > 0 && line("'\"") < = line("$") |<br />
     "    \   exe "normal g`\"" |<br />
     "    \ endif<br />
    endif " has("autocmd")</p>
<p>    " 自动完成<br />
    autocmd FileType python set omnifunc=pythoncomplete#Complete<br />
    autocmd FileType javascrīpt set omnifunc=javascrīptcomplete#CompleteJS<br />
    autocmd FileType html set omnifunc=htmlcomplete#CompleteTags<br />
    autocmd FileType css set omnifunc=csscomplete#CompleteCSS<br />
    autocmd FileType xml set omnifunc=xmlcomplete#CompleteTags<br />
    autocmd FileType php set omnifunc=phpcomplete#CompletePHP<br />
    autocmd FileType c set omnifunc=ccomplete#Complete<br />
 	autocmd FileType java set omnifunc=javacomplete#Complete<br />
    " auto complete<br />
    " inoremap } }<esc>: <cr>O<br />
" }</p>
<p>" C&#47;C++ Programming {<br />
    " C&#47;C++注释<br />
    set comments=:&#47;&#47;</p>
<p>    " Enable OmniCppComplete<br />
    set nocp<br />
    set completeopt=menu</p>
<p>	" Config OmniCppComplete<br />
	" autocomplete with .<br />
    let OmniCpp_MayCompleteDot = 1<br />
	" autocomplete with -><br />
    let OmniCpp_MayCompleteArrow = 1<br />
	" autocomplete with ::<br />
    let OmniCpp_MayCompleteScope = 1<br />
    " select first item (but don't insert)<br />
	let OmniCpp_SelectFirstItem = 2<br />
    " search namespaces in this and included files<br />
	let OmniCpp_NamespaceSearch = 2<br />
    " show function prototype (i.e. parameters) in popup window<br />
    let OmniCpp_ShowPrototypeInAbbr = 1 </p>
<p>	" Add STL tags<br />
	set tags+=~&#47;.myTags&#47;stl.tags</p>
<p>    " 修正自动C式样注释功能 <2005&#47;07&#47;16><br />
    set comments=s1:&#47;*,mb:*,ex0:&#47;</p>
<p>	" 临时：使用pthread的C源代码的编译<br />
	map <F4> :call PTHCompileRunGPP()<cr><br />
	func! PTHCompileRunGPP()<br />
	exec "w"<br />
	exec "!gcc -D_REENTRANT % -o %< -g -lpthread"<br />
	endfunc</p>
<p>    " C的编译和运行<br />
    map <f5> :call CCompileRunGpp()<cr><br />
    func! CCompileRunGpp()<br />
    exec "w"<br />
    exec "!gcc % -o %< -ansi -g -Wall "<br />
    endfunc</p>
<p>    " C++的编译和运行<br />
    map <f6> :call CPPCompileRunGpp()<cr><br />
    func! CPPCompileRunGpp()<br />
    exec "w"<br />
    exec "!g++ % -o %< -ansi -g -Wall "<br />
    endfunc</p>
<p>    " CTags<br />
	set completeopt=longest,menu </p>
<p>	" TagList<br />
    " 按照名称排序<br />
    let Tlist_Sort_type = "name"</p>
<p>    " 如果只有一个Buffer，kill窗口时也kill掉buffer<br />
    let Tlist_Exit_OnlyWindow = 1</p>
<p>	" 只显示一个文件的Tag<br />
	let Tlist_Show_One_File=1</p>
<p>	" Tlist Auto Open<br />
	let Tlist_Auto_Open=1</p>
<p>" }<&#47;pre><br />
<a id="more"></a><a id="more-400"></a><br />
配色文件：</p>
<pre download="ctw.vim">" local syntax file - set colors on a per-machine basis:<br />
" vim: tw=0 ts=4 sw=4<br />
" Vim color file<br />
" Based on "Murphy.vim"<br />
" Maintainer:	Ron Aaron <ron@ronware.org><br />
" Last Change:	2004 May 02<br />
" Modified by CTW<br />
" Last Modified : 20010 Apr 13</p>
<p>hi clear<br />
set background=dark<br />
if exists("syntax_on")<br />
  syntax reset<br />
endif<br />
let g:colors_name = "ctw"</p>
<p>hi Constant		term=underline ctermfg=LightGreen guifg=White	gui=NONE<br />
hi Ignore					   ctermfg=black	  guifg=bg<br />
hi PreProc		term=underline ctermfg=LightBlue  guifg=Wheat<br />
hi Search		term=reverse					  guifg=white	guibg=Blue<br />
hi Special		term=bold	   ctermfg=LightRed   guifg=green<br />
hi Error		term=reverse   ctermbg=Red	  ctermfg=White guibg=Red  guifg=White<br />
hi Todo			term=standout  ctermbg=Yellow ctermfg=Black guifg=Blue guibg=Yellow<br />
" From the source:<br />
hi Cursor										  guifg=Orchid	guibg=fg<br />
hi Directory	term=bold	   ctermfg=LightCyan  guifg=Cyan<br />
hi ErrorMsg		term=standout  ctermbg=DarkRed	  ctermfg=White guibg=Red guifg=White<br />
hi IncSearch	term=reverse   cterm=reverse	  gui=reverse<br />
hi ModeMsg		term=bold	   cterm=bold		  gui=bold<br />
hi MoreMsg		term=bold	   ctermfg=LightGreen gui=bold		guifg=SeaGreen<br />
hi NonText		term=bold	   ctermfg=Blue		  gui=bold		guifg=Blue<br />
hi Question		term=standout  ctermfg=LightGreen gui=bold		guifg=Cyan<br />
hi SpecialKey	term=bold	   ctermfg=LightBlue  guifg=Cyan<br />
hi StatusLine	term=reverse,bold cterm=reverse   gui=NONE		guifg=White guibg=darkblue<br />
hi StatusLineNC term=reverse   cterm=reverse	  gui=NONE		guifg=white guibg=#333333<br />
hi Title		term=bold	   ctermfg=LightMagenta gui=bold	guifg=Pink<br />
hi WarningMsg	term=standout  ctermfg=LightRed   guifg=Red<br />
hi Visual		term=reverse   cterm=reverse	  gui=NONE		guifg=white guibg=darkgreen</p>
<p>" What I modified<br />
hi Character										guifg=magenta<br />
hi cComment		term=bold		ctermfg=LightRed	guifg=lightblue<br />
hi Include											guifg=orange<br />
hi LineNr		term=underline	ctermfg=Yellow		guifg=white<br />
hi Macro											guifg=orange<br />
hi Normal		ctermbg=Black	ctermfg=lightgreen	guibg=Black		guifg=#FFFF7F<br />
hi Number											guifg=magenta	gui=bold<br />
hi PreCondit										guifg=orange<br />
hi Statement	term=bold		ctermfg=Yellow		guifg=turquoise gui=NONE<br />
hi cString											guifg=magenta<br />
hi Structure										guifg=turquoise</p>
<p>" Nothing happened<br />
hi Identifier	term=underline	ctermfg=LightCyan	guifg=white<br />
hi Operator											guifg=white		gui=NONE<br />
hi Type							ctermfg=LightGreen	guifg=turquoise	gui=none<&#47;pre></p>
