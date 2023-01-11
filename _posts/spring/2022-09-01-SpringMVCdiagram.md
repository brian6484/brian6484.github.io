---
layout: post
title: How does Spring MVC work?
category: Spring
tags:
  - Spring

---

## MVC
<img src="/assets/images/posts/spring/mvc/mvcdiagram.png" title="제목" alt="아무거나" width="400"/>

1) DispatcherServlet receives client's request in the form of url.

2) DispatcherServlet dispatches the task of selecting an 
appropriate controller to HandlerMapping via the client request url.
HandlerMapping selects the controller which is mapped to the incoming request URL and returns the (selected Handler) and Controller to DispatcherServlet.

3) DispatcherServlet dispatches the task of executing logic 
of that controller to HandlerAdapter.

4) HandlerAdapter calls the business logic process of Controller.

5) Controller executes the business logic, *sets the 
processing result in Model* and returns the logical name of view to HandlerAdapter.

6) DispatcherServlet dispatches the task of resolving the 
View corresponding to the View name to ViewResolver. 
ViewResolver returns the View mapped to View name.

7) DispatcherServlet dispatches the rendering process to
 View.

8) View renders Model data and returns the Response to client


