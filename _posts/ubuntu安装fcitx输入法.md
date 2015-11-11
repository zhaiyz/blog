title: ubuntu安装fcitx输入法
description: ubuntu安装fcitx输入法
date: 2015-11-09 22:02:21
category:
- ubuntu
tags:
- ubuntu
- 输入法
- fcitx
---
ubuntu自带的输入法是`ibus`，只是能用，远远不够用。搜狗也出了linux版的[输入法](http://pinyin.sogou.com/linux/?r=pinyin)，但是我遇到过3次，安装完成重启之后进入不了桌面的情况。我用的是fcitx输入法，本文就介绍下fcitx的安装与配置。

## 安装fcitx拼音
``` bash
sudo apt-get install fcitx-pinyin -y
```
以上命令运行完成之后，就已经安装好了，现在进行配置。执行
``` bash
 im-config
```
在弹出的提示窗口中选择`确定`和`是`，然后就能进入如下界面，选中`fcitx`。
![install fcitx](http://zhaiyz.qiniudn.com/images/blog/20151109/setup01.png)

## 注销或重启
注销或重启，以使前面的配置生效。

## 使用
使用`Ctrl`+`Space`就可以激活输入法，使用`Shift`就可以快速切换中英文输入。

<!--more-->

## 隐藏托盘中自带的输入法图标
安装完`fcitx`后，托盘中还会显示出系统自带的输入法图标，如下图中红框部分：
![install fcitx](http://zhaiyz.qiniudn.com/images/blog/20151109/setup02.png)
单击红框内容，在弹出的菜单中选择`文本输入设置`，在弹出的窗口中把`在菜单栏显示当前输入源`的复选框**不选中**，就可以了。如下图：
![install fcitx](http://zhaiyz.qiniudn.com/images/blog/20151109/config03.png)

## 安装五笔或五笔拼音
``` bash
sudo apt-get install fcitx-table-wubi -y
sudo apt-get install fcitx-table-wbpy -y
```
使用五笔的话，建议使用`fcitx-table-wbpy`，打字过程中遇到个不知道怎么折的，可以直接用拼音，很方便。
