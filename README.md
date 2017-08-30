####session
##index.jsp
```
<%@ page language="java" import="java.util.*" pageEncoding="UTF-8"%>
<%
String path = request.getContextPath();
String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
%>

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
  <head>
    <base href="<%=basePath%>">
   
    <title>一个简单文档</title>
	<meta http-equiv="pragma" content="no-cache">
	<meta http-equiv="cache-control" content="no-cache">
	<meta http-equiv="expires" content="0">    
	<meta http-equiv="keywords" content="keyword1,keyword2,keyword3">
	<meta http-equiv="description" content="This is my page">
	<!--
	<link rel="stylesheet" type="text/css" href="styles.css">
	-->
  </head>
  
  <body>
  		<form id="form1" name="form1" method="post" action="session.jsp">
  			<div align="cneter">
  				<table width="25%" border="0">
  					<tr>
  						<td width="40%"><div align="center">您的名字是：  </div></td>
  						<td width="60%">
  							<laber>
  								<div align="center">
  									<input type="text" name="name"/>
  								</div>
  							</laber>
  						</td>
  					</tr>
  					<tr>
  						<td colspan="2">
  							<lable>
  								<div align="center">
  									<input type="submit" name="Submit" value="提交" >
  								</div>
  							</lable>
  						</td>
  					</tr>
  				</table>
  			</div>
  		</form>
  </body>
</html>

```
###session.jsp
```
<%@ page language="java" import="java.util.*" pageEncoding="UTF-8"%>
<%
String path = request.getContextPath();
String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
%>

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
  <head>
    <base href="<%=basePath%>">
    
    <title>My JSP 'session.jsp' starting page</title>
    
	<meta http-equiv="pragma" content="no-cache">
	<meta http-equiv="cache-control" content="no-cache">
	<meta http-equiv="expires" content="0">    
	<meta http-equiv="keywords" content="keyword1,keyword2,keyword3">
	<meta http-equiv="description" content="This is my page">
	<!--
	<link rel="stylesheet" type="text/css" href="styles.css">
	-->

  </head>
  
  <body>
   <%
   	String name=request.getParameter("name");
   	session.setAttribute("name",name);
    %>
    <div align="cneter">
    	<form id="form1" name="form1" method="post" action="result.jsp">
    	<table width="28%" border="0">
    		<tr>
    			<td>您的名字是：</td>
    			<td><%=name %></td>
    		</tr>
    		<tr>
    			<td>您最喜欢去的地方是： </td>
    			<td><lable>
    				<input type="text" name="address">
    			</lable></td>
    		</tr>
    		<tr>
    			<td colspan="2"><label>
    				<div align="center">
    					<input type="submit" name="Submit" value="提交">
    				</div>
    			</label></td>
    		</tr>
    	</table>
    </div>
  </body>
</html>
```
###result.jsp
```
<%@ page language="java" import="java.util.*" pageEncoding="UTF-8"%>
<%
String path = request.getContextPath();
String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
%>

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
  <head>
    <base href="<%=basePath%>">
    
    <title>My JSP 'result.jsp' starting page</title>
    
	<meta http-equiv="pragma" content="no-cache">
	<meta http-equiv="cache-control" content="no-cache">
	<meta http-equiv="expires" content="0">    
	<meta http-equiv="keywords" content="keyword1,keyword2,keyword3">
	<meta http-equiv="description" content="This is my page">
	<!--
	<link rel="stylesheet" type="text/css" href="styles.css">
	-->

  </head>
  
  <body>
    <%
    	String name=(String)session.getAttribute("name");
    	String solution=request.getParameter("address");
     %>
     <form id="form1" name="form1" method="post" action="">
     	<table width="28%" border="0">
     		<tr>
     			<td colspan="2"><div align="center"><strong></strong></div></td>
     			<td width="41%"><div align="left">您的名字是：</div></td>
     			<td width="59%"><label>
     				<div align="left"><%=name %></div>
     			</label>
     			</td><br>
     			<tr>
     				<td><label>
     					<div align="left">您最喜欢去的地方是：</div>
     				</laber></td>
     				<td><div align="left"><%=solution %></div></td>
     			</tr>
     		</tr>
     	</table>
     </form>
  </body>
</html>

```
