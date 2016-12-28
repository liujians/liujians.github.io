### pm2命令

2016-12-26 liujians

最近花了不少时间做pm2的远程deploy

记下一些命令、方便以后查看

    pm2 start 
    
    pm2 restart

	pm2 stop
    
    pm2 save --用作开机重启
    
    pm2 startup --用作开机重启

	pm2 ecosystem --生成远程发布配置
	
	pm2 deploy ecosystem.config.js production setup

	pm2 deploy ecosystem.config.js production

	pm2 unstartup

___
本文出自————[http://liujians.me](http://liujians.me)