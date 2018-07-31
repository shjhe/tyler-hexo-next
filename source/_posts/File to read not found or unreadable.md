---
title: File to read not found or unreadable
date: 2018-07-30 14:42:00
updated: 2018-07-31 09:56:00
tags:
  - create-react-app
  - node-sass-chokidar
  - node-sass
  - bug
categories:
  - create-react-app
  - react
---

## 背景
最近用create-react-app构建react项目过程中，使用官方推荐的方法处理scss文件的编译问题，即`node-sass-chokidar`，编辑器使用VSCode，在修改scss文件并保存的过程中，出现编译失败的问题，报错内容为`File to read not found or unreadable`，具体如下
```javascript
{
  "status": 3,
  "message": "File to read not found or unreadable: E:/learn/react-app1/src/index.scss",
  "formatted": "Internal Error: File to read not found or unreadable: E:/learn/react-app1/src/index.scss\n"
}
```
## 解决
直接上github的Issue找，这种问题一般不会是个人问题，果不其然，发现了相关的Issue，一步一步跟进最终找到了解决方法，在node-sass项目的Issue下，解决要点：
* 由`marcosbozzani`大神做了修复，修复分支`bug-vscode-watch`
* 此时node-sass最新版本为`4.9`，版本中未处理此问题
* 需要手动修复，替换`node_modules/node-sass/lib/render.js`为[render.js](https://github.com/marcosbozzani/node-sass/blob/bug-vscode-watch/lib/render.js)

此问题并不是node-sass的问题，主要是vscode锁定了文件而造成了文件不可读，`marcosbozzani`大神是这么说的`The problem seems to be VSCode is still holding the file while node-sass try to access it.`

在此记录一下问题及解决方法，分享给有需要的朋友

## 补充（`亲测`）
在Linux下使用vscode编辑时，是不会出现这种问题的，所以其实也不能完全说是vscode的问题，要说也只能说是windows系统的问题，简直就是开发者的地狱呀！！[Deepin](https://www.deepin.org/)
> 我用的linux是Deepin的系统，对于一个国内的开发者，这个系统很友好，大部分开发相关的软件都能装上，在此推荐一下<br>如果在安装使用过程中遇到什么问题，可以一起讨论学习，本人装的是双系统