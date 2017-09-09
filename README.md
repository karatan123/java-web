Book.java

```
package bean;

public class Book {
	public static int PAGE_SIZE=2;
	private int id;
	private String name;
	public int getId(){
		return id;
	}
	public void setId(int id){
		this.id=id;
	}
	public String getName(){
		return name;
	}
	public void setName(String name){
		this.name=name;
	}
}

```

index.jsp

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
    
    <title>My JSP 'index.jsp' starting page</title>
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
    	<form action="AddBook.jsp" method="post" onsubmit="return check(this)">
    		<table align="center" width="450">
    			<tr>
    				<td align="center" colspan="2">
    				<h2>添加图书信息</h2>
    				<hr>
    			</tr>
    			<tr>
    				<td align="right">图书编号：</td>
    				<td><input type="text" name="id"></td>
    			</tr>
    			<tr>
    				<td align="right">图书名称：</td>
    				<td><input type="text" name="name"></td>
    			</tr>
    			<tr>
    				<td align="center" colspan="2">
    					<input type="submit" value="添加">
    				</td>
    			</tr>
    		</table>
    	</form>
  </body>
</html>


```

AddBook.jsp
```
<%@ page language="java" import="java.util.*,java.sql.*" pageEncoding="UTF-8"%>
<%
String path = request.getContextPath();
String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
%>

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
  <head>
    <base href="<%=basePath%>">
    
    <title>My JSP 'AddBook.jsp' starting page</title>
    
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
    <%request.setCharacterEncoding("utf-8"); %>
    <jsp:useBean id="book" class="bean.Book"></jsp:useBean>
    <jsp:setProperty property="*" name="book"/>
    <%
    	try{
    	Class.forName("com.mysql.jdbc.Driver");
    	String url="jdbc:mysql://localhost:3306/hhh";
    	String username="root";
    	String password="zhj1124.";
    	Connection conn=DriverManager.getConnection(url,username,password);
    	String sql="insert into book(id,name) value(?,?)";
    	PreparedStatement ps=conn.prepareStatement(sql);
    	ps.setInt(1,book.getId());
    	ps.setString(2,book.getName());
    	int row=ps.executeUpdate();
    	if(row>0){
    		out.print("添加了"+row+"条数据");
    	}
    	ps.close();
    	conn.close();
    	}catch(Exception e){
    		out.print("添加信息失败");
    		e.printStackTrace();
    	}
     %>
     <br>
     <a href="index.jsp">继续添加</a>
     <a href="servlet/FindServlet">查看图书</a>
  </body>
</html>

```
