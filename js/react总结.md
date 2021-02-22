react用于构建用户界面的js库 主要用来写html页面或者构建web应用
从mvc角度看 只是视图层 也就是只负责页面的渲染并非提供了完整的M和C的功能
react的特点:
1.声明式:只需要描述UI 就跟html一样 只需要描述页面结构 react负责渲染
2.基于组件
3.学习一次随处使用
react协作:
react负责创建dom  react-dom提供dom相关功能
createElement参数解释 :1.元素名称 2. 元素属性 3.第三个及以后的参数 元素的子节点
reactDom.render方法 1.要渲染的react元素 2.dom对象 用于指定渲染到页面的位置
createElement的缺点:繁琐不简洁  不直观 不优雅

jsx 是react声明式的体现 
|react完全是利用js自身的能力编写UI 而不是造轮子增强html功能
jsx中使用js表达式
单大括号里面可以写任意的js表达式
jsx本身也是js表达式
不能出现语句

条件渲染: 逻辑判断 三元 逻辑运算
列表渲染: map()方法  要添加key 并且保证key的唯一性 遍历创建的是谁 就给谁加key属性 尽量避免使用索引作为key

函数组件特征:1.必须以大写字母开头2.必须有返回值,表示组件的结构 如果无则返回null
类组件: 1.必须以大写字母开头 2. 类组件应该继承React.Component父类 从而可以使用父类中提供的方法属性3.类组件必须提供render()方法4.render方法必须有返回值 表示该组件的结构
react组件抽离为一个js文件的步骤:
1.创建xxx.js  2.在js文件中导入react 3.创建组件 4.导出组件 5.用到此组件的地方导入即可
react组件的事件处理是通过合成事件e来实现的 无需担心兼容性
state: 组件内的私有数据 通过对象去表述
setState: 1.修改数据 2.更新视图
|数据驱动视图
修改绑定this指向的三种方法:
1.class实例方法 把函数改成箭头函数  xxx(){} 改为 xxx = ()=>{}    实验性语法 需要通过babel编译 react脚手架已经集成babel可直接用 推荐
2.箭头函数 onClick = {()=>this.xxx()}
3.bind绑定
表单受控组件 抽离出来一个change函数控制所有的表单元素
1.给表单元素添加name属性 与state属性名保持一致
2.根据表单元素获取对应的值
3.在change事件处理程序中通过[name]来修改对应的state
非受控组件:
1.创建一个ref对象  this.xxxRef = React.createRef()   DOM中使用 ref={this.xxxRef}
2.获取值 this.xxxRef.current.value

props: 接收传递给组件的数据
传递数据:给组件标签添加属性  可以传递任意类型数据 jsx表达式也可以
接收数据: 函数组件通过参数props接收数据 类组件通过this.props 接收数据
组件通信:
1.父传子: props
2.子传父: 利用回调函数 父组件提供回调 子组件调用 将要传递的数据作为回调函数的参数   父组件定义函数但是不调用 子组件调用函数 通过参数向父组件传参
3.兄弟之间: 状态提升到公共的父组件  公共父组件职责:1.提供共享状态 2.提供共享状态的方法
context:跨组件传递数据 
1.React.createContext()创建provider(提供数据) 和Consumer(消费数据)两个组件  const {Provider,Consumer} = React.createContext()
通过<Provider value="要传递的值"> 组件 </Provider>作为父节点 然后定义value值
子组件获取 通过<Consumer>{data => console.log('data就是传递过来的值')} </Consumer>
props类型校验: 可借助prop-types包 通过propTypes.属性 定义类型

children属性:
组件标签的子节点 可以用props.children获取 可以是任意类型的值 jsx表达式函数等

生命周期:
创建时:
constructor:组件创建时 最先执行
render: 每次组件渲染都会触发 渲染UI不要在render中调用setState
componentDidMount:组件挂在完成Dom渲染后  一般进行网络请求 DOM操作
更新时: render和componentDidUpdate
造成更新的三种情况:1.New props 2.setState() 3.forceUpdate()强制更新
componentDidUpdate渲染结束之后操作   componentDidUpdate(prevProps)通过prevProps可以拿到更新前的props  不要在这个周期里面直接调用更新组件的方法 会造成无限递归 如果要写 需要写到流程判断里
卸载时: componentWillUnmount 组件卸载时 主要执行清理工作
 
render props模式:
推荐用children 替代render模式
高阶组件: 
高阶组件生产的组件 再填加的属性 不会传递到高阶组件

高阶组件props丢失的问题
原因:高阶组件没有往下传递props
解决方案: 渲染被包装的组件是 传递props

组件的极简模型: (state,props) => UI 组件内部提供state 接收外部传入的props数据 内部处理产出UI结构

setState:异步执行  调用多次setState最终只会触发一次render更新
this.setState({//一般写法 
  count: this.state.count + 1
})

this.setState((state,props)=>{//异步调用 但是state可以拿到最新的状态 
  return{
    count:state.count + 1
  }
})
this.setState((state,props)=>{
  return{
    count:state.count + 1
  }
},()=>{这里可以拿到状态更新后并且dom渲染后的最新状态})

jsx的转化过程 由babel/preset-react插件编译成createElement()方法 

通过setState更新state 组件更新机制是 更新当前组件以及当前组件下面所有的子组件
组件性能优化:
1.减轻state: 只存储跟组件渲染相关的数据(比如count/列表数据/loading) 
注意: 不用做渲染的数据不要放到state中 比如定时器id  对于需要在多个方法中用到的数据 应该放到this中 用法:直接this.xxx
2.避免不必要的重新渲染
解决方法: 使用钩子函数 shouldComponentUpdate(nextProps,nextState )