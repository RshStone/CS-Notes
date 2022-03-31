# Mybatis

## **What is Mybatis**

- 第一个支持自定义sql，存储过程，高级映射的持久层框架

- eliminates almost all of the JDBC code and manual setting of parameters and retrieval of results 

  减少了几乎所有的JDBC代码和人为的参数配置，解放了配置

- use [ simple XML or Annotations for configuration and map primitives, Map interfaces and Java POJOs (Plain Old Java Objects) ] to database records   

  使用Map接口和Java POJOs去数据库记录

## **Get Started**

**Building SqlSessionFactory from XML**

- MyBatis application centers around an instance of SqlSessionFactory. A SqlSessionFactory instance can be acquired by using the SqlSessionFactoryBuilder.    

  MyBatis应用核心围绕着SqlSessionFactory，SqlSessionFactory实例可以使用SqlSessionFactoryBuilder来获得。

- SqlSessionFactoryBuilder can build a SqlSessionFactory instance from an XML configuration file, or from a custom prepared instance of the Configuration class  

  SqlSessionFactoryBuilder 能够从XML配置文件或者从预先配置好的Configuration类的实例获得。

- From XML configuration file

  ```java
  String resource = "org/mybatis/example/mybatis-config.xml";
  InputStream inputStream = Resources.getResourceAsStream(resource);
  SqlSessionFactory sqlSessionFactory =
    new SqlSessionFactoryBuilder().build(inputStream);
  ```

  ```xml
  <?xml version="1.0" encoding="UTF-8" ?>
  <!-- validate the XML document. -->
  <!DOCTYPE configuration
    PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
    "http://mybatis.org/dtd/mybatis-3-config.dtd">
  <!-- The body of the environment element contains the environment configuration for transaction management and connection pooling -->
  <configuration>
    <environments default="development">
      <environment id="development">
        <transactionManager type="JDBC"/>
        <dataSource type="POOLED">
          <property name="driver" value="${driver}"/>
          <property name="url" value="${url}"/>
          <property name="username" value="${username}"/>
          <property name="password" value="${password}"/>
        </dataSource>
      </environment>
    </environments>
      
    <!-- The mappers element contains a list of mappers -->
    <mappers>
      <mapper resource="org/mybatis/example/BlogMapper.xml"/>
    </mappers>
  </configuration>
  ```



**Building SqlSessionFactory without XML**

- ```java
  DataSource dataSource = BlogDataSourceFactory.getBlogDataSource();
  TransactionFactory transactionFactory =
    new JdbcTransactionFactory();
  Environment environment =
    new Environment("development", transactionFactory, dataSource);
  Configuration configuration = new Configuration(environment);
  configuration.addMapper(BlogMapper.class);
  SqlSessionFactory sqlSessionFactory =
    new SqlSessionFactoryBuilder().build(configuration);
  ```

  

- **Acquiring a SqlSession from SqlSessionFactory**

  **Previous version**

  ```java
  try (SqlSession session = sqlSessionFactory.openSession()) {
    Blog blog = session.selectOne(
      "org.mybatis.example.BlogMapper.selectBlog", 101);
  }
  ```

  **Use BlogMapper Interface**

  ```java
  try (SqlSession session = sqlSessionFactory.openSession()) {
    BlogMapper mapper = session.getMapper(BlogMapper.class);
    Blog blog = mapper.selectBlog(101);
  }
  ```

  

- ### Exploring Mapped SQL Statements

  **1: xml**

  ```xml
  <?xml version="1.0" encoding="UTF-8" ?>
  <!DOCTYPE mapper
    PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
    "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
  <mapper namespace="org.mybatis.example.BlogMapper">
    <select id="selectBlog" resultType="Blog">
      select * from Blog where id = #{id}
    </select>
  </mapper>
  ```

  +Test 调用的Code

  ```java
  //方式一, 优先选择方式一 why? --> 省去了写Mapper和Mapper方法的过程
  BlogMapper mapper = session.getMapper(BlogMapper.class);
  Blog blog = mapper.selectBlog(101);
  ```

  ```java
  //方式二
  Blog blog = session.selectOne(
    "org.mybatis.example.BlogMapper.selectBlog", 101);
  ```

  **2: java annotations**

  ```java
  package org.mybatis.example;
  public interface BlogMapper {
    @Select("SELECT * FROM blog WHERE id = #{id}")
    Blog selectBlog(int id);
  }
  ```

  Pros:  a lot cleaner for simple statements

  Cons: Java Annotations are both limited and messier for more complicated statements. 

   

