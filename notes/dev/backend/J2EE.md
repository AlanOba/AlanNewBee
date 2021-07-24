# 

[TOC]



# Tomcat

## **启动和关闭**

**启动**

![image-20200104193544350](/Users/alan/Library/Application Support/typora-user-images/image-20200104193544350.png)

**关闭**

![image-20200104193625709](/Users/alan/Library/Application Support/typora-user-images/image-20200104193625709.png)

## **访问tomcat**

http://127.0.0.1:8080

## **更改端口号**

*server.xml*

![image-20200104193939564](/Users/alan/Library/Application Support/typora-user-images/image-20200104193939564.png)



## **部署java web服务器**

1.将java web源码放入webapps目录下

2.执行`sudo sh shutdown.sh` 关闭服务器，然后再输入

3.`sudo sh startup.sh` 打开服务器，表示服务器重启（会自动导入这个web）

4.地址输入http://localhost:8080/web/hello

## **tomcat目录结构**

> |- bin:存放tomcat的命令。
>
>     catalina.bat命令：
>    
>     startup.bat-> catalina.bat start
>    
>     shutdown.bat- > catalina.bat stop
>
> |- conf:存放tomcat的配置信息。其中server.xml文件是核心的配置文件。
>
> |-lib：支持tomcat软件运行的jar包。其中还有技术支持包，如servlet，jsp
>
> |-logs：运行过程的日志信息
>
> |-temp:临时目录
>
> |-webapps：共享资源目录。web应用目录。（注意不能以单独的文件进行共享）
>
> |-work：tomcat的运行目录。jsp运行时产生的临时文件就存放在这里
>
> |- WebRoot :web应用的根目录
>
> |-静态资源（html+css+js+image+vedio）
>
> |-WEB-INF：固定写法。
>
> |-classes：（可选）固定写法。存放class字节码文件
>
> |-lib：（可选）固定写法。存放jar包文件。
>
> |-web.xml
>
> ```markdown
>    注意：
> 
>    1）WEB-INF目录里面的资源不能通过浏览器直接访问
> 
>    2）如果希望访问到WEB-INF里面的资源，就必须把资源配置到一个叫web.xml的文件中
> ```

------

# http协议

