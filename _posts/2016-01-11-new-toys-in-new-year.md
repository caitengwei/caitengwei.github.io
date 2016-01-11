---
layout: post
title: New Toys in New Year
published: true
categories:
- Geek Stuff
- Programming
tags:
- hhkb
- karabiner
- hammerspoon
---

## HHKB Pro2 Type-S

2015年国庆去霓虹国旅游时，给自己买了一把 [HHKB Pro2 Type-S][1] 回来。

![不要脸的秀键盘](/assets/images/2015-01-11-HHKB.jpg)

然而回国后，一开始用 HHKB 就感到各种不习惯，好几个已经成为 muscle memory 的常用操作都不能用了。主要原因在于 HHKB ：

1. 把 Backquote(`) 挪到了键盘最右上角, 数字键 1 的最左边变成了 ESC
2. Backslash(\\) 挪到了 Equal(=) 的邮编，原来的位置被 Delete 取代

这3个键的新位置让我极度不习惯，但是因为剩下的键位都感觉很爽，所以又非常舍不得换。上周我好好研究了下解决这个问题的方法，最后找到一个对我来说还算比较满意的方案。

## Karabiner

HHKB for Mac 的跳线调整就不赘述了，这里主要用到一个键位 remap 的神器叫 [Karabiner][2]，把键位做了如下改动：

1. Shift + ESC --> Tilde(~)
2. Cmd + ESC --> 程序内窗口切换（OSX 默认的 Cmd + ` 组合键）
3. Delete --> Backslash(\\)
4. Backquote(`) --> Delete
5. Backslash(\\) --> Backquote(`)

其中第 2 条 remap 规则不是 Karabiner 内置支持的，但是可以自己配置实现。具体方法就是在 Karabiner 的Preferences 中编辑一个 private.xml，加入如下内容：

{% highlight xml %}
  <item><name>Private Settings</name>
    <item>
      <name>Change "left command + escape" to "move focus to next window in application".</name>
      <appendix>(You need to enable command-backquote (⌘`) shortcut from System Preferences.)</appendix>
      <identifier>remap.command_escape_to_command_backquote</identifier>
      <autogen>
        __KeyToKey__
        KeyCode::ESCAPE, ModifierFlag::COMMAND_L,
        KeyCode::BACKQUOTE, ModifierFlag::COMMAND_L
      </autogen>
    </item>
  </item>
{% endhighlight %}

这 5 条 remap 规则以上，立马整个操作都顺手了，原先在 Macbook 键盘上的常用键位都能继续用上。另外再加上一对 Emacs keybinding 的 remap 规则，立刻爽到不行。

终于明白为什么 Karabiner 被推荐为神器，真是哪里不爽改哪里，妈妈再也不用担心我用不了 HHKB。

再顺手贴一下我目前在用的一些 remap 规则：

![Karabiner规则](/assets/images/2015-01-11-Karabiner.png)

## Hammerspoon

这里再介绍一个很好用的工具 [Hammerspoon][3]。

用到这个主要是因为公司办公经常会带着 Macbook 到处开会，那么用 Macbook 的时候，就需要把 HHKB 的 remap 关掉，具体到 Karabiner 的操作就是切换 profile。然而拔出键盘后还要手动切一下 remap profile 也是挺不爽的事情，所以就 Google 到了 Hammerspoon 这个工具。

具体用途请直接看官网，这个工具也是一个自动化神器。对我来说比较明显的缺点是要用 Lua 写自动化脚本（which 我没写过）。但是脚本语言嘛，边用边学就好了。

这边要实现的功能就是让 Hammerspoon 监听 USB 设备插拔事件：

1. HHKB 插入 Macbook 时，自动切换到 HHKB remap profile
2. HHKB 拔出 Macbook 时，则切回 Macbook original profile
3. 另外加了一条小规则，如果我的鼠标无线接收器插入 Macbook 时，则打开一个反转鼠标滚轮方向的 APP，反之则杀掉这个 APP（因为和 touchpad 的三指单击功能有点冲突）

具体的配置如下：

{% highlight lua %}
local usbWatcher = nil

function usbDeviceCallback(data)
    -- print(data["productName"])
    if (string.match(data["productName"], "HHKB%s+Professional%s*") ~= nil) then
        -- HHKB 键盘映射自动切换
        if (data["eventType"] == "added") then
	    -- print(data["eventType"])
	    hs.execute('/Applications/Karabiner.app/Contents/Library/bin/karabiner select 0') -- HHKB profile
        elseif (data["eventType"] == "removed") then
	    hs.execute('/Applications/Karabiner.app/Contents/Library/bin/karabiner select 1') -- Macbook Original profile
        end
    elseif (string.match(data["productName"], "USB%s+Receiver%s*")) then
    	-- Scroll Reverser 根据无线鼠标接收器的插拔自动启动和退出
        if (data["eventType"] == "added") then
	    hs.application.launchOrFocusByBundleID('com.pilotmoon.scroll-reverser')
	elseif (data["eventType"] == "removed") then
	   apps = hs.application.applicationsForBundleID('com.pilotmoon.scroll-reverser')
	   for k, v in pairs(apps) do
	       v:kill()
	   end
	end
    end
end

usbWatcher = hs.usb.watcher.new(usbDeviceCallback)
usbWatcher:start()
{% endhighlight %}

## Ending

总之以上是最近特别想分享的一些小工具，都是因为败了一个 HHKB 又可以 kill 自己好多时间……

等过段时间自己不那么穷了，准备把 HHKB 的键帽都换成无刻，就更加不用在意原始键位这个事情了。

[1]: http://www.pfu.fujitsu.com/hhkeyboard/type-s/
[2]: https://pqrs.org/osx/karabiner/
[3]: http://www.hammerspoon.org/