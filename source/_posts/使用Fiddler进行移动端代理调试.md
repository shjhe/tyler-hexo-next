---
title: 使用Fiddler进行移动端代理调试
date: 2018-07-16 17:00:35
tags:
 - fiddler
 - 移动端代理
categories:
  - 前端工具
---

1. 打开options
> 菜单栏点击Tools，然后在弹出的下拉列表中点击第一个options

![20180716172421](/hexo/images/201807/20180716172421.png)

2. 配置HTTPS
> 如果需要的话，配置如图

![TIM截图20180716173134](/hexo/images/201807/TIM截图20180716173134.png)

2. 配置端口
> 配置如图

![TIM截图20180716173551](/hexo/images/201807/TIM截图20180716173551.png)

> 整体配置比较简单，如果网站是https的需要开启第二步，否则监听不到的，其次如果偏向H5的真机调试，推荐[spy-debugger](https://www.npmjs.com/package/spy-debugger)，这里有个weinre可以调试网页查看控制台输出，个人觉得很有用