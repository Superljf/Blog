#### JavaWeb

![image-20200506152510992](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200506152510992.png)





![image-20200506152529008](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200506152529008.png)

![image-20200506152544964](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200506152544964.png)

![image-20200506152627341](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200506152627341.png)

#### 修改配置

![image-20200506153257480](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200506153257480.png)

#### 

![image-20200506153354785](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200506153354785.png)

![image-20200506154518681](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200506154518681.png)

### Servlet技术

- javaEE 规范之一   规范就是接口
- javaWeb三大组件之一
- 接收客户端的请求 并响应客户端的请求

#### 手动实现Servlet程序

- alt enter
- alt insert

![image-20200506160018532](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200506160018532.png)

![image-20200506161519397](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200506161519397.png)

- 生命周期

![image-20200506163528358](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200506163528358.png)

![image-20200506164301968](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200506164301968.png)

![image-20200506165511772](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200506165511772.png)

![image-20200506165732939](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200506165732939.png)

![image-20200506165912968](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200506165912968.png)

ServletContext类 

什么是域对象

可以和Map一样存取数据的对象

而在Java中，却是只有方法这一说，因为Java是纯粹的面向对象的编程语言

对于一个 Servlet 类，我们日常最常用的方法是继承自 HttpServlet 类，提供了 Http 相关的方法，HttpServlet 扩展了 GenericServlet 类，而 GenericServlet 类又实现了 Servlet 类和 ServletConfig 类。

```java
//Servlet的生命周期:从Servlet被创建到Servlet被销毁的过程
//一次创建，到处服务
//一个Servlet只会有一个对象，服务所有的请求
/*
 * 1.实例化（使用构造方法创建对象）
 * 2.初始化  执行init方法
 * 3.服务     执行service方法
 * 4.销毁    执行destroy方法
 */
public class ServletDemo1 implements Servlet {

    //public ServletDemo1(){}

     //生命周期方法:当Servlet第一次被创建对象时执行该方法,该方法在整个生命周期中只执行一次
    public void init(ServletConfig arg0) throws ServletException {
                System.out.println("=======init=========");
        }

    //生命周期方法:对客户端响应的方法,该方法会被执行多次，每次请求该servlet都会执行该方法
    public void service(ServletRequest arg0, ServletResponse arg1)
            throws ServletException, IOException {
        System.out.println("hehe");

    }

    //生命周期方法:当Servlet被销毁时执行该方法
    public void destroy() {
        System.out.println("******destroy**********");
    }
//当停止tomcat时也就销毁的servlet。
    public ServletConfig getServletConfig() {

        return null;
    }

    public String getServletInfo() {

        return null;
    }
}
```

Servlet 是服务 HTTP 请求并实现 **javax.servlet.Servlet** 接口的 Java 类

```java
 public void init() throws ServletException
  {
      // 执行必需的初始化
      message = "Hello World";
  }

  public void doGet(HttpServletRequest request,
                    HttpServletResponse response)
            throws ServletException, IOException
  {
      // 设置响应内容类型
      response.setContentType("text/html");

      // 实际的逻辑是在这里
      PrintWriter out = response.getWriter();
      out.println("<h1>" + message + "</h1>");
  }
  
  public void destroy()
  {
      // 什么也不做
  }
}
```

## GET 方法

GET 方法向页面请求发送已编码的用户信息。页面和已编码的信息中间用 ? 字符分隔，如下所示：

```
http://www.test.com/hello?key1=value1&key2=value2
```

GET 方法是默认的从浏览器向 Web 服务器传递信息的方法，它会产生一个很长的字符串，出现在浏览器的地址栏中。如果您要向服务器传递的是密码或其他的敏感信息，请不要使用 GET 方法。GET 方法有大小限制：请求字符串中最多只能有 1024 个字符。

这些信息使用 QUERY_STRING 头传递，并可以通过 QUERY_STRING 环境变量访问，Servlet 使用 **doGet()** 方法处理这种类型的请求。

## 使用 Servlet 读取表单数据

Servlet 处理表单数据，这些数据会根据不同的情况使用不同的方法自动解析：

- **getParameter()：**您可以调用 request.getParameter() 方法来获取表单参数的值。
- **getParameterValues()：**如果参数出现一次以上，则调用该方法，并返回多个值，例如复选框。
- **getParameterNames()：**如果您想要得到当前请求中的所有参数的完整列表，则调用该方法。

Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/SuperLjf/.ssh/id_rsa):
Created directory '/c/Users/SuperLjf/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/SuperLjf/.ssh/id_rsa.
Your public key has been saved in /c/Users/SuperLjf/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:KJrBZ55ChZXYlYt4C85P320MOpXPIbzEyaot/mk+oQs chenfengd@hobj.com
The key's randomart image is:

![image-20200507145823759](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200507145823759.png)