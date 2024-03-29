---
title: IOS打包发布方式总结
author: SmalBox
cover: true
top: true
date: 2020-08-01 21:57:29
categories: Unity
tags:
  - IOS
  - 打包发布
---
# IOS打包发布方式总结

## 简介

   - IOS打包发布一般分为以下几种渠道：
      - AppStore
      - 数据线连接安装的机器直接安装到机器中
      - 打包出ipa文件，通过Itunes、各种安装助手、网页等方式安装
   - Appstore需要Apple的审核上架。
      - 审核需要各种手续，相对繁琐
      - 好处在于上架后用户方便安装使用
   - 数据线直连的方式多用于开发测试或者设备不多时自己或和朋友一起使用
   - 一般在实际分发时肯定不会连电脑一个一个安装，但是又不想上架AppStore走审核流程，那么就会打包出ipa包进行分发安装
      - 用Itunes安装需要连接电脑，不是很方便
      - 用安装助手相对好一些，但是也要借助电脑
      - 用网页安装的方式是一个比较友好的大规模分发的方式，只需要用户用safari打开网页，点击安装即可安装成功应用，用户体验较好。这也让市场中诞生了一些用此技术方式进行分发的网站，来帮助简化网页方式安装的部署门槛。

## 打包ipa通过网页方式发布App

### 简述

   - 网页用itms-services协议获取配置文件(ipa包、图标等地址在配置文件中)并根据其内容获取包数据，并通过Safari游览器调用ios系统服务安装下载的应用

### 工作原理及配置方式

   - 以下来详细描述各种发布ipa网站的核心工作原理（这些网站会增加一些额外的功能来方便用户和发布者，比如让用户扫描二维码打开网站之类的操作，这些不在本文讨论范围）。
   - 了解这些工作原理后，可以根据需要搭建自己的内网或公网发布平台，来供内部或外部的应用分发

   1. html中用如下如下协议链接来安装ipa包itms-services://?action=download-manifest&url=https://appInfo/manifest.plist
      - *(注：url地址更换成自己的配置文件地址，地址必须用 **https** 协议。)*

   2. ipa包的下载地址、图标下载地址在配置文件里，这里的地址 **可以用http协议。**

   3. 工作流配置方案：
       1. xcode中打包ipa，会有配置文件生成，得到ipa包和配置文件
       2. 修改配置文件中的ipa包和图标等的下载地址为接下来部署的地址
       3. 配置一个局域网或公网web服务器用来下载ipa包，例如在局域网某机器上配置web服务器，把ipa包复制到此服务器，得到http://192.168.0.2:8080/appName.ipa地址
       4. 配置一个局域网或公网web服务器用来下载配置文件，这里需要配置https协议的web服务器如同上一步得到https://192.168.0.2:8080/manifest.plist地址
       5. 用html写个下载页面，里面的a标签中的地址根据上面配置的举例修改成如下地址：itms-services://?action=download-manifest&url=https://192.168.0.2:8080/manifest.plist，在服务器中发布比html静态网页
       6. 此时用ios设备的Safari游览器访问发布的网页，点击写好的a标签，Safari游览器会调用系统功能来加载安装打包好的ipa包
       7. 补充：
          - 此方法根据实际应用场景，配置是外网服务器还是局域网服务器实现网页安装ipa包。
          - 安装后应用的开发者信任问题依赖打包ipa时使用的是什么权限的开发者账号。
