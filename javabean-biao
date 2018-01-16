#### DateBean.java
```
package bean;
import java.text.*;
import java.util.*;
public class DateBean {
	private String dateTime;
	private String week;
	private Calendar calendar=Calendar.getInstance();
	public String getDateTime(){
		Date currDate=Calendar.getInstance().getTime();
		SimpleDateFormat sdf=new SimpleDateFormat("yyyy年MM月dd日 HH点mm分ss秒");
		dateTime=sdf.format(currDate);
		return dateTime;
	}
	public String getWeek(){
		String[] weeks={"星期日","星期一","星期二","星期三","星期四","星期五","星期六"};
		int index=calendar.get(Calendar.DAY_OF_WEEK);
		week=weeks[index-1];
		return week;
	}
}

```



#### index.jsp
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
   	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>电子时钟</title>
	<meta http-equiv="pragma" content="no-cache">
	<meta http-equiv="cache-control" content="no-cache">
	<meta http-equiv="expires" content="0">    
	<meta http-equiv="keywords" content="keyword1,keyword2,keyword3">
	<meta http-equiv="description" content="This is my page">
	<!--
	<link rel="stylesheet" type="text/css" href="styles.css">
	-->
	<style type="text/css">
		#clock{
			width:420px;
			height:80px;
			background:#E0E0E0;
			font-size:25px;
			font-weight:bold;
			border:solid 5px orange;
			padding:20px;
		}
		#week{
			padding-top:15px;
			color:20px;
		}
	</style>
  </head>
  
  <body>
  	<jsp:useBean id="date" class="bean.DateBean" scope="application"></jsp:useBean>
  	<div align="center">
  		<div id="clock">
  			<div id="time">
  				<jsp:getProperty property="dateTime" name="date"/>
  			</div>
  			<div id="week">
  				<jsp:getProperty property="week" name="date"/>
  			</div>
  		</div>
  	</div>
  </body>
</html>

```
