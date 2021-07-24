

# Servlet学习笔记

## 基础

### 建立第一个JavaWeb程序

#### 1.启动tomcat

![image-20200201165254959](/Users/alan/Library/Application Support/typora-user-images/image-20200201165254959.png)

> sudo sh startup.sh

**检查是否启动成功：**http://127.0.0.1:8080/

#### 2.编写JavaWeb程序

build所需文件生成.class

**在tomcat的server.xml文件中设置程序路径**

```xml
	<Context path="/JavaWebTest" docBase="/Users/alan/JavaWebTest/web" debug="0" reloadable="false" />

```

#### 3.启动Javaweb程序

![image-20200201165758475](/Users/alan/Library/Application Support/typora-user-images/image-20200201165758475.png)



### Servlet获取参数

```java
//获取登录账户和密码为例
public class LoginServlet extends HttpServlet  {
    protected void doPost(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws ServletException , IOException
    {
        String name = httpServletRequest.getParameter("name");
        String password = httpServletRequest.getParameter("password");
        System.out.println("name: "+name);
        System.out.println("password: " +password);
    }
}
//将信息输出到tomcat的控制台下
```

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>登录页面</title>
</head>
<body>
    <form action="login" method="post">
        账号:<input type="text" name="name"><br>
        密码:<input type="password" name="password"><br>
        <input type="submit" value="登录">
    </form>
</body>
</html>
```

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<web-app>
    <servlet>
        <servlet-name>HelloServlet</servlet-name> <!-- 设置必须与servlet-mapping中的servlet-name相同-->
        <servlet-class>HelloServlet</servlet-class><!-- 一般设置为与servlet-name一样 -->
    </servlet>
    <servlet-mapping>
        <servlet-name>HelloServlet</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
    <servlet>
        <servlet-name>LoginServlet</servlet-name>
        <servlet-class>LoginServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>LoginServlet</servlet-name>
        <url-pattern>/login</url-pattern>
    </servlet-mapping>
</web-app>
```

==在Mac中像Windows一样查看Tomcat控制台信息==

在Windows系统中，通过startup.bat启动Tomcat之后会打开一个控制台，输出日志信息，在系统调试过程中，也会随时输入日志或错误信息，对开发很有帮助。
在Mac中，通过startup.sh启动Tomcat却只会输入几行信息告知Tomcat已经启动，而不会输出一些过程信息。
其实Mac也可以像Windows一样随时查看Tomcat控制台信息，具体步骤如下：
启动Tomcat之后，执行以下命令在终端中监视上一级logs日志文件夹下的**catalina.out**文件的变化：

```
tail -f ../logs/catalina.out
```

如果catalina.out文件的尾部内容有变化，就会立刻刷新显示在屏幕上。
要停止监视的话，就按下`ctrl+c`退出。

### 返回响应

```java
//把登录成功与否的信息返回到html页面上
public class LoginServlet extends HttpServlet  {
    protected void doPost(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws ServletException , IOException
    {
        String name = httpServletRequest.getParameter("name");
        String password = httpServletRequest.getParameter("password");
        String responseHtml = "111";
        if("admin".equals(name)&&"123".equals(password)){
            responseHtml = "<div style='color:green'>success</div>";
        }
        else{
            responseHtml="<div style='color:red'>fail</div>";
        }
        httpServletResponse.getWriter().println(responseHtml);
    }
}
```

### 调用流程

