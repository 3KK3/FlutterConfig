需要事先下载安装好的工具有：
* Xcode（提供iOS模拟器）
* Android Studio（提供安卓模拟器）
* IDEA（用来编写Flutter项目， 使用Android Studio或者VSCode也可，个人推荐使用IDEA）

---

**1.**  先下载Flutter SDK（内含Dart SDK）。可以去官网下载Zip文件，或者通过终端git方式下载：

`git clone -b beta https://github.com/flutter/flutter.git`

**2.** 下载完成后，手动解压Flutter SDK到某一目录下，或者使用命令行方式解压：
```
cd 要解压的目录
unzip 下载的Flutter SDK路径
```
**3.** 为了方便后续使用，需要将项目根目录下bin路径加入环境变量PATH中：
Finder前往文件夹：`~/.bash_profile`， `bash_profile`打开文件(该文件为隐藏文件， 如果不显示隐藏目录，可以先按`shift + command + .`显示隐藏目录)，
追加环境变量如下：
```
export PATH=$PATH:SDK安装目录/flutter/bin
```

**4.** 然后执行`flutter doctor`命令来运行Flutter检测程序, 并根据检测程序的提示安装所需要的插件
> **注意**：
Android Studio错误多半是因为Android Studio没有安装Flutter插件，新建一个Flutter项目，然后用Android Studio打开Flutter项目，Android Studio就会在右下角弹框提示你安装插件，然后点击提示框安装即可，详细步骤见后面几步。

**5.** 可以使用IDEA 或者命令行方式创建Flutter项目：
```
cd 到要保存项目的目录
flutter create 项目名称
```
> 注： 编写Flutter项目可以使用IDEA，IDEA需要安装Flutter组件，在 IDEA的 偏好设置-插件 中搜索、安装Flutter插件


**6.** 打开Android Studio， 然后用Studio打开前面创建的flutter项目，右下角会提示安装flutter插件，根据提示安装即可, 然后重启studio。

**7.** 安卓Studio菜单栏Tools - AVD Manager 添加安卓模拟器
> 注： 安装模拟器最后一步，模拟性能`Graphics`一栏选择硬件(hardware)模拟


---

使用命令行方式查看可使用的模拟器：
```
flutter emulator
```
然后复制出现的模拟器名字，然后执行：
```
flutter emulator --launch 模拟器名字
```
就会打开模拟器。

---

使用命令行方式运行项目:
```
cd 到项目目录下
flutter run
```

---
---

> 附 Flutter运行安卓模拟器报错解决：

1.如果卡在了gradle依赖分析(dependence analysis)这一步，是因为默认需要翻墙， 可以打开VPN 或者：

```
修改build.gradle文件,注释掉jcenter()，google()。使用阿里的镜像。原因是jcenter google库无法访问到导致的问题。虽然我有万能的爬墙工具，开启全局代理依然被我们伟大的发改委墙掉了！

buildscript {
    repositories {
        //google()
        //jcenter()
        maven { url 'https://maven.aliyun.com/repository/google' }
        maven { url 'https://maven.aliyun.com/repository/jcenter' }
        maven { url 'http://maven.aliyun.com/nexus/content/groups/public' }
    }

    dependencies {
        classpath 'com.android.tools.build:gradle:3.1.2'
    }
}

allprojects {
    repositories {
        //google()
        //jcenter()
        maven { url 'https://maven.aliyun.com/repository/google' }
        maven { url 'https://maven.aliyun.com/repository/jcenter' }
        maven { url 'http://maven.aliyun.com/nexus/content/groups/public' }
    }
}
```

2. 如果报错`gradle 27`多半是因为项目中gradle依赖的安卓SDK版本, 本地没有下载，解决方法：

方法1： 菜单`Tools - SDKManager `下载提示缺少的SDK版本号
方法2： 进入项目目录，找到文件：`android - app - build.gradle`修改build.gradle文件的中sdk版本号为本地已经下载的SDK版本号


---
---

> flutter项目安装第三方框架（package）的时候，因为墙的缘故直接执行`flutter packages get`可能会失败，可以执行如下：
```
export PUB_HOSTED_URL=https://pub.flutter-io.cn  
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn  
flutter packages get
```
