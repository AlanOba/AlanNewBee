[TOC]



# 选择器

```css
<style >
	td{
		background-color: grey;
	}
	p{
		color: red;
	} /*元素选择器*/
	#p1{
		color:blue;
	}  /*id选择题*/
	.pre{
		color:blue;
	}
	.after{
		color:green;
	} /*类选择器*/
	p.blue{
		color:blue;
	} /*特定的类选择器*/
</style>

<table border="1">
	<tr>
		<td>1</td>
		<td>2</td>
	</tr>
	<tr>
		<td>3</td>
		<td>4</td>
	</tr>
	<tr>
		<td>5</td>
		<td>6</td>
	</tr>
</table>

<p>这是一个p标签</p>
<p>这是一个p标签</p>
<p>这是一个p标签</p>

<p style="color :green">这也是一个p标签</p>
<p id="p1">test</p>

<p class="pre">前3个</p>
<p class="pre">前3个</p>
<p class="pre">前3个</p>
<p class = "after">后3个</p>
<p class = "after">后3个</p>
<p class = "after">后3个</p>
<p class = "blue">啦啦啦</p>
<span class="blue">啦啦啦</span>
```

# 尺寸

```css
<style >
	p#percentage{
		width:50%;
		height: 50%;
		background-color: pink;
	}
	p#pix{
		width: 180px;
		height: 50px;
		background-color: green;
	}
</style>
<p id="percentage">按比例设置尺寸50%宽 50%高</p>
<p id="pix">按象素设置尺寸  180px宽 50 px高</p>
```

# 背景

```css
 /*背景颜色*/
  p.gray{
		background-color: gray;
	}
	h1{
		background-color: transparent;
	}
	h2{
		background-color: rgb(255,0,255);
	}
	h3{
		background-color: #00ff00;
	}

<p class="gray">灰色</p>
<h1>灰色背景，默认即透明背景</h1>
<h2>紫色</h2>
<h3>绿色背景</h3>
/*背景图片*/
div#test{
		background-image: url(skill1.png)
		width:65px;
		height: 65px;
		background-repeat: repeat-x;/*重复*/
		background-size: contain; /*平铺*/
	}
<div id="test">
	这是一个有背景图的DIV
</div>

```

# 文本

```css
<style type="text/css">
	div#colorful{
		color:pink;
	}
	div,span{
		border:1px gray solid;
		margin:10px;
	}
	div#left{
		text-align: left;
	}
	div#right{
		text-align: right;
	}
	div#center{
		text-align:	center;
	}
	span#right{
		text-align: right;
	}
</style>
<div id="colorful">
	粉红色
</div>

<div id="left">
	左对齐
</div>
<div id="right">
	右对齐
</div>
<div id="center">
	居中
</div>
<span id="right">
	span看不出右对齐效果
</span>


/*文本修饰*/
	h1{
		text-decoration: overline;
	}
	h2{
		text-decoration: line-through;
	}
	h3{
		text-decoration: blink;
	}
	h4{
		text-decoration: underline;
	}
	.a{
		text-decoration: none;
	}

<h1>上划线</h1>
<h2>删除效果</h2>
<h3>闪烁</h3>
<h4>下划线</h4>
<a href="http://www.baidu.com">默认超链接</a>
<a class="a" href="http://www.baidu.com">去掉下划线的超链接</a>

/*行间距*/
	p{
		width: 200px;
	}
	.p{
		line-height: 200%;
	}
<p>默认行间距
默认行间距
默认行间距
默认行间距
默认行间距
默认行间距
默认行间距
默认行间距
默认行间距</p>
	<p class="p">
	200%行间距
	200%行间距
	200%行间距
	200%行间距
	200%行间距
	200%行间距
	200%行间距
</p>
/*字符间距*/
.p2{
	letter-spacing: 2;
}
/*单词间距*/
.p3{
  word-spacing:10;
}
/*首行缩进*/
.p4{
  text-indent:50;
}
/*大小写*/
<style>
p.u {text-transform:uppercase}全部大写
p.c {text-transform:capitalize}首字母大写
p.l {text-transform:lowercase}全部小写
</style>
/*空白格*/
<style>
p.n {white-space:normal}默认。多个空白格或者换行符会被合并成一个空白格
p.p {white-space:pre}有多少空白格，显示多少空白格，相当于pre标签,如果长度超出父容器也不会换行。
p.pw {white-space:pre-wrap}有多少空白格，显示多少空白格，相当于pre标签,如果长度超出父容器，会换行。
p.nw {white-space:nowrap}一直不换行，直到使用br
</style>

```

