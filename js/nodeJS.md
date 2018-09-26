# 内置模块
* http
* url
* events
* util
* fs


# 导出模块
## module.exports
1. 以对象形式导出  
```javascript
module.exports = {
    hello: hello,
    greet: greet
};
```
2. 键值的形式
```javascript
module.exports.foo = foo;
module.exports.bar = bar;
```
3. 函数赋值
```javascript
module.exports = greet;
```

## exports
1. 键值的形式
```javascript
exports.hello = hello;
exports.greet = greet;
```
2. ES6的导出方式  
变量的`导出-声明-赋值`必须同时完成
```javascript
export const a = 1;
export const incCounter = function() {
    counter ++;
}
```
`default`关键字，用于匿名变量的导出，类的导出也要用`default`
```javascript
export default { x: 1 };
export default function() {};
```


# 导入模块
## require
1. 指定模块名
```javascript
var greet = require('./hello');
```
模块名不用带扩展名，而且要使用相对路径的形式
2. ES6的导入方式
```javascript
import App from './App';
```
* 导入多个函数时，可以用`{func1,func2}`的形式导入多个函数
* 导入和导出的函数名称必须一致
* 导入的文件路径必须以`./`开头

3. 名称空间
使用`* as`给一个模块的多个函数起一个共同的名称空间，避免不同模块之间函数同名的冲突，此时函数名称要用`*`代替
```javascript
import * as math from './math.js';
```


# 全局变量
* console：控制台
* setTimeout：定时器
* setInterval：重复定时器
* clearInterval：清除定时  
* \_\_dirname：当前目录
* \_\_filename：当前文件
......

# 事件机制
**相关模块**：`events`, `util`  
1. 创建事件对象
```javascript
let e1 = new events.EventEmitter();
```

2. 注册事件和行为
```javascript
e1.on("eventName", function(eventParameter){});
```

3. 触发事件
```javascript
e1.emit("eventName",eventParameter);
```
4. 使用`util`实现时间继承
`util` 模块的`inherits(subClass,superClass)` 方法可实现类或对象之间的继承  
```javascript
const events = require("events");
const util = require("util");
let Person = function(name){
    this.name=name;
};
util.inherits(Person,events.EventEmitter);
```

# npm
## 下载安装模块
> npm install **moduleName**

使用`-g`选项可以为安装的模块设置全局的命令
> npm install -g **moduleName**

## package.json
用于记录项目中的依赖包，方便项目导出和重新添加依赖  
### 初始化package.json
> npm init

然后一路回车即可
### dependencies和devDependencies
`dependencies`是记录项目的所有依赖，使用`--save`参数可以在安装依赖时将依赖记录到`dependencies`的值中。
> npm install --save **moduleName**

`devDependencies`是记录开发环境的依赖，使用`--save-dev`可以记录依赖
> npm install --save-dev **moduleName**

### scripts
记录项目执行的相关命令，初始包括`start`, `test`命令。使用`run`可以执行命令。
> npm run **cmd**

# 文件操作
## fs模块
1. 同步读写
    * 读：`readFileSync("filePath","code-set")`
    * 写：`writeFileSync("filePath","content")`

```javascript
const fs = require("fs");
let read = fs.readFileSync("./hello.txt","utf8");
fs.writeFileSync("./nodejs.txt","This is Node JS.");
```

2. 异步读写
    * 读：`readFile("filePath","code-set",(err,data)=>{})`
    * 写：`writeFile("filePath","content",()=>{})`

```javascript
const fs = require("fs");
fs.readFile("./hello.txt","utf8",(err,data)=>{
    console.log("read complete!");
    fs.writeFile("./nodejs.txt","This is Node JS file.",()=>{
        console.log("write complete!");
    })
});
```
