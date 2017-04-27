# 史上最简单的 Spring MVC 教程（一）

## 1 简介

Spring MVC 属于 SpringFrameWork 的后续产品，已经融合在 Spring Web Flow 里面。Spring 框架提供了构建 Web 应用程序的全功能 MVC 模块，而 Spring MVC 就是其中最优秀的 MVC 框架。自从 Spring 2.5 版本发布后，由于支持注解配置，易用性得到了大幅度的提高；Spring 3.0 更加完善，实现了对 Struts 2 的超越。从现阶段来看，Spring MVC 是当前应用最多的 MVC 框架，而且在很多公司，通常会把 Spring MVC 和 Mybatis 整合起来使用。

## 2 框架原理

在 Spring MVC 框架中，从 Request（请求）开始，依次进入 DispatcherServlet（核心分发器） —> HandlerMapping（处理器映射） —> Controller（控制器） —> ModelAndView（模型和视图） —> ViewResolver（视图解析器） —> View（视图） —> Response（响应）结束，其中 DispatcherServlet、HandlerMapping 和 ViewResolver 只需要在 XML 文件中配置即可，从而大大提高了开发的效率，特别是对于 HandlerMapping，框架为其提供了默认的配置。具体可以参考如下 Spring MVC 框架的请求处理示意图：

![Spring MVC 框架图](http://img.blog.csdn.net/20170207154527170)


## 3 搭建 Spring MVC 框架


首先，我们需要下载 Spring MVC 框架的各种依赖包，下载地址为「[Spring MVC 框架依赖包](http://download.csdn.net/detail/qq_35246620/9743975)」；然后，创建 Java Web 项目，项目名随意取，在这里，咱们就不妨取为`springmvc-demo`，构建项目结构图如下：

![1](http://img.blog.csdn.net/20170426175025237)

在这里，咱们需要向`External Libraries`中导入相应的 jar 包，具体添加 jar 包的方法可以参考「[详述 IntelliJ IDEA 之 添加 jar 包](http://blog.csdn.net/qq_35246620/article/details/54705071)」。至于需要导入的 jar 包，在咱们事先下载的「[Spring MVC 框架依赖包](http://download.csdn.net/detail/qq_35246620/9743975)」中都可以找到，下面附上需要导入的 jar 名称：

```
spring-aop-3.2.2.jar			          		AOP
spring-aspects-3.2.2.jar					AOP
spring-beans-3.2.2.jar						核心包
spring-context-3.2.2.jar					扩展包
spring-context-support-3.2.2.jar		          	对扩展包支持
spring-core-3.2.2.jar						核心包
spring-expression-3.2.2.jar	spring		          	表达式
spring-web-3.2.2.jar						web b/s
spring-webmvc-3.2.2.jar						springmvc

com.springsource.org.aopalliance-1.0.0.jar			AOP
com.springsource.org.apache.commons.logging-1.1.1.jar	        通用日志
```







----------
———— ☆☆☆ —— [返回 -> 史上最简单的 Spring MVC 教程 <- 目录](https://github.com/guobinhit/springmvc-tutorial/blob/master/README.md) —— ☆☆☆ ————
