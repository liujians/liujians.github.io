### 垂直居中的集中方法

2016-12-xx liujians

简单概述、以后有机会再补充

我用的最多的是第一种

1.父元素relative，

子元素

	position:absolute;
	top:0;
	bottom:0;
	margin:auto;

2.父元素

	display:flex;
	align-items: center; 
    justify-content: center; 

3.父元素高度100%

子元素
	
	position: relative; /*脱离文档流*/
    top: 50%; /*偏移*/
    margin-top: @子元素一半的高度; 

(transform：translate(0，-50%)也是一样的道理)

4.table-cell的方式、不推荐所以不写出来了

___
本文出自————[http://liujians.me](http://liujians.me)