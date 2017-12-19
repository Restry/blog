---
title: 一步一步搭建Webpack+Babel环境【编写中】
tags:
  - Testing
  - Another Tag
---

文章开始前默认大家已经装好nodejs和喜欢的编辑器（推荐visual studio code，很强大哦），并且了解基本的包管理器使用方法

注：包管理器个人比较偏爱yarn，用npm的同学可以执行npm i yarn -g 来全局添加，linux、mac下记得sudo


## 目录结构
基础示例结构，可以自行按照爱好整理

``` 
- webapp
    - src                #代码开发目录
        - css            #css目录
        + img            #图片资源
        - js             #JS脚本
    - dist                #webpack编译打包输出目录，这个结构将会是webpack自动生成的
        + css                
        + js
    + node_modules        #所使用的nodejs模块
    package.json        #项目配置
    webpack.config.js    #webpack配置
    .babelrc              #babel配置
    README.md            #项目说明
```

## Webpack 设置

webpack.config.js webpack配置文件，详细的可以参考这里[官方配置](https://doc.webpack-china.org/configuration/)

### 初始化
``` bash
yarn init -y
```

### 下载依赖包

``` bash
yarn add webpack
```

### 更新webpack.config.js

``` js
const path = require('path');

module.exports = {
	entry: './src/app.js',
	output: {
		path: path.resolve(__dirname, "dist"),
		filename: 'bundle.js'
	},
	module: {
		loaders: [
			// 使用css-loader解析css模块
			{ test: /\.css$/, loader: 'style!css' },
			// html-loader
			{ test: /\.css$/, loader: 'html-loader' }
		]
	}
};
```

## Babel 设置
这里简单介绍一下Babel的使用场景：

> Babel环境介绍，详细请看[这里](http://www.ruanyifeng.com/blog/2016/01/babel.html)
1. babel-cli  ：命令行转码，直接在终端里面把es6语法的文件给转成es5
2. babel-node ：和node一样，只不过是多了es6的语法
3. babel-register ：babel-register模块改写require命令，为它加上一个钩子。此后，每当使用require加载.js、.jsx、.es和.es6后缀名的文件，就会先用Babel进行转码
4. babel-core ：如果某些代码需要调用Babel的API进行转码，就要使用babel-core模块
5. babel-polyfill ：Babel默认只转换新的JavaScript句法（syntax），而不转换新的API（比如Object.assign）都不会转码。
6. 浏览器环境 ： 就是直接到浏览器里面引用babel的脚本，然后在后面的js中写es6语法，<b>注意：babel6就不支持这样了</b>

> 到webpack里面用babel
1. babel-loader 让webpack引用js时用这个loader来解析
2. babel-core  babel核心，webpack在解析的时候会用到
3. .babelrc babe配置文件，用来设置一些通用的配置，默认配置如下：
``` js
{
  "presets": ["es2015","react","stage-3"], 
  // 设定转码规则，官方提供以下的规则集。
  /*
  # ES2015转码规则
  $ babel-preset-es2015

  # react转码规则
  $ babel-preset-react

  # ES7不同阶段语法提案的转码规则（共有4个阶段），选装一个
  $ babel-preset-stage-0
  $ babel-preset-stage-1
  $ babel-preset-stage-2
  $ babel-preset-stage-3
  */
  "plugins": []
}
```


### 添加必要依赖
``` bash
yarn add babel-loader babel-core  #loader 和核心，上面有介绍  
```

### 修改webpack.config.js
添加必要rule

``` js
    // 使用babel-loader解析js或者jsx模块并排队node_modules目录
    { test : /\.js|.jsx$/, loader : 'babel-loader', exclude: /node_modules/ },
```
### 修改.babelrc文件

先添加依赖

``` bash
yarn add babel-preset-env  #这是一个新的preset，为你识别当前环境并添加合适的转换
```
修改.babelrc
``` js
{
  "presets": ["env", 
    { //这个options的意思就是说自动给我转换成支持chrome52和
      //所有最近浏览器的最后两个版本，再加上ie9
      "targets": {
        "chrome": 52,
        "browsers": ["last 2 versions", "ie 9"]
      }
    }]
}
```
详细的babel-preset-env介绍请看[这里](http://blog.ttionya.com/article-1695.html?utm_source=tuicool&utm_medium=referral)，及[官网英文](http://babeljs.io/docs/plugins/preset-env/#examples-export-with-various-targets)


## package.json
到最后，添加一个build脚本 

```
{
  "name": "tumblr",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "build": "webpack --config webpack.config.js --progress --colors",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "babel-core": "^6.25.0",
    "babel-loader": "^7.0.0",
    "babel-preset-env": "^1.5.2",
    "tumblr.js": "^1.1.1",
    "webpack": "^2.6.1"
  }
}

```