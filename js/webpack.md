# webpack
* JS文件的打包工具
* 转化nodeJS语法中的`export`, `improt`等成分为浏览器能够识别的内容

## 下载安装
> npm install -g webpack  

> npm install -g webpack-cli

## 打包JS文件
将`main.js`中的代码和引用的模块的代码都打包到`all.js`文件中。

> webpack **main.js** -o **all.js**

## webpack.config.js
* 使用`webpack.config.js`文件配置管理webpack的工作
* 在项目根目录下创建该文件
* 使用nodeJS语法编写配置信息

```javascript
const path = require('path');

module.exports = {
    //打包的入口文件
    entry: './src/index.js',
    //打包的出口文件
    output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
    },
    //监听修改，自动打包
    watch:true
};
```

## 配置babel
babel主要用于JS文件打包时的语法翻译，可将ES版本高的代码翻译成低版本的代码，以兼容IE等浏览器  
**相关依赖**：`babel=-core`, `babel-loader`, `babel-preset-env`
> npm install --save-dev babel-core
npm install --save-dev babel-loader
npm install --save-dev babel-preset-env

## webpack-dev-server配置虚拟服务
更改启动项目的方式  
> webpack-dev-server --content-base **根路径** --port **端口**

在`webpack.config.js`的`output`参数中添加一项：
> publicPath:**自定义虚拟路径**
