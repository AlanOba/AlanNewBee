JavaScript用于网页和用户之间的交互，比如提交的时候，进行用户名是否为空的判断。 

完整的javascript由[语言基础](https://how2j.cn/k/javascript/javascript-type/428.html)，[BOM](https://how2j.cn/k/javascript/javascript-bom-window/449.html)和[DOM](https://how2j.cn/k/dom/dom-node/457.html)组成。本模块主要讲解javascript语言本身和BOM.

```javascript
<script type="text/javascript">
	document.write("Hello JavaScript");
</script>
<br>
<button onclick="document.getElementById('text').style.display='none'">隐藏文本</button>
<button onclick="document.getElementById('text').style.display='block'">显示文本</button>
<p id="text">这是一段可以被javascript隐藏的文本</p>
```

使用外部js文件

```css
<script src="hello.js"></script>

.js
document.write("hello js");
```

注释

```CSS
// 单行注释
/* */多行注释
```

变量声明

```CSS
<script type="text/javascript">
			var x = 10;  //var省略则为全局变量，不省略为局部变量
			document.write("变量x的值为"+x);
</script>
```

调试

```css
<script type="text/javascript">
			var x = 10;
			alert(1);//弹出
			document.write("变量x的值为"+x);
			alert(2);//弹出
</script>

<script type="text/javascript">
			var x = 10;
			console.log("x="+x);//控制台
			document.write("变量x的值为"+x);
			console.log("end");//控制台
		</script>
```

数据类型

```javascript
<script >
			var x;
			document.write("x的值为"+x+"它的类型为"+typeof x+"<br>");
			x = 10;
			document.write("x的值为"+x+"它的类型为"+typeof x+"<br>");
			x = 1.23;
			document.write("x的值为"+x+"它的类型为"+typeof x+"<br>");
			x = 0123;
			document.write("x的值为"+x+"它的类型为"+typeof x+"<br>");
			x = 0x12344;
			document.write("x的值为"+x+"它的类型为"+typeof x+"<br>");
			x = false;
			document.write("x的值为"+x+"它的类型为"+typeof x+"<br>");
			x = 'hello';
			document.write("x的值为"+x+"它的类型为"+typeof x+"<br>");
			x = "heihei";
			document.write("x的值为"+x+"它的类型为"+typeof x+"<br>");
</script>
```

类型转化

```javascript
<script type="text/javascript">//字符串为伪对象
			var a = "hello javascript";
			document.write("a的类型为"+typeof a+"<br>");
			document.write("a的长度为"+a.length+"<br>");
		</script>
		<script type="text/javascript">//任意类型转换为字符串
			var a = 10;
			document.write("a转换为默认字符串"+a.toString()+"<br>");
			document.write("a转换为二进制字符串"+a.toString(2)+"<br>");
			document.write("a转换为八进制字符串"+a.toString(8)+"<br>");
			document.write("a转换为十六进制字符串"+a.toString(16)+"<br>");
			//String 与toString 的区别：String转化null时->null
			//toString 转化null时->报错 后面代码不执行
		</script>
		<script type="text/javascript"> //字符串转换为数字
			var a = "20";
			document.write("a转换为数字"+parseInt(a)+"<br>");
			a = 3.14;
			document.write("a转换为数字"+parseFloat(a)+"<br>");
			a = "10abc";
			document.write("a转换为数字"+parseInt(a)+"<br>");
			a = "15adas12";
			document.write("a转换为数字"+parseInt(a)+"<br>");
			a = "hello"
			document.write("a转换为数字"+parseInt(a)+"<br>");
			//parseInt与Number的区别：Number对于非数字字符串均转化为NaN
		</script>
		<script type="text/javascript">//转换为Boolean
			/*
			当转换字符串时：
			非空即为true
			当转换数字时：
			非0即为true
			当转换对象时：
			非null即为true
			*/
		   document.write("空字符串''转换为布尔类型后的值为"+Boolean("")+"<br>");
		   document.write("非空字符串'abc'转换为布尔类型后的值为"+Boolean("abc")+"<br>");
		   document.write("数字0转换为布尔类型后的值为"+Boolean(0)+"<br>");
		   document.write("数字2转换为布尔类型后的值为"+Boolean(2)+"<br>");
		   document.write("空对象转换为布尔类型后的值为"+Boolean(null)+"<br>");
		   document.write("非空对象转换为布尔类型后的值为"+Boolean(new Object())+"<br>");
		</script>
```

函数

```javascript
function print(){
		document.write("这一句话由一个自定义函数打印"+"<br>");
}
print();
//带参数
function print(message){
		document.write(message+"<br>");
}
print("第一句话");
print("第二句话");
//带返回值
function calc(x,y){
					return x+y;
}
var sum = calc(1,2);
print(sum);
```

一些DOM知识补充

```javascript
//Document Object Model文档对象类型
<script type="text/javascript">
			 function get(){
				 var value = document.getElementById("num1").value;
				 document.getElementById("result").value ="从num1中取出的值为"+ value;
			 }
</script>
<input type="text" name="" id="num1" value="1" style="width: 200px;" />
<br>
<input type="text" name="" id="result" value="" style="width: 200px;"/>
<br>
<input type="button" value="取值" onclick="get()" />
  
//实现页面简易加法计算
<script type="text/javascript">
			 function get(){
				 var value1 = parseInt(document.getElementById("num1").value); 
				 var value2 = parseInt(document.getElementById("num2").value); 
				 var value3 = value1+value2;
				 document.getElementById("result").value = value3;
}
</script>
<input type="text" name="" id="num1" value="1" style="width: 30px;"/>
<span id="">+</span>
<input type="text" name="" id="num2" value="2" style="width: 30px;"/>
<span id="">=</span>
<input type="text" name="" id="result"  style="width: 30px;"/>
<button type="button" onclick="get()">运算</button>
```

综合练习

```javascript
<html>
	<head>
	</head>
	  <script >
	  	function generate(){
	  	   var location = $("location");
	  	   var companyType= $("companytype");
	  	   var companyName= $("companyname");
	  	   var bossName= $("bossname");
	  	   var money= $("money");
	  	   var product= $("product");
	  	   var unit= $("unit");
	  	   var result  = location +"最大"+companytype+companyname+"倒闭了，王八蛋老板"+bossname+"吃喝嫖赌，欠下了"+money+"个亿，"
	  	                            + "带着他的小姨子跑了!我们没有办法，拿着"+product+"抵工资!原价都是一"+unit+"多、两"+unit+"多、三"+unit+"多的"+product+"，"
	  	                            + "现在全部只卖二十块，统统只要二十块!"+bossname+"王八蛋，你不是人!我们辛辛苦苦给你干了大半年，"
	  	                            + "你不发工资，你还我血汗钱，还我血汗钱!";    
	  	
	  	   document.getElementById("result").value=result;   
	  	}
	  	function $(id){
	  	   var value = document.getElementById(id).value;
	  	   return value;
	  	}
	  </script>
	  <style type="text/css">
	      span{
	  		width: 100px;
	  		border:1px solid lightgrey;
	  		display:inline-block; 
	  	}
	  	input{
	  		width: 100px;
	  		height: 25px;
	  	}
	  	button#generate{
	  	   width:80px;
	  	   height:30px;
	  	}
	  	textarea{
	  	     width:100%;
	  	     height:150px;
	  	     margin-top:20px;
	  	}
	  </style>
	  <body>
	  <span>地名：</span>
	  <input type="text"  id="location" value="浙江" />
	  <span>公司类型：</span>
	  <input type="text"  id="companytype" value="互联网公司" />
	  <br><br>
	  <span>公司名称：</span>
	  <input type="text"  id="companyname" value="阿里九九" />
	  <span>老板姓名：</span>
	  <input type="text"  id="bossname" value="牛风" />
	  <br><br>
	  <span>money：</span>
	  <input type="text" id="money" value="一万" />
	  <span>产品：</span>
	  <input type="text"  id="product" value="贴膜" />
	  <br><br>
	  <span>价计量单位：</span>
	  <input type="text"  id="unit" value="百" />
	  <br><br><br>
	  <div align="center">
	  <button  id = "generate" onclick="generate()">生成</button>
	  <textarea id="result">浙江最大互联网公司阿里九九倒闭了，王八蛋老板牛风吃喝嫖赌，欠下了一万个亿，带着他的小姨子跑了!我们没有办法，拿着贴膜抵工资!原价都是一百多、两百多、三百多的贴膜，现在全部只卖二十块，统统只要二十块!牛风王八蛋，你不是人!我们辛辛苦苦给你干了大半年，你不发工资，你还我血汗钱，还我血汗钱!</textarea>
	  </div>
	</body>
</html>
```

事件

```javascript
  <script type="text/javascript">
		function showhello(){
			alert("Hello javascript");
		}
	</script>
	<body>
		<button type="button" onclick="showhello()">点击一下</button>
	</body>
```

错误处理

```javascript
<script type="text/javascript">
		function function1(){
			//函数1是存在的
		}
		try{
			document.write("调用不存在的函数funciton2"+"<br>");
			function2();
		}
		catch(err){
			document.write("捕捉到错误产生"+"<br>");
			document.write(err.message);
			document.write("<br>");
		}
</script>
```

  综合练习

```javascript
<style type="text/css">
	table{
	 border-collapse:collapse;
	}
	td{
		border: 1px solid silver;
		font-size: 12px;
		padding:5px;
	}
	
	
</style>


<!DOCTYPE html>
<html>
	<script type="text/javascript">
		//取幂函数
		function p(base,power){
			if(1==power)
				return base;
			if(0==power)
				return 1;
			var result = base;
			for(var i=0;i<power-1;i++){
				result = result *base;
			}
			return result;
		}
		
		/*取复利*/
		function fuli(rate, year){
			var result = 0;
			for(var i=year;i>0;i--){
			  result+=p(rate,i);
			}
			return result;
		}
		
		function caluate(){
			var initmoney = getNumberValue("initmoney");
			var rate = getNumberValue("getmoney");
			var year = getNumberValue("years");
			var each = getNumberValue("addmoney");
			var sum1 =(year-1) *each+initmoney;
			var sum3=each* fuli(  (1+rate/100),(year-1)) + initmoney*p( (1+rate/100) ,year);
			var sum2 = sum3-sum1;
			setValue("sum1",sum1);
			setValue("sum2",sum2);
			setValue("sum3",sum3);
			}
	
		function getNumberValue(id){
			return parseFloat(document.getElementById(id).value);
		}
		function setValue(id,value){
			
			document.getElementById(id).value= value;
			
			
		}
	</script>
	<body>
		<table >
			<tr>
			<td>
				起始资金
		    </td>	
			<td>
				<input type="text" name="" id="initmoney" value="10000" />
				<span>
				￥
				</span>
			</td>
			</tr>
			<tr>
			<td>
			     每年收益
			</td>	
			<td>
				<input type="text" name="" id="getmoney" value="5" />
				<span>
				 %
				</span>
			</td>
			</tr>
			<tr>
			<td>
				复利年数
			</td>	
			<td>
				<input type="text" name="" id="years" value="1" />
				<span>
				  年
				</span>
			</td>
			</tr>
			<tr>
			<td>
				每年追加资金
			</td>	
			<td>
				<input type="text" name="" id="addmoney" value="10000" />
				<span>
				  ￥
				</span>
			</td>
			</tr>
			<tr>
				<td colspan="2" align="center">
					<input type="button" value="计算" onclick="caluate()">
				</td>
			</tr>
			<tr>
			<td>
				本金和
			</td>	
			<td>
				<input type="text" name="" id="sum1" value="0" />
				<span>
				￥
				</span>
			</td>
			</tr>
			<tr>
			<td>
				利息和
			</td>	
			<td>
				<input type="text" name="" id="sum2" value="0" />
				<span>
				￥
				</span>
			</td>
			</tr>
			<tr>
			<td>
				本息和
			</td>	
			<td>
				<input type="text" name="" id="sum3" value="0" />
				<span>
				￥
				</span>
			</td>
			</tr>
		</table>
	</body>
</html>
```

数字

```javascript
<script type="text/javascript">
	//输出值
	function print(a){
		document.write(a+"<br>");
	}
	//输出类型
	function printtype(a){
		document.write(typeof a+"<br>");
	}
	var x = new Number(123);
	print(x);//123
	printtype(x);//object
	var y = 123;
	print(y);//123
	printtype(y);//number
	print(Number.MAX_VALUE);//Number类型最大1.7976931348623157e+308
	print(Number.MIN_VALUE);//Number类型最小5e-324
	var z = new Number("123abc");
	print(z);//NaN
	document.write((z==Number.NaN)+"<br>");//false
	document.write(isNaN(z)+"<br>");//true
	print(x.toFixed(3));//小数123.000
	var f = new Number("123.45678");
	print(f.toFixed(3));//123.457
	print(x.toExponential());//科学计数法形式1.23e+2
	print(f.toExponential());//科学计数法形式1.2345678e+2
</script>
```

字符串

|                                        |                                |                                                              |
| -------------------------------------- | ------------------------------ | ------------------------------------------------------------ |
| new String()                           | 创建字符串对象                 | [示例代码](https://how2j.cn/k/javascript/javascript-string/439.html#step1123) |
| 属性 length                            | 字符串长度                     | [示例代码](https://how2j.cn/k/javascript/javascript-string/439.html#step1124) |
| 方法 charAt charCodeAt                 | 返回指定位置的字符             | [示例代码](https://how2j.cn/k/javascript/javascript-string/439.html#step1125) |
| 方法 concat                            | 字符串拼接                     | [示例代码](https://how2j.cn/k/javascript/javascript-string/439.html#step1126) |
| 方法 indexOf lastIndexOf               | 子字符串出现的位置             | [示例代码](https://how2j.cn/k/javascript/javascript-string/439.html#step1127) |
| 方法 localeCompare                     | 比较两段字符串是否相同         | [示例代码](https://how2j.cn/k/javascript/javascript-string/439.html#step1128) |
| 方法 substring                         | 截取一段子字符串               | [示例代码](https://how2j.cn/k/javascript/javascript-string/439.html#step1129) |
| 方法 split                             | 根据分隔符，把字符串转换为数组 | [示例代码](https://how2j.cn/k/javascript/javascript-string/439.html#step1205) |
| 方法 replace                           | 替换子字符串                   | [示例代码](https://how2j.cn/k/javascript/javascript-string/439.html#step1814) |
| 方法 charAt 方法 concat 方法 substring | 返回基本类型                   |                                                              |

综合练习

```javascript
	<script type="text/javascript">
		function replace(){
			var A = document.getElementById("a").value;
			var B = document.getElementById("b").value;
			var str =document.getElementById("str").value;
			var newstr  = str.replace(A,B);
			document.getElementById("newstr").value = newstr;
		}
	</script>
	<body>
		<table >
			<tr>
				<td><span>源字符串：</span></td>
				<td><textarea type="text" id = "str" >example</textarea></td>
			</tr>
			<tr>
				<td><span>查询:</span></td>
				<td><input type="text"  id = "a" value="a" /></td>
			</tr>
			<tr>
				<td><span>替换为:</span></td>
				<td><input type="text"id = "b" value="e" /></td>
			</tr>
			<tr>
				<td><span>替换结果:</span></td>
				<td><textarea type="text" id = "newstr" ></textarea></td>
			</tr>
			<tr>
				<td colspan="2 " align="center"> <input type="button" value="替换" onclick="replace()"/></td>
			</tr>
		</table>
	</body>
```

数组

```javascript
	<script type="text/javascript">
		function print(s,v){
			document.write(s+''+v+"<br>");
		}
		function print2(s){
			document.write(s+"<br>");
		}
		function compare(x,y){
			return y-x;
		}
		function remove(a){
			var newarray = new Array();
			for(var i =0;i<a.length;i++)
			{
				if(check(a[i],newarray)==true)
					newarray.push(a[i]);
			}
			return newarray;
		}
		function check(value,a){
			for(i in a){
				if(a[i]==value)
					return false;
			}
			return true;
		}
		var x = new Array();
		print("通过new Array()创建一个空数组",x);
		var y = new Array(5);
		print("通过new Array(5)创建一个长度为5的数组，每个元素的值为undefine",y);
		var z = new Array(1,2,3,4,5,6);
		print("通过new Array(1,2,3,4,5,6)创建数组",z);
		print2(z.length);//数组长度
		print("当前数组是",z);
		for(var i=0;i<z.length;i++){
			print2(z[i]);
		}//第一种形式遍历
		for(i in z){
			print2(z[i]);	
		}//第二种形式遍历
		var f = new Array(0,0,0,0,0);
		var h = z.concat(f);
		print("连接后的数组为",h);
		var zz= z.join();
		print(zz,typeof zz);
		var ff = f.join("@");
		print(ff,typeof ff);
		// push pop在数组末尾添加/删除元素
		z.push(7);
		print2(z);
		z.pop();
		print2(z);
		// unshift shift 在数组开始添加/删除元素
		z.unshift(0);
		print2(z);
		z.shift();
		print2(z);
		//sort用于对数组进行排序从小到大
		z.sort();
		print2(z);
		//自定义排序
		z.sort(compare);
		print2(z);
		//
		var xx = new Array(3,2,3,3,3,4,1,5,2,9);
		xx = remove(xx);
		print2(xx);
		xx.sort();
		print2(xx);
	</script>
	<body>
	</body>
```

日期

```javascript
function log(a){
			document.write(a);
		}
		var d = new Date();
		log('new Date() '+d+"<br>");
		log("分别获取年月日:  ");
		log(d.getFullYear());
		log("/");
		log(d.getMonth()+1);
		log("/");
		log(d.getDate());
		log("<br>");
		log("分别获取时分秒毫秒:   ")
		log(d.getHours());
		log(":");
		log(d.getMinutes());
		log(":");
		log(d.getSeconds());
		log(":");
		log(d.getMilliseconds());
		log("<br>")
		var day = d.getDay();
		var weeks = new Array("星期天","星期一","星期二","星期三","星期四","星期五","星期六");
		log("今天是: "+weeks[day]+"<br>");
		log("从1970/1/1 08:00:00 到今天的毫秒数： "+ d.getTime()+"<br>");
		log("修改日期对象的值为世界末日:<br>");
		d.setFullYear(2012);
		d.setMonth(11); //月份是基0的，所以11表示12月
		d.setDate(12);
		d.setHours(0);
		d.setMinutes(0);
		d.setSeconds(0);
		log(d);
```

Math

```javascript
log(Math.E);//ln
	log(Math.PI);//圆周率
	log(Math.abs(-1));//绝对值
	log(Math.min(1,100));//最小值
	log(Math.max(1,100));//最大值
	log(Math.pow(3,3));//数的n次方
	log(Math.round(3.4));//四舍五入
	log(Math.round(3.5));//四舍五入
	log(Math.random());//随机数0～1
	for(var i =0;i<10;i++){
		log(Math.round(Math.random()*5)+5);
	}//10个5～10之间的随机数
```

自定义对象

```javascript
  //写成方法的形式	
  function hero(name){
		this.name = name;
		this.kill = function(){
			log(this.name+"正在杀敌!");
		}
	}
	//最垃圾方法
	var Hero = new Object();
	Hero.name = "盖伦";
	Hero.kill = function(){
		log(Hero.name + "正在杀敌!");
	}
	Hero.kill();
	
	//定义新hero
	var Timo = new hero("提莫");
	Timo.kill();
	var Soldier = new hero("皇子");
	Soldier.kill();
	//添加新方法
	hero.prototype.keng = function(){
		log(this.name+"正在坑队友!");
	}
	var Nuoshou = new hero("诺手");
	Nuoshou.keng();
```

BOM(Browser Object Model)浏览器对象模型

```javascript
//window窗口对象
<script type="text/javascript">
	function log(a){
		document.write(a+"<br>");
	}
	function newopenwindow(){
		myWindow = window.open("/");
	}
	log("文档内容");
	log("文档显示区域的宽度:  "+window.innerWidth);
	log("文档显示区域的高度:  "+window.innerHeight);
	log("浏览器的宽度:   "+window.outerWidth);
	log("浏览器的高度:  "+window.outerHeight);

	
</script>
<button type="button"onclick="newopenwindow()">打开一个新窗口</button>

//navigator浏览器对象
	log("<p>浏览器的名称: "+navigator.appName+"</p>");
	log("<p>浏览器的版本号: "+navigator.appVersion+"</p>");
	log("<p>浏览器的内部代码: "+navigator.addCodeName+"</p>");
	log("<p>操作系统: "+navigator.platform+"</p>");
	log("<p>是否使用cookies : "+navigator.cookieEnabled+"</p>");
	log("<p>浏览器的用户代理报头: "+navigator.userAgent+"</p>");

//screen屏幕对象
	log("用户的屏幕分辨率: "+screen.width+"*"+screen.height);
	log("可用的区域大小"+screen.availWidth+"*"+screen.availHeight);
//history历史对象

	function goBack(){
		history.back();
	}
	function goBacktwice(){
		history.go(-2);
	}
	<button type="button"onclick="goBack()">返回</button>
	<br>
	<button type="button"onclick="goBacktwice()"><返回上上次/button>

```



```javascript
//Location浏览器地址栏
<span >当前时间:</span>
<script>
	function log(a){
		document.write(a+"<br>");
	}
	var d = new Date();
 log(d.getHours()+":"+d.getMinutes()+":"+d.getSeconds()+":"+d.getMilliseconds());
	function refresh(){
		location.reload();
	}
	function jump(){
	  //方法1
	  //location="/";
	  //方法2
	  location.assign("/");
	}
	log("协议 location.protocol: "+location.protocol);
	log("主机名 location.hostname: "+location.hostname);
	log("端口号 (默认是80,没有即表示80)location.port: "+location.port);
	log("主机加端口号 location.host: " + location.host);
	log("访问路径 location.pathname: "+location.pathname);
	log("锚点 location.hash: "+location.hash);
	log("参数列表 location.search: "+location.search);
</script>

<button type="button"onclick=refresh()>刷新当前页面</button>
<br>
<button type="button"onclick=jump()>跳转到首页</button>

//弹出框
<script type="text/javascript">
	function log(a){
		document.write(a+"<br>");
	}
	function register(){
		alert("注册成功");
	}
	function del(){
		var d = confirm("是否要删除");
		alert(typeof d + " " + d);
	}
	function p(){
		var name = prompt("请输入用户名:");
		alert("您输入的用户名是"+ name);
	}
</script>
<button type="button"onclick="register()">注册</button>
<br>
<button type="button"onclick="del()">删除</button>
<br>
<button type="button"onclick="p()">输入</button>
```

```javascript
//计时器
	function printTime(){
		var date = new Date();
		var h  = date.getHours();
		var m  = date.getMinutes();
		var s =  date.getSeconds();
		document.getElementById('time').innerHTML = h+':'+m+':'+s;
	}
 	function showTimeinthreeSeconds(){
		setTimeout(printTime,3000);
	}//3秒打印一次当前时间，只打印一次
	var t = setInterval(printTime,1000);//一直打印当前时间，1s一次
	<div id = "time"></div>
	<button type="button" onclick="showTimeinthreeSeconds()">点击后3秒钟后显示当前时间，并且只显示一次</button>
		if(s%5==0){
			clearInterval(t);
		}//终止重复执行

```

**JSON**

```javascript
<script type="text/javascript">
	//JSON
	var gareen = {"name":"盖伦","hp":616};
	document.write("这是一个JSON对象: "+ gareen+"<br>");
	document.write("英雄名称: " +gareen.name+"<br>");
	document.write("英雄血量: " + gareen.hp + "<br>");
	
	//JSON数组
	var heros = 
	[
		{"name":"盖伦","hp":616},
		{"name":"提莫","hp":313},
		{"name":"死歌","hp":432},
		{"name":"火女","hp":389}
	]
	document.write("JSON数组大小："+heros.length+"<br>");
	document.write("第四个英雄是: "+heros[3].name+"<br>");
	
	//字符串->JSON对象
	var s1 = "{\"name\":\"盖伦\"";
	var s2 = ",\"hp\":616}";
	var s3 = s1 + s2 ;
	document.write("这是一个JSON格式的字符串: "+s3+"<br>");
	var gareen2 = eval("("+s3+")");
	document.write("这是一个JSON对象: " +gareen2+"<br>");
	//JSON对象->字符串
	document.write("这是一个JSON格式对象: "+gareen+"<br>");
	var gareenString = JSON.stringify(gareen);
	document.write("这是一个JSON字符串: "+gareenString+"<br>");
</script>


```



