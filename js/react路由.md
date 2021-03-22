spa单页面应用 : 就是只有一个html页面的应用程序 优点: 用户体验好 对服务器压力小 
为了有效的使用单个页面去管理原来多页面的功能  前端路由应运而生
路由的功能是 从一个视图跳转到另一个视图 本质就是url与组件之间设置对应关系
借助 react-router-dom 导入核心组件 import {BrowserRouter as Router, Route,Link} from 'react-router-dom'
用法 使用<Router></Router>包裹整个应用  Link是入口 Route是出口

路由跳转的三种方式:
1.路由表配置：参数地址栏显示
<Route path="/list/:id" component={List} />
html：<Link to='/list/2' >跳转列表页面</Link>
Js: this.props.history.push('/list/2');
List页面接收：
console.log(this.props.match.params.id)//传递过来的所有参数

2.query方法：参数地址栏不显示，刷新地址栏，参数丢失
html:<Link to={{ pathname: '/list', query: { name: 'xlf' } }}>跳转列表页面</Link>
Js方式：this.props.history.push({ pathname: '/list', query: { name: ' sunny' } })
List页面接收：console.log(this.props.location.query.name)//传递过来的所有参数

3.state方法：参数地址栏不显示，刷新地址栏，参数不丢失
Html： <Link to={{ pathname: '/list', state: { name: 'xlf' } }}>跳转列表页面</Link>
js：this.props.history.push({ pathname: '/list', state: { name: 'sunny' } })
List页面接收 console.log(this.props.location.state.name)//传递过来的所有参数

link导航 通过state传参 如果加target属性新页面打开 state的值会丢失