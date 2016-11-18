### MySql 聚合函数和IF的复杂嵌套

2016-11-18 liujians

在一个业务中、我需要做一个将原始打卡表做整合到一张整合表中、方便以后数据的查询又不会打乱原始数据

原始表中的记录是这样的

![](http://ogo5zlrgk.bkt.clouddn.com/img/table_2016-11-18.png)

现在需要整合,将相同日期，且相同用户的数据合并，并留出打卡时间的最大值最小值

这里中断一下留给大家想一下自己的思路

...

博主第一时间想到的是Group By

通过UserNumber和AttendanceDate分组、并用聚合函数求出ClockTime的最大值最小值

所以想到这样的一句Sql

	SELECT IF(COUNT(a.ClockTime)>1,MIN(a.ClockTime),IF(MIN(a.ClockTime)>'12:00:00',NULL,a.ClockTime)) 
	FROM a 
	GROUP BY a.UserNumber,a.AttendanceDate

如果按照UserNumber和AttendanceDate分组（合并相同ID并且相同时间的数据）、得到的结果集要求出最小值

如果ClockTime的总数大于一，说明有两条甚至以上时间记录，那我们求出最大值和最小值就OK了、如果小于等于1、

那么记录是不足的、再以12点为基准、判断是上午打卡还是下午打卡、另一条记作空

MySql的IF函数跟三元运算符类似、仔细看看其实很好理解

根据上面的结论整合之后

	SELECT a.UserNumber,a.AttendanceDate 
			,IF(COUNT(a.ClockTime)>1,MIN(a.ClockTime),IF(MIN(a.ClockTime)>'12:00:00',NULL,a.ClockTime)) AS myMin
			,IF(COUNT(a.ClockTime)>1,MAX(a.ClockTime),IF(MAX(a.ClockTime)>'12:00:00',a.ClockTime,NULL)) AS myMax 
	FROM a 
	GROUP BY a.UserNumber,a.AttendanceDate

这里在SQLyog IDE里面是没有问题的、可以查出并且是四列、要做的就是再插入到新表就OK了、一个人一天只有一条记录

在这里把代码嵌入到node中报错了

    ERR:this is incompatible with sql_mode=only_full_group_by


百度了好久、也找了好久问题

最后发现了问题、原因是

> 子if里的列必须要包一层聚合函数

> Group by 查出结果集如果查出的列不是Group by的条件列、则必须是聚合函数的列

就把子IF的结果套上对应的聚合函数吧

	SELECT a.UserId,a.AttendanceDate 
			,IF(COUNT(a.ClockTime)>1,MIN(a.ClockTime),IF(MIN(a.ClockTime)>'12:00:00',NULL,MIN(a.ClockTime))) AS myMin
			,IF(COUNT(a.ClockTime)>1,MAX(a.ClockTime),IF(MAX(a.ClockTime)>'12:00:00',MAX(a.ClockTime),NULL)) AS myMax 
	FROM a 
	GROUP BY a.UserNumber,a.AttendanceDate
___
本文出自————[http://liujians.me](http://liujians.me)