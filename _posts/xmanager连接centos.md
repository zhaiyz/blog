title: "Xmanager连接CentOS"
id: 117
date: 2011-10-24 20:53:35
tags: 
- CentOS
- linux
- Xmanager
categories: 
- linux
---

服务器端配置（CentOS-5.7-i386）
1、保证“/etc/inittab”里面的默认启动项为“id:5:initdefault:”。
2、修改“/etc/gdm/custom.conf”里面的内容为：
[security]
AllowRemoteRoot=true
[xdmcp]
Enable=true
Port=177
3、重新启动桌面:gdm-restart

Xmanager配置（Xmanager 3.0 build 0152)
1、打开Xbrowser
2、新建一个“Xstart Session”
3、在“General”页，填写“Session”、“Host”、“Protocol”选择“SSH”，“User Name”、“Password”填写“Host”对应的用户名和密码，保存密码。“Execution Command”选择“7 GNOME”。
4、在“X Server”页，“Server Profile”选择“Xstart sample”
5、单击确定
6、双击打开刚配置好的“Xstart Session”