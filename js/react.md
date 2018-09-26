## 准备工作
1. 安装NodeJS
2. 安装 `webpack`
> npm install -g webpack  
npm install -g webpack-cli

3. 初始化项目
> npm init -y

4. 创建项目目录
* node_module
* src
    * mian.js
* dist
    * bundle.js
* index.html
* package.json
* webpack.config.js

5. 配置`webpack.config.js`
```javascript
const path = require('path');
module.exports={
    entry: './src/main.js',
    output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'bundle.js'
    },
    watch:true,
    mode:"development"
}
```
