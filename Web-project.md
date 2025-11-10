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

```
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
    </dependencies>
```



##### Maven生命周期

> Maven 生命周期（Lifecycle）定义了一个 **项目从清理、编译、测试、打包到部署** 的完整流程。

* clean：清理工作
* default：核心工作，如 compile，test，package，install，deploy
* site：生成报告，项目文档

> 每套 Lifecycle 包含不同 phase（阶段），phase是有先后顺序的，Lifecycle互相独立
>
> 在同一套生命周期中，运行后面的，前面的phase都会运行







### - Java project

 `package org.example` 是分层命名空间（namespace separator） treated as `org/example/`

命名方式：反转的域名（reversed domain name); 域名是唯一的，反转后也能保证包名全局唯一，防止冲突





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
