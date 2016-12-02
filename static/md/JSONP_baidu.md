### 使用JSONP 跨域调取百度API

2016-12-02 liujians

这些日子做公司的项目、PC站要用到IP定位

就使用了百度2016年8月26日才推出的高精度IP定位、误差在80m范围内

前端调取百度API算跨域、所以这里就想到了JSONP

然而百度的工程师早就想到了给我们提供JSONP的接口、所以自然而然地在API传入参数就好了

http://api.map.baidu.com/highacciploc/v1?qterm=pc&ak=请输入您的AK&coord=bd09ll&callback_type=jsonp&callback=test

我们再callback_type参数中传入jsonp，并且在callback传入回调函数名

将回调函数做全局使用

	function test(data){
		//这里的data就是JSONP取到的数据对象
	}
	
	//返回结果例子
	{
	"content":{
			"location":	{
				"lat":30.653839,
				"lng":104.093354
				},
			"locid":"973d0dc2e6340f7bfc8eb29993a0de9d",
			"radius":30,
			"confidence":1.0
			},
	"result":{"error":161,"loc_time":"2016-12-02 09:17:51"}}

最重要的地方就是callback_type 和callback 两个参数了

___
本文出自————[http://liujians.me](http://liujians.me)