## Configuration  XML

- configuration

  - [properties](https://mybatis.org/mybatis-3/configuration.html#properties)

  - [settings](https://mybatis.org/mybatis-3/configuration.html#settings)

  - [typeAliases](https://mybatis.org/mybatis-3/configuration.html#typeAliases)

  - [typeHandlers](https://mybatis.org/mybatis-3/configuration.html#typeHandlers)

    A type alias is simply a shorter name for a Java type. 

    Reduce redundant typing of fully qualified classnames

    ```xml
    <typeAliases>
      <typeAlias alias="Author" type="domain.blog.Author"/>
      <typeAlias alias="Blog" type="domain.blog.Blog"/>
      <typeAlias alias="Comment" type="domain.blog.Comment"/>
      <typeAlias alias="Post" type="domain.blog.Post"/>
      <typeAlias alias="Section" type="domain.blog.Section"/>
      <typeAlias alias="Tag" type="domain.blog.Tag"/>
    </typeAliases>
    ```

  - [objectFactory](https://mybatis.org/mybatis-3/configuration.html#objectFactory)

  - [plugins](https://mybatis.org/mybatis-3/configuration.html#plugins)

  - [environments](https://mybatis.org/mybatis-3/configuration.html#environments)

    - environment
      - transactionManager
      - dataSource

  - [databaseIdProvider](https://mybatis.org/mybatis-3/configuration.html#databaseIdProvider)

  - [mappers](https://mybatis.org/mybatis-3/configuration.html#mappers)

## Mapper XML Files

[mybatis – MyBatis 3 | Mapper XML Files](https://mybatis.org/mybatis-3/sqlmap-xml.html)

The true power of MyBatis: see a savings of 95% of the code; was built to focus on the SQL

The Mapper XML files have only a few first class elements (in the order that they should be defined):

- `cache` – Configuration of the cache for a given namespace.
- `cache-ref` – Reference to a cache configuration from another namespace.
- `resultMap` – The most complicated and powerful element that describes how to load your objects from the database result sets.
- `parameterMap` – Deprecated! Old-school way to map parameters. Inline parameters are preferred and this element may be removed in the future. Not documented here.
- `sql` – A reusable chunk of SQL that can be referenced by other statements.
- `insert` – A mapped INSERT statement.
- `update` – A mapped UPDATE statement.
- `delete` – A mapped DELETE statement.
- `select` – A mapped SELECT statement.

## Dynamic SQL

**Cause:** How painful it is to conditionally concatenate strings of SQL together with JDBC or any similar framework.

**Result:** So that someone creates Dynamic SQL which can be downright painful to deal with.

MyBatis employs powerful OGNL based expressions(?) to eliminate most of the other elements:

- if
- choose (when, otherwise)
- trim (where, set)
- foreach

OGNL: Object-Graph Navigation Language (OGNL) is **an open-source Expression Language (EL) for Java**, which, while using simpler expressions than the full range of those supported by the Java language, allows getting and setting properties (through defined setProperty and getProperty methods, found in JavaBeans), and execution.  （简单理解的方式）

**If**

```xml
<select id="findActiveBlogWithTitleLike"
     resultType="Blog">
  SELECT * FROM BLOG
  WHERE state = ‘ACTIVE’
  <if test="title != null">
    AND title like #{title}
  </if>
</select>
```

Performance: 

​	provide an optional text search type of functionality

​	If you passed in no title, then all active Blogs would be returned. 

​	But if you do pass in a title, it will look for a title like that

## Java API

- [Directory Structure](https://mybatis.org/mybatis-3/java-api.html#directoryStructure)

- [SqlSessions](https://mybatis.org/mybatis-3/java-api.html#sqlSessions)

  

### SqlSessions

*The SqlSessionFactoryBuilder* ----- build(XML, annotations or hand coded Java configuration)  ----->  *The SqlSessionFactory* ----- contains methods for different ways -----------> *The SqlSession*

**SqlSessionFactoryBuilder**

contains the method to build *SqlSessionFactory*. 

```java
SqlSessionFactory build(InputStream inputStream)
SqlSessionFactory build(InputStream inputStream, String environment)
SqlSessionFactory build(InputStream inputStream, Properties properties)
SqlSessionFactory build(InputStream inputStream, String env, Properties props)
SqlSessionFactory build(Configuration config)
```