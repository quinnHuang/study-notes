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
