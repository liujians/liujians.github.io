### hexo主题制作入坑之旅

2016-12-10 liujians

hexo是一个挺好玩的东西、之前也写过ejs、所以打算写一套hexo的主题尝试一下

首先要全局安装hexo

	npm i hexo -g

然后找个目录初始化
	
	hexo init

---

中间要等待很久，因为他会自动帮你安装package.json的依赖

接下来全局安装yeoman

	cnpm i -g yo

然后安装生成主题结构目录工具

	npm i -g generator-hexo-theme	

建一个新主题目录

	md test
	cd test



	yo hexo-theme
	
___
本文出自————[http://liujians.me](http://liujians.me)