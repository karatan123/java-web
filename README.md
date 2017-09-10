el_request

```
<%
    	String[] arr={"java","java web","jsp"};
    	request.setAttribute("book",arr);
     %>
     <%
     	String[] arr1=(String[])request.getAttribute("book");
     	for(int i=0;i<arr1.length;i++){
     		request.setAttribute("request1",i);
     		%>
     		${request1}:${book[request1] }<br> 
     	<%}%>
      
```


el_session
```
 <%
   	List<String> list=new ArrayList<String>();
   	list.add("叉骨");
   	list.add("烤冷面");
   	list.add("百香林");
   	session.setAttribute("goodlist",list);
    %>
    <%
    	List<String> list1=(List<String>)session.getAttribute("goodlist");
    	for(int i=0;i<list1.size();i++){
    	request.setAttribute("request1",i);
     %>
    	${request1 }:${goodlist[request1] }<br>
    <%} %>
```
######  el逻辑运算
**el进行逻辑运算时表达式值确定时停止执行，只执行一次逻辑运算**
```
<%
    	request.setAttribute("username","mr");
    	request.setAttribute("password","123456");
     %>
     username=${username }<br>
     password=${password }<br>
     \${username!=""and (username=="mr") }:
     ${username!=""and(username=="mr") }<br>
     \${password!=""and(password=="2345") }:
     ${password!=""and(password=="3445") }
```
