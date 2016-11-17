### 使用jquery插件simscroll美化滚动条

2016-11-17 liujians

在建站过程中，花时间最多的无疑就是美化、

在这个看脸的年代、博客也是一样

选择了simscroll来美化滚动条，当然要先依赖jquery，确定你的代码引入了jquery

然后我们找到要绑定插件的容器，可以是整个页面中定义一个大容器、也可以给局部使用

插件必须指定一个高度、从而使页面高度超出你指定的高度时、超出部分使用滚动查看

	 $("#app").slimScroll({
	  	height: 600,
	  	alwaysVisible: true,
	 });

这里我给我最大的容器绑定了插件、并赋值高度700

可以看到效果，但是有瑕疵

我们可以把高度设置为当前页面高度，这样是不是就可以在用户打开时候固定了一个高度呢？

	$("#app").slimScroll({
	  	height: $(window).height(),
	  	alwaysVisible: true,
	});

既然是基于jquery的插件、用jquery的方法取window的高度不会有异议吧

这样做完了之后、发现依然有瑕疵、

如果用户喜欢来回拖拽页面的大小、导致窗口变化、那我们设置的岂不是没用了吗

所以这里给出了一个解决方案、就是监听窗口变化重新赋值

	function setScroll(){
	  $("#app").slimScroll({
	  	height: $(window).height(),
	  	alwaysVisible: true,
	  });
	}
	setScroll();
	$(window).on("resize",setScroll);

这样每次页面改变大小会重新定义插件了、代码具体放在那里取决于你的项目
___
本文出自————[http://liujians.me](http://liujians.me)