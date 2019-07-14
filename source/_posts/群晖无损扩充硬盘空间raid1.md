---
title: 群晖无损扩充硬盘空间raid1
author: SmalBox
cover: false
top: true
date: 2019-07-14 09:32:17
categories: DIY
tags:
  - 群晖Synology
  - raid1
  - 无损扩容
---
# 群晖无损扩充硬盘空间raid1

## **前言**

群晖（Synology）原本的500G raid1 硬盘阵列坏了一块硬盘，准备换一块新硬盘，但是500g的硬盘和1t硬盘只有10来元的差价，果断入手1t的。那么问题来了，原来的500G可以无损扩充吗，事实证明是可以的，**（重点是！黑白晖都可直插无损修复扩展）**。

接下来演示怎样无损扩展。

## **步骤概要**

   1. 换上1T硬盘，与原来的 500G硬盘 组500G的raid1
   2. 换上另一块1T硬盘，与第一块 500G硬盘 组500G的raid1
   3. 将500G的raid1扩容到1T的raid1

## **恢复到硬盘1**

   1. 将坏掉的硬盘换成新的1T硬盘，然后网页进入nas界面，点击**存储空间管理员**
       ![restoreToNewHardDiskOne1](restoreToNewHardDiskOne1.png)
   2. 在系统概况中看到绿色的未使用的硬盘，即说明硬盘安装无误，点击**存储空间**
       ![restoreToNewHardDiskOne2](restoreToNewHardDiskOne2.png)
   3. 在存储空间中能看到存储状态，点击**按建议在RAID Group设置下单机此处可继续**
       ![restoreToNewHardDiskOne3](restoreToNewHardDiskOne3.png)
   4. 在RAID Group 中，点击**管理**
       ![restoreToNewHardDiskOne4](restoreToNewHardDiskOne4.png)
   5. 点击**修复**
       ![restoreToNewHardDiskOne5](restoreToNewHardDiskOne5.png)
   6. 在选择硬盘界面，将左面的硬盘拖入右面
       ![restoreToNewHardDiskOne6](restoreToNewHardDiskOne6.png)
       ![restoreToNewHardDiskOne7](restoreToNewHardDiskOne7.png)
   7. 进行硬盘检查，默认是否，建议点击是，检查硬盘
       ![restoreToNewHardDiskOne8](restoreToNewHardDiskOne8.png)
   8. 之后会进行数据同步修复
       ![restoreToNewHardDiskOne9](restoreToNewHardDiskOne9.png)
       ![restoreToNewHardDiskOne10](restoreToNewHardDiskOne10.png)
   9. 如图，一个500G 一个1T 硬盘，存储空间500G， 即成功恢复到第一块硬盘
       ![restoreToNewHardDiskOne11](restoreToNewHardDiskOne11.png)

## **恢复到硬盘2**

   1. 将第二块1T硬盘换入到nas中，恢复步骤同上一步，会进行**数据同步**
       ![restoreToNewHardDiskTwo1](restoreToNewHardDiskTwo1.png)
   2. **一致性校验**
       ![restoreToNewHardDiskTwo2](restoreToNewHardDiskTwo2.png)
   3. 如图即恢复到2块1T硬盘组500G raid1的状态
       ![restoreToNewHardDiskTwo3](restoreToNewHardDiskTwo3.png)

## **扩充容量**

   1. 在存储空间中，点击编辑
       ![capacityExpansion1](capacityExpansion1.png)
   2. 将**配置容量**选择**最大化**，点击确定
       ![capacityExpansion2](capacityExpansion2.png)
   3. 显示**扩充文件系统中**
       ![capacityExpansion3](capacityExpansion3.png)
   4. 如图，扩充完成
       ![capacityExpansion4](capacityExpansion4.png)

## **总结**

   - 群晖的raid1还是很方便好用的，只要换上硬盘相互备份即可。*(黑白晖都可直插无损修复扩展)*
   - 群晖的系统我是装到硬盘里了。能让我这样直接抽盘换盘恢复备份，即说明，群晖的2.4G的系统分区也是在每个盘都有备份的。不管是哪个盘挂了，都能随意抽换恢复，体验很好。
   - *（**在恢复过程中有不清楚的，可以评论或发邮件联系我**）*