![“http协议”的图片搜索结果](http://www.ruanyifeng.com/blogimg/asset/2016/bg2016081901.jpg)

## **请求消息**

**请求消息** 由 ==请求行，请求头部，空行和请求数据==4部分组成

请求头部信息提供了如下信息: 
**Host**: 主机名
**User-Agent**: 浏览器基本资料
**Accept**: 浏览器能够识别的响应类型
**Accept-Language**: 浏览器默认语言
**Accept-Encoding**: 浏览器能够识别的压缩方式
**Referer**: 来路页面， /addHero 这个路径是通过addHero.html这个页面跳转过来的。
**Connecton**：是否保持连接

![image-20200106110629358](/Users/alan/Library/Application Support/typora-user-images/image-20200106110629358.png)

## 响应消息

**响应信息 **由==状态行，消息报头，响应正文==组成

消息报头中提供如下信息： 
**Content-Length:** 表示长度
**Content-Type**: 内容格式
**Date**: 日期
**Server**: 服务器类型

![image-20200106111209443](/Users/alan/Library/Application Support/typora-user-images/image-20200106111209443.png)

## **响应代码**

**200** 响应成功

**301** 客户端跳转-永久性跳转

**302**客户端跳转-临时性跳转

**304**资源未被修改

**404**访问页面不存在

**500**服务端错误



# 前后端分离

## **好处**

 html 页面的内容可以简单看成 包含数据部分和不包含数据部分。 所以先准备一个不包含数据的html， 把它传给浏览器，这个速度本身会非常快，因为没有最占时间的数据库操作部分。 然后再通过 Ajax 技术，仅仅从服务器获取“纯数据”，然后把纯数据显示在html上。
这样做的好处：

1. 即便是后台数据库比较花时间，但是用户体验也比前面的方式好，因为用户会先看到部分页面，过一小会儿再看到数据，比在空白页面打圈圈等待体验好。

2. 后端只提供数据，所以前后端开发耦合度降低了很多，整体开发效率可以得到较大提高。

## **三种形式**



**前端**：

原生Ajax/JQuery中的Ajax

JSON：数据传输格式

**后端：**

1.J2EE方式：使用Servlet做服务端

2.SSM方式：通过SpringMVC做服务端

3.Springboot方式：本质上也是通过 SpringMVC来做服务端

# Ajax

**A**synchronous **J**avaScript **A**nd **X**ML 实现异步刷新

example:使用AJAX 不通过刷新页面验证账号是否存在

![image-20200106150513851](/Users/alan/Library/Application Support/typora-user-images/image-20200106150513851.png)

![image-20200106150523607](/Users/alan/Library/Application Support/typora-user-images/image-20200106150523607.png)

## **请求和响应图示**

![image-20200106154436583](/Users/alan/Library/Application Support/typora-user-images/image-20200106154436583.png)

## **过程描述**

1.创建XHR对象

2.设置响应函数

3.设置要访问的页面

4.发出请求

5.当服务端的响应返回，响应函数被调用。

6.在响应函数中，判断响应是否成功，如果成功获取服务端返回的文本，并显示在span中。

### **创建XHR对象**

XML Http Request

> XHR对象是一个**javascript**对象，它可以在用户没有感觉的情况下，就像背后运行的一根小线程一般，**悄悄的**和服务器进行数据交互  AJAX就是通过它做到无刷新效果的

```javascript
<script>
  var xmlhttp = new XMLHttpRequest();
	document.write(xmlhttp);
</script>
//[object XMLHttpRequest]
```

### **设置响应参数**

> XHR对象的作用是和服务器进行交互，所以既会发消息给服务器，也能接受服务器返回的响应。 
> 当服务器响应回来的时候，调用怎么处理呢？ 
> 通过 xmlhttp.**onreadystatechange**=checkResult 就可以指定用checkResult 函数进行处理。

### **设置页面和发送请求**

```javascript
xmlhttp.open("GET",url,true);
xmlhttp.send(null);
/*null表示没有参数，因为参数已经通过“GET" 方式，放在url里了。只有在用"POST"，并且需要发送参数的时候，才会使用到send。
类似这样：xmlhttp.send("user="+username+"&password="+password)*/
```

### **处理响应消息**

在checkResult中处理

```javascript
function checkResult(){
  if(xmlhttp.readyState==4&&xmlhttp.status==200)
    document.getElementById('checkResult').innerHTML=xmlhttp.responseText;
}
```

xmlhttp.**readyState** 4 表示请求已完成
xmlhttp.**status** 200 表示响应成功
xmlhttp.**responseText**; 用于获取服务端传回来的文本
document.getElementById('checkResult').**innerHTML** 设置span的内容为服务端传递回来的文本



### **完整代码**

```javascript
<span>输入账号 :</span>
<input id="name" name="name" onkeyup="check()" type="text">  
<span id="checkResult"></span>

<script>
var xmlhttp;
function check(){
  var name = document.getElementById("name").value;
  var url = "https://how2j.cn/study/checkName.jsp?name="+name;
 
  xmlhttp =new XMLHttpRequest(); 
  xmlhttp.onreadystatechange=checkResult; //响应函数
  xmlhttp.open("GET",url,true);   //设置访问的页面
  xmlhttp.send(null);  //执行访问
}
function checkResult(){
  if (xmlhttp.readyState==4 && xmlhttp.status==200)
    document.getElementById('checkResult').innerHTML=xmlhttp.responseText;
}
</script>
```

**checkName.jsp**

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8" isELIgnored="false"%>

<%
	String name = request.getParameter("name");
	
	if("abc".equals(name))
	    out.print("<font color='red'>已经存在</font>");
	else 
		out.print("<font color='green'>可以使用</font>");
%>
```

# JQuery

## **example**

```javascript
<script src = "jquery.min.js"> </script>
<script >
	$(function(){
   $("#b1").click(function(){
      $("#d").hide();
   });
   $("#b2").click(function(){
      $("#d").show();
   });
});
</script>
<button id="b1">隐藏div</button>
<button id="b2">显示div</button>
<div id="d">
	这是一个div
</div>	
```

![image-20200107153145255](/Users/alan/Library/Application Support/typora-user-images/image-20200107153145255.png)

使用方法：把jquery.min.js和测试html放在同一个目录下

通过id获取元素：**$("#id")** 是一个**JQuery**对象

```javascript
<script src="https://how2j.cn/study/jquery.min.js"></script>
<script >
$(function(){
  document.write( $("#d") ); //[object Object]
  document.close();
});
</script>
<div id="d">Hello JQuery</div>
```

**监听**

```javascript
<script >
	$(function(){
		$("#bt").click(function(){
			alert("触发了点击事件");
		})
	})
</script>
<button id = "bt">点击</button>
```

## 常用方法

### val()取值

```javascript
<script >
	$(function(){
		$("#bt").click(function(){
			alert($("#input1").val());//默认值
		});
	});
</script>
<button id = "bt">取值</button><br><br>
<input type="text" id="input1" value="默认值" />
```

### html()、text()获取标签信息

```javascript
$(function(){
		alert($("#div1").text());//这里不同
});
</script>
<div id="div1">
	这是一个div标签
	<span id="span1">
		这是一个span标签
	</span>
</div>
```

**html**:获取元素内容,如果有子元素，保留标签

**text**获取元素内容,如果有子元素，不包含子元素标签



## CSS

### addClass

### removeClass

### toggleClass

### CSS函数

```javascript
<script src="jquery.min.js"></script>
<style >
	.addDemoClass{
		background-color: pink;
	}
</style>

<script>
$(function(){
	$("#button1").click(function(){
		$("#div1").addClass("addDemoClass");
	});
	$("#button2").click(function(){
		$("#div1").removeClass("addDemoClass");
	});
	$("#button3").click(function(){
		$("#div1").toggleClass("addDemoClass");
	});
	$("#button4").click(function(){
		$("#div2").css("background-color","blue");
	});
	$("#button5").click(function(){
		$("#div3").css({"background-color":"pink","color":"green"});
	})
});
</script>

	<button id ="button1">增加背景色</button>
	<br>
	<br>
	<button id = "button2">消除背景色</button>
	<br>
	<br>
	<button id = "button3">切换背景色</button>
	<br>
	<br>
	<button id = "button4">设置单一样式</button>
	<br>
	<br>
	<button id = "button5">设置多个样式</button>
	<div id="div1">
		这是一段文字
	</div>
	<div id ="div2">
		单一样式，只设置背景色
	</div>
	<div id="div3">
		多种样式，不仅设置背景色，还设置字体
	</div>
```

![image-20200114155927134](/Users/alan/Library/Application Support/typora-user-images/image-20200114155927134.png)

## 选择器

### 元素



```javascript
<script src ="jquery.min.js"></script>
<script type="text/javascript">
	$(function(){
		$("#b1").click(function(){
			$("div").addClass("pink");//here different
		});
	});
</script>

<style type="text/css">
	.pink{
		background-color: pink;
	}
</style>
<html>
	<button id = "b1">给所有div标签添加背景颜色</button>
	<div >
		div1
	</div>
	<br>
	<div >
		div2
	</div>
	<br>
	<div >
		div3
	</div>
</html>
```

![image-20200114163613862](/Users/alan/Library/Application Support/typora-user-images/image-20200114163613862.png)

### id

略 前文已经反复提到

### 类

```javascript
<script src ="jquery.min.js"></script>
<script type="text/javascript">
	$(function(){
		$("#b1").click(function(){
			$(".green").addClass("color");//here different
		});
	});
</script>

<style type="text/css">
	.color{
		background-color: green;
	}
</style>
<html>
	<button id = "b1">给class为".green"的标签添加背景颜色</button>
	<div class="green" >
		div1
	</div>
	<br>
	<div >
		div2
	</div>
	<br>
	<div >
		div3
	</div>
</html>
```

![image-20200114163932816](/Users/alan/Library/Application Support/typora-user-images/image-20200114163932816.png)

### 层级

```javascript
<script src ="jquery.min.js"></script>
<script type="text/javascript">
	$(function(){
		$("#b1").click(function(){
			$("#div3 span").addClass("color");//here different
		});
	});
</script>

<style type="text/css">
	.color{
		background-color: green;
	}
</style>
<html>
	<button id = "b1">给div3下的span添加颜色</button>
	<div >
		div
	</div>
	<br>
	<div >
		div
	</div>
	<br>
	<div id="div3">
		div
		<span>
			div
		</span>
	</div>
</html>
```

![image-20200114164719046](/Users/alan/Library/Application Support/typora-user-images/image-20200114164719046.png)

### 最先最后

```javascript
<script src ="jquery.min.js"></script>
<script type="text/javascript">
	$(function(){
		$("#b1").click(function(){
			$("div:first").addClass("color");
		});
		$("#b2").click(function(){
			$("div:last").addClass("color");
		});
	});
</script>
<style type="text/css">
	.color{
		background-color: mediumvioletred;
	}
</style>
<html>
	<button id = "b1">给满足条件的第一个标签添加背景色</button>
	<br>
	<button id = "b2">给满足条件的最后一个标签添加背景色</button>
	<div >div</div><br>
	<div >div</div><br>
  <div >div</div><br>
</html>
```

![image-20200114165126347](/Users/alan/Library/Application Support/typora-user-images/image-20200114165126347.png)

### 奇偶

```javascript
<script src ="jquery.min.js"></script>
<script type="text/javascript">
	$(function(){
		$("#b1").click(function(){
			$("div:even").css("background-color","red");
		});
		$("#b2").click(function(){
			$("div:odd").css("background-color","blue");
		});
	});
</script>

<html>
	<button id = "b1">给偶数号标签加背景色</button>
	<button id = "b2">给奇数号标签加背景色</button>
	<div >div</div> <br>
	<div >div</div> <br>
	<div >div</div> <br>
	<div >div</div> <br>
	<div >div</div> <br>
	<div >div</div> <br>
</html>
```

![image-20200114170158793](/Users/alan/Library/Application Support/typora-user-images/image-20200114170158793.png)

### 可见性

```javascript
<script src ="jquery.min.js"></script>
<script type="text/javascript">
	$(function(){
		$("#b1").click(function(){
			$("div:visible").hide();
		});
		$("#b2").click(function(){
			$("div:hidden").show();
		});
	});
</script>
<html>
	<button id = "b1">隐藏可见的</button>
	<button id = "b2">显示不可见的</button>
	<div><span>Hello JQuery1</span></div>
	<div><span>Hello JQuery2</span></div>
	<div><span>Hello JQuery3</span></div>
	<div><span>Hello JQuery4</span></div>
	<div><span>Hello JQuery5</span></div>
</html>
```

![image-20200114170807332](/Users/alan/Library/Application Support/typora-user-images/image-20200114170807332.png)

![image-20200114170819288](/Users/alan/Library/Application Support/typora-user-images/image-20200114170819288.png)

### 属性

```javascript
<script src = "jquery.min.js"></script>
<script type="text/javascript">
	$(function(){
		$("#b1").click(function(){
			$("div[id]").toggleClass("border");
		});
		$("#b2").click(function(){
			$("div[id='pink']").toggleClass("border");
		});
		$("#b3").click(function(){
			$("div[id!='pink']").toggleClass("border");
		});
		$("#b4").click(function(){
			$("div[id^='p']").toggleClass("border");
		});
		$("#b5").click(function(){
			$("div[id$='n']").toggleClass("border");
		});
		$("#b6").click(function(){
			$("div[id*='ee']").toggleClass("border");
		});
	});
</script>

<style type="text/css">
	.pink{
		background-color: pink;
	}
	.green{
		background-color: green;
	}
	.border{
		border: 1px blue solid;
	}
</style>

<html>
	<button id = "b1">给有id的标签加边框</button><br><br>
	<button id = "b2">给id=pink的标签加边框</button><br><br>
	<button id = "b3">给id不等于pink的标签加边框</button><br><br>
	<button id = "b4">给标签中以p开头的标签加边框</button><br><br>
	<button id = "b5">给标签中以n结尾的标签加边框</button><br><br>
	<button id = "b6">给标签中有ee的标签加边框</button><br><br>
	<div id = "pink">带有id为pink的标签</div>
	<div id = "green">带有id为green的标签</div>
	<div>不带id的标签</div>
</html>
```

### 表单对象

```javascript
<script src = 'jquery.min.js'></script>
<script>
	$(function(){
		$(".b").click(function(){
			var value = $(this).val();
			$("td[rowspan!=13] "+value).toggle(500);
		});
	});
</script>
<style>
	table{
		border-collapse: collapse;
		table-layout:fixed;
		width:80%;
	}
	table td{
		border-bottom:1px solid #ddd;
		padding-bottom:5px;
		padding-top:5px;
	}
	div button{
		display: block;
	}
	
</style>
<html>
	<table>
		<tr>
			<td rowspan="13" valign="top" width="150px">
				<div>
					<button value = ":input" class = "b">切换所有的input</button>
					<button value = ":button" class = "b">切换所有的button</button>
					<button value = ":radio" class = "b">切换所有的radio</button>
					<button value = ":checkbox" class = "b">切换所有的checkbox</button>
					<button value = ":text" class = "b">切换所有的text</button>
					<button value = ":password" class = "b">切换所有的password</button>
					<button value = ":file" class = "b">切换所有的file</button>
					<button value = ":submit" class = "b">切换所有的submit</button>
					<button value = ":image" class = "b">切换所有的image</button>
					<button value = ":reset" class = "b">切换所有的reset</button>
				</div>
			</td>
			<td width="120px">说明</td>
			<td width="120px">表单对象</td>
			<td width="">示例</td>
		</tr>
		<tr>
			<td>input按钮</td>
			<td>:button</td>
			<td><input type="button"value="input按钮"/></td>
		</tr>
		<tr>
			<td>button按钮</td>
			<td>:button</td>
			<td>Button按钮</td>
		</tr>
		<tr>
			<td>单选框</td>
			<td>:radio</td>
			<td><input type = "radio"></td>
		</tr>
		<tr>
			<td>复选框</td>
			<td>:checkbox</td>
			<td><input type="checkbox"></td>
		</tr>
		<tr>
			<td>文本框</td>
			<td>:text</td>
			<td><input type="text"/></td>
		</tr>
		<tr>
			<td>文本域</td>
			<td></td>
			<td><textarea></textarea></td>
		</tr>
		<tr>
			<td>密码框</td>
			<td>:password</td>
			<td><input type = "password"/></td>
		</tr>
		<tr>
			<td>下拉框</td>
			<td></td>
			<td><select><option>Option</option></select></td>
		</tr>
		<tr>
			<td>文件上传</td>
			<td>:file</td>
			<td><input type="file"/></td>
		</tr>
		<tr>
			<td>提交按钮</td>
			<td>:submit</td>
			<td><input type="submit"/></td>
		</tr>
		<tr>
			<td>图片型提交按钮</td>
			<td>:image</td>
			<td><input type="image"src="https://how2j.cn/example.gif"/></td>
		</tr>
		<tr>
			<td>重置按钮</td>
			<td>:reset</td>
			<td><input type="reset"/></td>
		</tr>
	</table>
</html>
```

![image-20200117123032359](/Users/alan/Library/Application Support/typora-user-images/image-20200117123032359.png)

### 表单属性

```javascript
<script src = 'jquery.min.js'> </script>
<script type="text/javascript">
	$(function(){
		$(".b").click(function(){
			var value = $(this).val();
			console.log(value)
			$("td[rowspan!=13] "+value).toggle(500);
		});
		$(".b2").click(function(){
			var value = $(this).val();
			console.log(value)
			var options = $("td[rowspan!=13] "+value);
			alert("选中了"+options.length + "条记录!");
		});
	});
</script>

<style type="text/css">
	table{
		border-collapse: collapse;
		table-layout: fixed;
		width: 80%;
	}
	table td{
		border-bottom :1px solid #ddd;
		padding-bottom :5px;
		padding-top :5px;
	}
	div button{
		display:block;	
	}
	.border{
		border :1px blue solid;
	}
</style>

<html>
	<table>
		<tr>
			<td rowspan="13" valign="top" width="120">
				<div >
					<button value=":enabled" class="b">切换:enabled</button>
					<button value=":disabled" class="b">切换:disabled</button>
					<button value=":checked" class="b">切换:checked</button>
					<button value=":selected" class="b2">:selected数量</button>
				</div>
			</td>
			<td width="120">说明</td>
			<td width="120">表单对象属性</td>
			<td width="100px">事例</td>
		</tr>
		<tr>
			<td>enabled按钮</td>
			<td>:enabled</td>
			<td><input type = "button" enabled = "enabled" value = "enabled的按钮"/></td>	
		</tr>
		<tr>
			<td>disabled按钮</td>
			<td>:disabled</td>
			<td><input type="button" disabled="disabled" value="disabled的按钮"/></td>
		</tr>
		<tr>
			<td>选中的复选框</td>
			<td>:checked</td>
			<td>
				<input type = "radio" checked = "checked"/><br>
				<input type = "radio"/><br>
				<input type = "checkbox"><br>
				<input type = "radio" checked = "checked"/>
			</td>
		</tr>
		<tr>
			<td>选中的下拉列表</td>
			<td>:selected</td>
			<td>
				<select size="3" multiple="multiple">
					<option selected="selected">苍老师</option>
					<option> 高树玛利亚</option>
					<option selected="selected">遥美</option>
				</select>
			</td>
		</tr>
	</table>
	<form>
	</form>
</html>
```

**:enabled**会选择**可用的输入元素** **注：**输入元素的默认状态都是可用 
**:disabled**会选择**不可用的输入元素** 
**:checked**会选择**被选中的单选框和复选框** **注：** checked在部分浏览器上(火狐,chrome)也可以选中selected的option 
**:selected**会选择**被选中的option元素**

## 筛选器

### first() last() eq(num)

首先通过 $("div") 选择了多个div元素，接下来做进一步的筛选
**first()** 第1个元素
**last()** 最后一个元素
**eq(num)** 第num个元素
**注:** num基0

```javascript
		$("#b1").click(function(){
			$("div").first().toggleClass("pink");
		});
		$("#b2").click(function(){
			$("div").last().toggleClass("pink");
		});
		$("#b3").click(function(){
			$("div").eq(4).toggleClass("pink");
		});
```

### 父 祖先

**parent()** 选取最近的一个父元素 
**parents()** 选取所有的祖先元素

```javascript
<script src="jquery.min.js"></script>
<script type="text/javascript">
	$(function(){
		$("#b1").click(function(){
			$("#currentDiv").parent().addClass("b");
		});
		$("#b2").click(function(){
			$("#currentDiv").parents().addClass("b");
		});
	});
</script>
<style type="text/css">
	div{
		padding :20px;
	}
	div#grandParentDiv{
		background-color: pink;
	}
	div#parentDiv{
		background-color: green;
	}
	div#currentDiv{
		background-color: red;
	}
	.b{
		border:2px solid black;
	}
