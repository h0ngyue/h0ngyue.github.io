---
layout:     post
title:      "gradle fundamentals"
subtitle:   ""
date:       2015-03-12 17:33:00
author:     "h0ngyue"
header-img: "img/post-bg-2015.jpg"
tags:
    - gradle
---

##### 自动运行当前目录下build.gradle里的任务名为taskName的任务
 
```
./gradlew [taskName]
```

##### 如果想运行其他非 build.gradle的脚本里的任务，比如叫 other.gradle里的hello task

```
./gradlew -b other.gradle hello
```

##### 停止当前的gradle任务
gradle stop

#### closure

##### 定义
```
def foo = "One million dollars"
def myClosure = {
    println "Hello from a closure"
    println "The value of foo is $foo"
}

myClosure()
```

##### closure可以当做值被传递

```
def bar = myClosure
def baz = bar
baz()
```

##### delegate

```
class GroovyGreeter {
    String greeting = "Default greeting"
    def printGreeting(){println "Greeting: $greeting"}
}

def myGroovyGreeter = new GroovyGreeter()

def greetingClosure = {
    greeting = "Setting the greeting from a closure"
    printGreeting()
}

// greetingClosure() // This doesn't work, because `greeting` isn't defined
greetingClosure.delegate = myGroovyGreeter
greetingClosure()
```

#### task之间的依赖
3个关键词：**dependsOn**， **mustRunAfter**， **shouldRunAfter**， **finalizedBy**

#####finalizedBy

```
task eatBreakfast {
    finalizedBy "brushYourTeeth"
    doLast{
        println "Om nom nom breakfast!"
    }
}

task brushYourTeeth {
    doLast {
        println "Brushie Brushie Brushie."
    }
}
```

那么gradle eatBreakfast ,则在eatBreakfast完成之后自动会调用brushYourTeeth

##### 高级依赖写法

```
task getEquipped {
    dependsOn tasks.matching{ task -> task.name.startsWith("putOn")}
    doLast {
        println "All geared up!"
    }
}
```

当前所有tasks里，名字以putOn开头的task，都是getEquipped task的依赖

#### 打印stacktrace

gradle是默认不打印出错堆栈的，所以打印出来的指令:

```
gradle --stacktrace  or -s
gradle --full-stacktrace or -S (能看gradle core code里的堆栈）
```