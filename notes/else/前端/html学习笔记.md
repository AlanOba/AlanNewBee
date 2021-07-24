

[TOC]

# 标题

```html
<h1>标题1</h1>
<h2>标题2</h2>
<h3>标题3</h3>
<h4>标题4</h4>
<h5>标题5</h5>
<h6>标题5</h6>
```

# 段落

```html
段落1 
段落2
段落3
<p>段落4 </p> 
<p>段落5 </p> 
<p>段落6 </p>
```

# 粗体

```html
<p>无粗体效果</p>
<b>b标签粗体效果</b>
<br/>
<strong>strong标签粗体效果</strong>
```

# 斜体

```html
<p>无斜体效果</p>

<i>使用 i 标签带来的斜体效果</i>
<br/>

<em>使用 em 标签带来的斜体效果</em>
```

# 预格式

```html
<p>这里是没有用预格式的情况：</p>
public class HelloWorld {
	public static void main(String[] args) {
		System.out.println("Hello World");
	}
}
<br/>
<br/>
<p>使用预格式的情况:</p>
<pre>
public class HelloWorld {

	public static void main(String[] args) {
		System.out.println("Hello World");
	}
}
</pre>
```

# 删除

```html
<p>无删除效果</p>
<del>使用del标签实现的删除效果</del>
<br/>
<s>使用s标签实现的删除效果，但是不建议使用，因为很多浏览器不支持s标签</s>
```

# 下划线

```html
<ins>使用ins标签实现的下划线效果</ins>
<br/>
<u>使用u标签实现的下划线效果，但是不建议使用</u>
```

# 图像

```html
显示图像 <img src="http://how2j.cn/example.gif"/> 网页
				<img src = file:///Users/alan/image/skill1.png /> 
设置宽高 <img width="200" height="200" src = file:///Users/alan/image/skill1.png /> 
<!-- img不能设置图像位置，需要用其他标签设置-->
<div align="left">
  <img src="http://how2j.cn/example.gif"/>
</div>
<div align="center">
  <img src="http://how2j.cn/example.gif"/>
</div>
<div align="right">
  <img src="http://how2j.cn/example.gif"/>
</div>
<!--如果图片不存在，默认会显示一个缺失图片，这是不友好的 
所以可以加上alt属性。 
当图片存在的时候，alt是不会显示的 
当图片不存在的时候，alt就会出现-->
  <img src="http://how2j.cn/example_not_exist.gif" />
  <br/>
  <img src="http://how2j.cn/example.gif" alt="这个是一个图片" />
  <br/>
  <img src="http://how2j.cn/example_not_exist.gif" alt="这个是一个图片" />
```

# 超链接

```html
<!-- 普通超链接-->
<a href="http://www.12306.com">12306</a>
<!-- 跳转到新页面超链接-->
<a href="http://www.12306.cn" target="_blank">http://www.12306.cn</a>
<!-- 带提示超链接-->
<a href="http://www.12306.com" title="跳转到http://www.12306.com">www.12306.com</a>
<!-- 图片超链接-->
<a href="http://www.12306.com">
<img src="http://how2j.cn/example.gif"/>
</a>
```

# 表格

```html
   <table border="1" width="200px"> 
		<tr>
			<td width="50%" align="left">a</td> 
			<td>b</td>
		</tr>
		<tr>
			<td align="center">a</td>
			<td>b</td>
		</tr>
		<tr>
			<td align="right">a</td>
			<td>b</td>
		</tr>
     <tr>
      <td colspan="2" >1，2</td>
  </tr><!--横跨两列，水平对齐-->
     <td rowspan="2">1,3</td> <!--横跨两行-->
     <tr bgcolor="gray"><!--设置单元格颜色-->
	</table>
```

# 列表

```html
<!--无序列表-->
<ul>
	<li>a</li>
	<li>b</li>
</ul>
<!--有序列表-->
<ol>
	<li>a</li>
	<li>b</li>
</ol>
```

# 块

