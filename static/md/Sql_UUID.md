### MySql中声明变量和UUID相关函数的使用

2016-11-28 liujians

工作中的项目做到用户权限部分了、需要将用户、功能、菜单还有几张关系表做初始化

说白了、就是插很多很多数据

那其实可以通过写个脚本、方便去复用和修改

用到了UUID、因为MySql的默认值是没有UUID的、所以只能通过插值的时候用UUID()的函数来做

因为UUID还有个依赖的关系、所以要用set的方法做变量声明

	SET @Role_User = UPPER(REPLACE(UUID(),'-',''));
	SET @Role_Admin = UPPER(REPLACE(UUID(),'-',''));

这里还用到两个函数、第一个是Replace

顾名思义、就是替换了、这里把生成出的UUID中的`-`横线删掉

然后用到了UPPER将其中的字幕转换成大写

之后就可以分开插入到几张表和关联表里了

___
本文出自————[http://liujians.me](http://liujians.me)