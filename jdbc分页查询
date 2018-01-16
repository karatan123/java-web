dao.java
```
package bean;
import java.sql.*;
import java.util.*;
public class dao {
	public Connection getConnection(){
		Connection conn=null;
		try{
			Class.forName("com.mysql.jdbc.Driver");
			String url="jdbc:mysql://localhost:3306/hhh";
			String username="root";
			String password="zhj1124.";
			conn=DriverManager.getConnection(url,username,password);
		}catch(ClassNotFoundException e){
			e.printStackTrace();
		}catch(SQLException e){
			e.printStackTrace();
		}
		return conn;
	}
	public List<Book> find(int page){
		List<Book> list=new ArrayList<Book>();
		Connection conn=getConnection();
		String sql="select * from book order by id desc limit ?,?";
		try{
			PreparedStatement ps=conn.prepareStatement(sql);
			ps.setInt(1,(page-1)*Book.PAGE_SIZE);
			ps.setInt(2,Book.PAGE_SIZE);
			ResultSet rs=ps.executeQuery();
			while(rs.next()){
				Book b=new Book();
				b.setId(rs.getInt("id"));
				b.setName(rs.getString("name"));
				list.add(b);
			}
			rs.close();
			ps.close();
			conn.close();
		}catch(SQLException e){
			e.printStackTrace();
		}
		return list;
	}
	public int findCount(){
		int count=0;
		Connection conn=getConnection();
		String sql="select count(*) from book";
		try{
			Statement stmt=conn.createStatement();
			ResultSet rs=stmt.executeQuery(sql);
			if(rs.next()){
				count=rs.getInt(1);
			}
			rs.close();
			stmt.close();
			conn.close();
		}catch(SQLException e){
			e.printStackTrace();
		}
		return count;
	}
}

```
servletfind
```
package bean;
import java.io.*;
import java.sql.*;
import javax.servlet.*;
import javax.servlet.http.*;
import java.util.*;
public class servletfind extends HttpServlet {
	protected void doGet(HttpServletRequest request,HttpServletResponse response)throws ServletException,IOException{
		int currPage=1;
		if(request.getParameter("page")!=null){
			currPage=Integer.parseInt(request.getParameter("page"));
		}
		dao d=new dao();
		List<Book> list=d.find(currPage);
		request.setAttribute("list",list);
		int pages;
		int count=d.findCount();
		if(count%Book.PAGE_SIZE==0){
			pages=count/Book.PAGE_SIZE;
		}else{
			pages=count/Book.PAGE_SIZE+1;
		}
		StringBuffer sb=new StringBuffer();
		for(int i=1;i<=pages;i++){
			if(i==currPage){
				sb.append("["+i+"]");
			}else{
				sb.append("<a href='servlet/servletfind?page="+i+"'>"+i+"</a>");
			}
			sb.append(" ");
		}
		request.setAttribute("bar",sb.toString());
		request.getRequestDispatcher("/product_list.jsp").forward(request,response);
	}
}

```
2.jap
```
<body>
    <a href="servlet/servletfind">分页查看信息</a>
  </body>
```
