---
title: 规范格式化url字符串
intro: 'url 补全为标准格式 '
comments: false
date: 2019-02-14 17:17:13
tags:
---

比如有个url字符串为  http:/www.baidu.com => http://www.baidu.com/
  http:/www.baidu.com?t=111  => http://www.baidu.com/?t=111

先把字符串转为URL对象，再获取href

    new URL(str).href