</style>
<html>
	<button id = "b1">改变parent()的边框</button>
	<button id = "b2">改变parents()的边框</button>
	<div id="grandParentDiv">
		祖先元素
		<div id="parentDiv">
			父亲元素
			<div id="currentDiv">
				当前元素
			</div>
		</div>
	</div>
</html>
```

![](/Users/alan/Library/Application Support/typora-user-images/image-20200117150944181.png)

![image-20200117151020895](/Users/alan/Library/Application Support/typora-user-images/image-20200117151020895.png)

###  儿子 后代

```javascript
<script src="jquery.min.js"></script>
<script type="text/javascript">
	$(function(){
		$("#b1").click(function(){
			$("#currentDiv").children().addClass("b");
		});
		$("#b2").click(function(){
			$("#currentDiv").find("div").addClass("b");
		});
	});
</script>
<style type="text/css">
	div{
		padding :20px;
	}
	
	div#currentDiv{
		background-color: red;
	}
	div#childrenDiv{
		background-color: green;
	}
	div#grandChildrenDiv{
		background-color: pink;
	}
	.b{
		border:2px solid black;
	}
</style>
<html>
	<button id = "b1">改变children()的边框</button>
	<button id = "b2">改变find()的边框</button>
	<div id="currentDiv">
		当前元素
		<div id ="childrenDiv">
			儿子元素1
			<div id="grandChildrenDiv">
				后代元素n
			</div>
		</div>
		<div id="childrenDiv">
			儿子元素2
			<div id="grandChildrenDiv">
				后代元素n
			</div>
		</div>
	</div>
