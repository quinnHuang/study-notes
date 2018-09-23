# 内置模块
* http
* url
* events
* util


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
```javascript
export let a = 1;
export function incCounter() {
    counter ++;
}
```
`default`关键字，用于匿名变量的导出
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
