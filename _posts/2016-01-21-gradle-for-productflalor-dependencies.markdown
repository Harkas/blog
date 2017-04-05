---
layout: post
title:  "Gradle--多渠道依赖问题"
date:   2016-01-21
categories: gradle build
description: gradle多渠道打包相关依赖的一些问题
---

## 前提

如果我们想用Gradle打出多渠道的包，需要在build.gradle脚本中加入代码：

```groovy
productFlavors {
    pro {
        packageName "com.androidtool.pro"
    }
    dev {
    }
}
```

## 情景一

如果各个渠道包需要依赖的库都是一样的，非常好说，在dependencies中加入相应依赖库即可，如果需求是需要对每个渠道包配置不同的dependencies，就需要对不同的渠道包进行分别配置，对于前提中的例子来说，可以在build.gradle中添加如下代码：

```groovy
android {
    /*其它相关代码*/
    productFlavors {
        pro {
          packageName "com.androidtool.pro"
        }
        dev {
        }
    }
}
dependencies {
    compile 'com.android.support:support-v4:22.2.0'
    proCompile project(':lib')
    devCompile project(':libnew')
}
```

以上，pro渠道包依赖lib, dev渠道包依赖libnew，**注意大小写，如是渠道依赖，为flavorCompile，如果是普通依赖，为compile**.

## 情景二

### 需求

如果需求是lib有几个渠道，对于app来讲，需要依赖某个渠道的lib，此时，如果只是在app的build.gradle中简单地写上
compile project(':lib')，这个时候依赖配置是不生效的。这是因为gradle本身有bug（据说这个问题已经在试图修复列表中），对于lib来说，只能编译默认的版本，即Release的配置版本,并且如果设置了渠道号，就不会编译出Release和Debug版本了。在app中直接使用compile，则是表明了我需要依赖lib的默认Release版本，但是Release版本已经不会被编译了，这个设置显然就会发生错误……（虽然不会报错，但是依赖是不生效的）~~

### 解决方案

值得庆幸的是，gradle设置了一个参数可以解决这个问题。如果设置了渠道号，则要在lib的build.gradle中声明**publishNonDefault true**，表示编译此lib的其它所有的编译版本：

```groovy
android {
    publishNonDefault true

    productFlavors {
        pro { }
        dev { }
    }
}
```

之后在app中的依赖中声明需要依赖的相应版本，如下代码所示（通过验证，如果app中没有声明相应的渠道号，刚编译会出现找不到devCompile的错误，所以lib和app中的渠道号应该保持相一致的）：

```groovy
android {
    /*其它相关代码*/
    productFlavors {
        pro { }
        dev { }
    }
}
dependencies {
    /*其它相关代码*/
    proCompile project(path:':lib', configuration:'proRelease') // or 'proDebug'
    devCompile project(path:':lib', configuration:'devDebug') // or 'devRelease'
}
```

## 情景三

此需求是情景二需求的延伸，即如果你的lib只有一个渠道，或你的app只需要依赖一个渠道，还有一个方法，不用声明**publishNonDefault true**，而是声明lib的默认配置为你所需要依赖的配置，**defaultPublishConfig"devRelease"**，这样在app中就不用按上面的格式写依赖了，直接写**compile project(':lib')**即可，如下：
在你的lib的build.gradle中，声明lib的默认编译版本：

```groovy
android {
    defaultPublishConfig "devRelease"
}
```

在你的app的build.gradle中，需要加上如下的依赖脚本：

```groovy
dependencies {
    /*其它相关代码*/
    compile project(':lib')
}
```

