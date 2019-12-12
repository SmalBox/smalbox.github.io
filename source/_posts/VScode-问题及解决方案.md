---
title: VScode 问题及解决方案
author: SmalBox
cover: false
top: false
date: 2019-12-12 23:18:31
categories: 软件
tags:
  - VScode
  - Q&A
---
# VScode 问题及其解决方案

## **前言**

在使用VScode中遇到的一些问题，在此帖中进行记录，持续更新……

## **Q&A**
   - **Q1: VScode在Mac下Vim插件长按hjkl键无法持续移动**
     - **A1:**
        - 在Mac终端下执行以下命令:
        - ``` bash
          $ defaults write com.microsoft.VSCode ApplePressAndHoldEnabled -bool false
          ```
        - 重启VScode即可
        <br>
        - 若要恢复，执行以下命令
        - ``` bash
          $ defaults write com.microsoft.VSCode ApplePressAndHoldEnabled -bool true
          ```

   - **Q2: 配置VScode终端字体**
      - **A2:**
         1. **Linux下配置VScode终端字体：**
            - 在Ubuntu 18.04.1LTS 下的解决方案（亲测可用），其他版本linux做参考。
            - ``` bash
              # 下载安装字体
              $cd /usr/share/fonts/truetype/
              $sudo git clone https://github.com/abertsch/Menlo-for-Powerline.git
              # 刷新字体
              $sudo fc-cache -f -v
              ```
            - 回到  VScode的用户设置.json  中加入以下代码
            - ``` bash
              "terminal.integrated.fontFamily": "Menlo for Powerline"
              ```
         2. **Mac下配置VScode终端字体：**
            - 在Mac 10.13.6下的解决方案（亲测可用），其他版本做参考。
            - ``` bash
              # 下载安装字体
              $cd /Library/Fonts
              $sudo git clone https://github.com/abertsch/Menlo-for-Powerline.git
              ```
            - 在vscode中设置字体：
            - ``` bash
              "terminal.integrated.fontFamily": "Menlo for Powerline"
              ```
         3. **Windows下配置VScode终端字体：**
            - win10 系统下测试有效。
            - 先[下载字体](https://github.com/abertsch/Menlo-for-Powerline)，下载好的字体点击打开安装
            - 在vscode中设置字体：
            - ``` bash
              "terminal.integrated.fontFamily": "Menlo for Powerline"
              ```