</html>
```

![image-20200117151743855](/Users/alan/Library/Application Support/typora-user-images/image-20200117151743855.png)

![image-20200117151806770](/Users/alan/Library/Application Support/typora-user-images/image-20200117151806770.png)

### 同级

**siblings():** 同级(同胞)元素

## 属性

```javascript
<script src="jquery.min.js" ></script>
<script type="text/javascript">
	$(function(){
		$("#b1").click(function(){
			alert("align属性为"+$("#h1").attr("align"));//获取已定义属性
		});
		$("#b2").click(function(){
			alert("自定义属性game为"+$("#h1").attr("game"));//获取自定义属性
		});
		$("#b3").click(function(){
			$("#h1").attr("align","right");//修改属性
		});
		$("#b4").click(function(){
			$("#h1").removeAttr("align");//删除属性
		});
	});
</script>
<html>
	<button id ="b1">点击获取align属性</button>
	<button id ="b2">点击获取自定义属性game</button><br>
	<button id ="b3">align属性修改为right</button>
	<button id ="b4">删除align属性</button>
	<h1 id="h1" align="center" game="LoL">居中标题</h1>
</html>
```

prop与attr的区别 

与**prop**一样**attr**也可以用来获取与设置元素的属性。
区别在于，对于**自定义属性**和**选中属性**的处理。
选中属性指的是 checked,selected 这2种属性

1. 对于自定义属性 attr能够获取，prop不能获取
2. 对于选中属性
   attr **只能获取初始值**， 无论是否变化
   prop 能够访问变化后的值，并且以**true|false**的布尔型返回。
    所以在访问表单对象属性的时候，应该采用prop而非attr

通过attr获取自定义属性 game  **LOL**

通过prop获取自定义属性 game **undefined**

通过attr获取 checked属性 **checked不能改变**

通过prop获取 checked属性 **true or false**

## 效果

### 显示 隐藏 切换

**显示 隐藏 切换** 分别通过**show()**, **hide()**,**toggle()**实现
也可以加上毫秒数，表示延时操作,比如**show(2000)**

### 向上滑动 向下滑动 滑动切换

**向上滑动 向下滑动 滑动切换** 分别通过**slideUp()**, **slideDown()**,**slideToggle()**实现 
也可以加上毫秒数，表示延时操作，比如**slideUp(2000)**

### 淡入 淡出 淡入淡出切换 指定淡入程度

**淡入 淡出 淡入淡出切换 指定淡入程度** 分别通过**fadeIn()**, **fadeOut()**,**fadeToggle()** **fadeTo()**实现
也可以加上毫秒数，表示延时操作，比如**fadeIn(2000)**
fadeTo跟的参数是0-1之间的小数。 0表示不淡入，1表示全部淡入

### 自定义动画效果

通过**animate** 可以实现更为丰富的动画效果 
animate()第一个参数为css样式 
animate()第二个参数为延时毫秒 
**注：** 默认情况下，html中的元素都是固定，并且无法改变的位置的。 为了使用animate()自定义动画效果，需要通过css把元素的**position设置为relative、absolute或者fixed**。

```javascript
<script>
$(function(){
var div = $("#d");
   $("#b1").click(function(){
    div.animate({left:'100px'},2000);
    div.animate({left:'0px',top:'50px',height:'50px'},2000);
   });
});
</script>
```

### 回调函数

```javascript
$(function(){
		var div = $("#d");
		$("#b").click(function(){
			div.animate({left:'100px',top:'0px'},2000);
			div.animate({top:'50px' ,left:'0px',height:'50px'},2000,function(){//here
				alert("动画演示结束");
			});
		});
	});
