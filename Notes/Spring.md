

SpringBoot2

## Spring In Action

**一些自考题**

- bean:

- DI: 让相互协作的软件组件保持松散耦合

- AOP: 把遍布应用各处的功能分离出来形成可重用的组件

  ![image-20210630175348595](Spring/003.png)

  使服务模块化，以声明方式将它们应用到需要影响的组件中去

- 
- 

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

   ![002](Spring/002.png)

   

   

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

     这块不是很理解，原文档文字如下:

     You can use the application context constructor to load bean definitions from all these XML fragments. This constructor takes multiple `Resource` locations, as was shown in the [previous section](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-instantiation). Alternatively, use one or more occurrences of the `<import/>` element to load bean definitions from another file or files. The following example shows how to do so:

     

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

   ​	Naming Beans（简单来讲，给beans命名，可以1个或者多个，多个的时候用`alias`标签）

   ​	Instantiating Beans:三种方式(具体实践还不太懂)

   ​		Instantiation with a Constructor

   ​		Instantiation with a Static Factory Method

   ​		Instantiation by Using an Instance Factory Method

   ​	

   1.4 Dependencies

   **Dependency Injection**

   ​	through constructor arguments, arguments to a factory method, or properties

   ​	The object does not look up its dependencies and does not know the location or class of the dependencies. As a result, your classes become easier to test, particularly when the dependencies are on interfaces or abstract base classes, which allow for stub or mock implementations to be used in unit tests.(具体怎么解耦的)

   ​	DI exists in two major variants: [Constructor-based dependency injection](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-constructor-injection) and [Setter-based dependency injection](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-setter-injection).

   - Constructor-based Dependency Injection

     The following example shows a class that can only be dependency-injected with constructor injection:

     ```java
     // a constructor so that the Spring container can inject a MovieFinder
     class SimpleMovieLister(private val movieFinder: MovieFinder) {
         // business logic that actually uses the injected MovieFinder is omitted...
     }
     ```

     

   The `ApplicationContext` supports constructor-based and setter-based DI for the beans it manages. It also supports setter-based DI after some dependencies have already been injected through the constructor approach. You configure the dependencies in the form of a `BeanDefinition`, which you use in conjunction with `PropertyEditor` instances to convert properties from one format to another. However, most Spring users do not work with these classes directly (that is, programmatically) but rather with XML `bean` definitions, annotated components (that is, classes annotated with `@Component`, `@Controller`, and so forth), or `@Bean` methods in Java-based `@Configuration` classes. These sources are then converted internally into instances of `BeanDefinition` and used to load an entire Spring IoC container instance.（不是很懂）

    ApplicationContext为其管理的bean支持基于构造函数和基于setter的DI。在一些依赖项已经通过构造函数方法注入之后，它还支持基于setter的DI。您可以以BeanDefinition的形式配置依赖项，将其与PropertyEditor实例结合使用，以将属性从一种格式转换为另一种格式。然而，大多数Spring用户并不直接使用这些类（即编程），而是使用xmlbean定义、带注释的组件（即用@Component、@Controller等注释的类）或基于Java的@Configuration类中的@bean方法。然后，这些源在内部转换为BeanDefinition的实例，并用于加载整个Spring IoC容器实例。 

   

   1.5 Bean Scopes

   1.6 Customizing the Nature of a Bean

   1.7 Bean Definition Inheritance

   1.8 Container Extension Points

   1.9Annotation-based Container Configuration
   
   



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

  ![image-20210523193526614](Spring/001.png)

  

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



