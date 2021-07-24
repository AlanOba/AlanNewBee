# JSP笔记

==Servlet:在java中写html代码很麻烦----->在html页面中写java代码很爽即引入了JSP(JavaServer Pages)==

**开头必备**

```jsp
<%@
	page contentType="text/html; charset=UTF-8"
  pageEncoding="UTF-8" 
  import="java.util.*"
%>
```

## 执行过程

![执行过程](https://stepimagewm.how2j.cn/1655.png)

**把jsp编译成Servlet的形式**

## 页面元素

![页面元素](https://stepimagewm.how2j.cn/1657.png)

<%="hello jsp"%> 相当于<%out.println("hello jsp");%>

实现在html页面以表格的形式显示一个for循环内容

```jsp
<%
    List<String> words = new ArrayList<String>();
    words.add("today");
    words.add("is");
    words.add("a");
    words.add("great");
    words.add("day");
%>
<table width="200px" align="center" border="1" cellspacing="0">
<%for (String word : words) {%>
<tr>
    <td><%=word%></td>
  	<%--<%out.print(word);%> --%>
</tr>
<%}%>
</table>
```

## include jsp

**指令include**

<%@include file="footer.jsp" %>

**动作include**

<jsp:include page="footer.jsp" />

**区别**

![image-20200226141550913](/Users/alan/Library/Application Support/typora-user-images/image-20200226141550913.png)

**传参**

![image-20200226141627867](/Users/alan/Library/Application Support/typora-user-images/image-20200226141627867.png)

## 跳转

**客户端跳转**

```jsp
<% 
  response.sendRedirect("hello.jsp");
%>
```

**服务端跳转**

```jsp
<%
request.getRequestDispatcher("hello.jsp").forward(request, response);
%>
<%--使用动作简化代码--%>
<jsp:forward page="hello.jsp"/>
```

## cookie

> Cookie是一种浏览器和服务器交互数据的方式。
>
> Cookie是由服务器端创建，但是**不会保存在服务器**。
>
> 创建好之后，发送给浏览器。浏览器**保存在用户本地**。
>
> 下一次访问网站的时候，就会把该Cookie发送给服务器。

==原理==

![cookie原理示意图](https://stepimagewm.how2j.cn/1675.png)

**setCookie**

```jsp
<%@
    page language="java"  contentType="text/html;charset=utf-8" pageEncoding="UTF-8" import="javax.servlet.http.Cookie"
%>
<% Cookie c = new Cookie("name","Alan");
    c.setMaxAge(24*60*60); <%--一天--%>
    c.setPath("/");    
		<%--Path表示访问服务器的所有应用都会提交这个cookie到服务端，如果其值是 /a, 那么就表示仅仅访问 /a 路径的时候才会提交 cookie--%>
    response.addCookie(c);
%>
<a href="getCookie.jsp">跳转到获取cookie的页面</a>
```

**getCookie**

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
         pageEncoding="UTF-8" import="javax.servlet.http.Cookie"%>
<%
    Cookie[] cookies = request.getCookies();
    if (null != cookies)
        for (int d = 0; d <= cookies.length - 1; d++) {
         out.print(cookies[d].getName() + ":" + cookies[d].getValue() + "<br>");
        }
%>
```

==out.print==在idea上会报bug，不用管。