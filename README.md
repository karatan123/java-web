FindServlet.java

```
package bean;
import java.sql.*;
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import java.util.*;
public class FindServlet extends HttpServlet {
	
	protected void doGet(HttpServletRequest request,HttpServletResponse response)throws ServletException,IOException{
		try{
				Class.forName("com.mysql.jdbc.Driver");
			String url="jdbc:mysql://localhost:3306/hhh";
			String username="root";
			String password="zhj1124.";
			Connection conn=DriverManager.getConnection(url,username,password);
			Statement stmt=conn.createStatement();
			String sql="select * from book";
			ResultSet rs=stmt.executeQuery(sql);
			List<Book> list=new ArrayList<Book>();
			while(rs.next()){
					Book book=new Book();
					book.setId(rs.getInt("id"));
					book.setName(rs.getString("name"));
					list.add(book);
			}
			request.setAttribute("list",list);
			rs.close();
			stmt.close();
			conn.close();
		}catch(ClassNotFoundException e){
			e.printStackTrace();
		}
		catch(SQLException e){
			e.printStackTrace();
		}
		request.getRequestDispatcher("/book.jsp").forward(request,response);
	}
}

```

book.jsp
```
<%@ page language="java" import="java.util.*,bean.Book" pageEncoding="UTF-8"%>
<%
String path = request.getContextPath();
String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
%>

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
  <head>
    <base href="<%=basePath%>">
    
    <title>My JSP 'book.jsp' starting page</title>
    
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
    <table align="center" width="450" border="1">
    	<tr>
    		<td align="center" colspan="4">
    			<h2>所有图书信息</h2>
    		</td>
    	</tr>
    	<tr align="center">
    		<td><b>ID:</b></td>
    		<td><b>书名：</b></td>
    		<td><b>修改书名</b></td>
    		<td><b>图书删除</b></td>
    	</tr>	
    	<%
    		List<Book> list=(List<Book>)request.getAttribute("list");
    		if(list==null||list.size()<1){
    			out.print("没有数据");
    		}else{
    			for(Book book : list){
    	%>
    	<tr align="center">
    		<td><%=book.getId() %></td>
    		<td><%=book.getName() %></td>
    	<td>
    		<form action="servlet/UpdateServlet" method="post" onsubmit="return check(this)">
    			<input type="hidden" name="id" value="<%=book.getId()%>">
    			<input type="text" name="name" size="3">
    			<input type="submit" value="修改">
    		</form>
    	</td>
    	<td>
    		<a href="servlet/DeleteServlet?id=<%=book.getId()%>">删除</a>
    	</td>
    	</tr>	
    	<%		
    	}
    	}
    	 %>
    </table>
  </body>
</html>


```
