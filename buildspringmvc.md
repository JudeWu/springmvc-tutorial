# 史上最简单的 Spring MVC 教程（一）

## 1 简介

Spring MVC 属于 SpringFrameWork 的后续产品，已经融合在 Spring Web Flow 里面。Spring 框架提供了构建 Web 应用程序的全功能 MVC 模块，而 Spring MVC 就是其中最优秀的 MVC 框架。自从 Spring 2.5 版本发布后，由于支持注解配置，易用性得到了大幅度的提高；Spring 3.0 更加完善，实现了对 Struts 2 的超越。从现阶段来看，Spring MVC 是当前应用最多的 MVC 框架，而且在很多公司，通常会把 Spring MVC 和 Mybatis 整合起来使用。

## 2 框架原理

在 Spring MVC 框架中，从 Request（请求）开始，依次进入 DispatcherServlet（核心分发器） —> HandlerMapping（处理器映射） —> Controller（控制器） —> ModelAndView（模型和视图） —> ViewResolver（视图解析器） —> View（视图） —> Response（响应）结束，其中 DispatcherServlet、HandlerMapping 和 ViewResolver 只需要在 XML 文件中配置即可，从而大大提高了开发的效率，特别是对于 HandlerMapping，框架为其提供了默认的配置。具体可以参考如下 Spring MVC 框架的请求处理示意图：

![Spring MVC 框架图](http://img.blog.csdn.net/20170207154527170)


## 3 搭建 Spring MVC 框架


首先，我们需要下载 Spring MVC 框架的各种依赖包，下载地址为「[Spring MVC 框架依赖包](http://download.csdn.net/detail/qq_35246620/9743975)」；然后，创建 Java Web 项目，项目名随意取，在这里，咱们就不妨取为`springmvc-demo`，构建项目结构图如下：

![1](http://img.blog.csdn.net/20170426175025237)

在这里，咱们需要向`External Libraries`中导入相应的 jar 包，具体添加 jar 包的方法可以参考「[详述 IntelliJ IDEA 之 添加 jar 包](http://blog.csdn.net/qq_35246620/article/details/54705071)」。至于需要导入的 jar 包，在咱们事先下载的「[Spring MVC 框架依赖包](http://download.csdn.net/detail/qq_35246620/9743975)」中都可以找到，下面附上需要导入的 jar 包名称：

```
spring-aop-3.2.2.jar			          		AOP
spring-aspects-3.2.2.jar					AOP
spring-beans-3.2.2.jar						核心包
spring-context-3.2.2.jar					扩展包
spring-context-support-3.2.2.jar		          	对扩展包支持
spring-core-3.2.2.jar						核心包
spring-expression-3.2.2.jar	                                spring 表达式
spring-web-3.2.2.jar						web b/s
spring-webmvc-3.2.2.jar						springmvc

com.springsource.org.aopalliance-1.0.0.jar			AOP
com.springsource.org.apache.commons.logging-1.1.1.jar	        通用日志
```

接下来，依次**建立控制器`TestController`**（即Java类）：

```
package com.hit.controller;

import org.springframework.web.servlet.ModelAndView;
import org.springframework.web.servlet.mvc.AbstractController;

/**
 * Created by 维C果糖 on 2017/4/22.
 */

public class TestController extends AbstractController {
    @Override
    protected ModelAndView handleRequestInternal(javax.servlet.http.HttpServletRequest request,
                                                 javax.servlet.http.HttpServletResponse response) throws Exception {

        System.out.println(request.getRequestURI());  // 获取Controller的名称，即地址

        return new ModelAndView("index");  // 逻辑名
    }
}

```
**配置`web.xml`文件**，主要是配置 DispatcherServlet，即核心分发器：
```
<?xml version="1.0" encoding="UTF-8"?>
<web-app version="2.5" xmlns="http://java.sun.com/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
	http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd">

    <!-- 配置 DispatcherServlet，对所有后缀为action的url进行过滤 -->
    <servlet>
        <servlet-name>action</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>action</servlet-name>
        <url-pattern>*.action</url-pattern>
    </servlet-mapping>
</web-app>
```

**编辑`index.jsp`页面**，用于显示结果，在这里最好将此 JSP 页面复制到 pages 目录一份，至于原因嘛，则是尽量将页面都统一放在一个目录之中：

```
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
	<head>
	    <title>Spring MVC</title>
	</head>
<body>
	This is my Spring MVC!
</body>
</html>
```
**建立`action-servlet.xml`配置文件**，主要是声明 Controller 和配置 ViewResolver，即控制器和视图解析器：

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                        http://www.springframework.org/schema/beans/spring-beans-3.2.xsd">

    <!-- 声明 Controller -->
    <bean name="/home.action" class="com.hit.controller.TestController" />

    <!-- 内部资源视图解析器，前缀 + 逻辑名 + 后缀 -->
    <bean id="internalResourceViewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/pages/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
</beans>
```

当咱们完成以上步骤之后，咱们就已经初步搭建了 Spring MVC 框架。接下来，再配置一下 web 服务器就可以进行测试啦！在这里，咱们使用的 web 服务器是 Tomcat，配置完的结果如下图所示：

![Tomcat](http://img.blog.csdn.net/20170427093943562)

 - 标注1：自定义 Tomcat 名称，可以随意取名；
 - 标注2：使用的 Tomcat 版本，点击`Configure`进行设置；
 - 标注3：为 web 服务器选择默认的浏览器；
 - 标注4：服务器访问路径；
 - 标注5：设置虚拟机参数；
 - 标注6：项目运行环境，即 JRE；
 - 标注7：端口号；
 - 标注8：部署 Tomcat 服务器。

如上图所示，点击 **标注8** 所示的`Deployment`，进入后进行如下配置：

![dey](http://img.blog.csdn.net/20170427100653590)

至此，Spring MVC 框架搭建成功，运行程序后，将在 Chrome 浏览器显示如下内容：

![jsp](http://img.blog.csdn.net/20170427101024504)


----------

**温馨提示**：在此项目中，由于使用 IDE 工具为 IntelliJ IDEA ，因此不用咱们自己建立`lib`包，直接将`jar`包导入`External Libraries`中即可。 



----------
———— ☆☆☆ —— [返回 -> 史上最简单的 Spring MVC 教程 <- 目录](https://github.com/guobinhit/springmvc-tutorial/blob/master/README.md) —— ☆☆☆ ————
