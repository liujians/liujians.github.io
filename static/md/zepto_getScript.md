### zepto拓展getScript函数用作跨域

2016-12-16 liujians

用到了、直接贴代码

	var _getScript = function(url, callback) {
	    var head = document.getElementsByTagName('head')[0],
	        js = document.createElement('script');
	
	    js.setAttribute('type', 'text/javascript'); 
	    js.setAttribute('src', url); 
	
	    head.appendChild(js);
	
	    //执行回调
	    var callbackFn = function(){
	            if(typeof callback === 'function'){
	                callback();
	            }
	        };
	
	    if (document.all) { //IE
	        js.onreadystatechange = function() {
	            if (js.readyState == 'loaded' || js.readyState == 'complete') {
	                callbackFn();
	            }
	        }
	    } else {
	        js.onload = function() {
	            callbackFn();
	        }
	    }
	}
	//如果使用的是zepto，就添加扩展函数
	if(Zepto){
	    $.getScript = _getScript;
	}

___
本文出自————[http://liujians.me](http://liujians.me)