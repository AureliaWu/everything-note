---
layout: "post"
title: "Docker"
date: "2019-06-13 18:52"
categories: microservice,Docker
tags: [Computer Language, microservice, Docker]
---

# 下载、安装及设置(win10)
1. 进入官网进行下载，下载地址: https://hub.docker.com/editions/community/docker-ce-desktop-windows

![docker下载](/data/img/docker/docker_download.png)

最新版需要登录下载，懒得找免登录下载方法，直接注册了个账号,点击`Get Docker`就可以下载啦~下载完就是傻瓜安装，一路next,下载+安装成就达成!

2. 打开cmd，输入`docker version`，出现以下页面表示成功~

![docker下载验证](/data/img/docker/docker_version.jpg)

3. 更换镜像地址(网上搜来的，暂时不知为啥要设)

安装完成后启动可爱的小鲸鱼~首次打开会提示要设置`Hyper-V`，点击确定后电脑自动重启。本部分忘记截图。重启后会在右下角出现萌萌的小鲸鱼图标~~ ![docker启动图标](/data/img/docker/docker_start_logo.png)

右击图标,选择`setting`,选择`Deamon`,在`Registry mirrors`中填入镜像地址:https://registry.docker-cn.com

![docker镜像设置](/data/img/docker/docker_setting.png)

设置完毕后docker会自动重启,打开cmd命令,输入`docker run hello-world`,出现以下页面表示成功

![docker镜像设置验证](/data/img/docker/docker_mirror.png) 

# 应用
业务需要，一脸懵逼的安装好了docker，接下来就是一脸懵逼的应用~

## 使用Docker打包Maven项目镜像
###  准备
-  Docker
-  一个SpringBoot项目
-  一个镜像仓库

### 开始
1. 创建Harbor项目
    - 在公司的Harbor仓库中新建一个项目,用于存放本次打包的镜像文件
2. 配置SpringBoot项目(添加docker配置)
    - 在`pom.xml`中引入docker依赖
    ![docker镜像设置验证](/data/img/docker/docker_mirror.png) 


1.创建harbor项目

2.配置springboot项目

3.配置本地docker的insecure-registries

4.配置maven的setting.xml中server

## 使用docker打包ofbiz项目

不是我打包的，我不知道怎么配置啊。。。o(╥﹏╥)o

直接运行`_docker_depoly`,此名称为自定义，可修改，至于在哪定义的，emmm... ...

![docker打包ofbiz](/data/img/docker/docker_ofbiz.png) 

前人铺路，后人踩坑，于是一运行就有了问题。

// 过几天再更新，emmm...

### 问题集锦

1. 提示用户

