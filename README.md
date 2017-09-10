el1

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