![流程图](https://stepimagewm.how2j.cn/7461.png)

### service()原理

LoginServlet继承了HttpServlet,同时也继承了一个方法 service(HttpServletRequest , HttpServletResponse )

实际上，在执行doGet()或者doPost()之前，都会先执行service(),由service()方法进行判断，到底该调用doGet()还是doPost()

可以发现，service(), doGet(), doPost() 三种方式的参数列表都是一样的。

所以，有时候也会**直接重写service()**方法，在其中提供相应的服务，就不用区分到底是get还是post了。

比如把前面的登录的LoginServlet，改为提供service方法，也可以达到相同的效果

```java
public class LoginServlet extends HttpServlet {
    protected void service(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        String name = request.getParameter("name");
        String password = request.getParameter("password");
        String html = null;
        if ("admin".equals(name) && "123".equals(password))
            html = "<div style='color:green'>success</div>";
        else
            html = "<div style='color:red'>fail</div>";
        PrintWriter pw = response.getWriter();
        pw.println(html);
    }
}
```

==当浏览器使用get方式提交数据的时候，servlet需要提供doGet()方法==

**哪些是get方式呢？**

form默认的提交方式
如果通过一个超链访问某个地址
如果在地址栏直接输入某个地址
ajax指定使用get方式的时候

==当浏览器使用post方式提交数据的时候，servlet需要提供doPost()方法==

**哪些是post方式呢？**
在form上显示设置 method="post"的时候
ajax指定post方式的时候

### 显示中文

#### 获取中文的参数

login.html中添加

```html
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
```

servlet.java中添加

```java
request.setCharacterEncoding("UTF-8"); 
```

之后在tomcat的控制台就可以显示中文了

#### 返回中文的响应

servlet.java中添加

```java
response.setContentType("text/html; charset=UTF-8");
```

之后在html页面上就可以显示中文了

### 生命周期

![image-20200203175130873](/Users/alan/Library/Application Support/typora-user-images/image-20200203175130873.png)

**实例化**和**初始化**函数只会执行一次

**销毁**的两种情况destroy()
在如下几种情况下，会调用destroy()

1. 该Servlet所在的web应用重新启动
   在server.xml中配置该web应用的时候用到了

```xml
<Context path="/" docBase="e:\\project\\j2ee\\web" debug="0" reloadable="false" />
```

 如果把 reloadable="**false**" 改为reloadable="**true**" 就表示有任何类发生的更新，web应用会**自动重启**
当web应用自动重启的时候，destroy()方法就会被调用

2. 关闭tomcat的时候 destroy()方法会被调用，但是这个一般都发生的很快，不易被发现。

```java
public LoginServlet(){
    System.out.println("LoginServlet 的构造方法被调用");
}
public void init(ServletConfig servletConfig){
    System.out.println("LoginServlet 的初始化方法被调用");
}
public void destroy() {
    System.out.println("destroy()");
}
```

### 页面跳转

准备好两个页面success.html fail.html

#### 服务端跳转

```java
if("admin".equals(name)&&"123".equals(password)){  httpServletRequest.getRequestDispatcher("success.html").forward(httpServletRequest,httpServletResponse);
}
else{
httpServletRequest.getRequestDispatcher("fail.html").forward(httpServletRequest,httpServletResponse);
}
```

#### 客户端跳转

```java
response.sendRedirect("fail.html");
```

==区别:==客户端跳转后网页地址的路径随之发生改变，服务端跳转不会。

![服务端跳转与客户端跳转图示](https://stepimagewm.how2j.cn/1602.png)

### 自启动

**意义:**

> 有的时候会有这样的业务需求：
> tomcat一启动，就需要执行一些初始化的代码，比如校验数据库的完整性等。
>
> 但是Servlet的生命周期是在用户访问浏览器对应的路径开始的。如果没有用户的第一次访问，就无法执行相关代码。
>
> 这个时候，就需要Servlet实现**自启动** 即，伴随着tomcat的启动，自动启动初始化，在初始化方法init()中，就可以进行一些业务代码的工作了。

Step1:

```xml
<!--web.xml-->
<servlet>
    <servlet-name>HelloServlet</servlet-name> <!-- 设置必须与servlet-mapping中的servlet-name相同-->
    <servlet-class>HelloServlet</servlet-class><!-- 一般设置为与servlet-name一样 -->
    <load-on-startup>10</load-on-startup><!--数值为级别，越小越优先-->
</servlet>
```

Step2:

```java
//HelloServlet.java
public void init(ServletConfig servletConfig){
    System.out.println("init of HelloServlet");
}
```



### request常用方法

#### 常用

**request.getRequestURL():** 浏览器发出请求时的完整URL，包括协议 主机名 端口(如果有)"
**request.getRequestURI():** 浏览器发出请求的资源名部分，去掉了协议和主机名"
**request.getQueryString():** 请求行中的参数部分，只能显示以get方式发出的参数，post方式的看不到
**request.getRemoteAddr():** 浏览器所处于的客户机的IP地址
**request.getRemoteHost():** 浏览器所处于的客户机的主机名
**request.getRemotePort():** 浏览器所处于的客户机使用的网络端口
**request.getLocalAddr():** 服务器的IP地址
**request.getLocalName():** 服务器的主机名
**request.getMethod():** 得到客户机请求方式一般是GET或者POST

```java
public class LoginServlet extends HttpServlet  {
protected void doPost(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws ServletException , IOException
    {
        System.out.println("浏览器发出请求时的完整URL，包括协议 主机名 端口(如果有): " + httpServletRequest.getRequestURL());
  //http://127.0.0.1:8080/JavaWebTest/login
        System.out.println("浏览器发出请求的资源名部分，去掉了协议和主机名: " + httpServletRequest.getRequestURI());///JavaWebTest/login
        System.out.println("请求行中的参数部分: " + httpServletRequest.getQueryString());
  //null
        System.out.println("浏览器所处于的客户机的IP地址: " + httpServletRequest.getRemoteAddr());//127.0.0.1
        System.out.println("浏览器所处于的客户机的主机名: " + httpServletRequest.getRemoteHost());//127.0.0.1
            System.out.println("浏览器所处于的客户机使用的网络端口: " + httpServletRequest.getRemotePort());//53941
            System.out.println("服务器的IP地址: " + httpServletRequest.getLocalAddr());
  //127.0.0.1
            System.out.println("服务器的主机名: " + httpServletRequest.getLocalName());
  //localhost
            System.out.println("得到客户机请求方式: " + httpServletRequest.getMethod());
  //POST
            String name = httpServletRequest.getParameter("name");
            String password = httpServletRequest.getParameter("password");
            String html = null;
            if("admin".equals(name)&&("123").equals(password)){
                html = "<div style='color:green'>验证成功</div>";
            }else{
            html = "<div style='color:red'>验证失败</div>";
        }
        httpServletResponse.setContentType("text/html;charset=UTF-8");
        httpServletResponse.getWriter().println(html);
    }
}
```

#### 获取参数

**request.getParameter()**: 是常见的方法，用于获取单值的参数
**request.getParameterValues():** 用于获取具有多值的参数，比如注册时候提交的 "hobits"，可以是多选的。
**request.getParameterMap():** 用于遍历所有的参数，并返回Map类型。

```java
public class RegisterServlet extends HttpServlet {
    public void doGet(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse)throws ServletException , IOException {
        System.out.println("获取单值参数name:"+httpServletRequest.getParameter("name"));
     		 //admin
        String[]hobits = httpServletRequest.getParameterValues("hobits");
        System.out.println("获取具有多值的参数hobits:"+ Arrays.asList(hobits));
      	//获取具有多值的参数hobits:[lol, dota]
        System.out.println("通过getParameterMap 遍历所有的参数:");
        Map<String,String[]> parameters = httpServletRequest.getParameterMap();
        Set<String> paramNames =parameters.keySet();
        for(String param :paramNames){
            String[]value = parameters.get(param);
            System.out.println(param+":"+Arrays.asList(value));
        }
      	/*
      	通过getParameterMap 遍历所有的参数:
				name:[admin]
				hobits:[lol, dota]
      	*/
    }
}
```

#### 获取头信息

```java
public class HelloServlet extends HttpServlet {
    public void doGet(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) {
        Enumeration<String>enumeration = httpServletRequest.getHeaderNames();
        System.out.println("-------------start-----------");
        int i=1;
        while(enumeration.hasMoreElements()){
            String headername = enumeration.nextElement();
            String value = httpServletRequest.getHeader(headername);
            System.out.printf("%d\t%s\t%s%n",i++,headername,value);
        }
        try{
            httpServletResponse.getWriter().println("<h1>Hello SErvlet!</h1>");
            httpServletResponse.getWriter().println(new Date().toString());
        }catch (IOException e){
            e.printStackTrace();
        }
    }
}
```

**request.getHeader()** 获取浏览器传递过来的头信息。
比如getHeader("user-agent") 可以获取浏览器的基本资料，这样就能判断是firefox、IE、chrome、或者是safari浏览器
**request.getHeaderNames()** 获取浏览器所有的**头信息名称**，根据头信息名称就能遍历出所有的头信息

在本例，修改HelloServlet,使其获取头信息
访问HelloServlet获取如下头信息:
host: 主机地址
user-agent: 浏览器基本资料
accept: 表示浏览器接受的数据类型
accept-language: 表示浏览器接受的语言
accept-encoding: 表示浏览器接受的**压缩方式**，是压缩方式，并非编码
connection: 是否保持连接
cache-control: 缓存时限

![image-20200208164131188](/Users/alan/Library/Application Support/typora-user-images/image-20200208164131188.png)

![image-20200208164141660](/Users/alan/Library/Application Support/typora-user-images/image-20200208164141660.png)

#### 服务端传参

**setAttribute**和**getAttribute**可以用来在进行服务端跳转的时候，在不同的Servlet之间进行数据共享

### response用法

#### 设置相应内容

之前提及的

> 通过response设置响应已经用得比较多了，在前面的Servlet学习中都是用到
> PrintWriter pw= **response.getWriter();**
> 通过response.getWriter(); 获取一个PrintWriter 对象
> 可以使用println(),append(),write(),format()等等方法设置返回给浏览器的html内容。

#### 设置响应格式 

```java
response.setContentType("text/html");
```


"text/html" 是即格式 ，在[request获取头信息](https://how2j.cn/k/servlet/servlet-request/555.html#step1609) 中对应的request.getHeader("accept").
"text/html" 是存在的，表示浏览器可以识别这种格式，如果换一个其他的格式， 比如 "text/lol" ，浏览器不能识别，那么打开此servlet就会弹出一个下载的对话框。

这样的手段也就常常用于实现下载功能

在chrome浏览器里实现下载功能，只需要把text/html改成其他的即可

#### 设置相应编码

设置响应编码有两种方式

```java
1. response.setContentType("text/html; charset=UTF-8");
2. response.setCharacterEncoding("UTF-8");
```

这两种方式都需要在response.getWriter调用之前执行才能生效。

他们的区别在于

```java
 response.setContentType("text/html; charset=UTF-8");
```


不仅发送到浏览器的内容会使用UTF-8编码，而且还通知浏览器使用UTF-8编码方式进行显示。所以总能正常显示中文

```java
 response.setCharacterEncoding("UTF-8"); 
```

 仅仅是发送的浏览器的内容是UTF-8编码的，至于浏览器是用哪种编码方式显示不管。 所以当浏览器的显示编码方式不是UTF-8的时候，就会看到乱码，需要手动再进行一次设置。

#### 301或者302客户端跳转

客户端有两种跳转
302 表示临时跳转
301 表示永久性跳转

302就是前面在[客户端跳转](https://how2j.cn/k/servlet/servlet-jump/551.html#step1567)章节用到过的

```java
response.sendRedirect("fail.html");
```

 301要使用另外的手段：

```java
response.setStatus(301);
response.setHeader("Location", "fail.html");
```

 用户感受不出这两种跳转的区别，但是可以借助[火狐的调试工具](https://how2j.cn/k/http/http-debug/569.html)看到响应的头信息是:
301 Moved Permanently。
301和302的区别主要在搜索引擎对页面排名的时候有影响，这是属于SEO范畴的概念，在此就不展开了。

#### 设置不使用缓存

使用缓存可以加快页面的加载，降低服务端的负担。但是也可能看到过时的信息，可以通过如下手段通知浏览器不要使用缓存 

```java
response.setDateHeader("Expires",0 );
response.setHeader("Cache-Control","no-cache");
response.setHeader("pragma","no-cache");
```

### Servlet上传文件（待分析）

==源码:==

```java
//UploadPhotoServlet.java
import org.apache.commons.fileupload.FileItem;
import org.apache.commons.fileupload.FileUploadException;
import org.apache.commons.fileupload.disk.DiskFileItemFactory;
import org.apache.commons.fileupload.servlet.ServletFileUpload;

import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.InputStream;
import java.util.Iterator;
import java.util.List;

public class UploadPhotoServlet extends HttpServlet {
    public void doPost(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse){
        String filename=null;
        try{
            DiskFileItemFactory factory = new DiskFileItemFactory();
            ServletFileUpload upload = new ServletFileUpload(factory);
            //设置文件上传大小限制为1M
            factory.setSizeThreshold(1024*1024);

            List items = null;
            try{
                items = upload.parseRequest(httpServletRequest);
            }catch (FileUploadException e){
                e.printStackTrace();
            }
            Iterator iter = items.iterator();
            while(iter.hasNext()){
                FileItem item = (FileItem)iter.next();
                if(!item.isFormField()){
                    //根据时间戳创建头像文件
                    filename = System.currentTimeMillis() +".jpg";
                    //通过getRealPath获取上传文件夹
                    String photoFolder =httpServletRequest.getServletContext().getRealPath("uploaded");
                    File f = new File(photoFolder,filename);
                    f.getParentFile().mkdirs();
                    //通过item.getInputStream()获取浏览器上传文件的输入流
                    InputStream is =item.getInputStream();
                    //复制文件
                    FileOutputStream fos = new FileOutputStream(f);
                    byte b[] = new byte[1024*1024];
                    int length=0;
                    while(-1!=(length=is.read(b))){
                        fos.write(b,0,length);
                    }
                    fos.close();
                }
                else{
                    System.out.println(item.getFieldName());
                    String value = item.getString();
                    value = new String(value.getBytes("ISO-8859-1"),"UTF-8");
                    System.out.println(value);
                }
            }
            String html="<img width='200' height='150' src='uploaded/%s' />";
            httpServletResponse.setContentType("text/html");
            httpServletResponse.getWriter().format(html,filename);
        }catch (FileNotFoundException e){
            e.printStackTrace();
        }catch (Exception e){
            e.printStackTrace();
        }
    }
}
```

```html
<!--upload.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
</head>
<body>
    <form method="post" action="uploadPhoto" enctype="multipart/form-data">
        英雄名称 <input name="heroName"  type="text"/> <br>
        上传图像<input name="filepath" type="file"/><br>
        <input type="submit" value="上传"/>
    </form>
</body>
</html>
```

## Serlvet+JSON

### Servlet提交数据

==原理：将html上input的数据传递到服务器，转换为JSON对象，再转换为Hero对象。==

```java
//submitServlet.java --core codes
String data = httpServletRequest.getParameter("data"); //这是一个JSON字符串
System.out.println("服务端接收到的数据是 "+data);
JSONObject json = JSONObject.fromObject(data);         //这是一个JSON对象
System.out.println("转换为JSON对象之后是 "+json);	
Hero hero = (Hero)JSONObject.toBean(json,Hero.class);  //这是一个Hero对象
System.out.println("转换为Hero对象之后是 "+hero);
```

html页面：==使用了jquery框架==

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta http-equiv="Content-Type" content="text/html;charset=utf-8">
    <title>用AJAX以JSON的方式提交数据</title>
    <script type="text/javascript" src="jquery.min.js"></script>
</head>
<body>
    <form >
        名称<input type="text" id="name"><br>
        血量<input type="text" id="hp"><br>
        伤害<input type ="text" id="damage"><br>
        <input type="button" value="提交" id="sender">
    </form>
    <div id="messageDiv"></div>
    <script>
        $('#sender').click(function(){
            var name=document.getElementById('name').value;
            var hp=document.getElementById('hp').value;
            var damage = document.getElementById('damage').value;
            var hero={"name":name,"hp":hp,"damage":damage};
            var url="submitServlet";

            $.post(
                url,
                {"data":JSON.stringify(hero)},
                function(data) {
                    alert("提交成功，请在Tomcat控制台查看服务端接收到的数据");
                });
        });

    </script>
</body>
</html>
```

### Servlet获取一个对象

**实现效果**：通过html页面点击，获取一个数据库中的对象hero，在html显示他的信息(name,hp,damage)

**所用技术**：Hero对象->JSONObject对象->json对象

```javascript
var json=JSON.parse(data); //转换为json对象
var name =json.hero.name; 
var hp = json.hero.hp;
//JSON.stringify() 将json对象转换为字符串
```

### Servlet获取多个对象

**实现效果**：通过html页面点击，获取多个数据库中的对象，显示他们的信息

```java
//Servlet
List<Hero> heros = new HeroDAO().list();
String result = JSONSerializer.toJSON(heros).toString();
httpServletResponse.setContentType("text/html;charset=utf-8");
httpServletResponse.getWriter().print(result);
```

```javascript
<script>
    $('#sender').click(function(){
        var url = "getManyServlet";
        $.post(
                url,
                function(result){
                    var heros = $.parseJSON(result);
                	  //转换为JSON对象
                    for(i in heros){
                        var old = $("#messageDiv").html();
                        var hero = heros[i];
                        $("#messageDiv").html(old+"<br>"+hero.id+"----"+hero.name+"----"+hero.hp+"----"+hero.damage);
                    }
                }
        );
    });
</script>
```