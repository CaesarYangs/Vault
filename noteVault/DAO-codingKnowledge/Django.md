# 1、什么是wsgi？

WSGI是Python在处理HTTP请求时，规定的一种处理方式。如一个HTTP Request过来了，那么就有一个相应的处理函数来进行处理和返回结果。WSGI就是规定这个处理函数的参数长啥样的，它的返回结果是长啥样的？至于该处理函数的名子和处理逻辑是啥样的，那无所谓。简单而言，WSGI就是规定了处理函数的输入和输出格式。

# 2、django请求的生命周期？

-   . 当用户在浏览器中输入url时,浏览器会生成请求头和请求体发给服务端  
    请求头和请求体中会包含浏览器的动作(action),这个动作通常为get或者post,体现在url之中.
-   . url经过Django中的wsgi,再经过Django的中间件,最后url到过路由映射表,在路由中一条一条进行匹配,  
    一旦其中一条匹配成功就执行对应的视图函数,后面的路由就不再继续匹配了.
-   . 视图函数根据客户端的请求查询相应的数据.返回给Django,然后Django把客户端想要的数据做为一个字符串返回给客户端.
-   . 客户端浏览器接收到返回的数据,经过渲染后显示给用户.

# 3、列举django的内置组件？

-   .Admin是对model中对应的数据表进行增删改查提供的组件
-   .model组件：负责操作数据库
-   .form组件：1.生成HTML代码2.数据有效性校验3校验信息返回并展示
-   .ModelForm组件即用于数据库操作,也可用于用户请求的验证


# 4、列举django中间件的5个方法？以及django中间件的应用场景？

-   .process_request : 请求进来时,权限认证
-   .process_view : 路由匹配之后,能够得到视图函数
-   .process_exception : 异常时执行
-   .process_template_responseprocess : 模板渲染时执行
-   .process_response : 请求有响应时执行

# 13、cookie和session的区别：

-   .cookie:  
    cookie是保存在浏览器端的键值对,可以用来做用户认证
-   .session：  
    将用户的会话信息保存在服务端,key值是随机产生的字符串,value值是session的内容  
    依赖于cookie将每个用户的随机字符串保存到用户浏览器上
-   Django中session默认保存在数据库中：django_session表
-   flask,session默认将加密的数据写在用户的cookie中

# 18、django中csrf的实现机制

-   第一步：django第一次响应来自某个客户端的请求时,后端随机产生一个token值，把这个token保存在SESSION状态中;同时,后端把这个token放到cookie中交给前端页面；
-   第二步：下次前端需要发起请求（比如发帖）的时候把这个token值加入到请求数据或者头信息中,一起传给后端；Cookies:{csrftoken:xxxxx}
-   第三步：后端校验前端请求带过来的token和SESSION里的token是否一致。

# 20、Django本身提供了runserver，为什么不能用来部署？(runserver与uWSGI的区别)

-   1.runserver方法是调试 Django 时经常用到的运行方式，它使用Django自带的  
    WSGI Server 运行，主要在测试和开发中使用，并且 runserver 开启的方式也是单进程 。
-   2.uWSGI是一个Web服务器，它实现了WSGI协议、uwsgi、http 等协议。注意uwsgi是一种通信协议，而uWSGI是实现uwsgi协议和WSGI协议的 Web 服务器。uWSGI具有超快的性能、低内存占用和多app管理等优点，并且搭配着Nginx就是一个生产环境了，能够将用户访问请求与应用 app 隔离开，实现真正的部署 。相比来讲，支持的并发量更高，方便管理多进程，发挥多核的优势，提升性能。


# 21、Django如何实现websocket？

-   django实现websocket官方推荐大家使用channels。channels通过升级http协议 升级到websocket协议。保证实时通讯。也就是说，我们完全可以用channels实现我们的即时通讯。而不是使用长轮询和计时器方式来保证伪实时通讯。他通过改造django框架，使django既支持http协议又支持websocket协议。

### 07.什么是WSGI？（初级）

WSGI(Web Server Gateway Interface，即Web服务器网关接口)是Python定义的Web服务器和Web应用程序或框架之间的一种简单而通用的接口。

它是Python为了解决Web服务器端与客户端之间的通信问题而产生的，它基于现存的CGI标准而设计。

其定义了Web服务器如何与Python应用程序进行交互，让Python写的Web应用程序可以和Web服务器对接起来。

---

### 08.uwsgi、uWSGI和WSGI的区别？（中级）

-   uwsgi：是uWSGI服务器实现的独有协议，用于Nginx服务与uWSGI服务的通信规范
    
-   uWSGI：是一个Web服务器，它实现了WSGI/uwsgi/HTTP等协议，用于接收Nginx转发的动态请求，处理后发个python应用程序
    
-   WSGI：用在python web框架（Django/Flask）编写的应用程序与web服务器之间的规范

### 09.Django的HttpRequest对象是在什么时候创建的？（中级）

class WSGIHandler(base.BaseHandler):
request = self.request_class(environ)

-   1.
-   2.

请求走到WSGIHandler类的时候，执行cell方法，将environ封装成了request。

### 11.列举django中间件的5个方法，以及django中间件的应用场景（初级）

process_request : 请求进来时,权限认证

process_view : 路由匹配之后,能够得到视图函数

process_exception : 异常时执行

process_template_responseprocess : 模板渲染时执行

process_response : 请求有响应时执行

### 12.简述Django对http请求的执行流程（初级）

在接受一个Http请求之前的准备,需启动一个支持WSGI网关协议的服务器监听端口等待外界的Http请求，比如Django自带的开发者服务器或者uWSGI服务器。

Django服务器根据WSGI协议指定相应的Handler来处理Http请求。

此时服务器已处于监听状态，可以接受外界的Http请求,当一个http请求到达服务器的时候,Django服务器根据WSGI协议从Http请求中提取出必要的参数组成一个字典（environ）并传入Handler中进行处理。

在Handler中对已经符合WSGI协议标准规定的http请求进行分析，比如加载Django提供的中间件，路由分配，调用路由匹配的视图等。

最后返回一个可以被浏览器解析的符合Http协议的HttpResponse。


### web框架的本质是什么？（初级）

web框架本质是一个socket服务端，用户的浏览器是一个socket客户端。

### 18.谈谈你对restful规范的认识（初级）

restful是一种软件架构设计风格，并不是标准，它只是提供了一组设计原则和约束条件，主要用于客户端和服务器交互类的软件。

就像设计模式一样，并不是一定要遵循这些原则，而是基于这个风格设计的软件可以更简洁，更有层次，我们可以根据开发的实际情况，做相应的改变。

它里面提到了一些规范，例如

1.restful 提倡面向资源编程,在url接口中尽量要使用名词，不要使用动词

2.在url接口中推荐使用Https协议，让网络接口更加安全

3.可以根据Http不同的method，进行不同的资源操作

4.在url中可以体现版本号

5.url中可以体现是否是API接口

6.url中可以添加条件去筛选匹配

7.响应式应该设置状态码

8.有返回值，而且格式为统一的json格式

9.返回错误信息

10.返回结果中要提供帮助链接，即API最好做到Hypermedia

