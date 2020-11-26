# 大杂烩

##### yarn npm的区别

**Yarn的优点？**
1.速度快 。速度快主要来自以下两个方面：
2.并行安装：无论 npm 还是 Yarn 在执行包的安装时，都会执行一系列任务。npm 是按照队列执行每个 package，也就是说必须要等到当前 package 安装完成之后，才能继续后面的安装。而 Yarn 是同步执行所有任务，提高了性能。
3.离线模式：如果之前已经安装过一个软件包，用Yarn再次安装时之间从缓存中获取，就不用像npm那样再从网络下载了。
4.安装版本统一
5.更简洁的输出
6.多注册来源处理
7.更好的语义化

**命令**
npm|yarn
---|:--:|---:
npm install|yarn
npm install react --save|yarn add react
npm uninstall react --save|yarn remove react
npm install react --save-dev|yarn add react --dev
npm update --save|yarn upgrade

[简书地址](https://www.jianshu.com/p/254794d5e741 "yarn npm的区别")

git 从远程拉取并创建一个本地分支
git fetch origin master:temp
Git merge temp
git branch -d temp
[git本地同步远程分支代码](https://blog.csdn.net/loongshawn/article/details/78864039)

[css图片加载失败后的优化处理](https://www.zhangxinxu.com/wordpress/2020/10/css-style-image-load-fail/)

浏览器缓存机制
- 强缓存
- 协商缓存
>强缓存是不需要发送HTTP请求的, 而协商缓存需要; 发送请求之前, 会先检查一下强缓存, 如果命中直接使用，否则就进入协商缓存流程

强缓存分为 
Expires强缓存 （对应HTTP/1.0）：表示有效期 指一个具体时间 但是如果服务器时间跟浏览器时间不一致时 可能造成缓存失效
Cache-Control强缓存（对应HTTP/1.1）：
1.返回头Response Headers 有 key 是 Cache-Control键值对；根据值判断是否缓存，如果有缓存就不会发送请求
2.优先级高于Expires ， 会覆盖Expires
3.指令分为 public和private：
public:客户端和代理服务器都可以缓存
private: 只有客户端（浏览器）缓存，服务器不缓存；
no-cache: 表示不进行强缓存验证, 而是用协商缓存来验证.
no-store: 所有内容都不会被缓存, 也不进行协商缓存
max-age: 过期时间, max-age=300表示在300s后缓存内容失效.
max-stale: 能容忍的最大过期时间。max-stale指令表示愿意接收一个已经过期了的响应。

Cache-Control 与 Expires 对比:
- Expires产于HTTP/1.0, Cache-control产于HTTP/1.1;
- Expires设置的是一个具体的时间, Cache-control 可以设置具体时常还有其它的属性;
- 两者同时存在, Cache-control的优先级更高;
- 在不支持HTTP/1.1的环境下, Expires就会发挥作用

**协商缓存**
协商缓存（前提是cache-control标识的 max-age 过期了，或者设置了协商缓存）
两种情况：1.协商缓存生效，返回304 Not Modified; 2.返回200数据库获取最新数据;
缓存标识(tag)也是有两种: Last-Modified 和 ETag;

协商缓存 Last-Modified / If-Modified-Since：
1.第一次向服务器请求这个资源，服务器返回资源时, 在响应体的header中添加Last-Modified, 值为该资源在服务器上最后的修改时间；
2.浏览器接收到后缓存文件和这个header，再次请求检测到有Last-Modified, 就会在请求头中添加If-Modified-Since这个header, 值就是Last-Modified；
3.服务器再次接收到该资源的请求, 则根据If-Modified-Since与服务器的最后修改时间做对比；
4.对比相同，返回304，不同则重新获取数据，返回200(同时返回最新的Last-Modified)

协商缓存：ETag / If-None-Match：
ETag其实与Last-Modefied的原理差不多, 不过它不是根据资源的最后修改时间来判断的, 而是通过一个唯一的标识；
1.在浏览器请求服务器资源的时候, 服务器根据当前文件的内容, 给文件生成一个唯一的标识, 若是文件发生了改变, 则这个标识就会改变
2.服务器会将这个标识ETag放到响应体的header中与请求的资源一起返回, 浏览器会缓存文件与这个header
3.下一次再次加载该资源时, 浏览器会将刚刚缓存的ETag放到请求体头部(request header)的If-None-Match里发送给服务器
4.服务器接收到了之后与该资源自身的ETag做对比, 一致,返回304知会客户端直接使用本地缓存;若是不一致, 返回200和最新的资源文件(包括最新的ETag)

ETag 与 Lasr-Modified 的对比：
Last-Modified缺点：
打开了缓存文件, 并没有进行修改, 也还是会改变最后修改时间, 导致缓存失败；
Last-Modified是以秒来计时的, 某个文件在一秒内被修改了很多次, 这时候的还是返回304；
有可能存在服务器没有准确获取文件修改时间，或者与代理服务器时间不一致等情形；
时间改变了，但是内容没有修改，还是认为文件被修改（etag没有这问题）

ETag缺点：
性能上的不足,只要文件发生改变,ETag就会发生改变. ETag需要服务器通过算法来计算出一个hash值；

总结：
- 准确度上ETag更强;
- 性能上Last-Modified更好;
- 两者都支持的话, ETag优先级更高.

缓存状态码：
未缓存：Status Code: 200
强缓Expires/Cache-Control存失效时，返回新的资源文件

强缓存：Status Code: 200 (from disk cache)
从磁盘当中取出的，不会请求服务器;
存在硬盘当中的，浏览器关闭后，再次打开仍会from disk cache；

强缓存：Status Code: 200 (from memory cache)
直接从内存中拿到的，不会请求服务器;
页面关闭内存释放，再次打开不会出现from memory cache；