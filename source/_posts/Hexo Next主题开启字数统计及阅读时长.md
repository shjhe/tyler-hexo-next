---
title: Hexo Next主题开启字数统计及阅读时长
date: 2018-07-04 11:34:56
tags: Hexo Next配置
categories: Hexo使用
---

> 注：Next主题版本 v6.3.0，以前的版本好像不是这么配置的

## 安装 hexo-symbols-count-time
> 注：只需要在hexo下安装此插件（ yarn npm 随意）

```bash
  yarn add hexo-symbols-count-time
```

## 配置
### hexo _config.yaml
> 这是显示的基础配置，next主题初始配置默认显示了，只需要hexo这边配置即可，注：修改此配置需要重启服务才能更新

``` yaml
  symbols_count_time:
    symbols: true # 文章字数
    time: true # 阅读时长
    total_symbols: true # 所有文章总字数
    total_time: true # 所有文章阅读中时长
```

### next _config.yaml
> 修改此配置无需要重启服务即可更新

``` yaml
  symbols_count_time:
    separated_meta: true  # 是否换行显示 字数统计 及 阅读时长
    item_text_post: true  # 文章 字数统计 阅读时长 使用图标 还是 文本表示
    item_text_total: false # 博客底部统计 字数统计 阅读时长 使用图标 还是 文本表示
    awl: 4
    wpm: 275
```

具体可查看 [symbols_count_time](https://github.com/theme-next/hexo-symbols-count-time)