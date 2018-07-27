---
title: Vue-Router路由嵌套理解
date: 2018-07-27 10:43:08
tags:
  - Vue-Router
categories:
  - Vue生态
  - 前端框架
---

## 背景
最近有个初学Vue的朋友问我，为什么我的两层路由跳不起来了，直接输url也不行？信息不是很充足及看不到源码的我，当时是那个一脸懵逼啊，心想这肯定是代码的问题，跟层级无关。接着我继续追问...(省略)...大致明白了情况，原来这位朋友没有理解Vue-Router嵌套的原理，下面整理了一下我对Vue-Router路由嵌套的理解

## Vue-Router嵌套路由
首先假设项目中有两个路由Profile和Posts，按写法把他们定义为一层路由，是`Root的子路由`，因此Root中要有`router-view`组件去承载子路由，才能实现子路由切换展示
### 一层路由
#### Root容器
```html
  <div>
    <h1>Root</h1>
    <!-- 承载子路由的容器 -->
    <router-view />
  </div>
```
#### 一层路由写法
```javascript
[
  {
    path: '/profile'
    component: profile // 组件引用 此处省略引用
  },
  {
    path: '/posts'
    component: posts // 组件引用 此处省略引用
  },
]
```

#### 一层路由展示
Root的子路由展示是在Root中的，切换路由其实只是切换了`router-view`容器的内容
```
/profile                              /posts
+------------------+                  +-----------------+
| Root             |                  | Root            |
| +--------------+ |                  | +-------------+ |
| | Profile      | |  +------------>  | | Posts       | |
| |              | |                  | |             | |
| +--------------+ |                  | +-------------+ |
+------------------+                  +-----------------+
```

### 二层路由
在上面的基础上，对profile加一层路由
#### profile容器
```html
  <div>
    <h1>profile</h1>
    <!-- 承载profile子路由的容器 -->
    <router-view />
  </div>
```

#### profile子路由
```javascript
[
  {
    path: '/profile'
    component: profile, // 此处不能少
    children: [
      {
        path: '/profile/list',
        component: profileList
      },
      {
        path: '/profile/item',
        component: profileItem
      }
    ]
  },
  ...
]
```

#### 二层路由展示
和一层路由相同的是，Profile的子路由是在Profile容器中切换展示的，`所以Profile路由的component是必不可少的`
```
/profile/list                         /profile/item
+------------------+                  +-----------------+
| Root             |                  | Root            |
| +--------------+ |                  | +-------------+ |
| | Profile      | |  +------------>  | | Profile     | |
| | +----------+ | |                  | | +---------+ | |
| | | list     | | |                  | | | item    | | |
| | |          | | |                  | | |         | | |
| | +----------+ | |                  | | +---------+ | |
| +--------------+ |                  | +-------------+ |
+------------------+                  +-----------------+
```

## 路由嵌套总结
任何子路由都是在其父路由的组件中切换显示，不管是多少层的路由嵌套，都是这样的理解，所以父路由需要有以下两点，二者缺一不可
* `有组件引用`
* `组件中有router-view组件`

而我那个朋友就是父路由没有引用组件，导致子路由没有承载容器，自然而然就出现了他说的不起效的情况，这里把经验分享给大家，希望能对初学者有帮助