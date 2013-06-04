---
layout: post
title: "Test in awk with command mv"
description: "测试一下代码"
category: 
tags: []
---
{% include JB/setup %}

今天碰到一个问题，我有一个列表，里面存储着，一堆文件名对应着此文件的描述，我要将描述变为那文件的文件名。
-
于是我就想办法，想到：

    $ awk '{print "mv",$2,$1}' filename > batch
    $ bash batch
可用。

在网上找到这种的：
-
假设文件夹a下有多个log文件，

1.log
2.log
3.log
……

现要求，如果某个log文件中存在 Normal termination 字段，则将该log文件`mv`到另一个文件夹b。

    $ ls *.log | xargs grep -l "Normal termination" | awk '{system("mv "$0" ../b")}
这个命令效率太低了，一开始我也是想到的`awk`的内置`FILENAME`参数，可以打印文件名，这样配合`system()`函数就可以移动文件了，但是匹配内容的行的想法没想出来。哎真笨啊，看到后面的帖子懂了。

    $ awk '/Normal termination/{system("mv "FILENAME" ../b")}' *.log
*.log文件其实可以这样作为最后的文件名来写，我怎么没想到呢。再给出黑哥的写法：

    $ mv -i $(grep -Frl --include=\*.log "Normal termination" .) ../b

