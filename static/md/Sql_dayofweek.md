### MySql 查询日期为星期几的几种方法

2016-11-22 liujians

有一个需求、根据周末和工作日不同的情况、做不同的数据处理、

那么就要区分星期几

这里查到了几种方法、顺便记录一下

> DAYNAME(date)

	mysql>SELECT DAYNAME('2016-11-22');
	//Tuesday

这种方法直接打印出是星期几，适合直接展示的时候用

> DAYOFWEEK(date)

	mysql>SELECT DAYOFWEEK('2016-11-22');
	//3

这种是标记数字1——7

1代表周日，7代表周六、因为外国人都是周日为第一天

> WEEKDAY(date)

	mysql>SELECT WEEKDAY('2016-11-22');
	//1

这种是周一到周日对应数组中的下标、从周一到周日分别对应0——6


___
本文出自————[http://liujians.me](http://liujians.me)