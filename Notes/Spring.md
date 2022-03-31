## Spring Framework Overview

- use the [GitHub Issues](https://github.com/spring-projects/spring-framework/issues).

- Stack Overflow. Click [here](https://stackoverflow.com/questions/tagged/spring+or+spring-mvc+or+spring-aop+or+spring-jdbc+or+spring-r2dbc+or+spring-transactions+or+spring-annotations+or+spring-jms+or+spring-el+or+spring-test+or+spring+or+spring-remoting+or+spring-orm+or+spring-jmx+or+spring-cache+or+spring-webflux+or+spring-rsocket?tab=Newest) 

- Reference: 

  Design pattern: http://w3sdesign.com/index0100.php （一个很好的在线学习设计模式的网站）

  **Design Patterns: Elements of Reusable Object-Oriented Software.** 	                	                     

   Erich Gamma, Richard Helm, Ralph Johnson, John Vlissides. Published October 1994. Copyright © 1995 by Addison-Wesley.  (The authors of the book are commonly referred to as "GoF" or "Gang of Four".) 	                    

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

- Addition

  **Factory method pattern**:

  **Creational pattern:**https://en.wikipedia.org/wiki/Creational_pattern

  - Current Problem: Object creation could result in design problems or in added complexity to the design

  - Aim: To solve the Current Problem

  - Two dominant ideas: 

    ​	Encapsulating knowledge about which concrete classes the system uses Or

    ​	Hiding how instances of these concrete classes are created and combined

  - Categories: object-creational patterns(Object creation) and Class-creational patterns(Class-instantiation)

  ​	

  

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







