DeleteServlet
```
package bean;
import java.sql.*;
import javax.servlet.*;
import javax.servlet.http.*;
import java.io.*;
public class DeleteServlet extends HttpServlet {
	protected void doGet(HttpServletRequest request,HttpServletResponse response)throws IOException,ServletException{
		int id=Integer.valueOf(request.getParameter("id"));
		try{
			Class.forName("com.mysql.jdbc.Driver");
			String url="jdbc:mysql://localhost:3306/hhh";
			String username="root";
			String password="zhj1124.";
			Connection conn=DriverManager.getConnection(url,username,password);
			String sql="delete from book where id=?";
			PreparedStatement ps=conn.prepareStatement(sql);
			ps.setInt(1,id);
			ps.executeUpdate();
			ps.close();
			conn.close();
		}catch(Exception e){
			e.printStackTrace();
		}
		response.sendRedirect("servlet/FindServlet");
	}
}

```
