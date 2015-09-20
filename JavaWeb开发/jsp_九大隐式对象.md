##Jsp 九大隐式对象



1. page
2. config
3. application
4. response
5. request
6. session
7. out
8. exception
9. pageContext


--------------------

1) out 
    相当于response。getWriter得到PrintWriter
    
##不同点
    1.out和response.getWriter获取到的流不同在于out这个对象本身就是一个缓冲区。利用out写出来
    的内容，会先缓冲到out缓冲区内，直到out缓冲区充满了整个页面结束时out缓冲区内容才会被写出到
    response缓冲区中，最终可以带到浏览器展示。
    
    -----------------------------------------------------------------------------
    
    page指令中的
             [buffer="none | 8kb | sizekb" ]可以用来禁用out缓冲区或设置out缓冲区的大小,默认
             8kb  [ autoFlush="true | false"]用来设置当out缓冲区满了以后如果在写入数据时out
             如何处理,如果是true,则先将满了的数据写到response中后再接受新数据,如果是false,则满
             了再写入数据直接抛异常 在jsp页面中需要进行数据输出时,不要自己获取response.getWriter,             
             而是要使用out进行输出,防止即用out又用response.getWriter而 导致输出顺序错乱的问题
    



##关键字 pageContext

pageContext
            (1)可以作为入口对象获取其他八大隐式对象的引用
                getException方法返回exception隐式对象 
                getPage方法返回page隐式对象
                getRequest方法返回request隐式对象 
                getResponse方法返回response隐式对象 
                getServletConfig方法返回config隐式对象
                getServletContext方法返回application隐式对象
                getSession方法返回session隐式对象 
                getOut方法返回out隐式对象
            (2)域对象,四大作用域的入口,可以操作四大作用域中的域属性
                
                作用范围: 当前jsp页面
                生命周期: 当对jsp页面的访问开始时,创建代表当前jsp的PageContext,                当对当前jsp页面访问结束时销毁代表当前jsp的pageContext
                作用:在当前jsp中共享数据
                
                    public void setAttribute(java.lang.String name,java.lang.Object value)
                    public java.lang.Object getAttribute(java.lang.String name)
                    public void removeAttribute(java.lang.String name)

                    public void setAttribute(java.lang.String name, java.lang.Object value,int scope)
                    public java.lang.Object getAttribute(java.lang.String name,int scope)
                    public void removeAttribute(java.lang.String name,int scope)
                    
                    PageContext.APPLICATION_SCOPE
                    PageContext.SESSION_SCOPE
                    PageContext.REQUEST_SCOPE
                    PageContext.PAGE_SCOPE 

                    findAttribute方法 -- 搜寻四大作用域中的属性,如果找到则返回该值,如果四大
                   
                    作用域中都找不到则返回一个null,搜寻的顺序是从最小的域开始向最大的域开始寻找
                    
            (3)提供了请求转发和请求包含的快捷方法
                pageContext.include("/index.jsp");
  		        pageContext.forward("/index.jsp");
    






















