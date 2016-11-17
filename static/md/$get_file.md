### 前端巧用$.get()将markdown文件内容读取，并直接显示在页面上

2016-11-14 liujians

最近在研究如何不依赖hexo或者Jekyll在github上搭建自己的博客

原因是想着作为一个前端可以基于vue去拓展，也可以顺便学习vue，以后用node做后端可以更深刻的理解这一套

然后又想到markdown很轻很快、如果可以用markdown记录博客、然后把文件甩上去、加入URL、让他们自己读取、是不是就方便了很多呢？

那么就有了现在的这种模式：[vue+vue-router+adminLte](https://github.com/liujians/vue-adminLte-vue-router?_blank) 结合 markdown文件的读取

今天这里主要说的是：markdown文件内容读取到本地，并直接显示再页面上

> 首先不知道markdown的coder们可要抓紧普及一下再回来[Markdown-入门指南](http://www.jianshu.com/p/1e402922ee32/?_blank)

对于vue+adminlte项目的整合可以参考我的开源demo——[SPA about vue-cli+adminLte+vue-router](https://github.com/liujians/vue-adminLte-vue-router)

对于现阶段的基本思路是：

1. 从列表页跳到文章页、将文件名作为固定参数传递过去
2. 文章页拿到参数、读取对应文件的内容
3. 将内容用markdown-it插件重新编译
4. 将内容写入节点

列表页

		<router-link :to="{name:'article',params:{fileName:'$get_file'}	}">
    		前端巧用$.get()将markdown文件内容读取到本地，并直接显示再页面上
    	</router-link>

webpack配置

		//由于我的项目使用vue-cli搭的，所以这里我用webpack的url-loader为img文件安排了路径,去掉了hash值,方便嵌入图片用
		{
        	test: /\.(png|jpe?g|gif|svg)(\?.*)?$/,
        	loader: 'url',
        	query: {
          		limit: 10000,
          		name: utils.assetsPath('img/[name].[ext]')
        	}
      	},
		{
        	test: /\.md$/,
        	loader: 'file',
        	query: {
          		name: utils.assetsPath('md/[name].[ext]')
        	}
      	},

文章页

		//file是读取的文件路径，这里用上一页传入的参数做字符串拼接
		
		var file = require("../md/"+this.$route.params.fileName+".md");
    	$.get(file).success(text=>{
    		console.log(text)
    		$(".content").html(md.render(text).replace(/^img_01^/,"<img src='/static/img/get_file_1.png' class='img-responsive' />"))
    	})



大功告成、现在每次添加文章只需要三步

1. 写好md文件
2. 在文章列表页加一个链接
3. 传入文件名给文章页

![](http://ogo5zlrgk.bkt.clouddn.com/get_file_1.png)

___
本文出自————[http://liujians.me](http://liujians.me)