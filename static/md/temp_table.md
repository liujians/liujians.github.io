### MySql 临时表的使用

2016-11-15 liujians

这是之前写到的一个功能、因为一直做前端，刚开始做后端的东西、很多稍复杂的查询都没有思路

现在的场景有个功能、批量审批用户的加班、相同用户累计调休时间。更新到userinfo表中

没听懂没关系，我们拆开看：

1. 审批的用户可能是多个
2. 批量审批中、如果有ID相同的用户需要累计被审批的时间相加
3. 不同用户的时间分开计算
4. 计算出结果后、更新到用户表的每个用户字段

按这样的逻辑来看、前台传过来的记录ID我们只需要查询出对应的userId和他们的审批时间集合、然后用group by 分组就好

显示出来的东西我们要更新到userinfo可能就稍微有点麻烦

我也是那次第一次听说有临时表的概念

听人讲了一下、那就要尝试一下

    CREATE TEMPORARY TABLE IF NOT EXISTS tmp 
    (
    UserId INT UNSIGNED NOT NULL,
    DurationTime DECIMAL(4,1) NOT NULL
    )
    ENGINE=MEMORY; -- change engine type if required e.g myisam/innodb
    
    INSERT INTO tmp (UserId, DurationTime) 
    (SELECT UserId,SUM(oq.OverTimeDuration) FROM overtimerequest oq WHERE oq.OverTimeRequestId IN (2,5,7,9) GROUP BY UserId);
    

首先创建一个临时表

用作记录每个用户对应的ID和审批时间集合（用作中间层）

然后把临时表的数据、用作表连接更新到userinfo表

	UPDATE userinfo ui 
    JOIN tmp 
        ON ui.UserId = tmp.UserId 
    SET ui.DurationTime = ui.DurationTime+tmp.DurationTime

最后别忘了删除临时表

	DROP TABLE tmp

over~
___
本文出自————[http://liujians.me](http://liujians.me)