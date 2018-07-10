---
title: window下使用node管理nginx
date: 2018-07-10 22:50:38
tags:
  - nginx
  - node
categories:
  - node工具
---

制作念头：项目开发者个人需要搭建个人的nginx，作为代理老项目和Vue服务端渲染项目，而nginx配置文件需要不断更新且共享，项目一开始使用Q群沟通更新配置，不用说这种方式肯定很Low，而且总所周知nginx在window下管理是有多麻烦，更新配置要关掉进程再重启，当然使用.bat脚本也可以方便操控，但是更新配置文件有头大了；因此我就想着如果能像在Linux操作nginx一样方便，那就方便多了，于是乎我就写用node写了这个工具，具体的使用方法如下：

## 安装

``` sh
npm install -g nginx-in-node
# or
yarn global add nginx-in-node
```
## 配置nginx [下载链接](http://nginx.org/en/download.html)

配置Path系统变量，目录级别到nginx.exe即可

## 使用
### 参数

```sh
node-nginx [-s [stop/reload/quit]] [-f [configPath]]
```

1. -s使用nginx默认的命令，含有stop/reload/quit
2. -f为自定义选择配置文件，文件路劲命令最好在git-bash下使用

### 常用命令
1. 常规启动
> 启动之前会先关闭已有的所有nginx进程，因此此命令也可为重启命令

```sh
node-nginx [-f configPath]
```

2. 重启

```sh
node-nginx -s reload [-f configPath]
```

3. 停止

```sh
node-nginx -s stop [-f configPath]
```
## 效果展示
![QQ截图20180710231815](/hexo/images/201807/QQ截图20180710231815.jpg)