```

## 事件

### 加载

页面加载有两种方式表示 
\1. **$(document).ready()**; 
\2. **$();** 这种比较常用 
图片加载用**load()**函数

```javascript
<script>
  $(document).ready(function(){
    $("#message1").html("页面加载成功");
  });
  $(function(){
    $("#img").load(function(){
      $("#message2").html("图片加载成功");
    });
  });
</script>
```

### 点击

**click()** 表示单击 
**dblclick()** 表示双击 
注: 空白键和回车键也可以造成click事件，但是只有**双击鼠标**才能造成dblclick事件

### 键盘

**keydown** 表示按下键盘
**keypress** 表示按住键盘
**keyup** 表示键盘弹起
这三者的区别分别表现在发生的 先后顺序，获取到的键盘按钮值，已经对输入框的文本取值这三方面
**先后顺序**： 按照 keydown keypress keyup 顺序发生
**键盘按钮值**：
通过event对象的**which**属性获取键盘的值
keydown和keyup 能获取所有按键，不能识别大小写
keypress 不能获取功能键，如F1 SHIFT等，能够识别大小写
**文本取值**：
keydown和keypress：不能获取最后一个字符
keyup： 获取所有字符
如图所例，敲入ab
发生的先后顺序是 keydown,keypress,keyup
keydown和keyup取到大写B的ASCII码表 66,keypress取到小写b的ASCII码表 98.
keydown和keypress只能取到文本值a, keyup可以取到ab

```javascript
<script src="jquery.min.js" ></script>
<script type="text/javascript">
	var order = 0;
	var clearTimer=null;
	$(function(){
		$("#i").keydown(function(e){
			var selector = "keydown";
			show(selector,e,$(this).val());
		});
		$("#i").keypress(function(e){
			var selector = "keypress";
			show(selector,e,$(this).val());
		});
		$("#i").keyup(function(e){
			var selector = "keyup";
			show(selector,e,$(this).val());
		});
	});
	function show(selector,e,inputvalue){
		clearTimeout(clearTimer);
		action(selector);
		key(selector,e);
		value(selector,inputvalue);
		clearTimer = setTimeout(clear,4000);
	}
	function action(selector){
		$("#"+selector+"Action").css("background-color","green");
		$("#"+selector+"Action").html("顺序: "+ (++order ) );
	}
	function key(selector,e){
		$("#"+selector+"Key").html(e.which);
	}
	function value(selector,value){
		$("#"+selector+"Value").html(value);
	}
	function clear(){
		order = 0;
		$("tr#action div").css("background-color","red");
		$("tr div").html("");
	}