# 字体

```css
	/*尺寸风格*/
	p.big{
		font-size:30px;
	}
	p.small{
		font-size:50%;
	}
	p.small2{
		font-size:0.5em;
	}
	p.n{
		font-style: normal;
	}
	p.i{
		font-style:italic;
	}
<p>正常大小</p>
<p class ="big">30px大小的文字</p>
<p class="small">50%比例大小的文字</p>
<p class="small2">0.5em大小的文字</p>
<p>正常文本</p>
<p class = "n">正常文本</p>
<p class="i">斜体文本</p>
/*粗细 字库*/
<style type="text/css">
	p.n{
		font-weight: normal;
	}
	p.b{
		font-weight:bold;
	}
p.f1{
  font-family:"Times New Roman";
}

p.f2{
  font-family:Arial;
}
p.f3{
  font-family:宋体;
}
p.f4{
  font-family:黑体;
}
p.f5{
  font-family:楷体;
}
p.f6{
  font-family:微软雅黑;
}
p.all{
	font:italic bold 30px "times new roman"
}
</style>
<p>正常字体</p>
<p class="n">正常字体</p>
<p class="b">加粗字体</p>
<p >默认字库 font family:default </p>
<p class="f1">设置字库 font-family: Times New Roman</p>
<p class="f2">设置字库 font-family: Arial</p>
<p class="f3">设置字库 font-family: 宋体, 这种字体是IE默认字体</p>
<p class="f4">设置字库 font-family: 黑体</p>
<p class="f5">设置字库 font-family: 楷体</p>
<p class="f6">设置字库 font-family: 微软雅黑, 这个字体是火狐默认字体</p>
<p class="all">斜体加粗30px的times new roman</p>
/*鼠标样式*/
span{
	cursor: crosshair;
}
<span >
	鼠标移上来后变成十字架
</span>
```

# 边框

```css
  .solid{
		border-style: solid;
	}
	.dashed{
		border-style: dashed;
	}
	.double{
		border-style: double;
	}
	.dotted{
		border-style: dotted;
	}
	.red{
   border-style:solid;
   border-color:red;
	}
	.border_width{
  border-width:1px;边框宽度
	}
	.set{   /*放在一起*/
   border:1px dotted LightSkyBlue;
}
	.div{
   width:150px;
   height:150px;
   border-top-style:solid;/*只有一个方向有边框*/
   border-top-color:red;
   border-top-width: 50px;
   background-color:lightgray;  
  }
/*有交界的地方都有边框*/
div.lefttop{
   width:150px;
   height:150px;
   border-top-style:solid;
   border-top-color:red;
   border-top-width: 50px;
   border-left-style:solid;
   border-left-color:blue;
   border-left-width: 50px;  
   background-color:lightgray;  
  }
   
  div.alldirection{
   width:150px;
   height:150px;
   border-top-style:solid;
   border-top-color:red;
   border-top-width: 50px;
   border-left-style:solid;
   border-left-color:blue;
   border-left-width: 50px;  
   border-bottom-style:solid;
   border-bottom-color:green;
   border-bottom-width: 50px;
   border-right-style:solid;
   border-right-color:yellow;
   border-right-width: 50px;     
   background-color:lightgray;  
  }
<div class="double">
	双线边框
</div>
<p class="dotted">点状</p>
<div class="dashed">
	虚线边框
</div>
<div class="solid">
	实线边框
</div>
<div class="red"> 实线红色边框  </div><br/>
<div class="lefttop">
左边和上边都有边框
</div>
<br>
<div class="alldirection">
四边都有边框　
</div>
/*
块级元素和内联元素的边框区别：	
可以看到，块级元素div默认是占用100%的宽度
常见的块级元素有div h1 p 等
而内联元素span的宽度由其内容的宽度决定
常见的内联元素有 a b strong i input 等*/
/*练习*/
<style >
	table{
		width: 100%;
		border-collapse: collapse;
	}
	tr{
		height: 45px;
		border-bottom-style: solid;
		border-bottom-color: lightgrey;
		border-bottom-width: 1px;
	}
	tr.odd{
		background-color: #f8f8f8;
	}
	td{
		width: 25%;
		text-align: center;
	}
	tr.head{
		border-bottom-width: 2px;;
	}
</style>
<table >
	<tr class="head">
		<td>id</td>
		<td>名称</td>
		<td>血量</td>
		<td>伤害</td>
	</tr>
	<tr class="odd">
		<td>1</td>
		<td>gareen</td>
		<td>340</td>
		<td>58</td>
	</tr>
	<tr class="even">
		<td>2</td>
		<td>tememo</td>
		<td>320</td>
		<td>76</td>
	</tr>
	<tr class="odd">
		<td>3</td>
		<td>annie</td>
		<td>380</td>
		<td>38</td>
	</tr>
	<tr class="even">
		<td>4</td>
		<td>deadbrothoer</td>
		<td>400</td>
		<td>90</td>
	</tr>
</table>

/*美人尖*/
div{
	    width:0px;
	    border-top:200px solid red;
	    border-left:200px solid white;
	    border-right:200px solid white;
	 }
```

