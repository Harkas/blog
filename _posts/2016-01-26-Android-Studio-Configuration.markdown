---
layout: post
title:  "Android Studio配置问题总结"
date:   2016-01-26
categories: Android Studio
description: Android Studio各种配置问题总结，持续更新
---

## 1、aidl文件的配置

在Eclipse中建立aidl文件后，ADT会在gen文件夹下会自动生成一个.java文件，调用者可以直接引用；但是在Android Studio开发环境中，新建一个aidl文件，不自动生成.java文件，直接引用的话，会出现如下错误：

```java
Cannot resolve symbol 'IMyAidlInterface'
```

###解决方法一:

在工程的Module目录下的src/main下新建一个aidl文件夹（只将aidl文件放入这个新建的aidl文件夹中，编译是不能通过的），并且在新建aidl文件夹下添加和AndroidManifest中相同包名的package，在这个package下面添加aidl文件。例如添加前的文件目录结构为：

![](/images/posts/android/android-studio-config1.png)

添加完成后的文件目录结构为：

![](/images/posts/android/android-studio-config2.png)

重新编译之后，就可以在app/build/generated/source/aidl/debug/下的package下面生成了相应的.java文件:

![](/images/posts/android/android-studio-config3.png)

###解决方法二:

如果你觉得层层创建目录很麻烦，则可以使用下面的方法。
将aidl文件放到你需要放置的路径下，如Module的package根目录src/main/java/package下:

![](/images/posts/android/android-studio-config4.png)

然后在app的build.gradle中加入标识aidl源文件路径的属性aidl.srcDirs：

```groovy
android {
    compileSdkVersion 22
    buildToolsVersion "21.1.2"
    
    /*相关代码*/
    
    sourceSets {
        main {
            aidl.srcDirs = ['src/main/java']
        }
    }
}
```

重新编译之后，就可以在app/build/generated/source/aidl/debug/下的package下面生成了相应的.java文件:

![](/images/posts/android/android-studio-config3.png)

注：使用上面的gradle配置脚本 **aidl.srcDirs = ['src/main/java']** 的时候，如果不放在pakeage的根目录下，也没有问题，放在任何你需要放置的地方：

![](/images/posts/android/android-studio-config5.png)

编译完成后，依然会在相应的build目录下面生成.java文件：

![](/images/posts/android/android-studio-config6.png)

