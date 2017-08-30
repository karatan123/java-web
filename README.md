```
###99乘法表
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
  		<%
  			String str="";
  			for(int i=1;i<=9;i++){
  			for(int j=1;j<=i;j++){
  				str+=j+"*"+i+"="+j*i;
  				str+="&nbsp";
  				}
  				str+="<br>";
  				}
  		 %>
  		 <table width="440" height="85" border="1" cellpadding="0" style="font:9pt"
  		 bordercolordark="#666666" bordercolorlight="#FFFFFF" bordercolor="#FFFFFF">
  		 <tr>
  		 	<td height="30" align="center">九九乘法表</td>
  		 </tr>
  		 <tr>
  		 	<td style="padding:3pt">
  		 		<%=str %>
  		 	</td>
  		 </tr>
  		 </table>
  </body>
</html>
```
