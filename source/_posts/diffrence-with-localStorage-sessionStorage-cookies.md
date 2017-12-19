---
title: sessionstorage, localstorage 和 Cookies 的差别
tags:
  - SessionStorage
  - LocalStorage
  - Cookies
  - Cache
  - 缓存
---

# 这三个东西的相似之处

- 都是运行在客户端
- 这三种都有自己不同的存储方式和过期控制

# 不同之处

## localStorage
- 没有到期时间
- 添加和删除只能通过js。或者可以通过清除浏览器缓存也可以清除localStorage数据。
- 可存储10mb
- 在当前域可用
- 常用于存储购物车之类的本地数据

## sessionStroage
- 类似于localStorage但是在浏览器关闭时会清除。不是tab页关闭，是整个浏览器。
- 可存储5mb，
- 在当前域可用
- 常用于存储购物车之类的本地数据


local和session支持大于或等于这些版本的浏览器：IE 8，Firefox 3.5，Safari 4，Chrome 4，Opera 10.5，iOS 2.0，Android 2.0
不随http传输，只到本地处理。

## cookies
- client端也可以通过js设置数据及过期时间，但主要用于服务器端的交互来设置缓存到本地。
- 每次http交互都会随request一起, 而localStorage与sessionStorage只能在客户端操作。可设置httponly只让网络传输使用。
- 可存储4kb文本。
- 安全性比其它两种高
- 常用存储token之类的标识信息


[详细介绍](http://tutorial.techaltum.com/local-and-session-storage.html)

[还有一篇写得不错的](http://jerryzou.com/posts/cookie-and-web-storage/)