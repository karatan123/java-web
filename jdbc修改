UpdateServlet,java

```
package bean;
import java.sql.*;
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class UpdateServlet extends HttpServlet {
	protected void doPost(HttpServletRequest request,HttpServletResponse response)throws ServletException,IOException{
	int id=Integer.valueOf(request.getParameter("id"));
	String name=request.getParameter("name");
	try{
		Class.forName("com.mysql.jdbc.Driver");
		String url="jdbc:mysql://localhost:3306/hhh";
		String username="root";
		String password="zhj1124.";
		Connection conn=DriverManager.getConnection(url,username,password);
		String sql="update book set name=? where id=?";
		PreparedStatement ps=conn.prepareStatement(sql);
		ps.setString(1,name);
		ps.setInt(2,id);
		ps.executeUpdate();
		ps.close();
		conn.close();
	}catch(Exception e){
		e.printStackTrace();
	}
	response.sendRedirect("/servlet/FindServlet");
	}
}

```