</script>
<style>
	tr#action div{
		background-color: red;
		height: 50px;
		border:solid 1px black;
	}
	tr#value div,tr#key div{
		background-color: #d1d1d1;
		height: 50px;
	}
	td{
		width: 25%;
	}
</style>
<html>
	输入框: <input id="i"/>
	<table width="100%">
		<tr >
			<td></td>
			<td>keydown</td>
			<td>keypress</td>
			<td>keyup</td>
		</tr>
		<tr id="action">
			<td>行为</td>
			<td><div id="keydownAction"></div></td>
			<td><div id="keypressAction"></div></td>
			<td><div id="keyupAction"></div></td>
		</tr>
		<tr id="key">
			<td>按键</td>
			<td><div id="keydownKey"></div></td>
			<td><div id="keypressKey"></div></td>
			<td><div id="keyupKey"></div></td>
		</tr>
		<tr id="value">
			<td>取值</td>
			<td><div id="keydownValue"></div></td>
			<td><div id="keypressValue"></div></td>
			<td><div id="keyupValue"></div></td>
		</tr>
	</table>
</html>
```

### 鼠标

**mousedown** 表示鼠标按下 
**mouseup**表示鼠标弹起 **mousemove**表示鼠标进入 
**mouseenter**表示鼠标进入 
**mouseover**表示鼠标进入 

**mouseleave**表示鼠标离开 
**mouseout**表示鼠标离开 

进入事件有3个 mousemove mouseenter mouseover 
**mousemove** ：当鼠标进入元素，**每移动一下**都会被调用 
**mouseenter** ：当鼠标进入元素，调用一下，**在其中移动，不调用** 
**mouseover**：当鼠标进入元素，调用一下，**在其中移动，不调用** 


mouseenter 和 mouseover的区别 
**mouseenter**: 当鼠标经过其子元素**不会**被调用 
**mouseover**：当鼠标经过其子元素**会**被调用 


mouseleave 和 mouseout的区别 
**mouseleave**: 当鼠标经过其子元素**不会**被调用 
**mouseout**：当鼠标经过其子元素**会**被调用

### 焦点

**focus()** 获取焦点 
**blur()** 失去焦点

### 改变

**change()** 内容改变 

**注：** 对于文本框，只有当该文本**失去焦点**的时候，才会触发change事件。

### 提交

**submit()** 提交form表单

### 绑定事件

以上所有的事件处理，都可以通过on() 绑定事件来处理

```javascript
$("selector").on("event",function);
```

 

### 触发事件

触发事件，在本例中，文档加载好之后，就触发dblclick双击事件，而不是通过去手动双击。

```javascript
$("selector").trigger("event");
```

## Ajax

### $.ajax()

```javascript
<script src="jquery.min.js"></script>
<div id="checkResult"></div>
请输入用户名:<input type="text" id="name" />
<script type="text/javascript">
	$(function(){
		$("#name").keyup(function(){
			var value = $(this).val();
			var page = "https://how2j.cn/study/checkName.jsp";
			$.ajax({
				url:page,
				data:{"name":value},
				success:function(result){
					$("#checkResult").html(result);
				}
			});
		});
	});