# 边距

```css
/*内边距*/
<style>
.red{
   border:5px solid red;
   background-color:green;
}
.pad-left{
   border:5px solid red;
   background-color:green;
   padding-left:50px;
}
.pad-left-one{
   border:5px solid red;
   background-color:green;
   padding: 20;
}
  
.pad-left-four{
   border:5px solid red;
   background-color:green;
   padding: 10 20 30 40;
}
.margin{
   border:1px solid red;
   background-color:green;
   margin-left:10px;
}
</style>
<span class="red"> 无内边距的span  </span><br/> <br/>
<span class="pad-left"> 左边距为50的span  </span><br/>
<span class="pad-left-one"> padding:20的span  </span> <br/> <br/> <br/> <br/>
<span class="pad-left-four">
padding: 10 20 30 40 的span </span> <br/> <br/> <br/> <br/>
/*如果缺少左内边距的值，则使用右内边距的值。
如果缺少下内边距的值，则使用上内边距的值。
如果缺少右内边距的值，则使用上内边距的值。
举例说明
这是完整4个的
padding: 10 20 40 80
如果只有3个
padding: 10 20 40
那么left取right
padding: 10 20 40 = padding: 10 20 40 20
如果只有两个
padding: 10 20
那么bottom取top，left取right
padding: 10 20 = padding:10 20 10 20
如果只有一个
padding:10
那么right取top，bottom取top，left取top
padding:10 = padding:10 10 10 10*/

/*外边距
元素外边距 
指的是元素边框和元素边框之间的距离 
属性： 
margin-left: 左外边距 
margin-right: 右外边距 
margin-top: 上外边距 
margin-bottom: 下外边距 */
<span class="red"> 无外边距的span  </span>
<span class="margin"> 有左外边距的span  </span>
/*综合使用*/
  .box{
		margin:10px;
		padding:10px;
		width: 70px;
	}
	div{
		border:1px solid grey;
		font-size: 70%;
	}
<div id="">
	其他元素
</div>

<div class="box">
	内容宽度70px <br>
	外边距10px  <br>
	内边距10px   <br>
</div>

<div id="">
	其他元素
</div>
```

# 超链接

```css
/*超链的不同状态*/
	a:link{   未访问
		color:blue;
	}
	a:visited{ 已访问
		color: red;
	}
	a:hover{   鼠标悬停
		color: green;
	}
	a:active{   鼠标点后未松开
		color: yellow;
	}
<a href="http://www.12306.com">超链的不同状态</a>
/*超链去除下划线*/
a.no_underline{
  text-decoration:none;
}
<a class="no_underline" href="http://www.12306.com">去除了下划线的超链</a>
```

# 隐藏

