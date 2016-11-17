### 单页应用中多说插件的重载插件

2016-11-16 liujians

由于我的博客是用vue自己搭的、所以很多东西跟别人的hexo或者Jekyll不太一样

在拓展多说这套评论插件的时候、遇到了一些小问题、这里分享给大家、也鼓励那些和我一样用自己的技术栈搭博客而不用生成的coder们

首先多说的通用代码已经很简单了、为了让不懂代码的站长们使用也是花了功夫的

html

    <div class="ds-thread" :data-thread-key="$route.params.fileName" :data-title="data_title" :data-url="data_url"></div>

js

	var duoshuoQuery = {short_name:"liujians"};
      (function() {
        var ds = document.createElement('script');
        ds.type = 'text/javascript';ds.async = true;
        ds.src = (document.location.protocol == 'https:' ? 'https:' : 'http:') + '//static.duoshuo.com/embed.js';
        ds.charset = 'UTF-8';
        (document.getElementsByTagName('head')[0] 
         || document.getElementsByTagName('body')[0]).appendChild(ds);
      })();

这里问题在于、我的blog是vue的SPA应用、用router跳转的时候评论插件不会重载、这就尴尬了

遇到问题先[https://segmentfault.com/](https://segmentfault.com/)

这里搜索 `多说` 找到一些结果

又看了一下、这里提供的文档
[http://dev.duoshuo.com/docs/50b344447f32d30066000147
](http://dev.duoshuo.com/docs/50b344447f32d30066000147)

发现了一个问题

引入他的JS之后是有个内置对象的、叫DUOSHUO

那么我们可不可以打印出这个对象看一下有什么方法呢？

一定是可以的

	if(window.DUOSHUO){
        console.log(DUOSHUO)
    }

第一次加载的时候没有出现、我们跳转了页面之后、看到打印结果
![](http://ogo5zlrgk.bkt.clouddn.com/D74B.tmp.jpg)


我们看到对象有很多方法、那么找一下有没有init这种初始化的方法呢？

大家顺着图找找吧、很多插件只要找到了内置对象、通常都是init的初始化、之前调用百度分享的时候也是类似的问题

这里是百度分享的初始化代码（原理是一样的）

	if(window._bd_share_main){
        window._bd_share_main.init();
    }

我们调用多说的初始化代码就可以了

	if(window.DUOSHUO){
        DUOSHUO.init()
    }

___
本文出自————[http://liujians.me](http://liujians.me)