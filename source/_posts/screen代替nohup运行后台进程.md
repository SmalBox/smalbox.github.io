---
title: screen代替nohup运行后台进程
date: 2018-11-08 19:37:56
author: Smalbox
categories: Linux
tags:
  - nohup
  - screen
  - 后台运行程序
---
# screen代替nohup运行后台进程

## **前言**

在linux中常用nohup和&配合将程序放在后台运行，但是当远程用ssh登陆时会遇到退出远程后进程就被杀掉了。

这里用screen来守护进程不会被杀掉。

## **具体流程**

1. 创建一个screen会话
   ``` bash
   $screen -S screenName
   ```
2. 启动脚本，服务之类的任何想要后台运行的东西
3. 退出screen会话
   ``` bash
   $screen -d
   ```
4. 如果想恢复会话（重新连接）
   ``` bash
   $screen -r screenName
   ```
5. 查看是否有screen会话及其状态
   ``` bash
   $screen -ls
   ```

*（此方法适用于bash，zsh等终端。可使用 man screen 查看详细信息）*