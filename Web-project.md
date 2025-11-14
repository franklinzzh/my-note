## Management System

### - Web标准

* HTML	负责网页结构
* CSS       负责样式 如颜色/布局
* JavaScript 负责网页行为交互
* 还有一些基于JS封装的框架 如Vue 

> **React** 和 **Vue** 都是基于 JavaScript 的前端框架/库
>
> * **React**：它被称为一个 **库**，主要关注 UI（用户界面）层的构建。React 提供了一些核心功能，如虚拟 DOM 和组件化，但它不包含像路由、状态管理等完整的解决方案。你需要手动引入其他工具（例如 **React Router** 和 **Redux**）来实现完整的功能。
> * **Vue**：Vue 是一个 **框架**，它不仅关注 UI，还提供了更多的开箱即用的功能，包括路由（通过 Vue Router）和状态管理（通过 Vuex）。Vue 提供了一个更完整的生态系统，可以帮助开发者构建应用的各个方面。



```html
<html>
  <head>
    <title>HTML Intro</title>
  </head>
  <body>
  	<h1>
        Quick Guide
    </h1>
    <img src = "img/img01">
  </body>
</html>
```



### - Ajax

Asynchronous Javascript And XML

> XML (Extensible Markup Language)

作用：

* 与服务器进行数据交换
* 异步交互：**不重新加载页面**，与服务器交换数据并更新部分网页的技术。（注册邮箱）
* <img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251109180640136.png" alt="image-20251109180640136" style="zoom:50%;" />



##### Axios

对Ajax进行封装，简化使用

<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251109180943063.png" alt="image-20251109180943063" style="zoom: 50%;" />

### - 前端Code Rule

##### URL查询条件

```javascript
'https://mywebsite.com/user/weekly/list?name=' + this.user.name + '&gender=' + this.user.gender
//could be simplified as
`https://mywebsite.com/user/weekly/list?name=${this.user.name}&geder=${this.user.gender}`
```

##### 同步&异步

> **Synchronous**：程序会 **阻塞等待** 前一个任务完成。期间页面完全不可动
>
> **Asynchronous**： 
>
> * 不阻塞主线程（JS 只有一个主线程）。
> * 异步任务完成后，会把回调放入 **事件队列（Event Queue）**，等待主线程空闲时执行
> * 前端代码自上而下运行，若其中部分为异步，则会继续先运行后面代码，直到异步代码完成后再加入回来
>
> 如果开发大型项目，多处异步，则可能出现后面代码报错，因为前面代码未返回结果，后面代码就已经运行
>
> 处理逻辑： `async` `await`

##### `async` `await`

> 提升代码可读性/可维护性
>
> `async` 用来声明一个异步方法
>
> `await` 等待异步任务执行；只在`async` 方法内部有效，取代`then` 函数

### Maven

##### 三大功能：

> * 管理依赖（Dependency Management）：在 `pom.xml` 中声明依赖即可自动下载
> * 标准项目构建流程，自动构建项目（Build）
>
> <img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251109202704325.png" alt="image-20251109202704325" style="zoom:50%;" />
>
> * 统一项目结构，方便管理版本和插件（Project Lifecycle）



##### 导入 `maven` 项目

* 将文件复制到项目中
* 导入项目下的 `pom.xml` 文件



##### **POM**

(Project Object Model)

<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251110112355056.png" alt="image-20251110112355056" style="zoom:50%;" />

> **POM (Project Object Model)** 是 Maven 项目的核心配置文件，文件名固定为：`pom.xml`

它定义了项目的：

* 基本信息（groupId、artifactId、version）
* 依赖（dependencies）
* 构建流程（build、plugins）
* 仓库、镜像、模块等。



##### Maven坐标

Maven坐标（Maven Coordinates） 是项目唯一标识

```
<groupId>org.example</groupId>
<artifactId>web-project</artifactId>
<version>1.0-SNAPSHOT</version>
```

| 元素       | 说明                           |
| ---------- | ------------------------------ |
| groupId    | 组织或公司名（一般是反转域名） |
| artifactId | 项目名或模块名                 |
| version    | 版本号                         |

> <version>
>
> * `SNAPSHOT `：功能不稳定，在开发版本
> * `RELEASE` ：稳定可发行版本



##### JAR

> JAR (Java Archive)
>
> * 编译好的 `.class` 文件（字节码）
> * 程序运行所需的资源文件（如 `application.yml`、图片、模板）
> * 一个 `META-INF/MANIFEST.MF` 文件，用来描述包的信息（版本、主类）

“**Write once, run anywhere**” 无需源码，也能直接运行

**JAR必要性：**

* 封装与复用：把一个项目变成可直接用的组件
* 部署与交付：让程序能直接运行
* 跨平台与安全：不用暴露源码
* 版本与依赖管理：明确版本和依赖关系
* 自动化构建与集成：跨平台、自动化、可持续集成

存放地址：maven repository - <groupId> - <artifactId>

> 为何不放项目中：为了依赖复用；与maven坐标绑定；标准化统一管理



##### Dependency

添加[repository](https://mvnrepository.com/)

```xml
		<!--配置依赖-->
    <dependencies>
        <dependency>
            <groupId>commons-io</groupId>
            <artifactId>commons-io</artifactId>
            <version>2.11.0</version>
            
            <!--排除不想要的其他依赖库-->
            <exclusions>
                <groupId>commons-xxx</groupId>
                <artifactId>commons-xxx</artifactId>
            </exclusions>
        </dependency>
        
        //If just adding junit-jupiter-api, you cannot use junit-jupiter-params
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter</artifactId>
            <version>5.13.4</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