</script>
```

### $.get()

简化

```javascript
<script src="jquery.min.js"></script>
<div id="checkResult"></div>
请输入用户名:<input type="text" id="name" />
<script type="text/javascript">
	$(function(){
		$("#name").keyup(function(){
			var value = $(this).val();
			var page = "https://how2j.cn/study/checkName.jsp";
			$.get(
				page,
				{"name":value},
				function(result){
					$("#checkResult").html(result);
				}
			);
		});
	});
</script>
```

### $.post()

```javascript
<script src="jquery.min.js"></script>
<div id="checkResult"></div>
请输入用户名:<input type="text" id="name" />
<script type="text/javascript">
	$(function(){
		$("#name").keyup(function(){
			var value = $(this).val();
			var page = "https://how2j.cn/study/checkName.jsp";
			$.get(
				page,
				{"name":value},
				function(result){
					$("#checkResult").html(result);
				}
			);
		});
	});		
</script>
```

$.post 使用3个参数
第一个参数: page 访问的页面
第二个参数: {name:value} 提交的数据
第三个参数: function(){} 响应函数
只有**第一个**参数是**必须的**，其他参数都是可选

### $.load

```javascript
<script src="jquery.min.js"></script>
<div id="checkResult"></div>
请输入用户名:<input type="text" id="name" />
<script type="text/javascript">
	$(function(){
		$("#name").keyup(function(){
			var value = $(this).val();
			var page = "https://how2j.cn/study/checkName.jsp";
      //另一种写法 var page = "https://how2j.cn/study/checkName.jsp?name="+value;
			$("#checkResult").load(page,{"name":value});
		});
	});	
