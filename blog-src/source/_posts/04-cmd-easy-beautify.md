---
layout: post
title: Re:从零开始让CMD控制台优雅一点点
date: 2020-03-12 08:30:00
updated: 2020-03-12 09:30:00
description: <img src='https://cdn.idealx.cn/blogimage/04/blog-04-cover.png' height=65% width=65%><br>介绍一个非常好看的字体XD<br>然后让黑漆漆的窗口稍微好看那么一点点。
categories: 
- [笔记本, 教程]
tags: 
- 正经
- 科学
- 教程
- CMD
- 终端
- 美化
permalink: post/cmd-easy-beautify.html
---

### 这是一款相当漂亮且适合编程的字体。

~~他们是这么说的...~~这是一款 Microsoft Yahei 和 Consolas 的混合字体，很适合在 Windows 和 Linux 平台下编程使用。字体名字叫 YaHei-Consolas-Hybrid。

> Microsoft Yahei ：微软雅黑是美国微软公司委托中国北大方正电子有限公司设计的一款全面支持ClearType技术的字体。~~别商用，惨不忍睹~~
>
> Consolas ：Consolas是一套等宽字体的字型，属无衬线字体，由Lucas de Groot设计。

下面提供 Github 中的下载地址：https://github.com/yakumioto/YaHei-Consolas-Hybrid-1.12

> Windows 系统可以直接下载 `.ttf` 的字体文件，然后点击安装即可。
>
> Linux 内核的系统按照上述网站中的简介安装即可。

> 还有一款非常标准而且好看的字体叫 “更纱黑体” ，不过最近似乎有新版本的修正，下次再存档记录吧。

### 修改CMD命令提示符的默认字体

#### 方法一：配置注册表

1、在键盘上敲击 `Windows` + `R` 键，输入 `regedit` 命令打开注册表

2、在左侧的文件夹中找到 `HKET_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Console\TrueTypeFont` 设置：

“936” = "YaHei Consolas Hybrid”

<fancybox>
<img src='https://cdn.idealx.cn/blogimage/04/blog-04-01.png' height=75% width=75%>
</fancybox>

#### 方法二：右击CMD窗口“属性“和”默认值“

<fancybox>
<img src='https://cdn.idealx.cn/blogimage/04/blog-04-02.png' height=60% width=60%>
</fancybox>

在字体里选择 `YaHei Consolas Hybrid` 即可。

> 特别注意：”默认值“ 为 cmd.exe 的默认值，“属性” 为当前 cmd 的快捷方式的设置（比如说用口令打开的cmd快捷方式或者 “开始” 菜单中的 “cmd命令指令符” 就是两个 cmd.exe 的快捷方式 ）。

接着，可以根据自己的需求选择更改一些背景的属性。（当然我懒就没改）

<fancybox>
<img src='https://cdn.idealx.cn/blogimage/04/blog-04-03.png'>
</fancybox>

然后，然后 CMD 就会好看一点了。~~（不得不说这个等宽字体是真的养眼）~~

### 后记

下次会介绍一些更好看的 “终端” 程序。也便于自己做个存档。如果有机会的话，下次会直接在博客中给一些下载链接的吧。~~两天更一篇博文就是水。~~