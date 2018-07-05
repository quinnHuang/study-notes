## 如何引用JavaScript
* 内部引用
```javascript
    <script type="text/javascript">
      document.write("Hello World!");
    </script>
  ```
* 外部引用
```javascript
    <script type="text/javascript" src="./main.js"></script>
```
---
## 创建变量
* 方式一
```javascript
    var name = 'Bob';
    var age = 16;
    var stuNo = 0012323;
```
* 方式二
```javascript
    var name = 'Bob',
        age = 16,
        stuNo = 0012323;
```
---
## 数据类型
JavaScript是一种 *弱类型* 或者说 *动态语言*  
* 原始类型
    1. Boolean（布尔类型）：包括true和false
    2. Null类型：null，表示空值
    3. Undefined类型：Undefined，表示未定义或未赋值
    4. Number(数字类型)：除了数字还包括 **+Infinity**（正无穷），**-Infinity**（负无穷）和 **NaN**（非数字）
    5. String（字符串类型）：用 **""**（双引号）或 **''**（单引号）包起来

* 对象类型：Object
  1. 使用构造函数创建对象
```javascript
      var o = new Object();
```
  2. 直接创建对象
  ```javascript
      var person = {
          name: 'Bob',
          age: 20,
          gender: 'male'
      };
```

* typeof操作符
对一个值使用typeof操作符可能返回下列某个字符串：
  * 'undefined' —— 未定义
  * 'boolean' —— 布尔值
  * 'string' —— 字符串
  * 'number' —— 数字值
  * 'object' —— 对象或null
  * 'function' —— 函数

  使用typeof的示例：
  ```javascript
    var message = 'some string';
    alert(typeof message); // "string"
    alert(typeof(message)); // "string"
    alert(typeof 95); // number
```
---
## 运算符
* 算数运算符
  * 加：+
  * 减：-
  * 乘：*
  * 除：/
  * 取模：%
  * 自增：++，右结合
  * 自减：--，右结合
* 赋值：=
* 算数运算与赋值结合
  * 加等于：+=
  * 减等于：-=
  * 乘等于：\*=
  * 除等于：/=
  * 取模等于：%=
* 关系运算符
  * 等于：==（只比较值，不比较类型）、===（严格等于）
  * 大于或大于等于：>、>=
  * 小于或小于等于：<、<=
* 逻辑运算符
  * 逻辑与运算符：&&
  语法: 运算结果 = 表达式1 && 表达式2
  只有两个表达式同为true，结果才能为true
  * 逻辑或运算符：||
  语法: 运算结果 = 表达式1 || 表达式2
  只有两个表达式只要有一个为true，结果就是true
  * 逻辑非运算符：!
  语法: 运算结果 = !表达式
  把true变成false，false变成true
* 非boolean类型转boolean类型
  * 转为false：null , NaN , 0 , 空字符串("") , undefined
  * 转为true：除以上的所有

## 条件分支
----
* if语句
  ```javascript
    if (condition){
      // 当 condition==true 时执行的语句块
    }
  ```
* if-else语句
  ```javascript
    if (condition){
      // 当 condition==true 时执行的语句块1
    } else {
      // 当 condition==false 时执行的语句块2
    }
  ```
* if-else if-else语句
  ```javascript
    if (condition1){
      // 当 condition1==true 时执行的语句块1
    } else if (condition2){
      // 当 condition2==true 时执行的语句块2
    } else {
      // 当 condition1==false && condition2==false 时执行的语句块3
    }
  ```
* switch语句
  ```javascript
    switch(n){
      case n1:
        执行代码块 1
        break;
      case n2:
        执行代码块 2
        break;
      default:
        与 case n1 和 case n2 不同时执行的代码块3
    }
  ```
