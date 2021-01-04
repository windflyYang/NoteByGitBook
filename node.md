**node**
Node.js 应用程序运行于单个进程中，无需为每个请求创建新的线程。 Node.js 在其标准库中提供了一组异步的 I/O 原生功能（用以防止 JavaScript 代码被阻塞），并且 Node.js 中的库通常是使用非阻塞的范式编写的（从而使阻塞行为成为例外而不是规范）。

当 Node.js 执行 I/O 操作时（例如从网络读取、访问数据库或文件系统），Node.js 会在响应返回时恢复操作，而不是阻塞线程并浪费 CPU 循环等待。

在 Node.js 中，可以毫无问题地使用新的 ECMAScript 标准，因为不必等待所有用户更新其浏览器，你可以通过更改 Node.js 版本来决定要使用的 ECMAScript 版本，并且还可以通过运行带有标志的 Node.js 来启用特定的实验中的特性。

另一个区别是 Node.js 使用 CommonJS 模块系统，而在浏览器中，则还正在实现 ES 模块标准。在实践中，这意味着在 Node.js 中使用 require()，而在浏览器中则使用 import

退出node执行环境
```
process.exit()
process.exit(1)//不同的退出码有不同的含义  程序退出时会返回该退出码
```
----
**读取环境变量**
Node.js 的 process 核心模块提供了 env 属性，该属性承载了在启动进程时设置的所有环境变量。默认情况下被设置为 development
***注意：process 不需要 "require"，它是自动可用的***
`process.env.NODE_ENV // "development"`

**命令行接收参数**
当使用以下命令调用 Node.js 应用程序时，可以传入任意数量的参数：
```
node app.js
node app.js joe 或
node app.js name=joe
```
获取参数值的方法是使用 Node.js 中内置的 process 对象。
它公开了 argv 属性，该属性是一个包含所有命令行调用参数的数组
第一个参数是 node 命令的完整路径。
第二个参数是正被执行的文件的完整路径。
所有其他的参数从第三个位置开始
```
const args = process.argv.slice(2)
```

最好的方法是使用 minimist 库，该库有助于处理参数：
```
const args = require('minimist')(process.argv.slice(2))
args['name'] //joe
```
但是需要在每个参数名称之前使用双破折号
`node app.js --name=joe`

**输出命令**
```
console.log()//打印
```
- %s 会格式化变量为字符串
- %d 会格式化变量为数字
- %i 会格式化变量为其整数部分
- %o 会格式化变量为对象

清空控制台
```
console.clear()
```
计数器
console.count()
打印堆栈踪迹
console.trace()
打印耗时
time() 和 timeEnd()

JWT认证机制 JSON Web Token
当前端有跨域的情况下 推荐用JWT认证机制 否则推荐Session机制
Session认证的局限性 :
Session认证必须配合cookie才能实现,由于cookie默认不支持跨域 所以当前端跨域请求后端接口的时候 需要做额外配置 
JWT的工作原理:
客户端登录 通过登录后拿到用户的账号信息 然后通过加密生成token字符串 客户端将token存储起来 当发送ajax请求的时候 通过请求头的Authorization字段 发送给服务器 服务器拿到token再还原成用户信息 返回给浏览器
用户信息通过Token字符串的形式,保存在客户浏览器中, 服务器通过还原Token字符串的形式来认证用户的身份.

JWT组成
通常由三部分组成 Header（头部） PayLoad（有效荷载）Signature（签名）三者之间使用 . 分割 Header.PayLoad.Signature
Payload 才是真正的用户信息 Header 跟 Signature只是安全相关的部分 为了包装Token的安全性