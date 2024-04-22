## 概念

- 服务器应用程序
- HTTP 请求响应处理
## 引入包

- servlet-api.jar
## Servlet 配置

- servlet 可以有多个 url-pattern
- servlet 可以有多个 servlet-mapping
- url-pattern 通配符
	- / - 匹配所有，不包含 jsp 文件
	- /\* - 匹配所有，包含 jsp 文件
	- /a/\* - 匹配前缀为 a 的路径
	- /\*\.a - 匹配后缀未 a 的路径
### web.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<webapp>
	<servlet>  
	    <servlet-name>UserServlet</servlet-name>  
	    <servlet-class>com.sf.lg.web.UserServlet</servlet-class>  
	</servlet>  
	<servlet-mapping>  
	    <servlet-name>UserServlet</servlet-name>  
	    <url-pattern>/user</url-pattern>  
	</servlet-mapping>
</webapp>
```
### 注解

```java
package com.sf.lg.web;

@WebServlet("/user")
class UserServlet extends HTTPServlet {
	@Override
	public void service() {}
}
```