### Js中constructor的用法

2017-02-07 liujians

首先列出可能现在用的比较多的、在构造函数中写

	class _mytest{
		constructor(x) {
			this.x = x;				
		}
		sayHello(){
			console.log("hello");
		}
	}

这种写法用作构造一个类模板

再来点可能用的不是很多的

	var test = [];//new Object()
	console.log(test.constructor==Array)//true
	
	var test = true;//new Boolean()
	console.log(test.constructor==Boolean)//true
	
	var test = {};//new Object()
	console.log(test.constructor==Object)//true
	
	var test = new Date();
	console.log(test.constructor==Date)//true
	
	var test = "";//new String()
	console.log(test.constructor==String)//true
	
	var test = function(){};//new Function()
	console.log(test.constructor==Function)//true

那么综上所述、再加上对象的思想、总结一下

	function _f(){
		this.a = "111"
		console.log(arguments)//[1,2,3]
		console.log(arguments.callee)
		console.log(arguments.constructor==Object)//true
	}
	_f(1,2,3)
	console.log(_f.constructor==Object)//false

最后这个false相信大家已经有了答案

构造他的是function、而不是Object

希望能够帮到大家
___
本文出自————[http://liujians.me](http://liujians.me)