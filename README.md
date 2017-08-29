//遍历jsp文档并报获文档中的全部标记和标记总数


<%@ page language="java" import="java.util.*" pageEncoding="UTF-8"%>
<%
String path = request.getContextPath();
String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
%>

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
  <head>
    <base href="<%=basePath%>">
    <script language="javascript">
    	var elementList="";
    	function getElement(node){
    		var total=0;
    		if(node.nodeType==1){
    			total++;
    			elementList=elementList+node.nodeNnme+"、";
    		}
    		var childrens=node.childNodes;
    		for(var m=node.firstChild;m!=null;m=m.nextSibling){
    			total+=getElement(m);
    		}
    		return total;
    	}
    	function show(){
    		var number=getElement(document);
    		elementList=elementList.substring(0,elementList.length-1);
    		alert("该文档包含："+elementList+"等"+number+"个标记！");
    		elementList="";
    	}
    </script>
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
  
  <body onload="show()">
  		欢迎访问哈哈哈哈哈网站！
  		<br>
  		<a href="http://www.baidu.com">http://www.baidu.com</a>
  </body>
</html>
