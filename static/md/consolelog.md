### 兼容IE8、使用log插件取代原始console.log

2016-12-05 liujians

IE8下面会报没有console这个对象、所以用log插件替换是不错的选择

log的blog:[http://patik.com/blog/complete-cross-browser-console-log/](http://patik.com/blog/complete-cross-browser-console-log/)

这个插件代码量很少、用法也非常简单、引入即可

使用起来就像这样：

	log(111,222,{test:"test"},new Date())

![](http://ogo5zlrgk.bkt.clouddn.com/image/consolelog.png)

打印出是一个数组、可以一次打印多个对象或字符串

好处是做字符串标志时候更方便了

比如：
	var test = [{ test:"test" },{test:"newtest"}];

这个JSON想要打印出来、但是之前的代码也加了一些打印、为了区分开、你可能是这样：

	console.log("====test======");
	console.log(test);

使用了log，你就可以：

	log("test",test);

___
本文出自————[http://liujians.me](http://liujians.me)

