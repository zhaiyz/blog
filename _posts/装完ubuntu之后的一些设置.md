title: 装完ubuntu之后的一些设置
description: 装完ubuntu之后的一些设置
date: 2015-11-04 22:29:54
category:
- ubuntu
tags:
- ubuntu
- 配置
---
安装ubuntu系统可以参考[一步一步安装ubuntu](/2015/11/01/一步一步安装ubuntu/)。安装完成之后需要根据自己的习惯进行一些配置，本文介绍一下我自己的一些配置。

## 换源
这肯定是第一件要做的事情。我建议是安装过程中不需要联网，等安装完成之后，根据自己的网络情况，找到一个速度快的源。这样再安装软件或是更新系统的时候才会快。以下为换源的图文步骤：
1. 单击桌面右上角的设置按钮，就是那个小齿轮。在弹出的菜单中选择`系统设置`，再在弹出的窗口中的`系统`设置中选择`软件和更新`。
![ubuntu config01](http://zhaiyz.qiniudn.com/images/blog/20151104/config01.png)
![ubuntu config02](http://zhaiyz.qiniudn.com/images/blog/20151104/config02.png)
2. 单击下载自中的下拉列表，选择`其他站点`，在`选择下载服务器`窗口的`中国`节点下面，选择一个自己访问比较快的源。不知道选择哪个的话，右边有一个`选择最佳服务器`，单击这个，让系统自己通过测试选择一个访问最快的站点。我一直在用`mirrors.aliyun.com`这个源，很快，很稳定。推荐使用。
![ubuntu config03](http://zhaiyz.qiniudn.com/images/blog/20151104/config03.png)
![ubuntu config04](http://zhaiyz.qiniudn.com/images/blog/20151104/config04.png)
3. 选择好服务器的时候，需要输入密码来确认操作，之后会提示`可用的软件列表信息已过时`，选择`重新载入`。
![ubuntu config05](http://zhaiyz.qiniudn.com/images/blog/20151104/config05.png)
![ubuntu config06](http://zhaiyz.qiniudn.com/images/blog/20151104/config06.png)
4. 经过以上操作，就完成了更换更新源的配置。

<!--more-->

## 更新
换完源之后，可以对系统和软件进行一次整体升级。使用`Ctrl+Alt+t`调出终端，输入`sudo apt-get update && sudo apt-get upgrade -y`，再根据提示输入密码就可以了。此步完成之后，系统本身和系统中的软件就都是最新版的了。以下为操作中的截图。
![ubuntu config08](http://zhaiyz.qiniudn.com/images/blog/20151104/config08.png)
![ubuntu config09](http://zhaiyz.qiniudn.com/images/blog/20151104/config09.png)

## 隐私
ubuntu现在默认是开启在线搜索的，我是认为这个没什么用，可以通过`系统设置`中的`安全和隐私`关闭。打开`安全和隐私`窗口后，选择`搜索`页。把`包含在线搜索结果`中的`开启`单击一下变成`关闭`就可以了。
![ubuntu config10](http://zhaiyz.qiniudn.com/images/blog/20151104/config10.png)

## 调整启用器
默认情况下左边的启用器中，包含了`LibreOffice`相关软件以及`Amazon`等软件。你可以根据自己的需求，进行移除。在选中应用的图标上右击，选择`从启动器解锁`即可。
