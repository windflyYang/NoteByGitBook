**NPM命令**
执行 npm root -g 可以看到全局安装包的文件位置

package.json
- name 设置了应用程序/软件包的名称。
- version 表明了当前的版本。
- description 是应用程序/软件包的简短描述。
- main 设置了应用程序的入口点。
- private 如果设置为 true，则可以防止应用程序/软件包被意外地发布到 npm。
- scripts 定义了一组可以运行的 node 脚本。
- dependencies 设置了作为依赖安装的 npm 软件包的列表。
- devDependencies 设置了作为开发依赖安装的 npm 软件包的列表。
- engines 设置了此软件包/应用程序在哪个版本的 Node.js 上运行。
- browserslist 用于告知要支持哪些浏览器（及其版本）。

>名称必须少于 214 个字符，且不能包含空格，只能包含小写字母、连字符（-）或下划线（_）。

