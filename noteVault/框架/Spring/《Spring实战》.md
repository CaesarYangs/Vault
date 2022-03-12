2
# 1st Round 笔记

[1.1 什么是Spring](https://potoyang.gitbook.io/spring-in-action-v5/di-1-zhang-spring-ru-men/1.1-shen-me-shi-spring)

任何不平凡的应用程序都由许多组件组成，每个组件负责自己的在整体应用程序中的那部分功能，并与其他应用程序元素协调以完成工作。在运行应用程序时，需要以某种方式创建这些组件并相互引用。

Spring 的核心是一个_容器_，通常称为 _Spring 应用程序上下文_，用于创建和管理应用程序组件。这些组件（或 bean）在 Spring 应用程序上下文中连接在一起以构成一个完整的应用程序

将 bean 连接在一起的行为是基于一种称为 _依赖注入_（DI）的模式。依赖项注入的应用程序不是由组件自身创建和维护它们依赖的其他 bean 的生命周期，而是依赖于单独的实体（容器）来创建和维护所有组件，并将这些组件注入需要它们的 bean。通常通过构造函数参数或属性访问器方法完成此操作。

注入：
从历史上看，引导 Spring 应用程序上下文将 bean 连接在一起的方式是使用一个或多个 XML 文件，这些文件描述了组件及其与其他组件的关系。
但是，在最新版本的 Spring 中，基于 Java 的配置更为常见。

与基于 XML 的配置相比，基于 Java 的配置具有多个优点，包括更高的类型安全性和改进的可重构性。即使这样，仅当 Spring 无法自动配置组件时，才需要使用 Java 或 XML 进行显式配置。

自动配置起源于 Spring 技术，即 _自动装配_ 和 _组件扫描_。借助组件扫描，Spring 可以自动从应用程序的类路径中发现组件，并将其创建为 Spring 应用程序上下文中的 bean。通过自动装配，Spring 会自动将组件与它们依赖的其他 bean 一起注入。

[1.2 检查Spring项目结构](https://potoyang.gitbook.io/spring-in-action-v5/di-1-zhang-spring-ru-men/1.2-chu-shi-hua-spring-ying-yong-cheng-xu/1.2.2-jian-cha-spring-xiang-mu-jie-gou)
```
你可能还会注意到，所有这三个依赖项的 artifact ID 中都有 _starter_ 这个词。Spring Boot starter 依赖项的特殊之处在于，它们本身通常没有任何库代码，而是间接地引入其他库。这些 starter 依赖提供了三个主要的好处：

-   构建的文件将会小得多，也更容易管理，因为不需要对每一个可能需要的库都声明一个依赖项。
    
-   可以根据它们提供的功能来考虑需要的依赖关系，而不是根据库名来考虑。如果正在开发一个 web 应用程序，那么将添加 web starter 依赖项，而不是一个编写 web 应用程序的各个库的清单。
    
-   不用担心 library 版本问题。可以相信的是，对于给定版本的 Spring Boot，可间接地引入的库的版本将是兼容的，只需要考虑使用的是哪个版本的 Spring Boot。
```

最后，构建规范以 Spring Boot 插件结束。这个插件执行一些重要的功能：

-   提供了一个 Maven 编译目标，让你能够使用 Maven 运行应用程序。这将在第 1.3.4 节中尝试实现这个目标。
-   确保所有的依赖库都包含在可执行的 JAR 文件中，并且在运行时类路径中可用。
-   在 JAR 文件中生成一个 manifest 文件，表示引导类（在本书例子中是 `TacoCloudApplication`）是可执行 JAR 的主类。

**引导应用程序**

因为将从一个可执行的 JAR 运行应用程序，所以在运行 JAR 文件时，有一个主类来执行是很重要的。还需要至少一个最小的 Spring 配置文件来引导应用程序。这就是将在 `TacoCloudApplication` 类中找到的内容，如下程序清单 1.2 所示。

```
package tacos;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class TacoCloudApplication {
    public static void main(String[] args) {
        SpringApplication.run(TacoCloudApplication.class, args);
    }
}
```

虽然 `TacoCloudApplication` 中只有很少的代码，但是其中包含了相当丰富的内容。最强大的代码行之一也是最短的代码行之一。`@SpringBootApplication` 注释清楚地表明这是一个 Spring 引导应用程序。但是 `@SpringBootApplication` 中有更多的东西。`@SpringBootApplication` 是一个组合了其他三个注释的复合应用程序：

-   `@SpringBootConfiguration` —— 指定这个类为配置类。尽管这个类中还没有太多配置，但是如果需要，可以将 Javabased Spring Framework 配置添加到这个类中。实际上，这个注释是`@Configuration` 注释的一种特殊形式。
    
-   `@EnableAutoConfiguration` —— 启用 Spring 自动配置。稍后我们将详细讨论自动配置。现在，要知道这个注释告诉 Spring Boot 自动配置它认为需要的任何组件。
    
-   `@ComponentScan` —— 启用组件扫描。这允许你声明其他带有 `@Component`、`@Controller`、`@Service` 等注释的类，以便让 Spring 自动发现它们并将它们注册为 Spring 应用程序上下文中的组件。


[1.3 编写Spring应用程序](https://potoyang.gitbook.io/spring-in-action-v5/di-1-zhang-spring-ru-men/1.3-bian-xie-spring-ying-yong-cheng-xu)
可以看到，这个类是用 `@Controller` 注释的。`@Controller` 本身并没有做多少事情。它的主要目的是将该类识别为组件扫描的组件。由于 `HomeController` 是用 `@Controller` 注释的，因此 Spring 的组件扫描会自动发现它，并在 Spring 应用程序上下文中创建一个 `HomeController` 实例作为 bean。

实际上，其他一些注释（包括 `@Component`、`@Service` 和 `@Repository`）的用途与 `@Controller` 类似。你可以用任何其他的注解来有效地注释 `HomeController`，它仍然可以工作。但是，选择 `@Controller` 更能描述该组件在应用程序中的角色。


Spring 附带了一个强大的 web 框架，称为 Spring MVC。Spring MVC 的核心是控制器的概念，这是一个处理请求并使用某种信息进行响应的类。对于面向浏览器的应用程序，控制器的响应方式是可选地填充模型数据并将请求传递给视图，以生成返回给浏览器的 HTML。

**自动重启应用程序**
更准确地说，当 DevTools 起作用时，应用程序被加载到 Java 虚拟机（JVM）中的两个单独的类加载器中。一个类装入器装入 Java 代码、属性文件以及项目的 src/main/path 中的几乎所有东西。这些项目可能会频繁更改。另一个类加载器加载了依赖库，它们不太可能经常更改。

当检测到更改时，DevTools 只重新加载包含项目代码的类加载器，并重新启动 Spring 应用程序上下文，但不影响其他类加载器和 JVM。尽管这一策略很微妙，但它可以略微减少启动应用程序所需的时间。

这种策略的缺点是对依赖项的更改在自动重新启动时不可用。这是因为类装入器包含依赖项库 不是自动重新加载。这意味着，每当在构建规范中添加、更改或删除依赖项时，都需要重新启动应用程序才能使这些更改生效。

这是使用 Spring 开发的一个重要好处。可以关注于满足应用程序需求的代码，而不是满足框架的需求。尽管确实需要不时地编写一些特定于框架的代码，但这通常只是代码库的一小部分。如前所述，Spring （通过 Spring Boot）可以被认为是 _无框架的框架_。

**Spring自动配置**
在 pom.xml 文件中，声明了对 Web 和 Thymeleaf 启动器的依赖。这两个依赖关系带来了一些其他的依赖关系，包括：

-   Spring MVC 框架
    
-   嵌入式 Tomcat
    
-   Thymeleaf 和 Thymeleaf 布局方言
    

它还带来了 Spring Boot 的自动配置库。当应用程序启动时，Spring Boot 自动配置自动检测这些库并自动执行：

-   在 Spring 应用程序上下文中配置 bean 以启用 Spring MVC
    
-   将嵌入式 Tomcat 服务器配置在 Spring 应用程序上下文中
    
-   为使用 Thymeleaf 模板呈现 Spring MV C视图，配置了一个 Thymeleaf 视图解析器
    

简而言之，自动配置完成了所有繁重的工作，让你专注于编写实现应用程序功能的代码。


---
# 2 开发Web应用程序
**Spring Web应用是在做什么：**
使用 Spring 构建的应用程序将执行各种操作，包括处理数据、从数据库中读取信息以及与其他应用程序进行交互。

**Spring MVC**
Model+View+Controller

在 Spring web 应用程序中，获取和处理数据是控制器的工作。
视图的工作是将数据渲染成 HTML 并显示在浏览器中。

应用程序的域是它所处理的主题领域 —— 影响应用程序理解的思想和概念。

@Slf4j
一个是 @Slf4j，它是 Lombok 提供的注释，在运行时将自动生成类中的 SLF4J（Java 的简单日志门面，[https://www.slf4j.org/](https://www.slf4j.org)）记录器。

@Data
在清单中看不到它们，部分原因是为了节省空间，但也因为使用了一个名为 Lombok 的出色库，它会在运行时自动生成这些方法。实际上，类级别的 `@Data` 注释是由 Lombok 提供的，它告诉 Lombok 生成所有缺少的方法，以及接受所有`final`属性作为参数的构造函数。通过使用 Lombok，可以让 `Ingredient` 的代码保持整洁。

## Controller
控制器是 Spring MVC 框架的主要参与者。它们的主要工作是处理 HTTP 请求，或者将请求传递给视图以呈现 HTML（浏览器显示），或者直接将数据写入响应体（RESTful）。

@Controller
此注释用于将该类标识为控制器并将其标记为组件扫描的候选对象，以便 Spring 将发现该类并在 Spring 应用程序上下文中自动创建 DesignTacoController 实例作为 bean。

@RequestMapping 
注释在类级应用时，指定该控制器处理的请求的类型。在本例中，它指定 DesignTacoController 将处理路径以 `/design` 开头的请求。

@GetMapping 与类级别的 @RequestMapping 配对使用，指定何时接收 `/design` 的 HTTP GET 请求，showDesignForm() 将用来处理请求。

**Spring MVC 请求映射**  ？后期需要详细查看

Model 是一个对象，它在控制器和负责呈现数据的视图之间传输数据。最后，放置在 Model 类属性中的数据被复制到 servlet 响应属性中，视图可以在其中找到它们。

视图控制器：一个只将请求转发给视图的控制器。
@Configuration

## Thymeleaf
控制器创建完成后，就该开始设计视图了。Spring 为定义视图提供了几个很好的选项，包括 JavaServer Pages（JSP）、Thymeleaf、FreeMarker、Mustache 和基于 Groovy 的模板。

像 Thymeleaf 这样的视图库被设计成与任何特定的 web 框架解耦。因此，他们不知道 Spring 的模型抽象，并且无法处理控制器放置在模型中的数据。但是它们可以处理 servlet 请求属性。因此，在 Spring 将请求提交给视图之前，它将模型数据复制到请求属性中，而 Thymeleaf 和其他视图模板选项可以随时访问这些属性。

Thymeleaf 模板只是 HTML 与一些额外的元素属性，指导模板在渲染请求数据。

例如，如果有一个请求属性，它的键是 “message”，你希望它被 Thymeleaf 渲染成一个 HTML `<p>` 标签，你可以在你的 Thymeleaf 模板中写以下内容：

```html
<p th:text="${message}">placeholder message</p>
```

当模板被呈现为 HTML 时，`<p>` 元素的主体将被 servlet 请求属性的值替换，其键值为 “message”。`th:text` 是一个 Thymeleaf 的命名空间属性，用于需要执行替换的地方。`${}` 操作符告诉它使用请求属性的值（在本例中为 “message”）。

如果在视图中查看 `<form>` 标签，可以看到它的 `method` 属性被设置为 POST。而且，`<form>` 没有声明 action 属性。这意味着在提交表单时，浏览器将收集表单中的所有数据，并通过 HTTP POST 请求将其发送到服务器，发送到显示表单的 GET 请求的同一路径 —— `/design` 路径。

## 声明验证规则
Spring 支持 Java's Bean Validation API（也称为 JSR-303；[https://jcp.org/en/jsr/detail?id=303](https://jcp.org/en/jsr/detail?id=303)）。这使得声明验证规则比在应用程序代码中显式地编写声明逻辑更容易。使用 Spring Boot，不需要做任何特殊的事情来将验证库添加到项目中，因为 Validation API 和 Validation API 的 Hibernate 实现作为Spring Boot web 启动程序的临时依赖项自动添加到了项目中。

---
# 3 处理数据
几十年来，关系数据库和 SQL 一直是数据持久化的首选。尽管近年来出现了许多替代数据库类型，但关系数据库仍然是通用数据存储的首选，而且不太可能很快被取代。

在处理关系数据时，Java 开发人员有多个选择。两个最常见的选择是 JDBC 和 JPA。Spring 通过抽象支持这两种方式，这使得使用 JDBC 或 JPA 比不使用 Spring 更容易。

---