```java
F:\Java\JDK\jdk-version\jdk-8\bin\java.exe -ea -Didea.test.cyclic.buffer.size=1048576 -javaagent:C:\Users\ASUS\AppData\Local\JetBrains\Toolbox\apps\IDEA-U\ch-0\203.7148.57\lib\idea_rt.jar=3862:C:\Users\ASUS\AppData\Local\JetBrains\Toolbox\apps\IDEA-U\ch-0\203.7148.57\bin -Dfile.encoding=UTF-8 -classpath C:\Users\ASUS\AppData\Local\JetBrains\Toolbox\apps\IDEA-U\ch-0\203.7148.57\lib\idea_rt.jar;C:\Users\ASUS\AppData\Local\JetBrains\Toolbox\apps\IDEA-U\ch-0\203.7148.57\plugins\junit\lib\junit5-rt.jar;C:\Users\ASUS\AppData\Local\JetBrains\Toolbox\apps\IDEA-U\ch-0\203.7148.57\plugins\junit\lib\junit-rt.jar;F:\Java\JDK\jdk-version\jdk-8\jre\lib\charsets.jar;F:\Java\JDK\jdk-version\jdk-8\jre\lib\deploy.jar;F:\Java\JDK\jdk-version\jdk-8\jre\lib\ext\access-bridge.jar;F:\Java\JDK\jdk-version\jdk-8\jre\lib\ext\cldrdata.jar;F:\Java\JDK\jdk-version\jdk-8\jre\lib\ext\dnsns.jar;F:\Java\JDK\jdk-version\jdk-8\jre\lib\ext\jaccess.jar;F:\Java\JDK\jdk-version\jdk-8\jre\lib\ext\jfxrt.jar;F:\Java\JDK\jdk-version\jdk-8\jre\lib\ext\localedata.jar;F:\Java\JDK\jdk-version\jdk-8\jre\lib\ext\nashorn.jar;F:\Java\JDK\jdk-version\jdk-8\jre\lib\ext\sunec.jar;F:\Java\JDK\jdk-version\jdk-8\jre\lib\ext\sunjce_provider.jar;F:\Java\JDK\jdk-version\jdk-8\jre\lib\ext\sunmscapi.jar;F:\Java\JDK\jdk-version\jdk-8\jre\lib\ext\sunpkcs11.jar;F:\Java\JDK\jdk-version\jdk-8\jre\lib\ext\zipfs.jar;F:\Java\JDK\jdk-version\jdk-8\jre\lib\javaws.jar;F:\Java\JDK\jdk-version\jdk-8\jre\lib\jce.jar;F:\Java\JDK\jdk-version\jdk-8\jre\lib\jfr.jar;F:\Java\JDK\jdk-version\jdk-8\jre\lib\jfxswt.jar;F:\Java\JDK\jdk-version\jdk-8\jre\lib\jsse.jar;F:\Java\JDK\jdk-version\jdk-8\jre\lib\management-agent.jar;F:\Java\JDK\jdk-version\jdk-8\jre\lib\plugin.jar;F:\Java\JDK\jdk-version\jdk-8\jre\lib\resources.jar;F:\Java\JDK\jdk-version\jdk-8\jre\lib\rt.jar;D:\Downloads\SpringiA4_SourceCode\Chapter_02\stereo-autoconfig\out\test\classes;D:\Downloads\SpringiA4_SourceCode\Chapter_02\stereo-autoconfig\out\test\resources;D:\Downloads\SpringiA4_SourceCode\Chapter_02\stereo-autoconfig\out\production\classes;D:\Downloads\SpringiA4_SourceCode\Chapter_02\stereo-autoconfig\out\production\resources;C:\Users\ASUS\.gradle\caches\modules-2\files-2.1\org.springframework\spring-context\4.0.7.RELEASE\8a4aa735f3691a1985381b3c6c69d32b835f51b4\spring-context-4.0.7.RELEASE.jar;C:\Users\ASUS\.gradle\caches\modules-2\files-2.1\org.springframework\spring-test\4.0.7.RELEASE\148c20e5170e6081dfcc5afefa613e27a7b1b814\spring-test-4.0.7.RELEASE.jar;C:\Users\ASUS\.gradle\caches\modules-2\files-2.1\com.github.stefanbirkner\system-rules\1.5.0\a98ed9e2775d57586a420d52b9bf8b2384edc58b\system-rules-1.5.0.jar;C:\Users\ASUS\.gradle\caches\modules-2\files-2.1\org.springframework\spring-aop\4.0.7.RELEASE\caadec5dc4ea4899d89004ff46053f8e391e0343\spring-aop-4.0.7.RELEASE.jar;C:\Users\ASUS\.gradle\caches\modules-2\files-2.1\org.springframework\spring-beans\4.0.7.RELEASE\fdd041f086972cc16f9b09ee420a98604cd0bc07\spring-beans-4.0.7.RELEASE.jar;C:\Users\ASUS\.gradle\caches\modules-2\files-2.1\org.springframework\spring-core\4.0.7.RELEASE\777e9502c4c2de150918a746fa22734d3eff81e0\spring-core-4.0.7.RELEASE.jar;C:\Users\ASUS\.gradle\caches\modules-2\files-2.1\org.springframework\spring-expression\4.0.7.RELEASE\46a4cfe181b1f15940b5ea7530fcad1f8b98c561\spring-expression-4.0.7.RELEASE.jar;C:\Users\ASUS\.gradle\caches\modules-2\files-2.1\commons-io\commons-io\2.10.0\79384da84646660c57b89aa86a5a1eb98af50e00\commons-io-2.10.0.jar;C:\Users\ASUS\.m2\repository\aopalliance\aopalliance\1.0\aopalliance-1.0.jar;C:\Users\ASUS\.gradle\caches\modules-2\files-2.1\commons-logging\commons-logging\1.1.3\f6f66e966c70a83ffbdb6f17a0919eaf7c8aca7f\commons-logging-1.1.3.jar;C:\Users\ASUS\.m2\repository\junit\junit\4.11\junit-4.11.jar;C:\Users\ASUS\.m2\repository\org\hamcrest\hamcrest-core\1.3\hamcrest-core-1.3.jar com.intellij.rt.junit.JUnitStarter -ideVersion5 -junit4 soundsystem.CDPlayerXMLConfigTest,play
Jun 21, 2021 4:05:59 PM org.springframework.test.context.TestContextManager retrieveTestExecutionListeners
INFO: Could not instantiate TestExecutionListener [org.springframework.test.context.web.ServletTestExecutionListener]. Specify custom listener classes or make the default listener classes (and their required dependencies) available. Offending class: [javax/servlet/ServletContext]
Jun 21, 2021 4:05:59 PM org.springframework.test.context.TestContextManager retrieveTestExecutionListeners
INFO: Could not instantiate TestExecutionListener [org.springframework.test.context.transaction.TransactionalTestExecutionListener]. Specify custom listener classes or make the default listener classes (and their required dependencies) available. Offending class: [org/springframework/transaction/interceptor/TransactionAttributeSource]
Jun 21, 2021 4:05:59 PM org.springframework.beans.factory.xml.XmlBeanDefinitionReader loadBeanDefinitions
INFO: Loading XML bean definitions from class path resource [META-INF/spring/soundsystem.xml]
Jun 21, 2021 4:06:00 PM org.springframework.context.support.GenericApplicationContext prepareRefresh
INFO: Refreshing org.springframework.context.support.GenericApplicationContext@17b1517: startup date [Mon Jun 21 16:06:00 CST 2021]; root of context hierarchy
Playing Sgt. Pepper's Lonely Hearts Club Band by The Beatles

org.junit.ComparisonFailure: 
<Click to see difference>


	at org.junit.Assert.assertEquals(Assert.java:115)
	at org.junit.Assert.assertEquals(Assert.java:144)
	at soundsystem.CDPlayerXMLConfigTest.play(CDPlayerXMLConfigTest.java:34)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:497)
	at org.junit.runners.model.FrameworkMethod$1.runReflectiveCall(FrameworkMethod.java:47)
	at org.junit.internal.runners.model.ReflectiveCallable.run(ReflectiveCallable.java:12)
	at org.junit.runners.model.FrameworkMethod.invokeExplosively(FrameworkMethod.java:44)
	at org.junit.internal.runners.statements.InvokeMethod.evaluate(InvokeMethod.java:17)
	at org.springframework.test.context.junit4.statements.RunBeforeTestMethodCallbacks.evaluate(RunBeforeTestMethodCallbacks.java:74)
	at org.springframework.test.context.junit4.statements.RunAfterTestMethodCallbacks.evaluate(RunAfterTestMethodCallbacks.java:83)
	at org.junit.rules.ExternalResource$1.evaluate(ExternalResource.java:48)
	at org.junit.rules.RunRules.evaluate(RunRules.java:20)
	at org.springframework.test.context.junit4.statements.SpringRepeat.evaluate(SpringRepeat.java:72)
	at org.springframework.test.context.junit4.SpringJUnit4ClassRunner.runChild(SpringJUnit4ClassRunner.java:233)
	at org.springframework.test.context.junit4.SpringJUnit4ClassRunner.runChild(SpringJUnit4ClassRunner.java:87)
	at org.junit.runners.ParentRunner$3.run(ParentRunner.java:238)
	at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:63)
	at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:236)
	at org.junit.runners.ParentRunner.access$000(ParentRunner.java:53)
	at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:229)
	at org.springframework.test.context.junit4.statements.RunBeforeTestClassCallbacks.evaluate(RunBeforeTestClassCallbacks.java:61)
	at org.springframework.test.context.junit4.statements.RunAfterTestClassCallbacks.evaluate(RunAfterTestClassCallbacks.java:71)
	at org.junit.runners.ParentRunner.run(ParentRunner.java:309)
	at org.springframework.test.context.junit4.SpringJUnit4ClassRunner.run(SpringJUnit4ClassRunner.java:176)
	at org.junit.runner.JUnitCore.run(JUnitCore.java:160)
	at com.intellij.junit4.JUnit4IdeaTestRunner.startRunnerWithArgs(JUnit4IdeaTestRunner.java:69)
	at com.intellij.rt.junit.IdeaTestRunner$Repeater.startRunnerWithArgs(IdeaTestRunner.java:33)
	at com.intellij.rt.junit.JUnitStarter.prepareStreamsAndStart(JUnitStarter.java:220)
	at com.intellij.rt.junit.JUnitStarter.main(JUnitStarter.java:53)


Process finished with exit code -1
```

