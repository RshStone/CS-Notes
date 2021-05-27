## Spring Framework Overview

What We Mean by "Spring":

- easy to create Java EE applications

- support for Groovy and Kotlin

-  supports a wide range of application scenarios

- open source. It has a large and active community 

- is divided into modules. Applications can choose which modules they need.

  Spring框架分为几个模块。应用程序可以选择他们需要的模块。核心是核心容器的模块，包括配置模型和依赖注入机制。除此之外，Spring框架还为不同的应用程序体系结构提供了基础支持，包括消息传递、事务数据和持久性以及web服务。它还包括基于Servlet的springmvcweb框架和springwebflux反应式web框架。

- Spring’s framework jars allow for deployment to JDK 9’s module path ("Jigsaw").

History of Spring and the Spring Framework

- came into being in 2003 as a response to the complexity of the early [J2EE](https://en.wikipedia.org/wiki/Java_Platform,_Enterprise_Edition) specifications
- Spring is, in fact, complementary to Java EE
  - Servlet API ([JSR 340](https://jcp.org/en/jsr/detail?id=340))
  - WebSocket API ([JSR 356](https://www.jcp.org/en/jsr/detail?id=356))
  - Concurrency Utilities ([JSR 236](https://www.jcp.org/en/jsr/detail?id=236))
  - JSON Binding API ([JSR 367](https://jcp.org/en/jsr/detail?id=367))
  - Bean Validation ([JSR 303](https://jcp.org/en/jsr/detail?id=303))
  - JPA ([JSR 338](https://jcp.org/en/jsr/detail?id=338))
  - JMS ([JSR 914](https://jcp.org/en/jsr/detail?id=914))

- supports the Dependency Injection ([JSR 330](https://www.jcp.org/en/jsr/detail?id=330)) and Common Annotations ([JSR 250](https://jcp.org/en/jsr/detail?id=250)) specifications,

- Spring Framework 5.0, Spring requires the Java EE 7 level (e.g. Servlet 3.1+, JPA 2.1+) as a minimum

  at the same time providing out-of-the-box integration with newer APIs at the Java EE 8 level (e.g. Servlet 4.0, JSON Binding API) when encountered at runtime

  keeps Spring fully compatible with e.g. Tomcat 8 and 9, WebSphere 9, and JBoss EAP 7.

- with the help of Spring Boot, applications are created in a devops- and cloud-friendly way, with the Servlet container embedded and trivial to change. As of Spring Framework 5, a WebFlux application does not even use the Servlet API directly and can run on servers (such as Netty) that are not Servlet containers.

- Spring continues to innovate and to evolve. Beyond the Spring Framework, there are other projects, such as Spring Boot, Spring Security, Spring Data, Spring Cloud, Spring Batch, among others. It’s important to remember that each project has its own source code repository, issue tracker, and release cadence. See [spring.io/projects](https://spring.io/projects) for the complete list of Spring projects.

Design Philosophy

- Provide choice at every level --> switch persistence providers through configuration without changing your code
- Accommodate diverse perspectives --> supports a wide range of application needs with different perspectives
- Maintain strong backward compatibility.
- Care about API design
- Set high standards for code quality

Feedback and Contributions

- use the [GitHub Issues](https://github.com/spring-projects/spring-framework/issues).
-  Stack Overflow. Click [here](https://stackoverflow.com/questions/tagged/spring+or+spring-mvc+or+spring-aop+or+spring-jdbc+or+spring-r2dbc+or+spring-transactions+or+spring-annotations+or+spring-jms+or+spring-el+or+spring-test+or+spring+or+spring-remoting+or+spring-orm+or+spring-jmx+or+spring-cache+or+spring-webflux+or+spring-rsocket?tab=Newest) 

## Core Technologies

1. ### The loC Container

   - covers all the technologies that are absolutely integral to the Spring Framework.
   -  Spring Framework’s Inversion of Control (IoC) container
   - Spring’s Aspect-Oriented Programming (AOP) technologies. 
   - Coverage of Spring’s integration with AspectJ  is also provided

   1.1. Introduction to the Spring IoC(Inversion of Control ) Container and Beans

   - also known as dependency injection (DI).

   - 它是这样一个过程：对象仅通过构造函数参数、工厂方法的参数或在对象实例构造或从工厂方法返回后在对象实例上设置的属性来定义它们的依赖关系（即它们使用的其他对象）。然后容器在创建bean时注入这些依赖项。这个过程基本上是bean本身的逆过程（因此称为控制反转），通过使用类的直接构造或服务定位器模式等机制来控制其依赖项的实例化或位置

   - The `org.springframework.beans` and `org.springframework.context` packages are the basis for Spring Framework’s IoC container. The [`BeanFactory`](https://docs.spring.io/spring-framework/docs/5.3.7/javadoc-api/org/springframework/beans/factory/BeanFactory.html) interface provides an advanced configuration mechanism capable of managing any type of object. [`ApplicationContext`](https://docs.spring.io/spring-framework/docs/5.3.7/javadoc-api/org/springframework/context/ApplicationContext.html) is a sub-interface of `BeanFactory`.

   - In short, the `BeanFactory` provides the configuration framework and basic functionality, and the `ApplicationContext` adds more enterprise-specific functionality. 

     For more information on using the `BeanFactory` instead of the `ApplicationContext,` see [The `BeanFactory`](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-beanfactory).

   -  beans: form the backbone of your application,  are instantiated, assembled, and managed by a Spring IoC container

   1.2 Container Overview

   i. `org.springframework.context.ApplicationContext` interface represents the Spring IoC container and is responsible for instantiating, configuring, and assembling the beans.
   
   ii. The container gets its instructions on what objects to instantiate, configure, and assemble by reading configuration metadata.

   iii. The configuration metadata is represented in XML, Java annotations, or Java code.

   iv. create an instance of [`ClassPathXmlApplicationContext`](https://docs.spring.io/spring-framework/docs/5.3.7/javadoc-api/org/springframework/context/support/ClassPathXmlApplicationContext.html) or [FileSystemXmlApplicationContext](https://docs.spring.io/spring-framework/docs/5.3.7/javadoc-api/org/springframework/context/support/FileSystemXmlApplicationContext.html)

   ![002](https://raw.githubusercontent.com/RshStone/CS-Notes/master/Notes/Spring/002.png)

   

   

   - Configuration Metadata

     i. traditionally supplied in a simple and intuitive XML format

     这些bean定义对应于构成应用程序的实际对象。通常，您定义服务层对象、数据访问对象（dao）、表示对象（如Struts操作实例）、基础结构对象（如Hibernate SessionFactories）、JMS队列等。通常，不在容器中配置细粒度域对象，因为创建和加载域对象通常是dao和业务逻辑的责任。但是，您可以使用Spring与AspectJ的集成来配置在IoC容器控制之外创建的对象。请参见使用AspectJ使用Spring注入依赖域对象。
   
     ```xml
     <?xml version="1.0" encoding="UTF-8"?>
     <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
             https://www.springframework.org/schema/beans/spring-beans.xsd">
     
         <bean id="..." class="...">  
             <!-- collaborators and configuration for this bean go here -->
         </bean>
     
         <bean id="..." class="...">
             <!-- collaborators and configuration for this bean go here -->
         </bean>
     
         <!-- more bean definitions go here -->
     
     </beans>
     ```
   
     ii. [Annotation-based configuration](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-annotation-config)
   
     iii. [Java-based configuration](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-java)
   
   - Instantiating a Container
   
     resource strings that let the container load configuration metadata from a variety of external resources, such as the local file system, the Java `CLASSPATH`, and so on.
   
     `ApplicationContext context = new ClassPathXmlApplicationContext("services.xml", "daos.xml");`
   
     `val context = ClassPathXmlApplicationContext("services.xml", "daos.xml")`
   
     #####  Composing XML-based Configuration Metadata
   
     ```xml
     <beans>
         <import resource="services.xml"/>
         <import resource="resources/messageSource.xml"/>
         <import resource="/resources/themeSource.xml"/>
     
         <bean id="bean1" class="..."/>
         <bean id="bean2" class="..."/>
     </beans>
     ```
   
     It is generally preferable to keep an indirection for such absolute locations [classpath:/config/services.xml] — for example, through "${…}" placeholders that are resolved against JVM system properties at runtime.
   
     ##### The Groovy Bean Definition DSL(Don't really understand)
   
     ```java
     beans {
         dataSource(BasicDataSource) {
             driverClassName = "org.hsqldb.jdbcDriver"
             url = "jdbc:hsqldb:mem:grailsDB"
             username = "sa"
             password = ""
             settings = [mynew:"setting"]
         }
         sessionFactory(SessionFactory) {
             dataSource = dataSource
         }
         myService(MyService) {
             nestedBean = { AnotherBean bean ->
                 dataSource = dataSource
             }
         }
     }
     ```
   
     
   
   - Using the Container
   
     Four ways to use the container (don't really understand with code)
   
      The `ApplicationContext` lets you read bean definitions and access them, as the following example shows
   
      The following example shows Groovy configuration:
   
     `GenericApplicationContext` in combination with reader delegates — for example, with `XmlBeanDefinitionReader` for XML files
   
     `GroovyBeanDefinitionReader` for Groovy files
   
   1.3 Bean Overview
   
   ​	Naming Beans
   
   ​	Instantiating Beans
   
   1.4 Dependencies
   
   1.5 Bean Scopes
   
   1.6 Customizing the Nature of a Bean
   
   1.7 Bean Definition Inheritance
   
   1.8 Container Extension Points
   
   1.9Annotation-based Container Configuration
   
   

## Building REST 

(Representational State Transfer)services with Spring（广泛应用在微服务领域）

- REST

  [表现层状态转换 - 维基百科，自由的百科全书 (wikipedia.org)](https://zh.wikipedia.org/wiki/表现层状态转换)

  

  表现层状态转换是根基于[超文本传输协议（HTTP）](https://zh.wikipedia.org/wiki/超文本传输协议)之上而确定的一组约束和属性，是一种设计提供万维网络服务的[软件构建风格](https://zh.wikipedia.org/wiki/軟件架構)。符合或兼容于这种架构风格（简称为 REST 或 RESTful）的网络服务，允许客户端发出以[统一资源标识符](https://zh.wikipedia.org/wiki/统一资源标志符)访问和操作网络资源的请求，而与预先定义好的无状态操作集一致化。因此表现层状态转换提供了在互联网络的计算系统之间，彼此资源可交互使用的协作性质（interoperability）。相对于其它种类的网络服务，例如SOAP服务，则是以本身所定义的操作集，来访问网络上的资源。

  

  目前在三种主流的[Web服务](https://zh.wikipedia.org/wiki/Web服务)实现方案中，因为REST模式与复杂的[SOAP](https://zh.wikipedia.org/wiki/SOAP)和[XML-RPC](https://zh.wikipedia.org/wiki/XML-RPC)相比更加简洁，越来越多的Web服务开始采用REST风格设计和实现。例如，[Amazon.com](https://zh.wikipedia.org/wiki/Amazon.com)提供接近REST风格的Web服务运行图书查询；[雅虎](https://zh.wikipedia.org/wiki/雅虎)提供的Web服务也是REST风格的。

  

  REST是设计风格而**不是**标准。REST通常基于[HTTP](https://zh.wikipedia.org/wiki/HTTP)、[URI](https://zh.wikipedia.org/wiki/URI)、[XML](https://zh.wikipedia.org/wiki/XML)以及[HTML](https://zh.wikipedia.org/wiki/HTML)这些现有的广泛流行的协议和标准。

  - 资源是由URI来指定。
  - 对资源的操作包括获取、创建、修改和删除，这些操作正好对应HTTP协议提供的GET、POST、PUT和DELETE方法。
  - 通过操作资源的表现形式来操作资源。
  - 资源的表现形式则是XML或者HTML，取决于读者是机器还是人、是消费Web服务的客户软件还是Web浏览器。当然也可以是任何其他的格式，例如JSON。

- 微服务

  **微服务**（英语：Microservices）是一种[软件架构风格](https://zh.wikipedia.org/wiki/软件架构)，它是以专注于单一责任与功能的小型功能区块 (Small Building Blocks) 为基础，利用模块化的方式组合出复杂的大型应用程序，各功能区块使用与语言无关 (Language-Independent/Language agnostic）的[API](https://zh.wikipedia.org/wiki/应用程序接口)集相互通信。

- aim

  use the Spring portfolio to build a RESTful service while leveraging the stackless features of REST.

- REST: the de-facto standard for building web services on the web

    - Pros: easy to build and easy to consume.

    - Why REST?

      embraces the precepts of the web, including its architecture, benefits, and everything else

    - By building on top of HTTP, REST APIs provide the means to build:

        - Backwards compatible APIs
        - Evolvable APIs
        - Scaleable services
        - Securable services
        - A spectrum of stateless to stateful services   

- Big picture

  We’re going to create **a simple payroll service** that manages the employees of a company. We’ll **store employee objects in a (H2 in-memory) database**, and **access them (via something called JPA)**. Then we’ll **wrap that with something** that will allow access over the internet (called the **Spring MVC layer**).

  - New keyword:

    microservices RESTful services: a software architecture, a style not a standard, independent small module for small building blocks

    建立Employee实例对象(Bean)新见到的东西

    ```java
    @Entity
    class Employee {
    
      private @Id @GeneratedValue Long id;
        
    //@Entity is a JPA annotation to make this object ready for storage in a JPA-based data store.
    
    //id, name, and role are attributes of our Employee domain object. id is marked with more JPA annotations to indicate it’s the primary key and automatically populated by the JPA provider.
        
    //引申到 Spring Data JPA to handle the tedious database interactions.
        地址 https://spring.io/guides/gs/accessing-data-jpa/
    ```

    #### Spring Date JPA

    - Spring Data JPA repositories

      Spring Data JPA repositories are interfaces with methods supporting creating, reading, updating, and deleting records against a back end data store. 

    - You need not write an implementation of the repository interface. Spring Data JPA creates an implementation when you run the application

    - Create an Application Class

      ```java
      package com.example.accessingdatajpa;
      
      import org.springframework.boot.SpringApplication;
      import org.springframework.boot.autoconfigure.SpringBootApplication;
      
      @SpringBootApplication
      public class AccessingDataJpaApplication {
      
        public static void main(String[] args) {
          SpringApplication.run(AccessingDataJpaApplication.class, args);
        }
      
      }
      ```

      `@SpringBootApplication` is a convenience annotation that adds all of the following:

      - `@Configuration`: Tags the class as a source of bean definitions for the application context.

      - `@EnableAutoConfiguration`: Tells Spring Boot to start adding beans based on classpath settings, other beans, and various property settings. For example, if `spring-webmvc` is on the classpath, this annotation flags the application as a web application and activates key behaviors, such as setting up a `DispatcherServlet`.

      - `@ComponentScan`: Tells Spring to look for other components, configurations, and services in the `com/example` package, letting it find the controllers.

      - 执行代码问题

        `No plugin found for prefix 'spring-boot' in the current project and in the plugin groups`

        原因：未在`pom.xml`文件所在位置执行命令

    - Build an executable JAR

      build the JAR file with `./mvnw clean package` and then run the JAR file, as follows:

      `java -jar target/gs-accessing-data-jpa-0.1.0.jar` 执行jar   

      注：和官方文档不太一样，没找到`gs-accessing-data-jpa-0.1.0.jar`

      `java -jar target/accessing-data-jpa-0.0.1-SNAPSHOT.jar`我改的命令运行成功

      

      进阶阅读**Converting a Spring Boot JAR Application to a WAR**

      这里粗略补充war和jar区别：

      war是JavaWeb可执行文件，通常在项目部署后转成war

      [Getting Started | Converting a Spring Boot JAR Application to a WAR](https://spring.io/guides/gs/convert-jar-to-war/)

    - 衍生阅读

      Accessing JPA Data with REST

      [Getting Started | Accessing JPA Data with REST (spring.io)](https://spring.io/guides/gs/accessing-data-rest/)

  - `EmployeeRepository`

      `interface EmployeeRepository extends JpaRepository<Employee, Long>`

      Spring makes accessing data easy. By simply declaring the following `EmployeeRepository` interface we automatically will be able to

      - Create new Employees

      - Update existing ones

      - Delete Employees

      - Find Employees (one, all, or search by simple or complex properties)

        ```java
        //Application执行代码
        //@SpringBootApplication is a meta-annotation that pulls in component scanning, autoconfiguration, and property support. 
        @SpringBootApplication
        public class PayrollApplication {
        
          public static void main(String... args) {
            SpringApplication.run(PayrollApplication.class, args);
          }
        }
        ```

  - `LoadDatabase`

      ```java
      @Configuration
      class LoadDatabase {
      
        private static final Logger log = LoggerFactory.getLogger(LoadDatabase.class);
      
        @Bean
        CommandLineRunner initDatabase(EmployeeRepository repository) {
      
          return args -> {
            log.info("Preloading " + repository.save(new Employee("Bilbo Baggins", "burglar")));
            log.info("Preloading " + repository.save(new Employee("Frodo Baggins", "thief")));
          };
        }
      }
      ```

      - Spring Boot will run ALL `CommandLineRunner` beans once the application context is loaded.
      - This runner will request a copy of the `EmployeeRepository` you just created.
      - Using it, it will create two entities and store them.

**HTTP is the Platform**

To wrap your repository with a web layer, you must turn to Spring MVC. 

- EmployeeController.java

  ```java
  @RestController
  class EmployeeController {
  
    private final EmployeeRepository repository;
  
    EmployeeController(EmployeeRepository repository) {
      this.repository = repository;
    }
  
  
    // Aggregate root
    // tag::get-aggregate-root[]
    @GetMapping("/employees")
    List<Employee> all() {
      return repository.findAll();
    }
    // end::get-aggregate-root[]
  
    @PostMapping("/employees")
    Employee newEmployee(@RequestBody Employee newEmployee) {
      return repository.save(newEmployee);
    }
  
    // Single item
    
    @GetMapping("/employees/{id}")
    Employee one(@PathVariable Long id) {
      
      return repository.findById(id)
        .orElseThrow(() -> new EmployeeNotFoundException(id));
    }
  
    @PutMapping("/employees/{id}")
    Employee replaceEmployee(@RequestBody Employee newEmployee, @PathVariable Long id) {
      
      return repository.findById(id)
        .map(employee -> {
          employee.setName(newEmployee.getName());
          employee.setRole(newEmployee.getRole());
          return repository.save(employee);
        })
        .orElseGet(() -> {
          newEmployee.setId(id);
          return repository.save(newEmployee);
        });
    }
  
    @DeleteMapping("/employees/{id}")
    void deleteEmployee(@PathVariable Long id) {
      repository.deleteById(id);
    }
  }
  ```

  - `@RestController` indicates that the data returned by each method will be written straight into the response body instead of rendering a template.

  - An `EmployeeRepository` is injected by constructor into the controller.

  - We have routes for each operation (`@GetMapping`, `@PostMapping`, `@PutMapping` and `@DeleteMapping`, corresponding to HTTP `GET`, `POST`, `PUT`, and `DELETE` calls). (NOTE: It’s useful to read each method and understand what they do.)

  - `EmployeeNotFoundException` is an exception used to indicate when an employee is looked up but not found.

    ```java
    class EmployeeNotFoundException extends RuntimeException {
    
      EmployeeNotFoundException(Long id) {
        super("Could not find employee " + id);
      }
    }
    ```

  - `EmployeeNotFoundAdvice.java`

    ```java
    @ControllerAdvice
    class EmployeeNotFoundAdvice {
    
      @ResponseBody
      @ExceptionHandler(EmployeeNotFoundException.class)
      @ResponseStatus(HttpStatus.NOT_FOUND)
      String employeeNotFoundHandler(EmployeeNotFoundException ex) {
        return ex.getMessage();
      }
    }
    ```

    - `@ResponseBody` signals that this advice is rendered straight into the response body.
    - `@ExceptionHandler` configures the advice to only respond if an `EmployeeNotFoundException` is thrown.
    - `@ResponseStatus` says to issue an `HttpStatus.NOT_FOUND`, i.e. an **HTTP 404**.
    - The body of the advice generates the content. In this case, it gives the message of the exception.

  - 

    



**一些概念**

- RPC(Remote Procedure Call)

- Hypermedia

    **Hypermedia**, an extension of the term [hypertext](https://en.wikipedia.org/wiki/Hypertext), is a [nonlinear medium](https://en.wikipedia.org/wiki/Nonlinear_medium) of information that includes graphics, audio, video, plain text and [hyperlinks](https://en.wikipedia.org/wiki/Hyperlink). 

    

    The [World Wide Web](https://en.wikipedia.org/wiki/World_Wide_Web) is a classic example of hypermedia, whereas a non-interactive [cinema](https://en.wikipedia.org/wiki/Movie_theatre) presentation is an example of standard multimedia due to the absence of hyperlinks.

- Hypermedia as the Engine of Application State (**HATEOAS**)

## Spring Boot

1. Introducing Spring Boot

   -  Spring Boot helps you to create stand-alone, production-grade Spring-based applications that you can run.

     **Primary goals：**

       Provide a radically faster and widely accessible getting-started experience for all Spring development.

       Be opinionated out of the box but get out of the way quickly as requirements start to diverge from the defaults.

       Provide a range of non-functional features that are common to large classes of projects (such as embedded servers, security, metrics, health checks, and externalized configuration).

       Absolutely no code generation and no requirement for XML configuration.

2. System Requirements

   Spring Boot 2.5.1-SNAPSHOT requires [Java 8](https://www.java.com/) and is compatible up to and including Java 16. [Spring Framework 5.3.7](https://docs.spring.io/spring-framework/docs/5.3.7/reference/html/) or above is also required.

   | Build Tool | Version               |

   | :--------- | :-------------------- |

   | Maven      | 3.5+                  |

   | Gradle     | 6.8.x, 6.9.x, and 7.x |


   supports the following embedded servlet containers：

   | Name         | Servlet Version |

   | :----------- | :-------------- |

   | Tomcat 9.0   | 4.0             |

   | Jetty 9.4    | 3.1             |

   | Jetty 10.0   | 4.0             |

   | Undertow 2.0 | 4.0             |


3. Installing Spring Boot

   - need [Java SDK v1.8](https://www.java.com/) or higher
   - You can use Spring Boot in the same way as any standard Java library. To do so, include the appropriate `spring-boot-*.jar` files on your classpath. 

   - Spring Boot is compatible with Apache Maven 3.3 or above. 

4. Developing Your First Spring Boot Application

   `@RestController`:  *stereotype* annotation. It provides hints for people reading the code and for Spring that the class plays a specific role. In this case, our class is a web `@Controller`, so Spring considers it when handling incoming web requests.

   

   `@RequestMapping`:  provides “routing” information. It tells Spring that any HTTP request with the `/` path should be mapped to the `home` method. The `@RestController` annotation tells Spring to render the resulting string directly back to the caller.

   

   `@EnableAutoConfiguration`. This annotation tells Spring Boot to “guess” how you want to configure Spring, based on the jar dependencies that you have added. Since `spring-boot-starter-web` added Tomcat and Spring MVC, the auto-configuration assumes that you are developing a web application and sets up Spring accordingly.

   - 要在`pom.xml`下执行 `mvn spring-boot:run`

   - 执行`mvn spring-boot:run` `出现cannot find symbol   symbol: class "RestController"`错误。解决办法：在`Intellij`里导入项目，然后根据自动提示，`import`所需的类，IDEA里成功运行，换到命令行，运行成功。

     

   ### Creating an Executable Jar

   To create an executable jar, we need to add the `spring-boot-maven-plugin` to our `pom.xml`. To do so, insert the following lines just below the `dependencies` section:

   If you want to peek inside, you can use `jar tvf`, as follows:

   `$ jar tvf target/myproject-0.0.1-SNAPSHOT.jar`

   `java -jar target/myproject-0.0.1-SNAPSHOT.jar`

5. 进阶学习

## Spring尚硅谷

### IOC容器

- 底层原理

  什么是IOC：

  ​	i. 控制反转， 对象创建和控制交给spring管理

  ​	ii. 使用目的： 降低耦合度

  ​	iii. 入门案例是ioc实现

  底层原理：

  ​	i. xml解析、工厂模式、反射

  原始方案——工厂模式——IOC容器 逐渐降低耦合度

  ![image-20210523193526614](https://raw.githubusercontent.com/RshStone/CS-Notes/master/Notes/Spring/001.png)

  

- IOC接口(`BeanFactory`)

  i. IOC思想基于IOC容器完成，	IOC容器底层就是对象工厂

  ii. Spring提供IOC容器实现的两种方式：（两种方式）

  ​	加载配置文件获取bean对象

   1. `BeanFactory`

      IOC容器基本实现方式： Spring里面内部使用，不提供开发人员使用

      *加载配置文件不会创建对象，使用对象采取创建对象

   2. `ApplicationContext`：`BeanFactory`的子接口，提供更多等强大功能，一般是开发人员使用

      *加载配置文件时会把配置文件对象进行创建

   3. `ApplicationContext`接口有实现类

      ```
      FileSystemXmlApplicationContext
      ClassPathXmlApplicationContext
      ```

      

- IOC操作Bean管理（基于xml）(基于注解)

  1、什么是Bean管理

  ​	Bean管理包括两个操作

  ​	i. Spring创建对象

  ​	ii. Spring注入属性

  2、Bean管理操作有两种方式

  (1)基于xml配置文件方式

  `<bean id="user"class="com.rshstone.spring5.User"></bean>`

  i. 在spring配置文件中，使用bean标签，标签里面添加对应属性，可以实现对象创建

  ii. 在bean标签中有很多属性，介绍常见的属性

  *id属性：唯一标识

  *class属性：类全路径(包类路径)

  ii. 创建类对象时，默认无参数构造方s法

  (2)基于xml方式注释方式

  i.  DI：依赖注入，就是注入属性 ，需要在创建对象时完成

  ​	DI和ioc的关系：DI时IOC中具体实现，

  ​	第一种使用set方法注入

  ​		<bean id = "" class = "">

  ​				<property name = "" value = "">

  ​				</property> 

  ​		</bean>

  ​	第二种使用有参数构造注入

  ​	i. 类里面创建有参构造

  ​	ii. 配置xml <bean id = "" class = "">

  ​				<constructor-arg name = "" value = "">

  ​				</constructor-arg> 

  ​				</bean>

  ​	第三种p名称空间注入(了解一下)

### AOP操作

### Jdbc Template

事务操作

Spring5新功能-Webflux