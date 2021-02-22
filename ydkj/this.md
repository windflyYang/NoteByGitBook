function foo() {
	console.log( this.bar );
}
var bar = "global";
var obj1 = {
	bar: "obj1",
	foo: foo
};
var obj2 = {
	bar: "obj2"
};

foo();				// "global"
obj1.foo();			// "obj1"
foo.call( obj2 );	// "obj2"
new foo();			// undefined
关于this如何被设置有四个规则，它们被展示在这个代码段的最后四行中：
foo()最终在非strict模式中将this设置为全局对象 —— 在strict模式中，this将会是undefined而且你会在访问bar属性时得到一个错误 —— 所以this.bar的值是global。
obj1.foo()将this设置为对象obj1。
foo.call(obj2)将this设置为对象obj2。
new foo()将this设置为一个新的空对象。
底线：要搞清楚this指向什么，你必须检视当前的函数是如何被调用的。它将是我们刚刚看到的四种中的一种，而这将会回答this是什么。
注意： 关于this的更多信息，参见本系列的 this与对象原型 的第一和第二章。