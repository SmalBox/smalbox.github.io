---
title: Unity导出Android工程
author: SmalBox
cover: false
top: false
date: 2019-11-25 00:52:34
categories:
   - Unity
tags:
   - Unity
   - Android
   - Export
---
# unity导出apk & 导出工程到AndroidStudio二次开发

本文将Uniyt导出Android工程的过程中需要注意的事项进行了阐述，对导出Android工程有其他疑问，可评论或邮箱联系我。

## 0. 项目准备
   - **unity 中配置 Android环境**
      - Edit -> Preferences
      - External Tools -> Adnroid 中选择好SDK JDK（默认安装Openjdk） NDK
      - *（在可以用unity hub的版本里，直接可安装好这三个模块，其中jdk和ndk可以用默认的，sdk可以选择AndroidStudio中安装）*
      - *(如果想要在 unity 中代理，须在在系统环境变量中添加HTTP_Proxy http://127.0.0.1:端口号 和 HTTPS_Proxy https://127.0.0.1:端口号)*

   - **AndroidStudio中配置环境(在[Android中文网](https://developer.android.google.cn/)下载AndroidStudio，建议3.1版本便于下载SDK)**
      - File -> Settings
      - **搜索 HTTP Proxy 设置代理**
         - Manual proxy configuration 中 设置 127.0.0.1 端口为本地外网开放端口
         - 点击 check connection 输入 android.com 检测是否代理成功
         *（设置代理成功可以下载sdk，更新包，在同步包时可以避免Gradle工具无法连接服务器，下载缓存而报错）*
      - **搜索 Android SDK 安装设置SDK**
         - 在 SDK Plantforms 中选择要安装的SDK和SDK工具
         - 在 SDK Update Sites 中选择Force https://... sources to be fetched using http://... 和 disable SDK diff patching
         - Apply后开始下载SDK

## 1. 选择平台
   - File -> BuildSettings 选择切换 android 平台

## 2. 项目设置-玩家设置
   - Edit -> ProjectSetting -> Player
   - 填写 Company Name , Product Name

## 3. 分辨率设置
   - 启动是否全屏，是否渲染外部安全区域等
   - 画面缩放
   - 宽高比
   - 默认方向
   - 允许自动旋转的方向
   - 其他设置

## 4. 启动时的画面logo
   - 可以在 Splash Image 中选择好启动标志和动画（免费个人版受到限制，无法取消unity自带logo）

## 5. 其他设置
   - **Ohter Settings**
      - 选择 Auto Graphics API *(如不选择，默认Vulkan、OpenGLES3、OpenGLES2的顺序，某些设备会标识硬件不支持)
   - 填写好 Package Name **注意：包名中不能有数字和特殊符号**
   - 选择好 Minimum API Level 和 Target API Level （automatic（highest installed））
   - Scripting Backend 用 mono
   - install Location 选择 Automatic *(默认是 Prefer External , 会导致某些sd卡有问题的虚拟机或者真机无法安装)*

## 6. 发布设置 签名打包
   - **Publishing Settings**
      - **首次没有签名key，选择创建新的keystore**
         - 选择 Browse Keystore 在资源管理器中选择存储在哪里
         - 在 Keystore password 中输入要创建key的密码，然后下面确认密码
         - 在 Key 中 Alias 选择 Create a new key
         - 在弹出框中填写好 Alias , Password , Confirm 
         - 点击 Create key
         - 在 Password 中填写密码
      - **在有签名时，选择 Use Existing Keystore**
         - 选择 Browse Keystore 找到key
         - 填写 Keystore password , confirm keystore password 
         - 选择 Alias 中key的名字 以及 对应的密码

## 7. unity 直接生成apk
   - Texture Compression ETC(default)
   - ETC2 fallback 32-bit
   - Build System Gradle *(在19之前的版本有这个选项可以选择internal，19的版本没有这个选项，只能使用Gradle)*
   - 点击 Build 选择apk要存储的位置，开始生成apk

## 8. unity 导出工程 AndroidStudio 二次开发
   - 选择 Gradle , ExportProject , DevelopmentBuild
   - 点击 Export ，导出项目
   - **用AndroidStudio打开项目**
      - AS会问，用AS的SDK还是项目的，推荐选择AS中的SDK，方便后续适配开发
      - AS会问，Gradle是用的项目的还是下载最新的，推荐点cancel，使用项目的Gradle
      - 在代理设置好，网络畅通的情况下，项目会由Gradle自动同步生成Android项目
      - 在AS中创建好目标配置的虚拟机，就可以点击 Run 运行项目到目标硬件机器

