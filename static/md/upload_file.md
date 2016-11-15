### 使用formidable做node的文件上传，并利用iframe让表单提交不跳转

2016-11-14 liujians

今天做功能做到了文件上传、之前做过img的上传是用的h5的fileReader对象转base64上传
遇到纯数据文件上传确实做的时候遇到了很多问题

开始的时候想的用ajax传（以前base64就是长字符串、可以用ajax），发现ajax只能传字符串、不然就要引用插件、对于现在的项目来说、引入插件也会变得冗余、所以寻求一个其他的方法

先没管那么多、先用表单传过去看看吧、发现传文件流需要给from表单一个比较重要的属性`enctype="multipart/form-data"`

这里是前台代码v-on：change的方法可以理解成onchange触发submit()

		<form id="fileForm" method="post" action="/data/import" enctype="multipart/form-data" >
        	<a href="#" class="btn btn-primary uploaderBtn">
       			上传
                <input type="file" id="test" name="files" v-on:change="importData('fileForm')"/>
            </a>
        </form>

提交之后、node这边应该用我们的主角formidable抓取请求了

首先install这一步是一定的

    npm install formidable --save-dev
	//fs文件操作模块（可选项）
	npm install formidable --save-dev

用require的方式引入

	var formidable = require('formidable');
	var fs = require('fs');

方法中我们要先new一个formidable对象并设置他的属性

	var form = new formidable();
	form.encoding = 'utf-8';		//设置编辑
    form.uploadDir = 'static'	 //设置上传目录
    form.keepExtensions = true;	 //保留后缀
    form.maxFieldsSize = 2 * 1024 * 1024;   //文件大小

调用form.parse()方法
	
	form.parse(req, (err, fields, files)=>{
		
		if (err) {
          console.log("文件上传报错"+err);
	      res.send(err);		
	    }
		//这里我把上传的文件读取出来
		var data = fs.readFileSync(files.files.path,'utf-8');
		//你要做的操作
		...
	}

到了这一步、上传可以实现了、但是前台传完文件之后会跳转到action的地址、这对于我来说是不想看到的

所以便有了iframe的出现

		<iframe name="testIframeName" style="display:none;"></iframe>
        <form target="testIframeName" id="fileForm" method="post" action="/data/import" enctype="multipart/form-data" >
        	<a href="#" class="btn btn-primary uploaderBtn">
        		上传
        		<input type="file" id="test" name="files" v-on:change="importData('fileForm')"/>
        	</a>
        </form>

改写了一下前台页面、加入了一个iframe并且把他们用target链接到一起、意义在于、form提交之后、iframe去跳转、form表单不会跳转、iframe是看不见的、所以达到了简单实现我们要的效果

___
本文出自————[http://liujians.me](http://liujians.me)