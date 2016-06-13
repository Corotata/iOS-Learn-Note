title: QorumLogs
date: 2016-06-27 15:12:38
tags:
---

##QorumLogs
Swift开发中，在面临Bug时，我们常常采用的方式就是暴力调试，今天我就介绍一款Swift中的Log日志，开源项目名为：QorumLogs，它能配合XcodeColors输出彩色的Log日志

###基本用法

~~~
QorumLogs.enabled = true
~~~
开启日志系统

~~~
QorumLogs.test()
~~~
输出测试日志，这时，我们就能看到五颜色的输出日志

~~~
QorumLogs.minimumLogLevelShown = 1
~~~
设置日志输出级别，他总共有四个级别，分别为Debug,Info,Warn和Error，通过设置，我们可以通过设置输出级别来过滤掉不想输出的日志

~~~
QorumLogs.onlyShowThisFile("ViewController")
~~~
设置只输出，ViewController这个文件的日志

~~~
QorumLogs.onlyShowTheseFiles("ViewController","AppDelegate")
~~~
设置指定多文件输出，值得注意的是，这里是大小写敏感的


~~~
QL1("Debug")
QL2("Info")
QL3("Warn")
QL4("Error")
~~~
QorumLogs内部定义的基本四种Tag输出


