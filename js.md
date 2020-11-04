**es6**

```
var count = 30; // 不会抛出错误
if (condition) { let count = 40; // 其他代码 }
```

if 语句内部创建了一个新的 count 变 量，而不是在同一级别再次创建此变量。在 if 代码块内部，这个新变量会屏蔽全局的 count 变量，从而在局部阻止对于后者的访问。

const 声明会阻止对于变量绑定与变量自身值的修改，这意味着 const 声明并不会阻止对 变量成员的修改

```
const person = { name: "Nicholas" };
// 工作正常
person.name = "Greg";
// 抛出错误
person = { name: "Greg" };
```

let 或 const ，虽然在全局作用域上会创建新的绑定，但不会有任何属性被添加到全局对象上。这也就意味着你不能使用 let 或 const 来覆盖一个全 局变量，你只能将其屏蔽

```
let RegExp = "Hello!"; console.log(RegExp); // "Hello!"
console.log(window.RegExp === RegExp); // false
const ncz = "Hi!"; console.log(ncz); // "Hi!"
console.log("ncz" in window); // false
```

在非严格模式下， arguments 对象总是会被更新以反映出具名参数的变化。因此当 first 与 second 变量被赋予新值时， arguments[0] 与 arguments[1] 也就相应地更新了，使得这 里所有的 === 比较的结果都为 true

```
function mixArgs(first, second) {
   console.log(first === arguments[0]); //true
   console.log(second === arguments[1]); //true
   first = "c"; 
   second = "d"; 
   console.log(first === arguments[0]); //true
   console.log(second === arguments[1]); //true
}

mixArgs("a", "b");
```

然而在 ES5 的严格模式下，关于 arguments 对象的这种混乱情况被消除了，它不再反映出 具名参数的变化。
```
function mixArgs(first, second) {
  "use strict";
   console.log(first === arguments[0]); //true
   console.log(second === arguments[1]); //true
   first = "c"; 
   second = "d"; 
   console.log(first === arguments[0]); //false
   console.log(second === arguments[1]); //false
}

mixArgs("a", "b");
```

然而在使用 ES6 参数默认值的函数中， arguments 对象的表现总是会与 ES5 的严格模式一 致，无论此时函数是否明确运行在严格模式下。参数默认值的存在触发了 arguments 对象与 具名参数的分离
```
function mixArgs(first, second = "b") {
   console.log(arguments.length); //1
   console.log(first === arguments[0]); //true
   console.log(second === arguments[1]); //false
   first = "c"; 
   second = "d" 
   console.log(first === arguments[0]); //false
   console.log(second === arguments[1]); //false
}
mixArgs("a");
```
本例中 arguments.length 的值为 1 ，因为只给 mixArgs() 传递了一个参数。这也意味着 arguments[1] 的值是 undefined ，符合将单个参数传递给函数时的预期；这同时意味着 first 与 arguments[0] 是相等的。改变 first 和 second 的值不会对 arguments 对象造 成影响，无论是否在严格模式下，所以你可以始终依据 arguments 对象来反映初始调用状 态。

**参数默认值表达式**
```
function getValue() { return 5; }
function add(first, second = getValue()) { 
  return first + second; 
}
console.log(add(1, 1)); // 2 
console.log(add(1)); // 6
```
此处若未提供第二个参数， getValue() 函数就会被调用以获取正确的默认值。需要注意的 是，仅在调用 add() 函数而未提供第二个参数时， getValue() 函数才会被调用，而在 getValue() 的函数声明初次被解析时并不会进行调用。这意味着 getValue() 函数若被写为 可变的，则它有可能会返回可变的值，例如：