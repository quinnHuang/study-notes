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
