---
title: 使用华为开发者空间云主机编译属于自己的Linux内核
date: 2024-10-31 18:11:35
tags: [技术分享,华为,Linux]
---
# 环境配置
右键桌面点击**Open Terminal Here**
![终端](http://6.nmccl.cn.eu.org:81/d/onedrive/%E5%9B%BE%E7%89%87/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-10-31%20180412.png)

## 下载Linux内核
打开终端后输入如下命令进入root权限
```bash
sudo -i
```
下载Linux内核源码(这里选择的是最新的6.11.5)
```bash
wget https://cdn.kernel.org/pub/linux/kernel/v6.x/linux-6.11.5.tar.xz
```
![img](http://6.nmccl.cn.eu.org:81/d/onedrive/%E5%9B%BE%E7%89%87/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-10-31%20180626.png)
出现这个就是下载完成了
```
2024-10-31 18:36:57 (100.2 kb/s) - 已保存linux-6.11.5.tar.xz [146975304/146975304])
```
解压linux内核
```bash
http://6.nmccl.cn.eu.org:81/d/onedrive/%E5%9B%BE%E7%89%87/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-10-31%20184255.png
```
到Linux内核源码存放文件中
```bash
cd linux-6.11.5/
```
下载并安装编译工具以及依赖
```bash
apt-get install git fakeroot build-essential ncurses-dev xz-utils libssl-dev bc flex libelf-dev bison
```
![img](http://6.nmccl.cn.eu.org:81/d/onedrive/%E5%9B%BE%E7%89%87/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-10-31%20180909.png)
这里输入y接着安装
![img](http://6.nmccl.cn.eu.org:81/d/onedrive/%E5%9B%BE%E7%89%87/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-10-31%20182634.png)

## 配置Linux内核编译
创建默认Linux配置文件
```bash
make defconfig
```


尽情定制你的Linux内核
```bash
make menuconfig
```
![img](http://6.nmccl.cn.eu.org:81/d/onedrive/%E5%9B%BE%E7%89%87/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-10-31%20185056.png)

## 开始编译
-j后面为线程数，一般情况是cpu核心数量的2倍
```bash
make -j 4
```
开始跑码等待完成
![img](http://6.nmccl.cn.eu.org:81/d/onedrive/%E5%9B%BE%E7%89%87/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-10-31%20185555.png)

