## jQuery

### 书城第一阶段

- 给注册绑定单击事件

- 验证用户名、密码、确认密码、邮箱验证、验证码

  具体步骤：

  1. 通过 `$("").val()` 获取对象
  2. 验证格式转为正则表达式对象/ /
  3. 利用正则表达 *.test()*判断

  几个注意的地方：

  - 邮箱验证正则表达
  - 验证码动态来自于服务器

## XML

- 什么是XML？

  可扩展性标记性语言

- 作用
  1. 用来保存数据,数据具有自我描述性
  2. 可作为项目模块的配置文件
  3. 还可以作为网络传输数据的格式（现在JSON为主）

- 语法
  1. 文档声明
  2. 元素（标签）
  3. xml属性
  4. xml注释
  5. 文本区域（CDATA区）

- 技巧：浏览器能帮你校验

## Servlet

- 创建Servlet程序

  2020后的版本创建普通module然后右键Add FrameWork Support。再选择WebApplication

  然后就可以create new servlet

- Servlet-url地址定位到Servlet程序的访问

  browser To mapping-url To mapping-servlet-name To servlet-servlet-name To servlet-servlet-class 

- Servlet生命周期

  1. `constructor`

  2. `init`

     1 and 2 分别执行一次

  3. service方法

     访问一次执行一次

  4. destroy

     终止时执行

- 请求的分发处理

  对于get请求和post请求采用不同方式分别执行

  获取请求方式：采用`ServletRequest`下的子类`HttpServletRequest`中的`getMethod()`方法获取请求方式

- 继承`HttpServlet`类的方式去实现`Servlet`程序
  1. 继承`HttpServlet`类的方式去实现`Servlet`程序
  2. 根据业务请求重写`doGet`或者`doPost`方法
  3. `web.xml`中配置`Servlet`程序的访问地址

-  使用IDEA生成Servlet程序
  - 不使用Java EE6+
  - 配置信息

- 整个Servlet类的继承体系

   Interface 

  <-- Class `GenericServlet` （做了很多空实现，持有`ServletConfig`类的引用）

  <-- Class `HttpServlet`(实现了service()方法，并实现了分发请求处理,`doGet`,`doPost`负责抛异常，不支持请求) 

  <-- 自定义的Servlet程序:我们根据业务需要去重写`doGet`,`doPost`方法

- `ServletConfig`类(**视频未完全看懂**)

  Servlet配置信息,每个Servlet程序都有自己的`ServletConfig`，但获取只能获取自己的

  - 三大作用:

    1、可以获取 Servlet 程序的别名 servlet-name 的值
    2、获取初始化参数 `init`-`param`
    3、获取 `ServletContext` 对象

- `ServletContext`类

  是什么

  1. 接口，上下文对象

  2. 一个web工程，只有一个`ServletContext`对象实例

  3. 域对象(存取数据的操作范围（像Map）)

     存`setAttribute()` `getAttribute`()  `removeAttribute`()

     范围指的是整个web工程

  4. `ServletContext` 是在 web 工程部署启动的时候创建。在 web 工程停止的时候销毁。

  存储数据

  - `getServletContext()` 

    return `getServletConfig().getServletContext()`

- Http协议

  - 什么是Http协议：客户端和服务端通信时，发送数据需要遵守的规则,协议中的数据叫报文

  - 格式

    客户端——请求(GET和POST)

    服务端——响应

    - GET请求:

      请求行：

      ​	请求方式：GET

      ​	资源路径

      ​	协议版本号 HTTP/1.1

      请求头：

      ​	key: value 

    - POST请求：

      请求行：

      ​	请求方式：POST

      ​	资源路径

      ​	协议版本号 HTTP/1.1

      请求头：

      ​	key: value 

      ​	**空行**

      请求体：发送给服务器的数据

    - 常见请求分别

      GET 请求有哪些：
      1、form 标签 method=get
      2、a 标签
      3、link 标签引入 css
      4、Script 标签引入 js 文件
      5、img 标签引入图片
      6、iframe 引入 html 页面
      7、在浏览器地址栏中输入地址后敲回车
      POST 请求有哪些：
      8、form 标签 method=post

    - 响应的HTTP协议格式

      1、响应行
      (1)响应的协议和版本号
      (2)响应状态码
      (3)应状态描述符
      2、响应头
      (1)key : value 不同的响应头，有其不同含义
      **空行**
      3、响应体 --->>>  就是回传给客户端的数据

    - 常见的响应码

      200 表示请求成功
      302 表示请求重定向（明天讲）
      404 表示请求服务器已经收到了，但是你要的数据不存在（请求地址错误）
      500 表示服务器已经收到请求，但是服务器内部错误（代码错误）

    - MIME 类型说明

      MIME 是 HTTP 协议中数据类型。
      MIME 的英文全称是"Multipurpose Internet Mail Extensions" 多功能 Internet 邮件扩充服务

- `HttpServletRequest`类

  - 作用

    请求——服务器（封装解析）——`Request`对象——`service`方法

  - 类的常用方法