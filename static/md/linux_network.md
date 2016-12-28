### Centos7安装完毕无法联网

2016-12-21 liujians

默认装好了Centos之后、ping不通ip

yum命令也要报源错误

找了一下问题、应该是没有连上网的问题

结果找到了一个解决方案：

1.cd /etc/sysconfig/network-scripts/

2.ls看一下文件列表

3.vi 第一个文件名

4.修改ONBOOT属性为yes

5.Esc,:wq保存

6.service network restart
___
本文出自————[http://liujians.me](http://liujians.me)