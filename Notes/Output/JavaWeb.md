## 书城第一阶段

- 给注册绑定单击事件

- 验证用户名、密码、确认密码、邮箱验证、验证码

  具体步骤：

    1. 通过 `$("").val()` 获取对象
    2. 验证格式转为正则表达式对象/ /
    3. 利用正则表达 *.test()*判断

  几个注意的地方：

    - 邮箱验证正则表达
    - 验证码动态来自于服务器

## 书城第二阶段

- `JavaEE`项目的三层框架

  ![image-20210418124226091](https://raw.githubusercontent.com/RshStone/CS-Notes/master/Notes/JavaWeb/001.png)

  分层的目的是为了解耦。解耦就是为了降低代码的耦合度。方便项目后期的维护和升级。

  ![image-20210418124703440](https://raw.githubusercontent.com/RshStone/CS-Notes/master/Notes/JavaWeb/002.png)

- 开发代码角度开发流程

  先创建书城需要的数据库和表

  id、用户名、密码、邮箱

  编写数据库表对应的 JavaBean 对象

  编写工具类 `JdbcUtils` `（这块代码比较固定，三部分static、getConnection, close）`

  i. 添加价包，有箭头标记的表示可以直接使用，两种添加方式

    1. WEB-INF下创建lib，复制价包,

       打开`File`下`Project Settings`下的`Library`导入价包到`Module`，

       在`Module`下选择你想要添加的具体模块，''依赖''添加`Library`

       选择`Artifacts`中的`Fix`

       `Apply` `Ok`

       有标记的价包表示可以使用

    2. jar包那右键`add as library`

  ii. 读取`jdbc.properties`属性配置文件

  iii. 从流中加载数据

  iv. 创建数据库连接池

  编写 `BaseDao`

  导包

  `dbutils`下的`queryRunner`类 Insert\Update\Delete 语句

  泛型 <T>T

  query时传进去参数 `(Class<T>type, String sql, Object...args)`

  ```java
  @param type 返回的对象类型
   * @param sql
  执行的 sql 语句
   * @param args sql 对应的参数值
   * @param <T>
  返回的类型的泛型
  ```

  ```java
  //利用queryRunner执行的语句
  queryRunner.query(connection,sql, new BeanListHandler<T>(type),args);
  //一行 new BeanListHandler<T>(type)
  //多行 new BeanListHandler<T>(type)
  //一行一列 new ScalarHandler()
  
  ```

  编写 `UserDao` 和测试

    - 构造器需要一个空的

    - `sql`语句注意``符号而不是''

    - ```java
    //能直接查看方法的功能，参数，返回值和说明
    /**
    * 登录
    * @param user
    * @return 如果返回 null，说明登录失败，返回有值，是登录成功
    */
    ```

编写 `UserService` 和测试

- `UserService`接口 一个业务一个方法 （登录、注册、查看）

- `UserServiceImpl`具体实现类，涉及数据库操作

- 快速生成`Test`, (Ctrl + Shift + T)

编写 `web` 层

1. 实现用户注册的功能

   `RegisterServlet`程序获取参数，检查是否正确

   ![image-20210419195256837](https://raw.githubusercontent.com/RshStone/CS-Notes/master/Notes/JavaWeb/003.png)

    - web阶段使用：base+相对
    - 框架阶段：绝对路径

2. 实现用户登录功能

## 书城第三阶段

- 页面`jsp`动态化

  1、在 html 页面顶行添加 page 指令。 2、修改文件后缀名为：`.jsp`
  3、使用 IDEA 搜索替换.html 为`.jsp`(快捷键：Ctrl+Shift+R)

- 抽取页面中相同内容

    - 在 `web`下的page下新建一个 `common`然后根据相同信息的类别进行分类(别的地方使用类似格式进行引用

      ```jsp
      <%@include file="/pages/common/footer.jsp"%>
      ```

      )

      `head.jsp`: base css script（直接copy即可）

      ```
      <%
          String basePath = request.getScheme()
                  + "://"
                  + request.getServerName()
                  + ":"
                  + request.getServerPort()
                  + request.getContextPath()
                  + "/";
      %>
          <base href=<%= basePath%>>
      ```

      `footer.jsp`

      `login_success_menu.jsp`

      `manager_menu.jsp`

- 登录，注册错误提示，及表单回显

    1. HTTP Status 500过程错误

  注意file = ""引号里面的空格问题

  ![image-20210508135945655](C:/Users/ASUS/AppData/Roaming/Typora/typora-user-images/image-20210508135945655.png)

    2. 相对路径使用不成功

       使用`jsp`静态包含后使用相对路径不成功

       `index.jsp`在`web`目录下，为什么`book/web/index.jsp`不成功

       `index.jsp`里的

       ```
       类似这种
       <a href="../../index.jsp">注销</a>&nbsp;&nbsp;
       <a href="../../index.jsp">返回</a>
       ```

       `login_success_menu.jsp`里的`<a href="../order/order.jsp">我的订单</a>`

       查看文件树: tree命令

- 代码优化

    1. `UserServlet`程序

       register, login belong to user module. 合并到`UserServlet`程序中

    2. 用户模块使用反射优化

       除了注册和登录还有其他比如添加用户，修改用户信息，修改密码等等

    3. 抽取`BaseServlet`程序(除了`UserServlet`程序外可能还会有`BookServlet`等模块)

       获取action参数值

       通过反射获取action对应的业务方法

       通过反射调用业务方法

- `BeanUtils`工具类的使用

  (报错最好版本降到和老师的一致)

  可以一次性把所有请求参数传到`JavaBean`对象中

  第三方工具类，需要导包

  Ctrl + Alt + T 可以选择抛异常等内容

  調用過程中調用了`set`方法，`EL`取值調用了`get`方法

  ```java
  //将1改成2
  public static void copyParamToBean(HttpServletRequest req, Object bean) //1
  public static void copyParamToBean(Map value, Object bean) //2 更为优雅
  //将Map(键值对)内容注入到bean对象中很常见
  //1有什么问题？
  //HttpServletRequest 或者是Servlet是Web层所独有的，service业务层，dao层没有，导致程序的耦合度高（设计小细节）
      
  ```

  ```java
  public static Object copyParamToBean(Map value, Object bean)
  User user = (User) WebUtils.copyParamToBean(req.getParameterMap(), new User());
  使用汎型
  public static <T>  T copyParamToBean(Map value, T bean)
  User user =  WebUtils.copyParamToBean(req.getParameterMap(), new User());  
  ```

## 书城第四阶段

使用EL表达式 修改表单回显

```jsp
<%=request.getAttribute("msg")==null?"":request.getAttribute("msg")%>
换成
${requestScope.msg}  <%--EL表达式--%>
```

## 书城第五阶段

- MVC概念

  Model 模型, View视图， Controller控制器

  MVC 最早出现在 JavaEE 三层中的 Web 层，它可以有效的指导 Web 层的代码如何有效分离，单独工作。 View 视图：只负责数据和界面的显示，不接受任何与显示数据无关的代码，便于程序员和美工的分工合作——
  JSP/HTML。 Controller 控制器：只负责接收请求，调用业务层的代码处理请求，然后派发页面，是一个“调度者”的角色——Servlet。 转到某个页面。或者是重定向到某个页面。 Model
  模型：将与业务逻辑相关的数据封装为具体的 JavaBean 类，其中不掺杂任何与数据处理相关的代码—— JavaBean/domain/entity/pojo。 MVC 是一种思想 MVC
  的理念是将软件代码拆分成为组件，单独开发，组合使用（目的还是为了降低耦合度）。

- 图书模块

    1. 编写图书模块的数据库表

       Generator shortcut Alt + Insert


2. 编写图书模块的JavaBean


3. 编写图书模块的Dao和测试Dao

     ```java
     //updateDao测试结果未解决bug
     ava.sql.SQLException: Unknown column 'img_path=' in 'field list' Query: update t_book set `name`=?,`author`=?,`price`=?,`sales`=?,`stock`=?,`img_path=`=? where id = ? Parameters: [大家都很搞笑!, Justin, 9999, 1100, 0, static/img/default.jpg, 22]
     ```

4. 编写图书模块的Service和测试Service

   模块关系。DAO查出基本数据，Service对数据进行操作，再传给Controller


5. 编写图书模块的Web层和页面联调测试

   ![image-20210509164742722](https://raw.githubusercontent.com/RshStone/CS-Notes/master/Notes/JavaWeb/007.png)

   为什么加manager?

   ```jsp
       <servlet>
           <servlet-name>BookServlet</servlet-name>
           <servlet-class>com.atguigu.web.BookServlet</servlet-class>
       </servlet>
       <servlet-mapping>
           <servlet-name>BookServlet</servlet-name>
           <url-pattern>/manager/bookServlet</url-pattern>
           <!--方便权限管理加了manager-->
       </servlet-mapping>
   ```

   前台: 普通用户使用 地址: `/client/bookServlet`

   后台：管理员使用 地址：`/manager/bookServlet`

    - 添加

      ![image-20210510142016615](https://raw.githubusercontent.com/RshStone/CS-Notes/master/Notes/JavaWeb/008.png)

      bug

      ```java
      req.getRequestDispatcher("/manager/bookServlet?action=list").forward(req,resp);
      //按下F5后用户请求会被重复记录
      使用重定向
      resp.sendRedirect(req.getContextPath() + "/manager/bookServlet?action=list");
      ```

    - 删除

      ![image-20210510144605363](https://raw.githubusercontent.com/RshStone/CS-Notes/master/Notes/JavaWeb/009.png)

      用户不小心删错了怎么办？——加一个标签提醒框

      ```javascript
      <script type="text/javascript">
              $(function (){
                  //给删除的a标签绑定单击事件，用于删除的确认提示操作
                  $("a.deleteClass").click(function (){
                      return confirm("你确定要删除【" + $(this).parent().parent().find("td:first").text() + "】?");
                  });
              });
          </script>
      ```

     - 修改
     
       ![010](https://raw.githubusercontent.com/RshStone/CS-Notes/master/Notes/JavaWeb/010.png)
     
       i. 数据回显到表单之中
     
       ii. 提交给服务器保存修改
       
       找很久的bug,封装bean对象时id没有封装上去，显示为0
       
       三个错误，我犯的
       
       id = NULL ,`daoImpl`里面get没有设置`selet id`
       
       `img_path= ?`写成了`img_path= = ?`
       
       ```jsp
       "/manager/bookServlet?action = list"
       //引号里的space 需要注意
       ```
       
       找bug时的问题，对于老师项目代码的配置问题，Tomcat(导入Artifact)——Project Structure的每一个部分

- 图书分页

    - 一般不会把数据全部一次性读取而是采用分页的方式，每页大概显示4条

    - 分页的流程

      ![image-20210512144008526](https://raw.githubusercontent.com/RshStone/CS-Notes/master/Notes/JavaWeb/011.png)

      分页可以是图书分页，用户分页，商家分页等等。所以采用泛型

      写的时候的错误: Number Format Exception

      ​ 弹幕给的一种思路：把`queryForPageTotalCount`返回值转为`Long`再转为`String`再转为`Integer`

    - 完善加首页，上页，下页，末页

    - 分页模块跳转到指定页数功能实现

      给按钮榜上单击事件+跳到指定页码

      数据边界检查可以放到`Page.java`里，反复使用

    - 分页模块中，页码1，2，3，4，5的显示

      需求：显示5个连续的页码，而且当前页码在中间。除了当前页码之外，每个页码都可以点击跳到指定页。

      i. 如果总页码小于等于5——页码范围：1-总页码

      ​ e.g. 3页 1, 2, 3

      ii. 总页码大于5的情况。假设一共10页

      ​ situation1: 当前页码为前面3个：1, 2, 3的情况——页码范围：1-5

      ​ 【1】,2,3,4,5

      ​ 1,【2】,3,4,5

      ​ 1,2,【3】,4,5

      ​ situation2: 当前页码为最后3个， 8, 9, 10，页码范围是：总页码减4-总页码

      6,7,【8】,9,10

      6,7,8,【9】,10

      6,7,8,9,【10】

      ​ situation3: 4,5,6,7,页码范围是：当前页码减2-当前页码加2

  5.12运行bug + 5.13解决

    - 分页对添加、修改、删除的影响

    - 前台分页的初步实现

      ![image-20210513141414473](https://raw.githubusercontent.com/RshStone/CS-Notes/master/Notes/JavaWeb/012.png)

      敲代码时的bug——`web/index.jsp`中的`jstl`不生效

      ![image-20210513151455736](https://raw.githubusercontent.com/RshStone/CS-Notes/master/Notes/JavaWeb/013.png)

      原因：没有完全理解`web/index.jsp`和`page//client/index.jsp`的作用。把二者代码写反了

      首页和尾页的Bug，不能显示。  `PageNo` 重新 `set`一下

    - 分页条的抽取

      前台和后台的分页条几乎一样，把它们抽取放到`Page`方法里

    - 价格区间搜索并分页的分析

      思路分析：

      ![image-20210513160905932](https://raw.githubusercontent.com/RshStone/CS-Notes/master/Notes/JavaWeb/014.png)

      50min写尝试自己写业务，challenging but interesting!!! 虽然没写出来多少

      `client.index.jsp` 需要把它的page地址改一改再加上隐藏域(用户看不到，`view page source`可以看到)

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

  2020后的版本创建普通module然后右键`Add` `FrameWork` `Support`。再选择`WebApplication`

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

- 使用IDEA生成Servlet程序
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

      1、可以获取 Servlet 程序的别名 servlet-name 的值 2、获取初始化参数 `init`-`param`
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

          ​ 请求方式：GET

          ​ 资源路径

          ​ 协议版本号 HTTP/1.1

          请求头：

          ​ key: value

        - POST请求：

          请求行：

          ​ 请求方式：POST

          ​ 资源路径

          ​ 协议版本号 HTTP/1.1

          请求头：

          ​ key: value

          ​    **空行**

          请求体：发送给服务器的数据

        - 常见请求分别

          GET 请求有哪些： 1、form 标签 method=get 2、a 标签 3、link 标签引入 css 4、Script 标签引入 js 文件 5、img 标签引入图片 6、iframe 引入 html 页面
          7、在浏览器地址栏中输入地址后敲回车 POST 请求有哪些： 8、form 标签 method=post

        - 响应的HTTP协议格式

          1、响应行
          (1)响应的协议和版本号
          (2)响应状态码
          (3)应状态描述符 2、响应头
          (1)key : value 不同的响应头，有其不同含义
          **空行**
          3、响应体 --->>>  就是回传给客户端的数据

        - 常见的响应码

          200 表示请求成功 302 表示请求重定向（明天讲） 404 表示请求服务器已经收到了，但是你要的数据不存在（请求地址错误） 500 表示服务器已经收到请求，但是服务器内部错误（代码错误）

          405

          ```
          The 405 (Method Not Allowed) status code indicates that the method
             received in the request-line is known by the origin server but not
             supported by the target resource.  The origin server MUST generate an
             Allow header field in a 405 response containing a list of the target
             resource's currently supported methods
          ```

        - MIME 类型说明

          MIME 是 HTTP 协议中数据类型。 MIME 的英文全称是"Multipurpose Internet Mail Extensions" 多功能 Internet 邮件扩充服务

- `HttpServletRequest`类

    - 作用

      请求——服务器（封装解析）——`Request`对象——`service`方法

    - 类的常用方法

      i. `getRequestURI`() 获取请求的资源路径 ii. `getRequestURL`() 获取请求的统一资源定位符（绝对路径） iii. `getRemoteHost`() 获取客户端的 ip 地址
      iv. `getHeader`() 获取请求头 v. `getParameter`() 获取请求的参数 vi.`getParameterValues`() 获取请求的参数（多个值的时候使用） vii. `getMethod`()
      获取请求的方式 GET 或 POST viii. `setAttribute`(key, value); 设置域数据 ix. `getAttribute`(key); 获取域数据
      x. `getRequestDispatcher`() 获取请求转发对象

      中文乱码问题：`setCharacterEncoding("UTF-8")`

    - 实践遇到的错误

      `web`.`xml`文件在进行类解析时，`servlet` 和 `servletII`下`src`下的 `directory`的 `com.atguigu.servlet`名字一样，具体解析过程不清楚

    - 路径

      **相对路径是**： . 表示当前目录 .. 表示上一级目录 资源名 表示当前目录/资源名
      **绝对路径**：
      http://ip:port/工程路径/资源路径 在实际开发中，路径都使用绝对路径，而不简单的使用相对路径。 1、绝对路径 2、base+相对

    - /斜杠对应的不同含义

      / 斜杠 如果被服务器解析，得到的地址是：http://ip:port/工程路径

      / 斜杠 如果被浏览器解析，得到的地址是：http://ip:port/

- `HttpServletResponse`类

    - 作用

      每次请求进来，`Tomcat` 服务器都会创建一个 `Response` 对象传递给 `Servlet` 程序去使用。

    - 两个输出流的说明

      字节流`getOutputStream`(); 常用于下载（传递二进制数据） 字符流`getWriter`();常用于回传字符串（常用）

    - 往客户端回传数据

    - 乱码解决

        1. `服务器setCharacterEncoding("UTF-8")`+浏览器通过响应头(`resp.setHeader`("Content-Type", "text/html; charset=UTF-8"))
           （不推荐!!!）

        2. `resp.setContentType`("text/html; charset=UTF-8")

           它会同时设置服务器和客户端都使用 UTF-8 字符集，还设置了响应头 此方法一定要在获取流对象之前调用才有效

    - 请求重定向

      请求重定向，是指客户端给服务器发请求，然后服务器告诉客户端说。我给你一些地址。你去新地址访问。

## JSP

1. ### 什么是`jsp`, 有什么用

   `jsp`: java server pages, Java的服务器页面

   主要作用代替`Servlet程序`回传html页面数据

   `servlet`程序回传html页面过程繁琐，开发成本、维护成本高

2. ### `jsp`语法

    - 头部文件声明

      `<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" %>`
      这是 `jsp` 文件的头声明。表示这是 `jsp` 页面。
      `language` 属性值只能是 java。 表示翻译的得到的是 java 语言的
      `contentType` 属性 设置响应头 `contentType` 的内容
      `pageEncoding` 属性 设置当前 `jsp` 页面的编码
      `import` 属性 给当前 `jsp` 页面导入需要使用的类包
      `autoFlush` 属性 设置是否自动刷新 out 的缓冲区，默认为 true
      `buffer` 属性 设置 out 的缓冲区大小。默认为 8KB
      `errorPage` 属性 设置当前 `jsp` 发生错误后，需要跳转到哪个页面去显示错误信息
      `isErrorPage` 属性 设置当前 `jsp` 页面是否是错误页面。是的话，就可以使用 `exception` 异常对象
      `session` 属性 设置当前 `jsp` 页面是否获取 `session` 对象,默认为 `true`
      `extends` 属性 给服务器厂商预留的 `jsp` 默认翻译的 servlet 继承于什么类

    - 脚本

        1. 声明脚本

           声明脚本格式如下：
           `<%!`
           `java 代码`
           `%>`
           在声明脚本块中，我们可以干 4 件事情 1.我们可以定义全局变量。 2.定义 static 静态代码块 3.定义方法 4.定义内部类 几乎可以写在类的内部写的代码，都可以通过声明脚本来实现

        2. 表达式脚本

           表达式脚本格式如下：
           `<%=表达式`
           `%>`
           表达式脚本 用于向页面输出内容。 表达式脚本 翻译到 `Servlet` 程序的 `service` 方法中 以 `out.print`() 打印输出
           `out` 是 `jsp` 的一个内置对象，用于生成 html 的源代码 注意：表达式不要以分号结尾，否则会报错 表达式脚本可以输出任意类型。 比如： 1.输出整型 2.输出浮点型 3.输出字符串 4.输出对象

        3. 代码脚本

           代码脚本如下：
           `<%`
           `java 代码`
           `%>`
           代码脚本里可以书写任意的 java 语句。 代码脚本的内容都会被翻译到 service 方法中。 所以 service 方法中可以写的 java 代码，都可以书写到代码脚本中

    - 三种注释

      // 单行 java 注释 /*
      多行 java 代码注释
      */ 单行注释和多行注释能在翻译后的 java 源代码中看见。
      <%-- jsp 注释 --%>
      `jsp` 注释在翻译的时候会直接被忽略掉
      <!-- html 注释 -->
      “玩转”Java 系列 html 的注释会被翻译到 java 代码中输出到 html 页面中查看

    - `jsp`九大内置对象

      `jsp`内置对象是指`Tomcat`在翻译`jsp`页面成为`servlet`源码后，内部提供的九大对象。

      `request` 对象 请求对象，可以获取请求信息
      `response` 对象 响应对象。可以设置响应信息
      `pageContext` 对象 当前页面上下文对象。可以在当前上下文保存属性信息
      `session` 对象 会话对象。可以获取会话信息。
      `exception` 对象 异常对象只有在 `jsp` 页面的 page 指令中设置 `isErrorPage=`"true" 的时候才会存在
      `application` 对象 `ServletContext` 对象实例，可以获取整个工程的一些信息。
      `config` 对象 `ServletConfig` 对象实例，可以获取 `Servlet` 的配置信息
      `out` 对象 输出流。
      `page` 对象 表示当前 `Servlet` 对象实例（无用，用它不如使用 this 对象）

    - `jsp`四大域对象

      `PageContext`(`PageContextImpl`类)、 同一个`jsp`文件

      `request` (`HttpServletRequest`类)、一次请求(同一个URL )

      session (`HttpSession类`)、同一个浏览器

      application (`ServletContext`类)、同一个服务器

      可以存储对象，优先顺序

      `pageContext` ===>> `request` ===>> `session` ===>> `application`

    - `jsp`常用标签

        1. 静态包含(最常用)

           `JavaEE`技术使用进行改变，主要用它做输出

           ```jsp
           <%@include file="footer.jsp"%>
           ```

           一旦单独监听界面，改一处，其他都修改

     2. 动态包含（功能丰富、可传参）

        传进去`JspRuntimeLibrary.include` 方法

        ```jsp
        <jsp:include page=""></jsp:include>
        ```

        

     3. 页面转发（与`req.getRequestDispatcher()功能一致`）

        ```jsp
        <jsp:forward page=""></jsp:forward>
        ```

- `servlet` + `jsp` 整个流程

  ![image-20210420193324931](https://raw.githubusercontent.com/RshStone/CS-Notes/master/Notes/JavaWeb/004.png)

- `Listener`监听器(三大组件之一) 讲spring时具体介绍

  是`JavaEE`的规范，也就是接口

  监听器的作用是，监听某种事物的变化。然后通过回调函数，反馈给客户（程序）去做一些相应的处理

    - `ServletContextListener`监听器

      监听`ServletContext`对象的创建和销毁

      调用方法：

      ```java
      public interface ServletContextListener extends EventListener {
      /**
      * 在 ServletContext 对象创建之后马上调用，做初始化
      */
      public void contextInitialized(ServletContextEvent sce);
      /**
      * 在 ServletContext 对象销毁之后调用
      */
      public void contextDestroyed(ServletContextEvent sce);
      }
      ```

      ​

      使用步骤：

      1、编写一个类去实现 `ServletContextListener`
      2、实现其两个回调方法 3、到 web.xml 中去配置监听器

## EL表达式

- Expression language

  代替`jsp`页面中表达式脚本在`jsp`页面中进行数据的输出

  更简洁

  格式：${表达式}

  `EL`在输出`null`值输出空串，`jsp`输出`null`字符串

- 搜索四个域的顺序

  和JSP一致

  从小到大顺序进行搜索

- EL表达式输出Bean普通属性，数组属性。List集合属性，map集合属性

  i.

- EL表达式的——运算

    - 关系运算 逻辑运算 算术运算 三元运算

    - `empty`运算: 空 true, 不空 false;

  ​ 空的情况:

  ​            ``null值为空，

  ​ 空串为空，

  ​            `Object`类型数组，

  ​ 长度为零

  ​            `list`集合，元素个数为零

  ​            `map`集合，元素个数为零

    - "."点运算输出—— Bean 对象中某个属性的值，[]中括号运算—— 输出有序集合中某个元素的值


- 11个隐含表达式对象

  变量 类型 作用
  `pageContext`    `PageContextImpl`            它可以获取 `jsp` 中的九大内置对象
  `pageScope`        `Map`<String,Object>        它可以获取 `pageContext` 域中的数据
  `requestScope`    `Map`<String,Object>        它可以获取 `Request` 域中的数据
  `sessionScope`    `Map`<String,Object>        它可以获取 `Session` 域中的数据
  `applicationScope`    `Map`<String,Object>    它可以获`ServletContext` 域中的数据
  `param`            `Map`<String,String>            它可以获取请求参数的值
  `paramValues`    `Map`<String,String[]>        它也可以获取请求参数的值，获取多个值的时候使用。
  `header`            `Map`<String,String>        它可以获取请求头的信息
  `headerValues`        `Map`<String,String[]>    它可以获取请求头的信息，它可以获取多个值的情况
  `cookie`            `Map`<String,Cookie>            它可以获取当前请求的 `Cookie` 信息

  `initParam`        `Map`<String,String>        它可以获取在 `web.xml` 中配置的<context-param>上下文参数

    1. EL获取四个特定域的属性

## JSTL标签库

- JSP Standard Tag Library 主要是为了替换代码脚本

- 标签库

  ![005](https://raw.githubusercontent.com/RshStone/CS-Notes/master/Notes/JavaWeb/005.png)

  `<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>`

- core核心库标签的使用

  i. <c:set />（使用很少）

  ​ 作用：set 标签可以往域中保存数据

  ii. <c:if />

  ​ if 标签用来做 if 判断。

  iii. <c:choose> <c:when> <c:otherwise>标签

  ​ 作用：多路判断。`c:when`必须配上 `c:choose`

  iv. <c:forEach />

  ​ 作用：遍历输出使用。

    2. 遍历 Object 数组

    3. 遍历 Map 集合

    4. 遍历 List 集合---list 中存放 Student 类，有属性：编号，用户名，密码，年龄，电话信息

## 文件的上传和下载

- 上传步骤
    1. 要有一个form标签，method= post请求
    2. `form`标签的`encType`属性值必须为`multipart/form-data值`
    3. 在`form`标签中使用`input type=file`添加上传的文件
    4. 编写服务器代码(servlet)接受，处理上传的数据

- `commons-fileupload.jar`常用API声明

  commons-fileupload.jar 和 commons-io.jar 包中，我们常用的类有哪些？
  `ServletFileUpload` 类，用于解析上传的数据。
  `FileItem` 类，表示每一个表单项。
  `boolean ServletFileUpload.isMultipartContent(HttpServletRequest request);`
  判断当前上传的数据格式是否是多段的格式。
  `public List<FileItem> parseRequest(HttpServletRequest request)`
  解析上传的数据
  `boolean FileItem.isFormField()`
  判断当前这个表单项，是否是普通的表单项。还是上传的文件类型。 true 表示普通类型的表单项 false 表示上传的文件类型
  `String FileItem.getFieldName()`
  获取表单项的 name 属性值
  `String FileItem.getString()`
  获取当前表单项的值。
  `String FileItem.getName();`
  获取上传的文件名
  `void FileItem.write( file );`
  将上传的文件写到 参数 file 所指向抽硬盘位置 。

- 文件的下载

  ![image-20210422184135042](https://raw.githubusercontent.com/RshStone/CS-Notes/master/Notes/JavaWeb/006.png)

  方案一：`URLEncoder` 解决 `IE` 和谷歌浏览器的 附件中 文名问题。

  方案二：`BASE64` 编解码 解决 火狐浏览器的附件中文名问 题

## Cookie

- ​ 什么是cookie

  服务器通知客户端保存键值对的一种技术

  客户端有了cookie后，每次请求发送给服务器

  每个cookie大小不能超过4kb

- 如何创建cookie

- 服务器如何获取cookie

  通过一行代码`req.getCookies():Cookie[]`获取

- 修改cookie的值

  方案一：

  先创建一个要修改的同名的Cookie对象

  在构造器同时赋予新的Cookie值

  调用`response.addCookie(Cookie);`

  方案二：

  先查找到需要修改的Cookie对象

  调用`setValue()`方法赋予新的Cookie值

  调用`response.addCookie()`

- Cookie的生命控制

  指的是如何管理Cookie什么时候被销毁

  `setMaxAge()`

  正数，表示在指定的秒数后过期 负数，表示浏览器一关，Cookie 就会被删除（默认值是-1） 零，表示马上删除 Cookie

- Cookie有效路径Path的设置

  path属性可以有效过滤哪些Cookie可以发送给服务器，哪些不发。path属性是通过请求的地址来进行有效的过滤

- 免用户名登录

  ![image-20210515152927287](https://raw.githubusercontent.com/RshStone/CS-Notes/master/Notes/JavaWeb/image-20210515152927287.png)

## Session会话

- 什么是Session

  是一个接口(`HttpSession`)

  用来维护客户端和服务器之间关联的一种技术

  每个客户端都有自己的Session会话

  Session会话中，我们经常来保存用户登录之后的信息

- 如何创建和获取

  `request.getSession()`第一次是创建，之后是获取

  `isNew();` 判断是不是刚创建出来的 true/false

  每个会话都有一个身份码

  `getId()`得到Session的会话值

- Session域数据的存取

  