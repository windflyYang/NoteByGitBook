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

JS 为函数提供了两个不同的内部方法： [[Call]] 与 [[Construct]] 。当函数未使用 new 进行调用时， [[call]] 方法会被执行，运行的是代码中显示的函数体。而当函数使用 new 进行调用时， [[Construct]] 方法则会被执行，负责创建一个被称为新目标的新的对象，并且使用该新目标作为 this 去执行函数体。拥有 [[Construct]] 方法的函数被称为构造器。
并不是所有函数都拥有 [[Construct]] 方法，因此不是所有函数都可以用 new 来 调用 箭头函数就未拥有new方法

```
function Person(name) { 
   if (this instanceof Person) { 
      this.name = name; // 使用 new 
   } else { 
      throw new Error("You must use new with Person.") 
   } 
}
var person = new Person("Nicholas"); 
var notAPerson = Person("Nicholas"); // 抛出错误
```
此处对 this 值进行了检查，来判断其是否为构造器的一个实例：若是，正常继续执行；否 则抛出错误。这能奏效是因为 [[Construct]] 方法创建了 Person 的一个新实例并将其赋值 给 this 。可惜的是，该方法并不绝对可靠，因为在不使用 new 的情况下 this 仍然可能 是 Person 的实例，正如下例：
```
function Person(name) { 
   if (this instanceof Person) { 
      this.name = name; // 使用 new 
   } else { 
      throw new Error("You must use new with Person.") 
   } 
}
var person = new Person("Nicholas"); 
var notAPerson = Person.call(person, "Michael"); // 奏效了！
```
调用 Person.call() 并将 person 变量作为第一个参数传入，这意味着将 Person 内部的 this 设置为了 person 。对于该函数来说，没有任何方法能将这种方式与使用 new 调用区 分开来。
为了解决这个问题， ES6 引入了 new.target 元属性。元属性指的是“非对象”（例如 new ） 上的一个属性，并提供关联到它的目标的附加信息。当函数的 [[Construct]] 方法被调用 时， new.target 会被填入 new 运算符的作用目标，该目标通常是新创建的对象实例的构造 器，并且会成为函数体内部的 this 值。而若 [[Call]] 被执行， new.target 的值则会是 undefined
通过检查 new.target 是否被定义，这个新的元属性就让你能安全地判断函数是否被使用 new 进行了调用。
```
function Person(name) { 
   if (typeof new.target !== "undefined") { 
      this.name = name; // 使用 new 
   } else { 
      throw new Error("You must use new with Person.") 
   } 
}
var person = new Person("Nicholas"); 
var notAPerson = Person.call(person, "Michael"); // 出错！
```
使用 new.target 而非 this instanceof Person ， Person 构造器会在未使用 new 调用时 正确地抛出错误。 也可以检查 new.target 是否被使用特定构造器进行了调用，
```
function Person(name) { 
   if (new.target === Person) { 
      this.name = name; // 使用 new 
   } else { 
      throw new Error("You must use new with Person.") 
   } 
}
function AnotherPerson(name) { 
   Person.call(this, name); 
}
var person = new Person("Nicholas"); 
var anotherPerson = new AnotherPerson("Nicholas"); // 出错！
```
>警告：在函数之外使用 new.target 会有语法错误。

**typeof instanceof**
typeof 一元运算
- 运算数为数字 typeof(x) = "number" 
- 函数 typeof(x) = "function" 
- 字符串 typeof(x) = "string" 
- 布尔值 typeof(x) = "boolean" 
- 对象,数组和null typeof(x) = "object" 
判断一个变量是否存在
```
if(typeof a !== 'undefind')
if(a) //如果a没有被定义会报错 
instanceof 运算符用来测试一个对象在其原型链中是否存在一个构造函数的 prototype 属性
instanceof 用于判断一个变量是否某个对象的实例
参数：object（要检测的对象.）constructor（某个构造函数）
描述：instanceof 运算符用来检测 constructor.prototype 是否存在于参数 object 的原型链上
```
**箭头函数**
- 没有 this 、 super 、 arguments ，也没有 new.target 绑定： this 、 super 、 arguments 、以及函数内部的 new.target 的值由所在的、最靠近的非箭头函数来决定
- 不能被使用 new 调用： 箭头函数没有 [[Construct]] 方法，因此不能被用为构造函 数，使用 new 调用箭头函数会抛出错误。
- 没有原型： 既然不能对箭头函数使用 new ，那么它也不需要原型，也就是没有 prototype 属性。 
- 不能更改 this ： this 的值在函数内部不能被修改，在函数的整个生命周期内其值会 保持不变。 
- 没有 arguments 对象： 既然箭头函数没有 arguments 绑定，你必须依赖于具名参数或 剩余参数来访问函数的参数。 
- 不允许重复的具名参数： 箭头函数不允许拥有重复的具名参数，无论是否在严格模式 下；而相对来说，传统函数只有在严格模式下才禁止这种重复。

箭头函数的声明规则
- 如果没有参数 必须用一对小括号
- 如果只有一个参数 可以直接写 而不需要其他语法  var reflect = value => value;
- 如果有多个参数 必须带上小括号 多个参数之间逗号隔开 var sum = (num1, num2) => num1 + num2;
- 如果创建一个空函数 后面必须用{} var doNothing = () => {};  
- 如果函数体内有多行语句 也必须用{}包裹
- 若箭头函数想要从 函数体内向外返回一个对象字面量，就必须将该字面量包裹在圆括号内 var getTempItem = id => ({ id: id, name: "Temp" });将对象字面量包裹在括号内，标示了括号内是一个字面量而不是函数体。

JS 中使用函数的一种流行方式是创建立即调用函数表达式（ immediately-invoked function expression ， IIFE ）
```
let person = ((name) => { 
   return { getName: function() { return name; } }; 
})("Nicholas"); 
console.log(person.getName()); // "Nicholas"
```

箭头函数没有this绑定 意味着箭头函数内部的this值只能通过查找作用域确定。如果箭头函数被包含在一个非箭头函数内，那么 this 值就会与该函数的相等；否则， this 值就会是全局对象（在浏览器中是 window ，在 nodejs 中是 global ）
>由于箭头函数的 this 值由包含它的函数决定，因此不能使用 call() 、 apply() 或 bind() 方法来改变其 this 值
