vue 只有实例被创建时就已经存在data中的数据才是响应式的

不要在选项 property 或回调上使用箭头函数，比如 created: () => console.log(this.a) 或 vm.$watch('a', newValue => this.myMethod())。因为箭头函数并没有 this，this 会作为变量一直向上级词法作用域查找，直至找到为止，经常导致 Uncaught TypeError: Cannot read property of undefined 或 Uncaught TypeError: this.myMethod is not a function 之类的错误


<!-- ![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1") -->
![alt text](/public/img/lifecycle.png)

vue的每个组件都会各自独立维护自己的状态,因为每用一次组件就有一个实例被创建
一个组件的data 必须是一个函数 因此每个实例可以维护一份被返回对象的独立的拷贝

v-bind 可以动态赋值