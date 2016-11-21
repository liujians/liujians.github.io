### Js 将字符串对象转换成对象的三种方法

2016-11-21 liujians

如果某天从后端返回的对象莫名其妙的变成了字符串、需要前端处理成对象、再去取值的话

那就需要用到、字符串强转对象了

首先我们要转换的东西可能是这个样子：

	'{"name":"test"}'

JSON的标准写法应该是KEY和VALUE都带引号的

我们要将这样的字符串转为对象、有三种方法可以参考使用

第一种可能是大家用的非常之多的、用JSON对象下面的方法`.parse()`

写起来可能是这样的：

	var jsonData = '{"name":"test"}';
	var obj = JSON.parse(jsonData)
	console.log(obj.name);//"test"

`JSON.parse()`和`JSON.stringify()` 是我用的比较多的方法

第二种是利用JS的eval()函数

	var jsonData = '{"name":"test"}';
	var obj= eval('('+ jsonData +')');
	console.log(obj.name);//"test"

这里要解释一下、为什么要再eval里面头尾加入圆括号、因为`eval()`是以函数语句解析的、那么其中的{}大括号会用作标记为作用域、或者方法体类似的概念、我们想要把他解析成对象就不会成功了

	eval('{}')
	eval('({})')//返回的是一个obj

第三种是用Function对象

	var jsonData = '{"name":"test"}';
	var obj = new Function('return ' + jsonData)();
	console.log(obj.name);//"test"

原理比较类似第二种、将return 拼接字符串对象、放入function

执行的时候、由于将字符串解析成了语句、所以return出去的是一个对象

以上就是今天所要说的三种方法、欢迎补充！

___
本文出自————[http://liujians.me](http://liujians.me)