title: 一步一步安装ubuntu
date: 2015-11-01 17:56:24
description: 一步一步安装ubuntu
category: ubuntu
tags:
- ubuntu
- 安装
---
我最开始接触到的ubuntu版本是8.04，中间各种折腾，到12.04版出来的时候，就把ubuntu作为开发系统使用。认为相比windows，使用ubuntu开发还是方便很多。本文将图文介绍一下ubuntu的安装过程，使用的版本是`ubuntu 14.04 lts`。安装过程是在`virtualbox`中进行的。如果是开发电脑，建议是至少8G内存，最好再是SSD。

国内也有不少ubuntu的镜像网站，比如`http://mirrors.aliyun.com/ubuntu-releases/`，`http://mirrors.163.com/ubuntu-releases/`等。下载好`ubuntu-14.04.3-desktop-amd64.iso `文件，使用刻录软件烧到光盘中，或是使用[LinuxLive USB Creator](http://www.linuxliveusb.com/)把系统刻录到u盘中。以下为详细步骤说明和截图。

<!--more-->

1. 用刻录好系统的光盘或是u盘启用后，会到这个页面，默认语言是`English`。
![ubuntu install step01](http://zhaiyz.qiniudn.com/images/blog/20151101/step01.png)
2. 修改语言为`中文(简体)`，安装界面中的英文就变成了汉字，点击`安装Ubuntu`。
![ubuntu install step02](http://zhaiyz.qiniudn.com/images/blog/20151101/step02.png)
3. 在这个页面中，可以先不连接到网络，也不用选中`安装中下载更新`和`安装这个第三方软件`，这些内容等到安装完成之后再统一进行操作。如果安装的时候开着无线，可能会有连接到无线的提示，都选择不连接。选择`继续`进入下一界面。
![ubuntu install step03](http://zhaiyz.qiniudn.com/images/blog/20151101/step03.png)
4. 在这一步中，默认中`清除整个磁盘并安装Ubuntu`，这个会自动的根据电脑内存等信息进行分区。我建议还是使用自定义分区，选择`其他选项`，再点击`继续`。
![ubuntu install step04](http://zhaiyz.qiniudn.com/images/blog/20151101/step04.png)
![ubuntu install step05](http://zhaiyz.qiniudn.com/images/blog/20151101/step05.png)
5. 在这个页面，进行自定义分区，选中`/dev/sda`点击`新建分区表`，在弹出的提示框中选择`继续`。
![ubuntu install step06](http://zhaiyz.qiniudn.com/images/blog/20151101/step06.png)
![ubuntu install step07](http://zhaiyz.qiniudn.com/images/blog/20151101/step07.png)
6. 选中`空闲`行，再点击下面的`+`。我一直以来的分区方式是，把所有空间都分区根目录，不分`swap`。挂载点选择`/`，点击`确定`。
![ubuntu install step09](http://zhaiyz.qiniudn.com/images/blog/20151101/step09.png)
![ubuntu install step10](http://zhaiyz.qiniudn.com/images/blog/20151101/step10.png)
7. 在这个页面上选择`现在安装`，会提示没有分交换分区，点击`继续`。下一页面会提示是否将分区写入磁盘，选择`继续`。
![ubuntu install step11](http://zhaiyz.qiniudn.com/images/blog/20151101/step11.png)
![ubuntu install step12](http://zhaiyz.qiniudn.com/images/blog/20151101/step12.png)
![ubuntu install step13](http://zhaiyz.qiniudn.com/images/blog/20151101/step13.png)
8. 这是一个选择时区的页面，默认就是`Shanghai`，就不做修改了，如果不是这个时区，就在地图上点一下，选择`Shanghai`，选择`继续`。
![ubuntu install step14](http://zhaiyz.qiniudn.com/images/blog/20151101/step14.png)
9. 这是一个选择键盘布局的页面，保持默认，选择`继续`。
![ubuntu install step15](http://zhaiyz.qiniudn.com/images/blog/20151101/step15.png)
10. 需要在这个页面填写上登录名以及密码信息，按自己的情况填写即可。密码太短会有警告，不管这个。点击`继续`。
![ubuntu install step16](http://zhaiyz.qiniudn.com/images/blog/20151101/step16.png)
11. 之后就是自动安装的过程，不需要再进行配置。安装程序会根据之前配置的信息，把系统安装好。如果当前是连网状态，安装的过程中会下载一些包。但这些都是可以点击`Skip`跳过去。
![ubuntu install step17](http://zhaiyz.qiniudn.com/images/blog/20151101/step17.png)
![ubuntu install step19](http://zhaiyz.qiniudn.com/images/blog/20151101/step19.png)
12. 等安装成功后，会出现下面这个界面进行提示。点击`现在重启`。
![ubuntu install step22](http://zhaiyz.qiniudn.com/images/blog/20151101/step22.png)
13. 重启的过程中会提示把安装介质移出的提示，把光盘或u盘拿走后，敲击键盘上的`Enter`。
![ubuntu install step23](http://zhaiyz.qiniudn.com/images/blog/20151101/step23.png)
14. 系统重启完成后会到登录页面，输入之前设定的密码，按`Enter`。然后就能进入到安装好的系统中。
![ubuntu install step26](http://zhaiyz.qiniudn.com/images/blog/20151101/step26.png)
![ubuntu install step27](http://zhaiyz.qiniudn.com/images/blog/20151101/step27.png)
15. Enjoy it。
