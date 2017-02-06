### Promise对象的链式调用

2016-12-06 liujians

Promise对象是解决异步回调嵌套的一种方案

现在封装Promise的库很多、像q,bluebrid等等

Promise对象下调用.then方法就可以把异步排个顺序

那么只要返回Promise对象、.then就可以继续下去

首先我们定义三个异步方法

	var test ={
		func1:function(){
			var data = new Promise(function(resolve){
				setTimeout(function(){
					resolve("ajax结果111")
				},200)
			})
			return data;
		},
		func2:function(){
			var data = new Promise(function(resolve){
				setTimeout(function(){
					resolve("ajax结果222")
				},100)
			})
			return data;
		},
		func3:function(){
			var data = new Promise(function(resolve){
				setTimeout(function(){
					resolve("ajax结果333")
				},500)
			})
			return data;
		}
	}

假设三个方法分别三个ajax

然后

	test.func1().then(function(value){
		console.log(value)
		//do something...
	})

那如果想要三个ajax顺序请求、并依赖上一个ajax的结果，该怎么写呢？

可能你会这样做：

	test.func1().then(function(value){
		console.log(value)
		test.func2().then(function(value){
			console.log(value)
			test.func3().then(function(value){
				console.log(value)
				//do something...
			})
		})
	})

但是这样写跟ajax嵌套一样代码越多越看不清楚...改起来也麻烦

所以要链式调用、并让三个方法顺序执行

	test.func1().then(function(value){
		console.log(value)
		//do something...
		return test.func2();
	}).then(function(value){
		console.log(value)
		return test.func3();
	}).then(function(value){
		console.log(value)
	})	

使用return链式调用、这样代码就清晰明了

也可以直接
	
	test.func1().then(test.func2()).then(test.func3()).then(function(value){
		console.log(value)
	})

希望可以帮助到大家

补充、使用async和await可以这样写：

	async function __f(){
		try{
			var a = await test.func1();
			console.log(a);
		} catch(err){
			console.log(err);
		}
		var b = await test.func2().catch(function (err){
	    	console.log(err);
	  	});
		console.log(b);
		var c = await test.func3();
		console.log(c);
	}
___
本文出自————[http://liujians.me](http://liujians.me)