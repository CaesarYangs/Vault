*Spring Boot 的核心配置文件有哪几个？它们的区别是什么？*
Spring Boot 的核心配置文件是 application 和 bootstrap 配置文件。

application 配置文件这个容易理解，主要用于 Spring Boot 项目的自动化配置。

bootstrap 配置文件有以下几个应用场景。

- 使用 Spring Cloud Config 配置中心时，这时需要在 bootstrap 配置文件中添加连接到配置中心的配置属性来加载外部配置中心的配置信息；
- 一些固定的不能被覆盖的属性；
- 一些加密/解密的场景；

*Spring Boot 的配置文件有哪几种格式？它们有什么区别？*
.properties 和 .yml，它们的区别主要是书写格式不同。

*Spring Boot 的核心注解是哪个？它主要由哪几个注解组成的？*
启动类上面的注解是@SpringBootApplication，它也是 Spring Boot 的核心注解，主要组合包含了以下 3 个注解：

@SpringBootConfiguration：组合了 @Configuration 注解，实现配置文件的功能。

@EnableAutoConfiguration：打开自动配置的功能，也可以关闭某个自动配置的选项，如关闭数据源自动配置功能： @SpringBootApplication(exclude = { DataSourceAutoConfiguration.class })。

@ComponentScan：Spring 组件扫描。

*开启 Spring Boot 特性有哪几种方式？*
1）继承 spring-boot-starter-parent 项目

2）导入 spring-boot-dependencies 项目依赖

*你如何理解 Spring Boot 中的 Starters？ 以及 Starters 的工作原理*
Starters 可以理解为启动器，它包含了一系列可以集成到应用里面的依赖包，你可以一站式集成 Spring 及其他技术，而不需要到处找示例代码和依赖包。如你想使用 Spring JPA 访问数据库，只要加入 spring-boot-starter-data-jpa 启动器依赖就能使用了。

- 我个人理解 SpringBoot 就是由各种 Starter 组合起来的，我们自己也可以开发 Starter
- 在 SpringBoot 启动时由@SpringBootApplication 注解会自动去 maven 中读取每个 starter 中的 spring.factories 文件,该文件里配置了所有需要被创建 spring 容器中的 bean，并且进行自动配置把 bean 注入 SpringContext 中 //（SpringContext 是 Spring 的配置文件）

作者：小杰要吃蛋
链接：https://juejin.cn/post/6844904125709156359
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

*你如何理解 Spring Boot 配置加载顺序？*
在 Spring Boot 里面，可以使用以下几种方式来加载配置。
1）properties 文件；
2）YAML 文件；
3）系统环境变量；
4）命令行参数；

