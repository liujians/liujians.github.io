### win10设置虚拟化以使用linux64位虚拟机

2016-12-21 liujians

临近发布自己做的第一个管理系统到生产了、做测试要自己装一个linux虚拟机

这里使用的是VirtualBox Red Hat(64bit)

装好了VirtualBox后选择linux发现没有64位、都是32位的

网上找了一下原因、是因为windows要开启虚拟化

虚拟化设置的方法我参考了[这里](http://jingyan.baidu.com/article/8ebacdf0df465b49f65cd5d5.html)

然后重启电脑、发现win10重启按什么都不会进入Bios、

继续网上找原因、结果是win10自带开机快速启动

关于临时关闭快速启动的方法我参照的是[这里](http://www.downxia.com/zixun/351.html)

全都设置好后、重启电脑、64bit就可以选择了

![](http://ogo5zlrgk.bkt.clouddn.com/image/virtual.png)

___
本文出自————[http://liujians.me](http://liujians.me)