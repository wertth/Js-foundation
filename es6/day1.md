# 1.es6 基础
 es6环境: 基本除了Ie6-11 都可以支持es6
 
## Webpack


#### js 循环 tips
```js
Label : {
    //这里是代码块
    if(condition) break Label; //break 可用于终结标签 
    //
} 
```

#### js switch
```js
switch(x){
    case 'a': //严格相等
        ...
        break;
} // switch case 运行任意表达式 
```


#### 函数 
1. 注意: js 的函数 为值修改 是原来存储变量的拷贝
2. 现在的js已经支持默认参数 而在一些老代码中 为了实现默认参数有如下方式
```js
function f1(variable1, variable2){
    variable1 = variable1 || "not given"
        ...
}
```
3. 注意现代js 支持控制运算符号 如下例子：
```js
function f1(variable1){
    console.log(f1 ?? 'not given') // 注意这里是空值合并运算符 
    // 如 a ??  b 如果a 定义的 则a 如果b为非定义的 则为b 等价于 (a !== null && a !== undefined) ? a : b
}
f1()
'not given'
f1(a)
a 
```
4. 函数的返回值 ，若函数无return 或 return ； 则函数返回 undefined 
例子:
```js
function func(){}
func() == undefined
true
```
练习1.  重写以下函数 并使得代码量最小
```js
function checkAge(age) {
  if (age > 18) {
    return true;
  } else {
    return confirm('Do you have your parents permission to access this page?');
  }
}
```
答案:
```js
function checkAge(age){ return (age>18)?true:confirm('Do you have your parents permission to access this page?') }
function checkAge(age){ return (age>18)||confirm('Do you have your parents permission to access this page?') }
```
5. 注意: 函数 在js中本质为一个值 而非特殊数据结构 如下，函数可复制
```js
function sayHi() {   // (1) 创建
  alert( "Hello" );
}

let func = sayHi;    // (2) 复制

func(); // Hello     // (3) 运行复制的值（正常运行）！
sayHi();
```

### 回调函数
```js
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}

function showOk() {
  alert( "You agreed." );
}

function showCancel() {
  alert( "You canceled the execution." );
}

// 用法：函数 showOk 和 showCancel 被作为参数传入到 ask
ask("Do you agree?", showOk, showCancel);
```
```js
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}

ask(
  "Do you agree?",
  function() { alert("You agreed."); },
  function() { alert("You canceled the execution."); }
);
```
6.严格模式下，当一个函数声明在一个代码块内时，它在该代码块内的任何位置都是可见的。但在代码块外不可见。(注意当在代码块中做函数声明时，外部不可见，若是改成函数表达式赋值，则外部可见)
例如：
```js
if(age > 18){
    function welcome() {
        ...
    }
}
welcome() //undefined
if(age > 18 ){
    let welcome = function () {
        ...
    }
}
welcome() // undefined
let welcome;
if(age > 18 ){
     welcome = function () {
    ...
    }
}
welcome() // ok

```
7.在执行代码块之前，内部算法会先处理函数声明。所以函数声明在其被声明的代码块内的任何位置都是可见的