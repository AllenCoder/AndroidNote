##Jsp 的映射
1. Jsp 的映射

```java

	<servlet>
        <servlet-name>index</servlet-name>
        <jsp-file>/index.jsp</jsp-file>
    </servlet>
    <servlet-mapping>
        <servlet-name>index</servlet-name>
        <url-pattern>/jsp/*</url-pattern>
    </servlet-mapping>
    
```
2. Jsp最佳实践

	*** 
	不管是jsp还是Servlet,虽然都可以开发动态Web资源，但是这两门
	技术的各自特点，在长期的软件实践中，人们逐渐的把servlet作为
	web应用中的控制器组件来使用，而把JSP技术作为数据显示的模板来
	使用。
	
3. 原因：

	* 让jsp既用java代码产生动态数据，又做美化会导致页面难以维护。
	* 让Servlet既产生数据，又在里面嵌套HTML代码美化数据，同样
也会导致程序的可读性插，难以维护。
	* 因此最好的方法是根据这两门的技术的特点，让他们各自负责各的
Servlet只负责响应请求产生数据，并把数据通过转发技术带给jsp,数
聚的显示的jsp来做。