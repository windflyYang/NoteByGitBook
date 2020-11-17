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