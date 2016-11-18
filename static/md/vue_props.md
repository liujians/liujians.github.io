### 使用Vue的props做父子组件的通信

2016-11-18 liujians

vue比较方便的就是自己抽象组件、做代码分离和代码复用、

抽离出的组件有自己的数据、自己的方法

那么抽离出的组件如果需要依赖传入参数怎么办呢？

这里给出一种方案、就是用props做父子通信

首先就用我博客的头部组件代码为例

	<template>
		<div class="content-header">
			<h1>
				{{title}}
				<small>{{v}}</small>
			</h1>
			<ol class="breadcrumb">
				<li v-for="(i,index) in menuList" v-bind:class="{ active: i.isActive}">
					<router-link :to="{name:i.url}">{{i.text}}</router-link>
				</li>
				<!-- <li class="active">异常考勤记录</li> -->
			</ol>
			
		</div>
	</template>
	<script>
		export default {
		  name: 'content_header',
		  data(){
		  	return {
		  		title:"Welcome",
		  		v:"liujians.me"
		  	}
		  },
		  props: ['menuList']
		}
	</script>

仔细看的话代码并不难、这里v-for用到了一个menuList、但是我们的data里面并没有menuList

所以menuList的含义是、哪个页面使用、就需要传递参数进来、对应的模板就会变化

页面的引用就可以用 import 或者 require :

	import contentHeader from './content_header'

然后在你的Vue实例中引用：

	export default{
		data(){
	      	return {
		        menuList:[
		          {
		            text:"建站笔记",
		            isActive:"true",
		            url:"createNote"
		          }
		        ]
			}
		},
		components:{
	      contentHeader,
	    }
	}

页面上的组件就绑定页面中的menuList数组就可以传递过去了

	<content-header v-bind:menuList="menuList"></content-header>

页面上引用完毕、可以达到我们想要的效果了

___
本文出自————[http://liujians.me](http://liujians.me)