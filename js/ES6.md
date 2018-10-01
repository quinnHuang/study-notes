# ECMAScript
1. 1996.11 -- ES 1.0 - Netscape
2. 1998.06 -- ES 2.0
3. 1999.12 -- ES 3.0 - 广泛支持
4. 2007.10 -- ES 4.0 - 过于激进，惨遭废除
5. 2008.07 -- ES 3.1 - 代号 `Harmony`
6. 2009.12 -- ES 5.0
7. 2010.11 -- ES 5.1 - ISO国际标准
8. 2015.06 -- ES 6.0

# 兼容性
### 浏览器
* IE10+
* Chrome
* Firefox
* NodeJS

### 解决方法
1. 在线转换
2. 提前转换

# ES6 - 变量
### var声明存在的问题
1. 可以重复声明同一个变量
2. 无法限制变量的修改
3. 没有块级作用域

### let与const
1. 限制变量的声明，避免重复声明同一个变量
2. let用于声明变量，const用于声明常量
3. 加入了块级作用域的限制

# ES6 - 箭头函数
```javascript
(args) => {
    express
}
```

1. 如果只有一个参数，则括号可以省略
2. 如果方法体只有一个`return`的表达式，则`{}`和`return`都可以省略

# ES6 - 剩余参数
```javascript
(p1,p2,...args) => {
    express
}
```

1. `...args`表示剩余的所有参数，是一个数组的形式
2. `args`是参数的名称，可自定义
3. 剩余参数必须放在参数列表的最后一个
4. 剩余参数又成可变参数、参数扩展

# ES6 - ...
## 数组展开
```javascript
let arr = [1,2,'a',true];
console.log(...arr);
```

1. 使用`...`表示将数组展开，去掉方括号，将值一个个取出
2. 可以与函数参数`console.log(...arr)`，也可以用于数组赋值`let arr3 = [...arr1,...arr2]`等
3. 不能直接用在等于号后面

## 对象展开
```javascript
let p1 = {name:"xaioming", age:18};
let p2 = {...p1}
```
不论是对象展开还是数组展开，都是对数据的深拷贝

# ES6 - 默认参数
```javascript
let run = (speed = 10, time = 10) => {
    express
}
```

1. 支持函数定义时使用等号对参数进行默认值的赋值

# ES6 - 解构
1. 解构主要用于变量的赋值
2. 解构表达式等号两边的结构必须一样，`[]=[]`,`{}={}`
3. 解构的变量声明和赋值必须在一个表达式完成
4. 解构将右边变量对应位置的值赋值给左边的变量

## 数组解构
```javascript
let [a, b] = [12, "ab"];
let [json, arr, num] = [ {name:"xiaoming", age:18}, ["a", "b"], 100];
```

## 对象解构
```javascript
let {name, age} = {name:"xaioming", age:18};
```

1. 对象解构时左边的变量名必须和右边对象的`key`相同
2. 实际上是这样解构的：通过左右两边相同的`key`将`value`进行赋值
```javascript
let {name:myName, age:myAge} = {name:"xaioming", age:18}；
```
3. 当右边的`key`和`value`是同一个变量名时，可以简写一个

## 数组-对象混用
```javascript
let [{name, age}, [cn, en], json, arr] = [
    {name:"xaioming", age:18},
    [100, 89],
    {a:1, b:2},
    [1, 2, 3]
]
```

# ES6 - 数组
## reduce
```javascript
let result = arr.reduce((previousReturn,current,currentIndex) => {})
```

* previousReturn:表示上一次return的结果，默认初始值是数组的第一个元素
* current:当前的值，从数组的第二个元素开始
* currentIndex:当前元素的下标，从1开始

# ES6 - 字符串新方法
1. startsWith(subStr)
2. endsWith(subStr)

# ES6 - 字符串模板
```javascript
let name = "xiaoming";
let age = 18;

let introduce = `I am ${name}.
I am ${age} years old.`
```

* 使用反单引号(**\`**)包含字符串，使用`${}`直接在字符串中引入变量
* 支持字符串折行，而不用输入`\n`

# ES6 - 面向对象
## class 关键字
```javascript
class Person {
    constructor(name,age) {
        this.name=name;
        this.age=age;
    }
    sayHelloTo(friend){
        return `Hello, ${friend.name}.`;
    }
    sayBye(){
        return `Good Bye!`;
    }
}
```

## extends 继承
```javascript
class Student extends Person {
    constructor(name, age, major) {
        super(name,age);
        this.major=major;
    }
    study(){
        return `I am studying ${this.major}`;
    }
    sayHelloTo(teacher){
        return `Hello, Mr. ${teacher.name}`;
    }
}
```

# ES6 - json
## 标准json写法
1. 只能使用双引号
2. 所有`key`要用双引号包裹起来

```javascript
let json={"name":"xioaming","age":12}
```

## JSON内置对象
* **JSON.stringify(obj)**: 将一个json对象转换为字符串，该json对象可以不是标准json
* **JSON.parse(str)**: 将一个标准json对象的字符串转换成json对象

## json简写
1. 当`key`与`value`的变量名相同时，可以只写一个
```javascript
let name="xiaoming";
let age=18;
let p1={name,age};
```

2. 当`value`是函数时，可以省略`:functiin`
```javascript
let json = {
    run(speed){
        return `Speed is ${speed}km/h`;
    }
}
json.run(10);
```

# ES6 - Promise
Promise是ES6的内置对象，用于处理异步请求
1. 创建Promise对象，构造方法接受哟个函数，函数有两个参数，`resolve`请求成功的函数，`reject`请求失败的函数，同时在函数中发送Ajax请求
```javascript
let pro1 = new new Promise((resolve, reject)=> {
    //Ajax请求
});
```
2. 使用Promise对象的`then(resolveFun,rejectFun)`方法，为Promise对象传递`resolve`和`reject`参数，同时发送请求
```javascript
pro1.then(
    (resolveParam)=>{},
    (rejectParam)=>{}
)
```
3. 使用Promise内置对象的`all(promiseArr)`函数，接收多个Promise对象，再用`then`函数执行，而`then`传递的参数是所有请求结果的数组，而只有所有Promise请求都成功才会执行`resolve`函数
```javascript
Promise.all([pro1,pro2]).then(
    (resolveParams)=>{},
    (rejectParams)=>{}
)
```
4. `race`函数，与`all`相似，但只要有一个成功就执行`resolve`函数
5. Jquery中的`$.ajax()`函数的返回值就是一个Promise对象
6. 使用方式
```javascript
createPromise=(path)=>{
    new Promise(...)
}
Promise.all([
    createPromise(path1),
    createPromise(path2),
    ...]).then(
    (results) => {},
    (err) => {}
)
```
