---
title: React 性能优化【一】
category: react
tags:
  - react
  - performance
  - optimizing
date: 2017-07-23 23:01:22
---


# Production Build
在webpack中设置环境变量

# 直接引用
建议使用已经编译好的文件，简单大方，直接引用:

``` html
<script src="https://unpkg.com/react@15/dist/react.min.js"></script>
<script src="https://unpkg.com/react-dom@15/dist/react-dom.min.js"></script>
```

# react

## 加上这样一样插件，是因为生产环境的一些常量转换问题带来的性能影响

``` json // package.json
  "babel": {
    "env": {
      "production": {
        "plugins": [
          "transform-react-constant-elements",
          "transform-react-inline-elements"
        ]
      }
    }
  },
```

