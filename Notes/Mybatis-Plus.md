资源：

官方网站:  [快速开始 | MyBatis-Plus (baomidou.com)](https://baomidou.com/pages/226c21/#配置)

github: [baomidou/mybatis-plus: An powerful enhanced toolkit of MyBatis for simplify development (github.com)](https://github.com/baomidou/mybatis-plus)

## 有趣的地方

中文开源项目中很好的一个项目，国产改进。成都的自由职业者做了很多生态圈的东西。

## 为什么使用它而不是Mybatis

[MyBatis-Plus (opens new window)](https://github.com/baomidou/mybatis-plus)（简称 MP）是一个 [MyBatis (opens new window)](https://www.mybatis.org/mybatis-3/)的增强工具，在 MyBatis 的基础上只做增强不做改变，为简化开发、提高效率而生。

![001](Mybatis-Plus/001.png)

### 特性

- **无侵入**：只做增强不做改变，引入它不会对现有工程产生影响，如丝般顺滑

- **损耗小**：启动即会自动注入基本 CURD，性能基本无损耗，直接面向对象操作

- **强大的 CRUD 操作**：内置通用 Mapper、通用 Service，仅仅通过少量配置即可实现单表大部分 CRUD 操作，更有强大的条件构造器，满足各类使用需求

- **支持 Lambda 形式调用**：通过 Lambda 表达式，方便的编写各类查询条件，无需再担心字段写错

- **支持主键自动生成**：支持多达 4 种主键策略（内含分布式唯一 ID 生成器 - Sequence），可自由配置，完美解决主键问题

- **支持 ActiveRecord 模式**：支持 ActiveRecord 形式调用，实体类只需继承 Model 类即可进行强大的 CRUD 操作

- **支持自定义全局通用操作**：支持全局通用方法注入（ Write once, use anywhere ）

- **内置代码生成器**：采用代码或者 Maven 插件可快速生成 Mapper 、 Model 、 Service 、 Controller 层代码，支持模板引擎，更有超多自定义配置等您来使用

- **内置分页插件**：基于 MyBatis 物理分页，开发者无需关心具体操作，配置好插件之后，写分页等同于普通 List 查询

- **分页插件支持多种数据库**：支持 MySQL、MariaDB、Oracle、DB2、H2、HSQL、SQLite、Postgre、SQLServer 等多种数据库

- **内置性能分析插件**：可输出 SQL 语句以及其执行时间，建议开发测试时启用该功能，能快速揪出慢查询

- **内置全局拦截插件**：提供全表 delete 、 update 操作智能分析阻断，也可自定义拦截规则，预防误操作

  

### 框架结构

![002](Mybatis-Plus/002.jpg)

## 快速入门

​	搭环境  -> 配置 ->  测试

​	application.properties 和 application.yml有什么不同。你理解了吗？

https://www.baeldung.com/spring-boot-yaml-vs-properties

这两个的作用是什么？

​	他们俩都是Spring的外部配置文件（外部配置手段不只这两种）。好处：在不同环境下使用相同代码也可以生效。 兼容性，匹配性。 可以修改SpringBoot自动配置的默认值，之前的是SpringBoot给我们配置好了。

​	定义很绕，可以搜一下。

​	以前的配置文件使用xml来配置，对比yaml和xml配置端口。

```yml
server:
	port: 8080
```

```xml
<server>
	<port>8081</port>
</server>
```

yaml的轻巧，使用键值对的形式。

yaml可以和properties共存吗？ 答案是可以的，他们俩有优先级顺序。 yaml > properties 