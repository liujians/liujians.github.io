### 闲暇时候写的一个node爬虫

2017-01-17 liujians
	
其实就是针对它网站的规则去抓取数据

具体细节看代码吧

	var fs = require('fs');
	var request = require("request");
	var cheerio = require("cheerio");
	var mkdirp = require('mkdirp');
	var path = require('path');


	// 从第几页开始抓取
	var pageNum = 1;

	//目标网址
	var url = 'http://jandan.net/ooxx/page-'+pageNum+'#comments';
	 
	//本地存储目录
	var dir = './images';
	 
	//创建目录
	mkdirp(dir, function(err) {
		if(err){
			console.log(err);
		}
	});
	
	//发送请求

	function req(url){
		request(url, function(error, response, body) {
			if(!error && response.statusCode == 200) {
				var $ = cheerio.load(body);
				$("#comments img").each(function(){
					var src = $(this).attr("src")
					if(src!=""){
						console.log("正在下载"+src)
						var filename = parseUrl(src)
						download(src,filename)
					}
				})
				if($(".cp-pagenavi .next-comment-page").attr("href")){
					console.log("下一页是："+$(".cp-pagenavi .next-comment-page").attr("href"))
					req($(".cp-pagenavi .next-comment-page").attr("href"))
				}else{
					console.log("没了")
				}
			}
		})
	}
	req(url)

	function parseUrl(url){
		var filename = path.basename(url);
		return filename;
	}

	function download(src,filename){
		if(src.substr(0,4)!="http"){
			src = "http:"+src
		}
		console.log(src)
		request(src).on("error",function(err){
			return false;
		}).pipe(fs.createWriteStream(dir + "/" + filename)).on("close",function(){
			console.log("成功下载"+src);
		}).on("error",function(err){
			return false;
		})
	}

___
本文出自————[http://liujians.me](http://liujians.me)