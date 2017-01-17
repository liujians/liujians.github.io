### cppt-cli的起源

2016-12-30 liujians

年底了、任务渐渐的转化为学习、

想写一个cli、方便以后自己做PPT、顺带学习和复习node

首先全局安装了yo

>npm install -g yo

全局安装generator-cli-starter

>npm install -g generator-cli-starter

构建目录

>yo cli-starter

输入对应的项目名、命令名

	? Your project name cppt-cli
	? Your command name cppt
	   create bin\cppt.js
	   create package.json
	√ Project cppt-cli generated!!!

好了、现在输入cppt

会出现hello world

然后需要安装commander这个包

>npm install --save commander

读取package.json中的version
	
	var info = require('../package.json');
	program
		.version(info.version)

输入cppt -V

就可以打印出版本啦

接下来我安装了path模块和colors模块、还有fs模块

以后会用到他们

创建lib和config文件夹、方便我们做代码、配置的拆分和维护


___
本文出自————[http://liujians.me](http://liujians.me)