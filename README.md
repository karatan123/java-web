#####bean.Email.java
```
package bean;

import java.io.*;

public class Email implements Serializable{
	private static final long  serialVersionUID=1L;
	private String mailAdd;
	private boolean email;
	public Email(){
	}
	public Email(String mailAdd){
		this.mailAdd=mailAdd;
	}
	public boolean isEmail(){
		String regex="\\w+([-+.']\\w+)*@\\w+([-.]\\w+)*\\.\\w+([-.]\\w+)*";
		if(mailAdd.matches(regex)){
			email=true;
		}
		return email;
	}
	public String getMailAdd(){
		return mailAdd;
	}
	public void setMailAdd(String mailAdd){
		this.mailAdd=mailAdd;
	}
}
```



####inex.jsp
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
  		<form action="result.jsp" method="post">
  			<table align="center" width="300" border="1" height="150">
  				<tr>
					<td colspan="2" align="center">
						<b>邮箱认证系统</b>
					</td>  				
  				</tr>
  				<tr> 
  					<td align="right">邮箱地址：</td>
  					<td><input type="text" name="mailAdd"></td>
  				</tr>
  				<tr>
  					<td colspan="2" align="center">
  						<input type="submit">
  					</td>
  				</tr>
  			</table>
  		</form>
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
<%@ page import="bean.Email" %>
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
    	<div align="center">
    		<%
    			String mailAdd=request.getParameter("mailAdd");
    			Email email=new Email(mailAdd);
    			if(email.isEmail()){
					   out.print(mailAdd+"<br>是一个标准的邮箱地址"); 			
    			}else{
   					   out.print(mailAdd+"<br>不是一个标准邮箱地址"); 			
       			}
    		 %>
    	</div>
  </body>
</html>
```