```java
:compileJava UP-TO-DATE
:processResources UP-TO-DATE
:classes UP-TO-DATE
:compileTestJava UP-TO-DATE
:processTestResources UP-TO-DATE
:testClasses UP-TO-DATE
:test
Jun 21, 2021 4:12:31 PM org.springframework.test.context.support.AbstractContextLoader generateDefaultLocations
INFO: Detected default resource location "classpath:/soundsystem/CNamespaceReferenceTest-context.xml" for test class [soundsystem.CNamespaceReferenceTest]
Jun 21, 2021 4:12:31 PM org.springframework.test.context.support.AbstractDelegatingSmartContextLoader processContextConfiguration
INFO: GenericXmlContextLoader detected default locations for context configuration [ContextConfigurationAttributes@bc6a271 declaringClass = 'soundsystem.CNamespaceReferenceTest', classes = '{}', locations = '{classpath:/soundsystem/CNamespaceReferenceTest-context.xml}', inheritLocations = true, initializers = '{}', inheritInitializers = true, name = [null], contextLoaderClass = 'org.springframework.test.context.ContextLoader'].
Jun 21, 2021 4:12:31 PM org.springframework.test.context.support.AnnotationConfigContextLoaderUtils detectDefaultConfigurationClasses
INFO: Could not detect default configuration classes for test class [soundsystem.CNamespaceReferenceTest]: CNamespaceReferenceTest does not declare any static, non-private, non-final, inner classes annotated with @Configuration.
Jun 21, 2021 4:12:31 PM org.springframework.test.context.TestContextManager retrieveTestExecutionListeners
INFO: Could not instantiate TestExecutionListener [org.springframework.test.context.web.ServletTestExecutionListener]. Specify custom listener classes or make the default listener classes (and their required dependencies) available. Offending class: [javax/servlet/ServletContext]
Jun 21, 2021 4:12:31 PM org.springframework.test.context.TestContextManager retrieveTestExecutionListeners
INFO: Could not instantiate TestExecutionListener [org.springframework.test.context.transaction.TransactionalTestExecutionListener]. Specify custom listener classes or make the default listener classes (and their required dependencies) available. Offending class: [org/springframework/transaction/interceptor/TransactionAttributeSource]
Jun 21, 2021 4:12:31 PM org.springframework.beans.factory.xml.XmlBeanDefinitionReader loadBeanDefinitions
INFO: Loading XML bean definitions from class path resource [soundsystem/CNamespaceReferenceTest-context.xml]
Jun 21, 2021 4:12:31 PM org.springframework.context.support.GenericApplicationContext prepareRefresh
INFO: Refreshing org.springframework.context.support.GenericApplicationContext@5e0e6a05: startup date [Mon Jun 21 16:12:31 CST 2021]; root of context hierarchy
Playing Sgt. Pepper's Lonely Hearts Club Band by The Beatles

expected:<... Band by The Beatles[]
]
>
<Click to see difference>

org.junit.ComparisonFailure: expected:<... Band by The Beatles[]
]
>
	at org.junit.Assert.assertEquals(Assert.java:115)
	at org.junit.Assert.assertEquals(Assert.java:144)
	at soundsystem.CNamespaceReferenceTest.play(CNamespaceReferenceTest.java:26)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.junit.runners.model.FrameworkMethod$1.runReflectiveCall(FrameworkMethod.java:47)
	at org.junit.internal.runners.model.ReflectiveCallable.run(ReflectiveCallable.java:12)
	at org.junit.runners.model.FrameworkMethod.invokeExplosively(FrameworkMethod.java:44)
	at org.junit.internal.runners.statements.InvokeMethod.evaluate(InvokeMethod.java:17)
	at org.springframework.test.context.junit4.statements.RunBeforeTestMethodCallbacks.evaluate(RunBeforeTestMethodCallbacks.java:74)
	at org.springframework.test.context.junit4.statements.RunAfterTestMethodCallbacks.evaluate(RunAfterTestMethodCallbacks.java:83)
	at org.junit.rules.ExternalResource$1.evaluate(ExternalResource.java:48)
	at org.junit.rules.RunRules.evaluate(RunRules.java:20)
	at org.springframework.test.context.junit4.statements.SpringRepeat.evaluate(SpringRepeat.java:72)
	at org.springframework.test.context.junit4.SpringJUnit4ClassRunner.runChild(SpringJUnit4ClassRunner.java:233)
	at org.springframework.test.context.junit4.SpringJUnit4ClassRunner.runChild(SpringJUnit4ClassRunner.java:87)
	at org.junit.runners.ParentRunner$3.run(ParentRunner.java:238)
	at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:63)
	at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:236)
	at org.junit.runners.ParentRunner.access$000(ParentRunner.java:53)
	at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:229)
	at org.springframework.test.context.junit4.statements.RunBeforeTestClassCallbacks.evaluate(RunBeforeTestClassCallbacks.java:61)
	at org.springframework.test.context.junit4.statements.RunAfterTestClassCallbacks.evaluate(RunAfterTestClassCallbacks.java:71)
	at org.junit.runners.ParentRunner.run(ParentRunner.java:309)
	at org.springframework.test.context.junit4.SpringJUnit4ClassRunner.run(SpringJUnit4ClassRunner.java:176)
	at org.gradle.api.internal.tasks.testing.junit.JUnitTestClassExecuter.runTestClass(JUnitTestClassExecuter.java:114)
	at org.gradle.api.internal.tasks.testing.junit.JUnitTestClassExecuter.execute(JUnitTestClassExecuter.java:57)
	at org.gradle.api.internal.tasks.testing.junit.JUnitTestClassProcessor.processTestClass(JUnitTestClassProcessor.java:66)
	at org.gradle.api.internal.tasks.testing.SuiteTestClassProcessor.processTestClass(SuiteTestClassProcessor.java:51)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.gradle.internal.dispatch.ReflectionDispatch.dispatch(ReflectionDispatch.java:35)
	at org.gradle.internal.dispatch.ReflectionDispatch.dispatch(ReflectionDispatch.java:24)
	at org.gradle.internal.dispatch.ContextClassLoaderDispatch.dispatch(ContextClassLoaderDispatch.java:32)
	at org.gradle.internal.dispatch.ProxyDispatchAdapter$DispatchingInvocationHandler.invoke(ProxyDispatchAdapter.java:93)
	at com.sun.proxy.$Proxy2.processTestClass(Unknown Source)
	at org.gradle.api.internal.tasks.testing.worker.TestWorker.processTestClass(TestWorker.java:109)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.gradle.internal.dispatch.ReflectionDispatch.dispatch(ReflectionDispatch.java:35)
	at org.gradle.internal.dispatch.ReflectionDispatch.dispatch(ReflectionDispatch.java:24)
	at org.gradle.internal.remote.internal.hub.MessageHub$Handler.run(MessageHub.java:377)
	at org.gradle.internal.concurrent.ExecutorPolicy$CatchAndRecordFailures.onExecute(ExecutorPolicy.java:54)
	at org.gradle.internal.concurrent.StoppableExecutorImpl$1.run(StoppableExecutorImpl.java:40)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
	at java.lang.Thread.run(Thread.java:748)


soundsystem.CNamespaceReferenceTest > play FAILED
    org.junit.ComparisonFailure at CNamespaceReferenceTest.java:26
1 test completed, 1 failed
:test FAILED
FAILURE: Build failed with an exception.
* What went wrong:
Execution failed for task ':test'.
> There were failing tests. See the report at: file:///D:/Downloads/SpringiA4_SourceCode/Chapter_02/stereo-xmlconfig/build/reports/tests/test/index.html
* Try:
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output.
BUILD FAILED
Total time: 3.984 secs
```