```html
这没有标签
<div> 这是一个div </div>
<span>这是一个span</span>
<!--重复设置-->
<img style="margin-left:50px" src="http://how2j.cn/example.gif"/>
  <br/>
 <img style="margin-left:50px" src="http://how2j.cn/example.gif"/>
<!--一次设置-->
<div style="margin-left:100px" >
 <img src="http://how2j.cn/example.gif"/>
  <br/>
 <img src="http://how2j.cn/example.gif"/>
</div>
<!--div与span区别
div是块元素，即自动换行 
常见的块元素还有h1,table,p 
span是内联元素，即不会换行 
常见的内联元素还有img,a,b,strong-->
<div>
 第一个div
</div>
<div>
 第二个div
</div>
<span>
 第一个span
</span>
<span>
 第二个span
</span>
```

# 字体

```html
<font color="green">绿色默认大小字体</font>
<br>
<font color="blue" size="+2">蓝色大2号字体</font>
<br>
<font color="red" size="-2">红色小2号字体</font>
<!--颜色表示方式-->
<font color="red" >用red表示红色字体</font>
<br>
<font color="#ff0000" >用#ff0000表示红色字体</font>
```

# 内联框架

```html
<iframe src="http://how2j.cn/" width="600px" height="400px">
</iframe>
```

# 表单元素

```html
<!--文本框-->
<input type  = "text"/><br />
<input type  = "text" size = "20"/><br />
<input type="text" value="有初始值的文本框" /><br />
<input type="text" placeholder="请输入账号" /><br />
<!--密码框-->
<input type = "password" /><br>
<!--表单-->
<form action="http://how2j.cn/study/login.jsp" >
账户:<input type="text" name="name" /><br>
密码:<input type="text" name = "password"/> <br>
<input type = "submit" value = "登陆"><br>
</form> <br>
<!--get和post的区别 
get 
是form默认的提交方式 
如果通过一个超链访问某个地址，是get方式 
如果在地址栏直接输入某个地址，是get方式 
提交数据会在浏览器显示出来 
不可以用于提交二进制数据，比如上传文件 
post 
必须在form上通过 method="post" 显示指定 
提交数据不会在浏览器显示出来 
可以用于提交二进制数据，比如上传文件
-->
<!--单选框-->
单选1 <input type="radio"><br>
单选2 <input type ="radio"><br>
默认选中<input type ="radio" checked="checked"><br>
<p>今天晚上做什么?</p>
学习java<input type="radio" name="activity" value="学习java"> <br>
东京热<input type = "radio" name = "activity" value = "tokyohot" ><br>
dota<input type = "radio" name = "activity" value="dota"> <br>
LOL<input type = "radio" name = "activity" value = "lol"> <br>
<!--复选框-->
<p>今天晚上做什么？</p>
学习java<input type="checkbox" value="学习java" > <br/>
东京热<input type="checkbox" checked="checked"  name="activity" value="tokyohot" > <br/>
dota<input type="checkbox" value="dota" > <br/>
LOL<input type="checkbox" value="lol"> <br/>
<!--下拉列表-->
<select size="2"  multiple="multiple">
	<option >苍老师</option>
	<option selected="selected">高树玛利亚</option>
	<option selected="selected">遥美</option>
</select>
<!--文本域-->
<textarea>abc
def
</textarea>
<br>
<textarea cols="30" rows="8">123456789012345678901234567890
1234567890
1234567890
1234567890
1234567890
1234567890
1234567890
1234567890</textarea>
<!--按钮-->
<input type="button" value="一个按钮"> 普通按钮不具有提交form效果

<form action="/study/login.jsp">
账号：<input type="text" name="name"> <br/>
密码：<input type="password" name="password" > <br/>
<input type="submit" value="提交">
<input type="reset" value="重置">
</form>

图像提交
<form action="/study/login.jsp">
账号：<input type="text" name="name"> <br/>
密码：<input type="password" name="password" > <br/>
<input type="image" src="http://how2j.cn/example.gif">
</form>

<button>按钮</button>
<button><img src=file:///Users/alan/images/skill1.png></button>
<button><img src="http://how2j.cn/example.gif"/></button>

<form action="/study/login.jsp">
账号：<input type="text" name="name"> <br/>
密码：<input type="password" name="password" > <br/>
<button type="submit">登陆</button>
</form>
```

