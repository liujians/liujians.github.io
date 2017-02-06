### CSS/CSS3中的变量

2017-02-04 liujians

过完年了、荒废了七天、回来也要学习一下东西

css的变量通常用作属性赋值

	:root {
	  --深蓝: #369;
	}
	.test{
		background: var(--深蓝);
	}

可以使用中文、普通写是赋值、用var调用

作用域跟css的作用域优先级一样

	：root>#test>.test>div>*

CSS3的calc计算

	body {
	  --size: 20;   
	  font-size: calc(var(--size) * 1px);
	}

附：张鑫旭的响应式变量布局分列

	.box {
	    --columns: 4;
	    --margins: calc(24px / var(--columns));
	    --space: calc(4px * var(--columns));
	    --fontSize: calc(20px - 4 / var(--columns));
	}
	@media screen and (max-width: 1200px) {
	    .box {
	        --columns: 3;
	    }
	}
	@media screen and (max-width: 900px) {
	    .box {
	        --columns: 2;
	    }
	}
	@media screen and (max-width: 600px) {
	    .box {
	        --columns: 1;
	    }
	}

___
本文出自————[http://liujians.me](http://liujians.me)