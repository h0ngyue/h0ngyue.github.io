---
layout:     post
title:      "在ubuntu上安装node.js环境~"
subtitle:   ""
date:       2015-01-29 12:00:00
author:     "h0ngyue"
header-img: "img/post-bg-2015.jpg"
tags:
    - node.js
    - ubuntu
    - env
---

先安装编译环境

```shell
apt-get update
apt-get install python gcc make g++
```

装6.x的方法， 如果想装node v7可以看[node.js官网](https://nodejs.org)，有更详细的说明

```
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
```

通过以下命令来安装编译安装一些我们必需的本地插件。

```
sudo apt-get install -y build-essential
```

装git

```
apt-get install g++ curl make libssl-dev apache2-utils git-core
```

