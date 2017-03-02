### JS的一个类和继承的题目

2017-02-23 liujians

今天在segmentfault上答了几个问题

发现有一个问题还是比较有趣的、在此做下记录

### 题目：

用js实现一个类P 
包含成员变量a，成员变量b成员函数sum 
sum输出a与b的和
a,b默认值都为0

实现一个类M
M继承自P
在P的基础上增加成员变量c
成员变量函数sum变成a,b,c的和

看着挺简单的一道题、这里就相当用ES6的class来做

结果如下：

		class P{
			constructor() {
				this.a = 0;
				this.b = 0;
				this.sum = function(){
					console.log(this.a+this.b);
					return this.a+this.b
				}
			}
			
		}
		class M extends P{
			constructor(a, b) {
			    super(a, b ); // 调用父类的constructor(a,b)
			    this.c = 0;
			    this.sum = function(){
					console.log(this.a+this.b+this.c);
					return this.a+this.b+this.c
				}
			}
			
		}
		var p = new P()
		console.log(p)
		p.sum();
		var m = new M()
		console.log(m)
		m.sum()

___
本文出自————[http://liujians.me](http://liujians.me)