</script>
```

load比起 [$.get](https://how2j.cn/k/jquery/jquery-ajax/474.html#step1000),[$.post](https://how2j.cn/k/jquery/jquery-ajax/474.html#step999) 就更简单了 
$("#id").load(page,[data]); 
**id**: 用于显示AJAX服务端文本的元素Id 
**page**: 服务端页面 
**data**: 提交的数据，可选。 在本例中，直接在page里加上了参数列表

### 格式化form下的输入数据

```javascript
<script src="jquery.min.js"></script>
<a href="https://how2j.cn/study/checkName.jsp">https://how2j.cn/study/checkName.jsp</a>
<form id="form">
	输入用户名:<input id="name" type="text" name="name"/><br>
	输入年龄:<input id="age" type="text" name="age"/><br>
	输入密码:<input id="password" type="text" name="password"/>
</form>
<script type="text/javascript">
	$(function(){
		$("input").keyup(function(){
			var url = "https://how2j.cn/study/checkName.jsp";
			var data = $("#form").serialize();
			var link = url+"?"+data;
			console.log(link);
      //控制台日志的输出信息为：
      // https://how2j.cn/study/checkName.jsp?name=av&age=cc&password=s
			$("a").html(link);
			$("a").attr("href",link);
		});
	});
</script>
```

![image-20200129153537504](/Users/alan/Library/Application Support/typora-user-images/image-20200129153537504.png)

## 数组操作

```javascript
<script src="jquery.min.js"></script>
<script type="text/javascript">
	var a = new Array(5,2,4,2,3,3,1,4,2,5);
	$.each(a,function(i,n){
		document.write("元素"+"[" +i+"] :" + n+"<br>");
	});//遍历
	document.write("#####分割线#####<br>");
	a.sort();//从大到小排序
	$.unique(a);//去重复
	$.each(a,function(i,n){
		document.write("元素"+"[" +i+"] :" + n+"<br>");
	});//遍历
	document.write($.inArray(6,a)+"<br>");
	document.write($.inArray(1,a));//判断元素是否存在，存在返回数组下标，不存在返回-1
</script>
```

## JSON

```javascript
<script src="jquery.min.js"></script>
<script type="text/javascript">
	var str = "{\"name\":\"盖伦\",\"hp\":1000}";
	document.write("这是一个JOSN格式的字符串 "+str+"<br>");
	var gareen = $.parseJSON(str);
	document.write("这是一个JOSN对象 "+gareen);
</script>
```

## 对象转换

### JQuery转DOM



### DOM转JQuery