*Spring Boot 有哪几种读取配置的方式？*
Spring Boot 可以通过 @PropertySource,@Value,@Environment, @ConfigurationProperties 来绑定变量，具体请看这篇文章《 [Spring Boot 读取配置的几种方式](https://link.segmentfault.com/?enc=LEutNWfAiaf4uc5ZnUhwww%3D%3D.UCJG7gRG9G8RuyNEOdHLUGwxh%2B58XpCYA0l%2FXpCqZu4CQwLADSRtN1TwhpU6kVazFAdfcF0hV%2BinZl4jC0A9pw%3D%3D) 》。

*SpringBoot事物的使用*
SpringBoot的事物很简单，首先使用注解EnableTransactionManagement开启事物之后，然后在Service方法上添加注解Transactional便可。

*Async异步调用方法*
在SpringBoot中使用异步调用是很简单的，只需要在方法上使用@Async注解即可实现方法的异步调用。
注意：需要在启动类加入@EnableAsync使异步调用@Async注解生效。

*什么是 JavaConfig？*
-   Spring JavaConfig 是 Spring 社区的产品，Spring 3.0引入了他，它提供了配置 Spring IOC 容器的纯Java 方法。因此它有助于避免使用 XML 配置。使用 JavaConfig 的优点在于：
    
    -   面向对象的配置。由于配置被定义为 JavaConfig 中的类，因此用户可以充分利用 Java 中的面向对象功能。一个配置类可以继承另一个，重写它的@Bean 方法等。
        
    -   减少或消除 XML 配置。基于依赖注入原则的外化配置的好处已被证明。但是，许多开发人员不希望在 XML 和 Java 之间来回切换。JavaConfig 为开发人员提供了一种纯 Java 方法来配置与 XML 配置概念相似的 Spring 容器。从技术角度来讲，只使用 JavaConfig 配置类来配置容器是可行的，但实际上很多人认为将JavaConfig 与 XML 混合匹配是理想的。
        
    -   类型安全和重构友好。JavaConfig 提供了一种类型安全的方法来配置 Spring容器。由于 Java 5.0 对泛型的支持，现在可以按类型而不是按名称检索 bean，不需要任何强制转换或基于字符串的查找。
        
-   常用的Java config：
    
    -   @Configuration：在类上打上写下此注解，表示这个类是配置类
    -   @ComponentScan：在配置类上添加 @ComponentScan 注解。该注解默认会扫描该类所在的包下所有的配置类，相当于之前的 <context:component-scan >。
    -   @Bean：bean的注入：相当于以前的< bean id="objectMapper" class="org.codehaus.jackson.map.ObjectMapper" />
    -   @EnableWebMvc：相当于xml的<mvc:annotation-driven >
    -   @ImportResource： 相当于xml的 < import resource="applicationContext-cache.xml">

*什么是 YAML？*
- YAML 是一种人类可读的数据序列化语言。它通常用于配置文件。与属性文件相比，如果我们想要在配置文件中添加复杂的属性，YAML 文件就更加结构化，而且更少混淆。可以看出 YAML 具有分层配置数据。
- 
YAML 现在可以算是非常流行的一种配置文件格式了，无论是前端还是后端，都可以见到 YAML 配置。那么 YAML 配置和传统的 properties 配置相比到底有哪些优势呢？

-   配置有序，在一些特殊的场景下，配置有序很关键
-   简洁明了，他还支持数组，数组中的元素可以是基本数据类型也可以是对象
-   相比 properties 配置文件，YAML 还有一个缺点，就是不支持 @PropertySource 注解导入自定义的 YAML 配置。
    
### Shiro 框架
-   **Authentication（认证）：**用户身份识别，通常被称为用户“登录”
-   **Authorization（授权）：**访问控制。比如某个用户是否具有某个操作的使用权限。
-   **Session Management（会话管理）：**特定于用户的会话管理,甚至在非web 或 EJB 应用程序。
-   **Cryptography（加密）：**在对数据源使用加密算法加密的同时，保证易于使用。

**Shiro 认证过程**
![](https://pic4.zhimg.com/80/v2-2531156d2e6fb3ec0702f1d1ed795f43_1440w.jpg)

1.  首先调用 Subject.login(token) 进行登录，其会自动委托给 Security Manager，调用之前必须通过 SecurityUtils.setSecurityManager() 设置；
2.  SecurityManager 负责真正的身份验证逻辑；它会委托给 Authenticator 进行身份验证；
3.  Authenticator 才是真正的身份验证者，Shiro API 中核心的身份认证入口点，此处可以自定义插入自己的实现；
4.  Authenticator 可能会委托给相应的 AuthenticationStrategy 进行多 Realm 身份验证，默认 ModularRealmAuthenticator 会调用 AuthenticationStrategy 进行多 Realm 身份验证；
5.  Authenticator 会把相应的 token 传入 Realm，从 Realm 获取身份验证信息，如果没有返回 / 抛出异常表示身份验证失败了。此处可以配置多个 Realm，将按照相应的顺序及策略进行访问。

**Shiro 授权过程**
![](https://pic1.zhimg.com/80/v2-66b6458df10fd05db4aea732b0199080_1440w.jpg)

**自定义 Realm**
从上面我们了解到实际进行权限信息验证的是我们的 Realm，Shiro 框架内部默认提供了两种实现，一种是查询`.ini`文件的`IniRealm`，另一种是查询数据库的`JdbcRealm`，这两种来说都相对简单，感兴趣的可以去[【这里】](https://link.zhihu.com/?target=http%3A//how2j.cn/k/shiro/shiro-tutorial/1720.html%23nowhere)瞄两眼，我们着重就来介绍介绍自定义实现的 Realm 吧。

有了上面的对认证和授权的理解，我们先在合适的包下创建一个【MyRealm】类，继承 Shirot 框架的 AuthorizingRealm 类，并实现默认的两个方法：
