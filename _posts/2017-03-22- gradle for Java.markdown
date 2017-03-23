---
layout:     post
title:      "gradle for Java"
subtitle:   ""
date:       2015-03-22 17:33:00
author:     "h0ngyue"
header-img: "img/post-bg-2015.jpg"
tags:
    - gradle
---

ref: [QuickStart](https://docs.gradle.org/current/userguide/tutorial_java_projects.html#javaQuickstart)

ref: [Full Doc](https://docs.gradle.org/current/userguide/java_plugin.html)

#### Multi-project build - common configuration

Notice that our sample applies the Java plugin to each subproject. This means the tasks and configuration properties we have seen in the previous section are available in each subproject. So, you can compile, test, and JAR all the projects by running gradle build from the root project directory.

Also note that these plugins are only applied within the subprojects section, not at the root level, so the root build will not expect to find Java source files in the root project, only in the subprojects.

```
subprojects {
    apply plugin: 'java'
    apply plugin: 'eclipse-wtp'

    repositories {
       mavenCentral()
    }

    dependencies {
        testCompile 'junit:junit:4.12'
    }

    version = '1.0'

    jar {
        manifest.attributes provider: 'gradle'
    }
}

```

####working with Repos and deps


```
repositories {
	flatDir {
		dirs 'libs'
	}
}

dependencies {
    compile 'commons-io:commons-io:2.5' // 2. Add commons-io dependency
    compile fileTree(dir: 'libs', include: '*.jar') // fileTree way	 compile files('libs/foo.jar', 'libs/bar.jar').  // files way
}

```

#### 查看dependencies
 
 ```
 gradle dependencies
 ```
 
 查看某个特殊配置的依赖（比如runtime的）
 
 ```
 gradle dependencies --configuration runtime
 ```
 
 解决依赖冲突常用的指令
 以下指令查看了所有最终依赖commons-logging的配置，都会列出来，以及如果有冲突，gradle是如何解决的
 
 ```
 gradle dependencyInsight --dependency commons-logging
 ```