# 史上最简单的 Spring MVC 教程（一）

## 1 简介

Spring MVC 属于 SpringFrameWork 的后续产品，已经融合在 Spring Web Flow 里面。Spring 框架提供了构建 Web 应用程序的全功能 MVC 模块，而 Spring MVC 就是其中最优秀的 MVC 框架。自从 Spring 2.5 版本发布后，由于支持注解配置，易用性得到了大幅度的提高；Spring 3.0 更加完善，实现了对 Struts 2 的超越。从现阶段来看，Spring MVC 是当前应用最多的 MVC 框架，而且在很多公司，通常会把 Spring MVC 和 Mybatis 整合起来使用。

## 2 框架原理

在 Spring MVC 框架中，从`Request（请求）`开始，依次进入`DispatcherServlet（核心分发器）` —> `HandlerMapping（处理器映射）` —> “Controller（控制器）” —> “ModelAndView（模型和视图）” —> “ViewResolver（视图解析器）” —> “View（视图）” —> “Response（响应）”结束，其中 DispatcherServlet、HandlerMapping 和 ViewResolver 只需要在 XML 文件中配置即可，从而大大提高了开发的效率，特别是对于 HandlerMapping，框架为其提供了默认的配置。Spring MVC 框架的结构图如下所示：








## 3 搭建 Spring MVC 框架







----------
———— ☆☆☆ —— [返回 -> 史上最简单的 Spring MVC 教程 <- 目录](https://github.com/guobinhit/springmvc-tutorial/blob/master/README.md) —— ☆☆☆ ————
