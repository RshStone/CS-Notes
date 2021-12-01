## Spring Framework Overview

- use the [GitHub Issues](https://github.com/spring-projects/spring-framework/issues).
- Stack Overflow. Click [here](https://stackoverflow.com/questions/tagged/spring+or+spring-mvc+or+spring-aop+or+spring-jdbc+or+spring-r2dbc+or+spring-transactions+or+spring-annotations+or+spring-jms+or+spring-el+or+spring-test+or+spring+or+spring-remoting+or+spring-orm+or+spring-jmx+or+spring-cache+or+spring-webflux+or+spring-rsocket?tab=Newest) 

### Design Philosophy

- Provide choice at every level --> switch persistence providers through configuration without changing your code
- Accommodate diverse perspectives --> supports a wide range of application needs with different perspectives
- Maintain strong backward compatibility.
- Care about API design
- Set high standards for code quality

## Core Technologies

### 本笔记阅读的注意事项

代码部分以 `Java`为主， 一般有 `Kotlin` or `Gradle`版本

### The loC Container

- covers all the technologies that are absolutely integral to the Spring Framework.
-  Spring Framework’s Inversion of Control (IoC) container
- Spring’s Aspect-Oriented Programming (AOP) technologies. 
- Coverage of Spring’s integration with AspectJ  is also provided

#### 1.1.IOC

 **Introduction to the Spring IoC(Inversion of Control ) Container and Beans**

- also known as dependency injection (DI).

- procedure:

  *It is a process whereby objects define their dependencies (that is, the other objects they work with) only through constructor arguments, arguments to a factory method, or properties that are set on the object instance after it is constructed or returned from a factory method. *

  *The container then injects those dependencies when it creates the bean. This process is fundamentally the inverse 

  of the bean itself controlling the instantiation or location of its dependencies by using direct construction of classes or a mechanism such as the Service Locator pattern.*

- Two basis for IoC

  The `org.springframework.beans` and `org.springframework.context` packages are the basis for Spring Framework’s IoC container. 

  The [`BeanFactory`](https://docs.spring.io/spring-framework/docs/5.3.7/javadoc-api/org/springframework/beans/factory/BeanFactory.html) (**basic functionality**) interface provides an advanced configuration mechanism capable of managing any type of object. 

  [`ApplicationContext`](https://docs.spring.io/spring-framework/docs/5.3.7/javadoc-api/org/springframework/context/ApplicationContext.html) (**more enterprise-specific functionality**)is a sub-interface of `BeanFactory`.

  - Easier integration with Spring’s AOP features
  - Message resource handling (for use in internationalization)
  - Event publication
  - Application-layer specific contexts such as the `WebApplicationContext` for use in web applications.

  beans: form the backbone of your application,  are instantiated, assembled, and managed by a Spring IoC container

#### 1.2 Container Overview

- org.springframework.context.ApplicationContext

  `org.springframework.context.ApplicationContext` interface represents the Spring IoC container and is responsible for instantiating, configuring, and assembling the beans.

  The configuration metadata: XML, Java annotations, or Java code.

- create an instance of [`ClassPathXmlApplicationContext`](https://docs.spring.io/spring-framework/docs/5.3.7/javadoc-api/org/springframework/context/support/ClassPathXmlApplicationContext.html) or [FileSystemXmlApplicationContext](https://docs.spring.io/spring-framework/docs/5.3.7/javadoc-api/org/springframework/context/support/FileSystemXmlApplicationContext.html)


![002](Spring/002.png)



Configuration Metadata

i. traditionally supplied in a simple and intuitive XML format

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



ii. other forms of metadata with the Spring container

 [Annotation-based configuration](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-annotation-config)   

​	`@Required @Autowired @Primary @Resource`等等

 [Java-based configuration](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-java)

​	see the [`@Configuration`](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/Configuration.html), [`@Bean`](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/Bean.html), [`@Import`](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/Import.html), and [`@DependsOn`](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/DependsOn.html) annotations.



Bean definitions(actual objects) make up your application

**Objects** (service layer objects, data access objects (DAOs), presentation objects such as Struts `Action` instances, infrastructure objects such as Hibernate `SessionFactories`, JMS `Queues`, and so forth. ) 

You can use Spring’s integration with AspectJ to configure objects that have been created outside the control of an IoC container. See [Using AspectJ to dependency-inject domain objects with Spring](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#aop-atconfigurable)

Instantiating a Container

resource strings that let the container load configuration metadata from a variety of external resources, such as the local file system, the Java `CLASSPATH`, and so on.

```java
ApplicationContext context = new ClassPathXmlApplicationContext("services.xml", "daos.xml");
```

```kotlin
val context = ClassPathXmlApplicationContext("services.xml", "daos.xml")
```



#####  Composing XML-based Configuration Metadata

```xml
<beans>
    <import resource="services.xml"/>
    <import resource="resources/messageSource.xml"/>
    <import resource="/resources/themeSource.xml"/>

    <bean id="bean1" class="..."/>
    <bean id="bean2" class="..."/>
</beans>
//external bean definitions services.xml, messageSource.xml, and themeSource.xml

```



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



**Using the Container**

​	Four ways to use the container (don't really understand with code)

1.  ApplicationContext

   **ClassPathXmlApplicationContext**

   ```java
   // create and configure beans
   ApplicationContext context = new ClassPathXmlApplicationContext("services.xml", "daos.xml");
   
   // retrieve configured instance
   PetStoreService service = context.getBean("petStore", PetStoreService.class);
   
   // use configured instance
   List<String> userList = service.getUsernameList();
   ```

   **GenericGroovyApplicationContext**

   ```java
   ApplicationContext context = new GenericGroovyApplicationContext("services.groovy", "daos.groovy");
   ```

   

2. GenericApplicationContext

   **XmlBeanDefinitionReader**

   ```java
   GenericApplicationContext context = new GenericApplicationContext();
   new XmlBeanDefinitionReader(context).loadBeanDefinitions("services.xml", "daos.xml");
   context.refresh();
   ```

    **GroovyBeanDefinitionReader**

   ```java
   GenericApplicationContext context = new GenericApplicationContext();
   new GroovyBeanDefinitionReader(context).loadBeanDefinitions("services.groovy", "daos.groovy");
   context.refresh();
   ```

   

#### 1.3 Bean Overview

​	A Spring IoC container managers one or more beans.

​	With container: `BeanDefinition` objects

`BeanDefinition` objects contain metadata:

- A package-qualified class name

- Bean behavioral configuration elements

- References to other beans that are needed for the bean to do its work.

- Other configuration settings to set in the newly created object 		

  metadata contains properties:

| Property                 | Explained in…                                                |
| ------------------------ | ------------------------------------------------------------ |
| Class                    | [Instantiating Beans](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-class) |
| Name                     | [Naming Beans](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-beanname) |
| Scope                    | [Bean Scopes](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-scopes) |
| Constructor arguments    | [Dependency Injection](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-collaborators) |
| Properties               | [Dependency Injection](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-collaborators) |
| Autowiring mode          | [Autowiring Collaborators](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-autowire) |
| Lazy initialization mode | [Lazy-initialized Beans](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-lazy-init) |
| Initialization method    | [Initialization Callbacks](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-lifecycle-initializingbean) |
| Destruction method       | [Destruction Callbacks](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-lifecycle-disposablebean) |

`BeanDefinition` objects contain information on how to create a specific bean.

`ApplicationContext` implementations also permit the registration of existing objects that are created outside the container (by users).

How: 

​	access `getBeanFactory()` method

​	returns the BeanFactory `DefaultListableBeanFactory` implementation

​	supports this registration through the `registerSingleton(..)` and `registerBeanDefinition(..)` methods





​	**Naming Beans**

简单来讲，给beans命名，可以1个或者多个，多个的时候用`alias`标签

Need to know: Every bean has one or more identifiers

Bean Naming Conventions: 

​	 start with a lowercase letter and are camel-cased from there

​	examples: accountManager`, `accountService`, `userDao`, `loginController

##### Aliasing a Bean outside the Bean Definition

```xml
<alias name="fromName" alias="toName"/>
```



##### Instantiating Beans

1. Instantiation with a Constructor

```xml
<bean id="exampleBean" class="examples.ExampleBean"/>

<bean name="anotherExample" class="examples.ExampleBeanTwo"/>
```

2. Instantiation with a Static Factory Method

```xml
<bean id="clientService"
    class="examples.ClientService"
    factory-method="createInstance"/>
```

Corresponding Class:

```java
public class ClientService {
    private static ClientService clientService = new ClientService();
    private ClientService() {}

    public static ClientService createInstance() {
        return clientService;
    }
}
```



3. Instantiation by Using an Instance Factory Method

```xml
<!-- the factory bean, which contains a method called createInstance() -->
<bean id="serviceLocator" class="examples.DefaultServiceLocator">
    <!-- inject any dependencies required by this locator bean -->
</bean>

<!-- the bean to be created via the factory bean -->
<bean id="clientService"
    factory-bean="serviceLocator"
    factory-method="createClientServiceInstance"/>
```

```java
public class DefaultServiceLocator {

    private static ClientService clientService = new ClientServiceImpl();

    public ClientService createClientServiceInstance() {
        return clientService;
    }
}
```



**Determining a Bean’s Runtime Type**

`BeanFactory.getType` call for the specified bean name

bean metadata definition: combined with a declared factory method or being a `FactoryBean` class which may lead to a different runtime type of the bean.



#### 1.4 Dependencies

**What will learn** 

How you go from defining a number of bean definitions that stand alone to a fully realized application where objects collaborate to achieve a goal.

#### **Dependency Injection**

**DI:** a process whereby objects define their dependencies (that is, the other objects with which they work) only through constructor arguments, arguments to a factory method, or properties 

**Benefit:** Code is cleaner with the DI principle, and decoupling is more effective when objects are provided with their dependencies.

DI exists in two major variants: [Constructor-based dependency injection](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-constructor-injection) and [Setter-based dependency injection](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-setter-injection).

- Constructor-based Dependency Injection

  Constructor-based DI is accomplished by the container invoking a constructor with a number of arguments, each representing a dependency. Calling a `static` factory method with specific arguments to construct the bean is nearly equivalent, and this discussion treats arguments to a constructor and to a `static` factory method similarly. 

  **(what is static factory method)**
  
  The following example shows a class that can only be dependency-injected with constructor injection:
  
  ```java
  // a constructor so that the Spring container can inject a MovieFinder
class SimpleMovieLister(private val movieFinder: MovieFinder) {
      // business logic that actually uses the injected MovieFinder is omitted...
  }
  ```
  
  The template of the basic constructor-based DI 
  
  ```xml
  <bean id="beanOne" class="x.y.ThingOne">
          <constructor-arg ref="beanTwo"/>
          <constructor-arg ref="beanThree"/>
  </bean>
  ```
  
  **Constructor Argument Resolution**
  
  Constructor argument resolution matching occurs by using the argument’s type. 
  
  Example:
  
  The class:
  
  ```java
  package x.y;
  
  public class ThingOne {
  
      public ThingOne(ThingTwo thingTwo, ThingThree thingThree) {
          // ...
      }
  }
  ```
  
  
  
  Full `xml`: 
  
  ```xml
  <beans>
      <bean id="beanOne" class="x.y.ThingOne">
          <constructor-arg ref="beanTwo"/>
          <constructor-arg ref="beanThree"/>
      </bean>
  	
      <bean id="beanTwo" class="x.y.ThingTwo"/>
  
      <bean id="beanThree" class="x.y.ThingThree"/>
  </beans>
  ```
  
  **Constructor argument type matching**
  
  
  
  ```xml
  <bean id="exampleBean" class="examples.ExampleBean">
      <constructor-arg type="int" value="7500000"/>
      <constructor-arg type="java.lang.String" value="42"/>
  </bean>
  ```
  
  **Constructor argument index**
  
  In addition to resolving the ambiguity of multiple simple values, specifying an index resolves ambiguity where a constructor has two arguments of the same type.
  
  ```xml
  <bean id="exampleBean" class="examples.ExampleBean">
      <constructor-arg index="0" value="7500000"/>
      <constructor-arg index="1" value="42"/>
  </bean>
  //	The index is 0-based.
  ```
  
  
  
  **Constructor argument name**
  
  For value disambiguation:
  
  ```xml
  <bean id="exampleBean" class="examples.ExampleBean">
      <constructor-arg name="years" value="7500000"/>
      <constructor-arg name="ultimateAnswer" value="42"/>
  </bean>
  ```
  
  **Take care**
  
  To make this work out of the box, your code must be compiled with the debug flag enabled so that Spring can look up the parameter name from the constructor.
  
  To not use debug. Use the [@ConstructorProperties](https://download.oracle.com/javase/8/docs/api/java/beans/ConstructorProperties.html) JDK annotation to explicitly name your constructor arguments
  
  ```java
  package examples;
  
  public class ExampleBean {
  
      // Fields omitted
  
      @ConstructorProperties({"years", "ultimateAnswer"})
      public ExampleBean(int years, String ultimateAnswer) {
          this.years = years;
          this.ultimateAnswer = ultimateAnswer;
      }
  }
  ```
  
  

- **Setter-based Dependency Injection**  (The preceding one is *Constructor-based Dependency Injection*)

  ​	The `ApplicationContext` supports constructor-based and setter-based DI for the beans it manages.

  ​	It also supports setter-based DI after some dependencies have already been injected through the constructor approach. (use Both of two)

  ​	Configure the dependencies in the form of a `BeanDefinition` which you use in conjunction with `PropertyEditor` instances to convert properties from one format to another.

  ​	However, most Spring users do not work with these classes directly (that is, programmatically) but rather with XML `bean` definitions, annotated components (that is, classes annotated with `@Component`, `@Controller`, and so forth), or `@Bean` methods in Java-based `@Configuration` classes. 

  ​	These sources are then converted internally into instances of `BeanDefinition` and used to load an entire Spring IoC container instance.  (将Spring user使用各种方式定义的bean definitions转换成 BeanDefinition实例)

  

  Template:

  ```xml
  <!-- setter injection using the nested ref element -->
      <property name="beanOne">
          <ref bean="anotherExampleBean"/>
      </property>
  
      <!-- setter injection using the neater ref attribute -->
      <property name="beanTwo" ref="yetAnotherBean"/>
      <property name="integerProperty" value="1"/>
  ```

  

  **Constructor-based or setter-based DI?**

  [Core Technologies (spring.io)](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-constructor-injection)

  The Spring team generally advocates constructor injection, as it lets you implement application components as immutable objects and ensures that required dependencies are not `null`







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





