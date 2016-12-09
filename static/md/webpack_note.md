### webpack 笔记(一有机会就更新)

2016-12-08 liujians

	# 全局安装
	$ npm install webpack -g
	# 安装 webpack 依赖
	$ npm install webpack --save-dev
	# 查看 webpack 版本信息
	$ npm info webpack
	# 使用 Webpack 开发工具
	$ npm install webpack-dev-server --save-dev
	# 将入口文件（entry）打包成bundle 自动载入引入的JS
	$ webpack entry.js bundle.js
	# 安装loader
	$ npm install css-loader style-loader
	# 下载babel-loader模块
	$ npm install --save-dev babel-loader
	# 下载babel-preset-es2015，这样确保babel能解析ES6的最新特性
	$ npm install --save-dev babel-preset-es2015
	$ npm install babel-core --save-dev
	# 输出内容带有进度、颜色、结果输出为JSON
	$ webpack --progress --colors --watch --json
	# 开启监听模式
	$ webpack --watch
	# 压缩混淆脚本
	$ webpack -p
	# 生成map映射文件，告知打包到那里了
	$ webpack -d
	# inline模式启动server
	$ webpack-dev-server --inline


> 关于配置项
	
	module.loader: 其中test是正则表达式，对符合的文件名使用相应的加载器./.css$/会匹配 xx.css文件，但是并不适用于xx.sass或者xx.css.zip文件.
	url-loader: 它会将样式中引用到的图片转为模块来处理; 配置信息的参数“?limit=8192”表示将所有小于8kb的图片都转为base64形式。
	entry: 模块的入口文件。依赖项数组中所有的文件会按顺序打包，每个文件进行依赖的递归查找，直到所有模块都被打成包；
	output：模块的输出文件，其中有如下参数：
	filename: 打包后的文件名
	path: 打包文件存放的绝对路径。
	publicPath: 网站运行时的访问路径。
	relolve.extensions: 自动扩展文件的后缀名，比如我们在require模块的时候，可以不用写后缀名的。
	relolve.alias: 模块别名定义，方便后续直接引用别名，无须多写长长的地址
	plugins 是插件项;

> 插件

	new webpack.optimize.UglifyJsPlugin({
      	compress: {
      	  warnings: false
      	},
		except: ['$super', '$', 'exports', 'require']
    }),
	new HtmlWebpackPlugin({
      filename: 'index.html',
      template: 'index.html',
      inject: true
    })
___
本文出自————[http://liujians.me](http://liujians.me)