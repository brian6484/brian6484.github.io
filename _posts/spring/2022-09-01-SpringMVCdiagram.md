---
layout: post
title: How does Spring MVC work?
category: Spring
tags:
  - Spring

---

## MVC
MVC pattern focuses on separating each layer's function.

Model manages data and business logic (DAO, DTO, Service)

View handles the result of business logic and displays User Interface.
Display can be html, jsp, Thymeleaf, etc or if the server is
in REST API, JSON response

Controller takes care of client's request and connects Model
with View. Model and View are not connected by themselves btw.

<img src="/assets/images/posts/spring/mvc/mvcdiagram.png" title="제목" alt="아무거나" width="400"/>

DispatcherServlet: is in charge of whole MVC 처리과정 from
client request to server response

HandlerMapping: decides which controller will take care of
this incoming client request

HandlerAdapter: calls the appropriate method using handler
info decided by *HandlerMapping*

ViewResolver: Generates View according to Controller's
처리 결과 (data)

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

## Servlet
Following servlet's implementation rules in taking care of 
client request and outputting response is one of Java's web 
programming tech.

It is used in Controller in MVC.

> Servlet - a technique to use Java to make web

