---
title: 安装Gitment及常见问题解决
date: 2018-10-24 19:13:59
author: SmalBox
categories: 前端
tags:
  - Gitment
---
# 安装Gitment评论模块 & 常见问题解决

## **前言**

本文记录了本博客添加gitment评论模块的过程，并对配置过程中碰到的问题与其解决方案作出阐述。
因每个hexo选择的主题不一样，所以主题的文件结构会有所不同，具体操作也会有所不同，所以本文也尽可能的写出配置思路，来帮助不同主题的hexo博主配置自己主题的gitment评论模块。

对gitment的介绍就不多说了，就是利用GitHub的issue来做评论，能同步issue里的留言。具体详细可以去看项目介绍：[Gitment项目地址](https://github.com/imsun/gitment).

> 大致描述一下gitment的配置：
  - 首先是两个配置文件，一个css文件一个js文件。gitment的开发者用远程连接的方式将两个文件引入hexo中。但是实际操作中会遇到问题（最后常见问题中会写解决方案），其中的js文件中需要访问作者自己搭建的服务器，但是现在作者的服务器不好使了，会导致全都配置好了，但是报错。所以要下载到本地的自己项目中，然后在项目中自己引用这两个文件（具体操作本文安装部分会写到）。

  - 其次就是由于主题不同，有的主题的作者在开始设计主题的时候就为用户写好了gitment的配置代码，只需用户在主题的_config.yml中开启并填写好配置参数即可。有的主题没有预制好gitment的配置代码，就需要用户自己去在样式模板中添加gitment代码。

## **概览**

  1. 安装gitment到主题
  2. 注册OAuth application
  3. 配置gitment到hexo主题中
  4. 初始化评论
  5. 常见问题解决

### **1.安装gitment到主题**

由于有的hexo主题预置gitment模块，有的没有，所以分两种情况来说。

  1. **主题已经集成了gitment模块 看这里～**
  - 需要博主自己查看一下自己的主题结构，找到 **themes** 下的 **_config.yml** 文件，在文件中找到gitment模块的相关参数，然后在 **enable** 选项后面写上 **true** 即可完成安装过程。

  如图所示： ![gitmentConfig](gitmentConfig.png)

  2. **主题没有集成gitment模块 根本配置在这里～**
  - 如果在自己的 **themes** 的 **_config.yml** 中没有看到 **gitment**相关选项，就要自己配置。
  - 这时就要用到gitment作者的安装方法了。前言中说到的两个文件一个css一个js，只要将这两个文件引入自己主题的母板中就完成了安装。由于作者的提供是js文件中需要改动，所以这里要将提供是文件下载下来到自己的博客中，根据自己的文件结构防治css和js文件。然后在模板文件中引用两个文件。
  
  - [css文件下载地址](https://imsun.github.io/gitment/style/default.css)
  - [js文件下载地址](https://imsun.github.io/gitment/dist/gitment.browser.js)

  ``` html
  <!--(将以下添加到模板文件中（这个引用路径是一个例子，根据自己的目录引用)-->

  <link rel="stylesheet" href="/libs/gitment/default.css">
  <script src="/libs/gitment/gitment.browser.js"></script>
  ```

*（注：本质上安装就是在主题模板文件中引入一个css和一个js文件。集成gitment模块的主题只不过是做到了代码分离，让需要配置的参数在_config.yml中统一配置。gitment作者给出的方法是在给没有集成的主题中的根本引入办法。如果你能看懂主题作者的组织结构，那完全可以给自己的主题集成gitment模块。因主题结构不一样我就不详细举例了。）*

### **2.注册OAuth application**

因为gitment是利用了github的issue，所以要注册OAuth application，来获取配置参数为接下来的配置做准备。

[点击此处](https://github.com/settings/applications/new)来注册，一个新的 OAuth Application。其他内容可以随意填写，但要确保填入正确的 callback URL（一般是评论页面对应的域名，如 https://smalbox.top）。

注册后会给两个字符串 **Client ID** 和 **Client Secret** , 这两个下面配置的时候要用。

### **3.配置Gitment到hexo主题中**

同样的，也是一种预置gitment和自己配置分两种来说。

  1. **主题已经集成了gitment模块 看这里～** 
  - 只需在 **_config.yml** 中找到刚才开启gitment的那里，下面有四个参数要添加。
  
  如图所示：![gitmentConfiged](gitmentConfiged.jpeg)

  2. **主题没有集成gitment模块 根本配置在这里～**
  - 在刚才添加的母版中继续添加如下代码：

``` html
<div id="container"></div>
<script>
var gitment = new Gitment({
  owner: '你的 GitHub ID',
  repo: '存储评论的 repo',
  oauth: {
    client_id: '你的 client ID',
    client_secret: '你的 client secret',
  },
})
gitment.render('container')
</script>
```
  - 将以上的代码中的四个参数按照提示填好即可。

### **4.初始化评论**

理论上按照以上配置完发布即可看到评论区了。只不过每一个帖子下面的评论区都要初始化才能开始评论。

根据gitment作者的说法，只要到用博主的github账号登录后点击初始化就可以使用了。

### **5.常见问题解决**

  - 评论点击登录，登录GitHub之后跳转回来的时候不能正常跳回刚才贴纸那页。每次跳到主页。

**解决办法：** 在注册OAuth application时的回调地址有问题，尝试写绑定的域名，而不是用 “https://用户名.github.io”

  - 报错 “[object ProgressEvent]”

**原因：** 在母版中调用的js文件中，有访问gitment作者的服务器代码，而作者的服务器不好使了。

**解决办法：** 自己搭建一个服务器（需要有一个vps来辅助搭建服务器，当然下面我也会提供一个我搭建好的服务器）

  1. 在服务器中clone作者的服务器源码

``` bash
git clone https://github.com/SmalBox/gh-oauth-server.git
```
  2. 进入项目，下载依赖，并启动

``` bash
npm install && nohup npm start &
```
*(注：如果运行失败，可能是nodejs没有安装好，请安装nodejs。然后再重新运行命令,如果成功,在项目目录下的nohup.out文件中的最后，会提示正在监听3000端口。这里需要用nginx将证书搞定，用https访问，否则默认http还是会报错。证书的问题我就不啰嗦了，证书参考[这个帖子的 11.后续优化 部分](https://www.bugprogrammer.me/2018/05/19/phpnginxmysql.html#more),端口转发请参考[这个帖子](https://segmentfault.com/a/1190000002797606))*

  3. 替换js文件中的作者服务器为自己服务器

在作者的js文件中搜索以下字符串：
``` bash
https://gh-oauth.imsun.net
```
将其替换成刚才搭建服务器的地址即可。

**OK大功告成，可以去测试一下了。可以在本站的下面回复评论测试。**

**如果有任何问题，可以在下面评论或者通过邮件联系我。**
