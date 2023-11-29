---
layout: "post"
title: "Uniapp"
date: "2023年11月9日14:20:41"
categories: framework,Uniapp
tags: [Computer Language, framework,Uniapp]
---

# Uniapp开发安卓APP
## 离线缓存与数据持久化
离线缓存： 将网络请求的数据缓存到本地，用户在没有网络链接的情况下可以继续访问已缓存的数据。
Uniapp使用`uni.setStorageSync`和`uni.getStorageSync`来实现

> uni-app的Storage在不同端的实现不同, App端为原生的plus.storage，无大小限制，不是缓存，是持久化的

# Uniapp离线打包安卓APK
## 步骤
### 一些下载
1. 下载安装`Android Studio`,[下载地址](https://developer.android.google.cn/studio/index.html)
2. 下载HbuilderX最新的SDK,[下载地址](https://nativesupport.dcloud.net.cn/AppDocs/download/android.html#)

### HbuilderX离线打包
1. `HbuilderX`界面选择`发行 -> 原生APP-本地打包 -> 生成本地打包APP资源`
2. 打包完成后会在控制台输出打包生成的文件地址`xxxx/__UNI__XXX/xxx`,`__UNI__XXX`是本项目对应的Appid
3. 将下载的HbuilderX最新的SDK解压，使用`Android Studio`打开包中的`HBuilder-Integrate-AS`文件夹
4. 将`HBuilder-Integrate-AS\simpleDemo\src\main\assets\apps\`下的所有文件删除，替换成步骤2中生成的整个`__UNI__XXX/`文件夹
5. 将`src/main/assets/data/dcloud_control.xml`中的`APPID`修改为上面的`__UNI__XXX`
6. `Android Studio`界面选择`Build -> Generate Signed Bundle/APK...`,在跳出的弹窗页面选择APK,选择`Next`,进入下一步
7. 首次生成选择`Create new ...`,`key store path`要在`simpleDemo`文件夹下，可以直接放在根目录；密码和别名都可以自定义，点击`ok`开始生成签名文件
	注：
	- 此步骤是在生成签名文件，由于下载的Demo包是Gradle，可能会出现生成签名出错的问题，目前遇到的基本都是提示`invalid keystore format`
	- `invalid keystore format`很可能是因为项目本身的JDK版本和电脑环境变量的JDK版本不一致，将两者调成JDK12是可以运行的
8. 在`/simpleDemo/build.gradle`中配置信息，`keyAlias`为刚刚填写的key的别名，`keypassword`为自定义的密码，`StorageFile`为刚刚生成的文件名
9. 查看刚生成的签名文件(此处以`test.keystore`为例)的签名，进入到`test.keystore`文件夹，在命令行输入`keytool -list -v -keystore test.keystore`
10. 步骤9中查看的签名可能只会有`SHA1`和`SHA256`两种，但实际配置时还需要`MD5`签名，则只能使用[另一种方法](#jump)查看
11. 登录UniAPP开发者中心管理应用，进入相应的应用，选择`各平台信息`标签，如果没有则自己新建一个
12. 配置信息中的包名需要填写在`/simpleDemo/build.gradle`文件的`applicationId`中
13. 填写步骤10中的`MD5`信息、`SHA1`信息、`SHA256`信息，提交后会生成对应的APPKey
14. 将生成的APPKey填入`src/main/AndroidManifest.xml`的`android:value`
15. `\src\main\res\drawable`文件夹下的`icon.png`、`push.png`、`splash.png`分别对应APP的logo、消息推送logo、启动页图片，可改成自定义
16. 在`\src\main\res\values\strings.xml`中修改APP的名称
17. `Android Studio`界面选择`Build -> Build Bundle(s)/APK(s) -> Build APK(s)`开始打包
18. 打包后的文件位置在`\build\outputs\apk\debug\simpleDemo-debug.apk`(`\release\simpleDemo-release.apk`不是自定义的apk包，为啥？？？有待继续研究)

#### <span id="jump">查看签名文件的`SHA1` `SHA256` `MD5`信息</span>
生成`test.keystore`文件后，在`Android Studio`的`HBuilder-Integrate-AS`项目根目录下打开终端，输入`./gradlew signingReport`命令

正常情况下能获取到`SHA1` `SHA256` `MD5`信息，如果报错则查看jdk版本是否一致

**如果修改过环境变量，需要重启`Android Studio`再操作**

	
## 参考文章： 
1. [uniapp离线打包安卓APP全过程](https://blog.csdn.net/qq_26282869/article/details/127012224)
2. [HBuilderX离线SDK (Android)](https://nativesupport.dcloud.net.cn/AppDocs/download/android.html#)
3. [Android 连接第三方模拟器](https://blog.csdn.net/m0_62059090/article/details/127425912)
4. [uniapp离线打包在Android Studio创建的jsk证书无法获取MD5的问题](https://blog.csdn.net/Ysmooth_Alone/article/details/130176427)

