# java security
## 信息泄露问题
### 现象
如没有及时删除开发人员使用的调试页面等情况，攻击者有掌握更多信息的可能，从而发起有效攻击
### 解决方案
对于浏览器一个目录或文件的服务器重定向到自定义的404错误页面，或者删除敏感信息。
加个404页面
web.mxl

```xml
  <error-page>
    <error-code>404</error-code>
    <location>/error/404.html</location>
  </error-page>
```

## xss攻击
### 现象
恶意攻击者往Web页面里插入恶意的Script代码，当用户浏览该页之时，嵌入其中Web里面的Script代码会被执行，从而达到恶意攻击用户的目的。
### 解决方案
XSSFilter.java
XSSRequestWrapper.java

## 跨站点伪造请求（CSRF）
### 现象
别人可以通过form表单等一系列方式，伪造某一站点的请求，将数据跨站点提交

### 解决方案
1. 使用POST代替GET
2. 检查并验证HTTP Referer字段
3. 使用Token验证。

#### 检查并验证HTTP Referer字段
1. referer校验：

```java
  // 从 HTTP 头中取得 Referer 值
  String referer = ((HttpServletRequest) servletRequest).getHeader("Referer");
```

2. 校验自己的referer是不是自己想要的


3. web.xml配置filter

```xml
	<!--验证 Referer-->
	<filter>
		<filter-name>refererFilter</filter-name>
		<filter-class>***.RefererFilter</filter-class>
	</filter>
	<filter-mapping>
		<filter-name>refererFilter</filter-name>
    <url-pattern>/*</url-pattern>
    <dispatcher>REQUEST</dispatcher>
	</filter-mapping>
	
```

## 疑难杂症
### maven使用jre的jar包

```xml
					<compilerArgs> 
						<arg>-verbose</arg>
						<arg>-Xlint:unchecked</arg>
			      <arg>-Xlint:deprecation</arg>
			            <!--<arg>-bootclasspath</arg>
			            <arg>${env.JAVA_HOME}/jre/lib/rt.jar</arg>
						<arg>${env.JAVA_HOME}/jre/lib/jce.jar</arg>-->
						<arg>-extdirs</arg> 
	          <arg>${project.basedir}/WebContent/WEB-INF/lib</arg>
					</compilerArgs>
```