```css
/*使用display:none; 隐藏一个元素，这个元素将不再占有原空间 “坑” 让出来了
使用 visibility:hidden;隐藏一个元素，这个元素继续占有原空间，只是“看不见”*/
<style>
div.d{
  display:none;
}
div.v{
  visibility:hidden;
}
</style>

<div>可见的div1</div>
<div class="d">隐藏的div2,使用display:none隐藏</div>
<div>可见的div3</div>
<div class="v">隐藏的div4,使用visibility:hidden隐藏</div>
<div>可见的div5</div>

```

# CSS文件

```css
/*css文件来自网络*/
<link rel="stylesheet" type="text/css" href="https://how2j.cn/study/style.css" />
<p class="p1">红色</p>
<span class="span1">蓝色</span>
/*css文件来自本地*/
<link rel="stylesheet" type="text/css" href="style.css"/>  相对路径
/*优先级*/
!就近原则!
```

# 定位

```css
/*绝对定位*/
<style type="text/css">
	p.abs{
		position: absolute;
		left:100px;
		top:100px;
	}
	.absdiv{
		width:60px;
		height: 60px;
		background-color: grey;
		position: absolute;
		left:50px;
		top:50px;
	}
</style>
<p>test1</p>
<p>test2</p>
<div class="absdiv"> 
	<p class="abs">this is a test lalalala</p> 相对于父类
</div>
<p>test4</p>
<p>test5</p>
/*元素重合问题*/
<style type="text/css">
	img#p1{
		position: absolute;
		left:60px;
		top:20px;
		z-index: 1;
	}
	img#p2{
		position: absolute;
		left: 60px;
		top:120px;
		z-index: -1;
	}
</style>
<div>
	<p>正常的文字</p>
	<p>正常的文字</p>
	<p>正常的文字</p>
	<p>正常的文字</p>
	<p>正常的文字</p>
	<p>正常的文字</p>
	<p>正常的文字</p>
	<img id="p1"src="https://how2j.cn/example.gif" >
	<img id="p2"src="https://how2j.cn/example.gif" >
</div>
/*相对定位*/
与绝对定位不同的是，相对定位不会把该元素从原文档删除掉，而是在原文档的位置的基础上，移动一定的距离
<style>
p.r{
  position: relative;
  left: 150px;
  top: 50px;
}
</style>
<p >正常文字1</p>
<p >正常文字2</p>
<p class="r" >相对定位的文字3</p>
<p >正常文字4</p>
<p >正常文字5</p>
```

# 浮动

```css
<style type="text/css">
/*浮动的框可以向左或向右移动，直到它的外边缘碰到包含框或另一个浮动框的边框为止。 */
	div.r{
		float:right
	}
	div.l{
		float:left
	}
</style>
<style type="text/css">
	div{
		width:320px;
	}
	.l{
		float:left;
	}
	.clearp{
		clear:left;
	}
</style>
/*不浮动情况*/
<div >
	<img src="https://how2j.cn/example.gif"/>
<p>当图片不浮动时，文字就会换行出现在下面
  当图片不浮动时，文字就会换行出现在下面
  当图片不浮动时，文字就会换行出现在下面
  </p>
  </div>
/*浮动的情况*/
<div  >
	<img class="l"src="https://how2j.cn/example.gif"/>
<p>当图片不浮动时，文字就会换行出现在下面
  当图片不浮动时，文字就会换行出现在下面
  当图片不浮动时，文字就会换行出现在下面</p>
  </div>
 /*取消浮动的情况*/
 <div >
 	<img class="l"src="https://how2j.cn/example.gif"/>
	<p class="clearp">当图片不浮动时，文字就会换行出现在下面
	  当图片不浮动时，文字就会换行出现在下面
	  当图片不浮动时，文字就会换行出现在下面
	</p>
 </div>

/*水平排列div*/
<style>
div#floatingDiv{
  width:200px;
}
div#floatingDiv div{
   float:left;
}
</style>
默认的div排列是会换行的
 
 <div>
       菜单1
 </div>
 <div>
       菜单2
 </div>
 <div>
       菜单3
 </div>
 
如果使用float就可以达到水平排列的效果，通常会用在菜单，导航栏等地方
 
如果超出了父容器，还会有自动换行的效果
 
<div id="floatingDiv">
  <div>
       菜单1
 </div>
 <div>
       菜单2
 </div>
 <div>
       菜单3
 </div>
 <div>
       菜单4
 </div>
 <div>
       菜单5
 </div>
 <div>
       菜单6
 </div>
</div>
```