```



##### 依赖范围

```xml
<scope>...</scope>
<scope>compile</scope> //默认，主程序，测试，打包，都可以使用
<scope>test</scope> //仅测试程序内可以使用
```



##### Maven生命周期

> Maven 生命周期（Lifecycle）定义了一个 **项目从清理、编译、测试、打包到部署** 的完整流程。

* clean：清理工作
* default：核心工作，如 compile，test，package，install，deploy
* site：生成报告，项目文档

> 每套 Lifecycle 包含不同 phase（阶段），phase是有先后顺序的，Lifecycle互相独立
>
> 在同一套生命周期中，运行后面的，前面的phase都会运行



```bash
del /s *.lastUpdated //删除未下载成功的依赖
```



### - Web基础

##### HTTP协议



###### -HTTP `Request` Header

> `Client` generated this one

<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251113124636803.png" alt="image-20251113124636803" style="zoom:50%;" />

<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251113134038948.png" alt="image-20251113134038948" style="zoom:50%;" />



<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251113133952338.png" alt="image-20251113133952338" style="zoom:50%;" />



###### -HTTP `Response` Header

> `Server` generated this one

![image-20251113134241118](/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251113134241118.png)

![image-20251113165935578](/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251113165935578.png)

<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251113155711073.png" alt="image-20251113155711073" style="zoom:50%;" />

**HTTP Status Codes** 

| Status  | Meaning               | Typical Cause                                                |
| ------- | --------------------- | ------------------------------------------------------------ |
| **200** | Request succeeded     | The client’s request was valid and the server successfully returned data. |
| **404** | Resource not found    | Incorrect URL, missing endpoint, or the requested resource has been removed. |
| **500** | Internal server error | A server-side failure occurred, often due to an unhandled Java exception in the backend. |

<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251113163033114.png" alt="image-20251113163033114" style="zoom:50%;" />



##### `package` 命名

 `package org.example` 是分层命名空间（namespace separator） treated as `org/example/`

命名方式：反转的域名（reversed domain name); 域名是唯一的，反转后也能保证包名全局唯一，防止冲突



##### `@RestController`

```java
@Controller
@ResponseBody //Return JSON AUTOMATICALLY
public @interface RestController {
    @AliasFor(
        annotation = Controller.class
    )
    String value() default "";
}
```



##### DTO & Repository

**① 安全性**

> 不把数据库字段直接暴露给前端。

**② 防止前端乱改敏感字段**

> * passwordHash
> * role
> * isDeleted
> * internalFlag
>
> 这些字段在 Entity 中存在，但 DTO 中不能出现。

**③ 避免数据库结构变化影响前端**

> 如果 Entity 改动了，DTO 不需要改动。

**④ 更清晰的业务结构**

> DTO = 视图层模型
> Entity = 数据层模型

##### 分层解耦

###### - 三层架构

* Controller
* Service
* Dao

###### - 分层解耦



###### - `IOC` & `DI` 入门

<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251113184315625.png" alt="image-20251113184315625" style="zoom:50%;" />



###### - IOC详解

<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251113194541864.png" alt="image-20251113194541864" style="zoom:50%;" />



###### - `DI`详解

<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251113211536802.png" alt="image-20251113211536802" style="zoom:50%;" />



<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251113211728090.png" alt="image-20251113211728090" style="zoom:50%;" />

### - MySQL

##### Startup 的数据库架构演进（真实流程）

> **阶段 A：MVP 初期**
>
> * 本地数据库：MySQL Docker
> * 线上数据库：单机 MySQL (EC2)
>
> **阶段 B：上线初期**
>
> * Prod 使用 RDS + 只读副本
> * Dev、Staging 各自独立数据库
>
> **阶段 C：增长期**
>
> * 增加缓存（Redis）
> * 增加消息队列（Kafka / RabbitMQ）
> * 将读写分离
> * 数据库分库分表（分租户 / 分地域）
>
> **阶段 D：成熟期**
>
> * 数据仓库（BigQuery / Snowflake）
> * 数据管道（Airflow）
> * 实时分析（ClickHouse / Druid）







### - 测试

##### 测试阶段

![image-20251110152707506](/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251110152707506.png)

##### **测试方法**

* 白盒
* 黑盒
* 灰盒
* <img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251110152823341.png" alt="image-20251110152823341" style="zoom:50%;" />

<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251110152948115.png" alt="image-20251110152948115" style="zoom:50%;" />



##### JUnit 单元测试

* 写出可自动执行的测试代码
* 检查代码逻辑是否正确
* 自动验证函数的输入输出结果是否符合预期

1. 在 `pom.xml` 中，引入JUnit依赖
2. 在 `test/java` 目录下，创建测试类，编写测试方法，并在方法上注明 `@Test`

> 单元测试
>
> `类` 命名规范：XxxxxTest：`public class UserServiceTest`
>
> 内部方法命名规定：必须声明 `public void xxxxx（）`

###### 常见注解

<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251110184850931.png" alt="image-20251110184850931" style="zoom:50%;" />

**测试执行相关注解**

| 注解                 | 说明                                                         | 备注                                   |
| -------------------- | ------------------------------------------------------------ | -------------------------------------- |
| `@Test`              | 表示这是一个**测试方法**，JUnit 会自动识别并执行它。         | 最常见的注解，用于单元测试。           |
| `@ParameterizedTest` | 表示这是一个**参数化测试方法**，即同一个测试方法会用不同参数运行多次。 | 使用这个注解后，不需要再加 `@Test`。   |
| `@ValueSource`       | 指定参数化测试的**数据来源**，为测试方法提供多个输入值。     | 必须与 `@ParameterizedTest` 搭配使用。 |
| `@DisplayName`       | 给测试类或测试方法取一个**更友好的名字**（默认是方法名）。   | 方便测试报告中显示更直观的名称。       |

**生命周期（执行顺序）相关注解**

| 注解          | 说明                               | 执行频率       | 常用用途                               |
| ------------- | ---------------------------------- | -------------- | -------------------------------------- |
| `@BeforeEach` | 在**每个测试方法执行前**运行一次   | 每个测试执行前 | 初始化测试资源（准备工作）             |
| `@AfterEach`  | 在**每个测试方法执行后**运行一次   | 每个测试执行后 | 清理资源（释放工作）                   |
| `@BeforeAll`  | 在**所有测试方法执行前**只运行一次 | 整个类前一次   | 全局初始化（例如启动数据库、加载配置） |
| `@AfterAll`   | 在**所有测试方法执行后**只运行一次 | 整个类后一次   | 全局清理（例如关闭连接、释放资源）     |

为何 `@BeforeAll` 的方法需要 `static` ？

* 因为调用时没有实例存在

> `static` :
>
> * 不依赖对象实例；
> * 可以直接通过类调用（例如 `MyTestClass.beforeAll()`）；
> * 能在实例创建之前被调用。





###### `Assertion` 方法

```
assertEquals(Object expected, Object actual，String message) //检查两个值是否相等，不相等 返回错误信息（可隐藏）
```

```
assertThrows(exceptionClass, executable)

// expectedType 期望抛出的异常类型
// executable Executable（函数式接口）() -> {...}
public static <T extends Throwable> T assertThrows(
        Class<T> expectedType,
        Executable executable
)
// 示例
assertThrows(IllegalArgumentException.class, () -> calculator.divide(10, 0));
```

> 所有assert都存在重载方法，可以不指定 `message` 
>
> * `assertEquals(Object expected, Object actual，String message)`
> * `assertEquals(Object expected, Object actual)`
