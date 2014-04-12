title: Ubuntu安装最新版本nodejs
date: 2014-04-06 22:36:58
categories: ubuntu
tags: [ubuntu, nodejs]
description: Ubuntu安装最新版本nodejs
keywords: ubuntu, nodejs
---
Ubuntu官方源里面的nodejs版本有点低，有些基于nodejs的应用需要使用高版本，以下命令可以安装最新的稳定版本nodejs。
``` bash
sudo apt-get update
sudo apt-get install -y python-software-properties python g++ make
sudo add-apt-repository -y ppa:chris-lea/node.js
sudo apt-get update
sudo apt-get install nodejs
```

---
全文完
