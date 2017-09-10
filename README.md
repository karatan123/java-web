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