# 显示方式

==隐藏==

```css
<style type="text/css">
	div.d{
		display: none;
	}
</style>

<div id="">
	第一个模块
</div>
<div class="d">
	第二个模块
</div>
<div id="">
	第三个模块
</div>
```

==块级元素==

```css
块级元素会自动在前面和后面加上换行，并且在其上的width和height也能够生效
div默认是块级元素,span默认是内联元素(不会有换行,width和height也不会生效)

<style type="text/css">
	div,span{
		border:1px solid lightgray;
		margin:10px;
		width:200px;
		height:100px;
	}
	.d{
		display: block;
	}
</style>	

<div id="">
	这是一个普通的div
</div>

<span id="">
	这是一个普通的span
</span>
<span id="">
	这是一个普通的span
</span>
<span class="d">
	这是一个升级为块元素的span
</span>
```

==内联元素== 与块级元素相反，这里省略

==内联-块级==

```css
使用场景：既需设置块大小，又能使块处于同一行中
	<style type="text/css">
		span{
			display: inline-block;
			margin:10px;
			border: 1px solid gray;
			width: 150px;
			height: 50px;
		}
	</style>	
	
<span id="">
	这是第一个span元素
</span>
<span id="">
	这是第二个span元素
</span>
<span id="">
	这是第三个span元素
</span>
```

==其他display==

**list-item** 显示为列表
**table** 显示为表格
**inline-table** 显示为前后无换行的表格
**table-cell** 显示为单元格

# 水平居中

==内容居中==

```css
<style type="text/css">
	div{
		border:1px solid grey;
		margin: 10px;
	}
</style>	
	<div align="center">
		通过设置属性align="center" 居中的内容
	</div>
	<div style="text-align: center">
		通过样式style="text-align:center" 居中的内容
	</div>

```

==元素居中==

```css
<style>
  div{
     border: solid 1px lightgray;
     margin: 10px;
  }
  span{
     border: solid 1px lightskyblue;
  }
</style>
<div> 默认情况下div会占用100%的宽度,所以无法观察元素是否居中</div>

<div style="width:300px;margin:0 auto">
  设置本div的宽度，然后再使用样式 margin: 0 auto来使得元素居中</div>
<span style="width:300px;margin:0 auto">
  span 是内联元素，无法设置宽度，所以不能通过margin:0 auto居中</span>
<div style="text-align:center">
  <span>span的居中可以通过放置在div中，然后让div text-align实现居中</span>
</div>
```

# 左侧固定

```CSS
<style>
 .left{
   width:200px;
   float:left;
   background-color:pink
  }
  .right{
    overflow:hidden;
    background-color:lightskyblue;
  }
</style>

<div class="left">左边固定宽度</div>

<div class="right">右边自动填满</div>

```

# 垂直居中

```css
line-height方式
<style>
#d {
line-height: 100px;
} 
div{
  border:solid 1px lightskyblue;
}
</style>

<div id="d">line-height 适合单独一行垂直居中</div>
table方式
<style type="text/css">
	#d{
		display: table-cell;
		vertical-align: middle;
		height:200px;
	}
	div{
		border:1px solid grey;
	}
</style>
<div id="d">
	<img src="https://how2j.cn/example.gif">
</div>
```

# 左右固定

```css
<style type="text/css">
	.left{
		width:200px;
		float:left;
		background-color: pink;
	}
	.right{
		width:200px;
		float:right;
		background-color:pink;
	}
	.center{
		background-color: #ADD8E6;
		margin:0 100px;
	}
</style>
	<div class = "left">
		左边固定宽度
	</div>
	<div class = "right">
		右边固定宽度
	</div>
	<div class = "center">
		中间自适应
	</div>
```

# 贴在下方

```css
<style type="text/css">
	#div1{
		position: relative;
		width:90%;
		height: 200px;
		background-color: #0000FF;
	}
	#div2{
		position: absolute;
		bottom: 0px;
		width:100%;
		height: 50px;
		background-color: #FF0000;
	}
</style>

<div id="div1">
	<div id="div2">
		无论上面的怎么变，下面的一直贴在下面
	</div>	
</div>

```

