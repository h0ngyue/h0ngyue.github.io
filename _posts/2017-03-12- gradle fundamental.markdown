---
layout:     post
title:      "gradle fundamentals"
subtitle:   ""
date:       2015-01-29 12:00:00
author:     "h0ngyue"
header-img: "img/post-bg-2015.jpg"
tags:
    - node.js
    - ubuntu
    - env
---

#### 自动运行当前目录下build.gradle里的任务名为taskName的任务
 
```
./gradlew [taskName]
```

#### 如果想运行其他非 build.gradle的脚本里的任务，比如叫 other.gradle里的hello task

```
./gradlew -b other.gradle hello
```