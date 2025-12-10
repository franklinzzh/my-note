## Management System



### - 项目流程

<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251115175920799.png" alt="image-20251115175920799" style="zoom:50%;" />

**① 设计数据结构（DB 设计）**

例如 user 表、product 表、order 表…

**② 写接口文档（Swagger 或 Markdown）**

包含：

* URL
* method
* request body
* response body
* 返回格式
* 示例
* 错误码

**③ Start coding：按接口文档开发后端**

Controller → Service → Mapper → XML → 测试



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



##### - ‼️语句顺序

```sql
1. FROM        （选表）
2. WHERE       （过滤行）
3. GROUP BY    （分组）
4. HAVING      （过滤组）
5. SELECT      （计算列）
6. ORDER BY    （排序）
7. LIMIT       （分页）
```

`COUNT(*)` 会执行 `WHERE/GROUPBY/HAVING`，不会执行 `LIMIT`

`COUNT(*)` in SQL is executed as a completely *separate query*.



##### - `Where`

**Always write `WHERE` in `UPDATE`  and `DELETE` clause !!!**



##### - Update Execution Summery

* 1. MySQL determines the target rows

> When an `UPDATE` statement is executed, MySQL first identifies which rows *would* be affected.
> This stage does **not** modify any data; it only selects the potential rows.

* 2.  MySQL checks all constraints before applying changes

> Before modifying any row, MySQL performs a full validation pass. It checks:
>
> * Unique constraints
> * Foreign key constraints
> * Data type conversions
> * NOT NULL requirements

* 3. MySQL aborts if any constraint would be violated

> If MySQL determines that the final result of applying the update would violate any constraint (such as creating duplicate values for a unique column), it **aborts the entire operation immediately**.





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





##### SQL语句

> * DDL (Data Defination Language)	定义
> * DML (Data Manipulation  Language)    操作，CRUD
> * DCL  (Data Query Language )  查询



###### <img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251114123607219.png" alt="image-20251114123607219" style="zoom:30%;" />



###### - DDL

* 数据库

```sql
show databases;
select database(); //target one
use database_name; 
create database if not exists database_name default charset utf8mb4; //default utf8mb4
delete data if exists
```



1. 



###### - DQL

The SQL engine works like this:



<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251114165035470.png" alt="image-20251114165035470" style="zoom:40%;" />



```sql
-- typeId is 1 or 9
SELECT * FROM baiology.user WHERE user_type_id in '1,9'; 
-- only one char in username
SELECT * FROM baiology.user WHERE user_name like '_';
-- start as a/A in username
SELECT * FROM baiology.user WHERE user_name like 'a%';
-- include bb in username
SELECT * FROM baiology.user WHERE user_name like '%bb%';
```



##### Basic Query

```sql
-- Select all column name from a table in order
SELECT GROUP_CONCAT(column_name ORDER BY ordinal_position)
FROM information_schema.columns
WHERE table_schema = 'tlias'
  AND table_name = 'emp';

-- COUNT
-- count doesn't include null value
select count(id) from user; -- cound {id} not null
select count(*) from user; -- efficient one
select count(1) from user; -- same as count(*)

select avg(salary) from user;

-- GROUP BY
SELECT dept, AVG(salary)
FROM emp
GROUP BY dept;

-- error! cannot casually use SELECT * after group by
select * from user group by user_type_id; 

select user_type_id, count(1) from user group by user_type_id;
-- find users registered at date'2024-01-01' and after, group by user type, return group count larger than 5 users
-- WHERE -> GROUP BY -> HAVING
select user_type_id, count(1)from user where create_time >= '2024-01-01' group by user_type_id having count(1) >= 5; 

-- ORDER BY
select id, user_name from user order by create_time, update_time desc;

-- LIMIT
select id, user_name from user order by create_time, user_type_id desc limit 0, 5;
-- show i page
select id, user_name from user order by create_time, user_type_id desc limit (i-1)*5, 5;
```

`GROUP BY `必须搭配聚合函数

* `COUNT()` → 数量
* `SUM()` → 求和
* `AVG()` → 求平均
* `MAX()` → 最大值
* `MIN()` → 最小值



##### `foreign key`

```sql
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_name VARCHAR(50) NOT NULL
);

CREATE TABLE orders (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    amount DECIMAL(10,2) NOT NULL,

    CONSTRAINT fk_orders_users -- fk_<child_table>_<parent_table>
        FOREIGN KEY (user_id)
        REFERENCES users(id)
        ON DELETE CASCADE   -- 删除user时自动删除order
        ON UPDATE CASCADE
);
```

```sql
-- 建完表后，添加外键
alter table  表名  add constraint  外键名称  foreign key(外键字段名) references 主表(主表列名);
```

> 虽然确保了两张表数据的一致性和完整性，但很不常用
>
> 缺点：
>
> * 影响增、删、改的效率（需要检查外键关系）。
> * 仅用于单节点数据库，不适用于分布式、集群场景。
> * 容易引发数据库的死锁问题，消耗性能。

解决方案：[逻辑外键]()



##### `Delete table data with fk`

```sql
SET FOREIGN_KEY_CHECKS = 0;

TRUNCATE TABLE orders;
TRUNCATE TABLE users;

SET FOREIGN_KEY_CHECKS = 1;
```



##### `Join`

笛卡尔积

> emp 的每一行 × dept 的每一行，会全部组合成结果。

```sql
select * from  emp , dept;
```

`JOIN`

Inner Join / Outer Join

> correct one

```sql
-- inner join, only show data exists on both tables
SELECT * FROM emp JOIN dept ON emp.dept_id = dept.id;

-- left outer join, show all data in left, even if right not exists
SELECT * FROM emp LEFT JOIN dept ON emp.dept_id = dept.id;
-- right outer join, show all data in left, even if left not exists
SELECT * FROM emp RIGHT JOIN dept ON emp.dept_id = dept.id;

-- 查询所有员工的ID，姓名，及所属的部门名称
select emp.id, emp.name, dept.name from emp left join dept on emp.dept_id = dept.id;
```



##### Subquery

标量子查询（Scalar Subquery）

```sql
SELECT * FROM t1 WHERE column1 = (SELECT column1 FROM t2 ...);
```

列子查询（Column Subquery）

```sql
WHERE column1 IN (SELECT dept_id FROM dept)
```

行子查询（Row Subquery）

```sql
WHERE (a,b) = (SELECT x,y FROM t2 WHERE id=1)
```

表子查询（Table Subquery）

```sql
SELECT * FROM (SELECT id,name FROM t2) AS temp;
```

Example 

`Scalar Subquery`

```sql
-- 查询 最早入职 的员工信息
select * from emp where emp.entry_date = ?;
select min(emp.entry_date) from emp;
select * from emp where (select min(emp.entry_date) from emp);

-- 查询在 阮小五 入职之后入职的员工信息
select emp.entry_date from emp where emp.name = '阮小五';
select * from emp where emp.entry_date > (select emp.entry_date from emp where emp.name = '阮小五');
```

`Column Subquery`

```sql
-- 查询 "教研部" 和 "咨询部" 的所有员工信息
select dept.id from dept where dept.name = '教研部' OR dept.name = '咨询部';
select * from emp where emp.dept_id in (select dept.id from dept where dept.name = '教研部' OR dept.name = '咨询部');
```

`Row Subquery`

```sql
-- 查询与 "李忠" 的薪资 及 职位都相同的员工信息
select emp.salary, emp.job from emp where emp.name = '李忠';
select * from emp where (salary, job) = (select emp.salary, emp.job from emp where emp.name = '李忠');
```

`Table Subquery`

```sql
-- 获取每个部门中薪资最高的员工信息
select emp.id, max(emp.salary) from emp group by dept_id;
select * from emp e, (select emp.id, max(emp.salary) as max_salary from emp group by dept_id) a where e.id = a.id and e.salary = a.max_salary;
```

##### More examples

```sql
-- 查询 "教研部" 性别为 男，且在 "2011-05-01" 之后入职的员工信息 。
select * from emp as e, dept as d where e.dept_id = d.id and d.name = '教研部' and gender = 1 and entry_date > '2011-05-01';

-- 查询工资 低于公司平均工资的 且 性别为男 的员工信息 。
select * from emp CROSS JOIN salary < (select avg(salary) from emp) t where and gender = 1;
```

> `CROSS JOIN` saved avg druing this query lifetime.

```sql
-- 查询部门人数超过 10 人的部门名称
select dept.name from emp as e join dept as d on e.dept_id = d.id group by e.dept_id having count(e.id) > 10;
```

> cannot using `GROUP BY`  inside 'WHERE'
>
> * WHERE 过滤的是“行” → GROUP BY 之前存在的数据
> * HAVING 过滤的是“组” → GROUP BY 之后才出现的数据
>
> Order: FROM → WHERE → GROUP BY → HAVING

```sql
-- 查询在 "2010-05-01" 后入职，且薪资高于 10000 的 "教研部" 员工信息，并根据薪资倒序排序。
select e.* from emp as e, dept as d on e.dept_id = d.id where e.entry_date > '2010-05-01' and e.salary > 10000 and d.name = '教研部' order by e.salary desc;

-- 查询工资 低于本部门平均工资的员工信息 。
select * from emp as e join dept as d on e.dept_id = d.id where ((id, salary) = (select dept_id, avg(salary) from emp group by dept_id)) as a having d.id = a.id and e.salary < a.salary;
```



### - MyBatis

simpilfied JDBC on Dao

##### JDBC vs. MyBatis

> JDBC：
>
> * 配置文件是硬编码
> * 处理SQL语句繁琐
> * 启动释放资源，资源浪费，性能降低
>
> MyBatis
>
> * `.yml`文件统一配置，修改配置文件无需重新编译
> * `@Mapper` 接口自动解析，封装对象
> * `spring.datasource` 从数据库连接池获取链接，用完放回，可复用

##### 数据库连接池

> * 是一个容器，负责分配、管理数据库连接
> * 允许重复使用现有数据库连接，不用重复建立 (资源复用；提升响应速度)
> * 释放超过最大空闲时间的连接

标准接口：`DataSource`

```java
Connection getConnection() throw SQLException;
```



##### #{...} vs. ${...}

> `#{}` 是预编译参数占位符（PreparedStatement）——安全、会防 SQL 注入
>
> `${}` 是字符串拼接——危险、不做任何转义

```
SELECT * FROM user WHERE id = #{id}
//Mybatis 自动把#转成？
SELECT * FROM user WHERE id = ?
```



##### `Mapper.xml`

> SQL语句过长，可以存放到 `resource` 下的Mapper中
>
> 注意：`copy reference`  后将 `com.franklin.mapper`  改为 `com/franklin/mapper`



```xml
<mapper namespace="com.franklin.mapper.EmpMapper">
    <select id="getAll" resultType="com.franklin.entity.Emp">
    </select>
</mapper>
```

* `namespace` : Binds this XML to a specific Mapper interface.
* `id` : The method name in the mapper interface.
* `resultType` : The Java class used to map each row returned by a `SELECT` .







### - 依赖注入

> `DI (Dependency Injection)`
>
> * `@Autowired` --使用较少
> * 构造器注入

字段注入（Autowired）：

> 运行时注入：Spring 容器初始化 Bean 后， Spring 会用反射把 @Autowired 字段赋值



构造器注入（RequiredArgsConstructor）：

> 构造时注入：Java new 对象过程

* 强制使用  final，依赖集中在顶部，方便查看
* 依赖是类构造过程的一部分，不能为 null
* 若依赖为 null，new UserService() **直接报错**
* 方便测试



# - 实战开发

### - Springboot 注解

##### `@Target`

这个注解可以放在哪些位置

#####  `@Retention`

注解在运行时是否可见

* RUNTIME: JVM 运行期可读 → Spring 必须用

##### `@Documented`

生成 API 文档时显示注解



##### `@RequestMapping`

> 用来定义一个 Controller 的 URL 路径映射，以及它支持的 HTTP 方法（GET/POST/...）。



---



##### `@ModelAttribute`

可省略

> 是 Spring MVC 中用来进行参数绑定（Data Binding）的注解。它负责把请求参数（尤其是 queryString、form-data）转换成 Java 对象，并自动注入到方法参数中。如 queryString -- DTO



##### `@PathVariable`

`http://localhost:8080/depts/1`

```java
@GetMapping("/depts/{id}")
public Result getDept(@PathVariable Integer id) {}
```



##### `@RequestBody`

Required to recieve `.json` data from front-end

```
PUT - http://localhost:8080/depts 请求参数：{"id": 1, "name": "研发部"}
```

```java
@PutMapping("/depts")
public Result updateDept(@RequestBody Dept dept) {}
```

> @RequestBody注解的作用：将 HTTP请求体中的JSON或XML数据，自动绑定（反序列化）到后端的Java对象上

Don't use `@RequestBody` on `QueryParamDTO param`, which is come from queryString, not .json body.

---



`@ModelAttribute` 绑定的是 URL 参数（queryString 或 form-data）。

* 本质都是 Key=Value 参数对。
* 适用于 GET 请求 和 表单 POST。
* 根据字段名匹配 DTO 属性
* 自动做类型转换（String → Integer / LocalDate）

 `@RequestBody` 绑定的是 JSON（或 XML）请求体。

* 适用于 POST / PUT / PATCH 发送 JSON。
* 将 JSON 反序列化成 Java 对象
* 必须 Content-Type=application/json

---



##### `@RequestParam`

```java
// for required param
@RequestParam(defaultValue = "1")
// for not required param
@RequestParam(defaultValue = "") //works for String

@RequestParam(required = false)

@RequestParam("file") MultipartFile image // want to connect different names
```

**Rules:**

* `@RequestBody` can only have one in a method
* With `@RequestParam` , order doesn't matter

> Primitive & simple types (`int`, `Integer`, `String`, `Integer[]`): Not required `@RequestParam` 
>
> Collection types (`List<T>`, `Set<T>`) : Required `@RequestParam` 
>
> Complex objects (`User`, `Employee`) with no annotation: Required  `@RequestBody` 

**Order:**

> @PathVariable
>
> @RequestParam
>
> pagination vars (page, pageSize)
>
> @RequestBody (if any)
>
> HttpServletRequest / HttpServletResponse
>
> authentication principal (e.g. @AuthenticationPrincipal)

```java
//if front-end input ?ids=1,2,3
//either way in controller will works
@RequestParam(required = false) List<Integer> ids
Integer[] ids
```

Prefer `List` to recieve data:

* Mutable & Flexibility: 
  * List size is mutable; 
  * Directly using `list.add()` ,  `list.remove()` without copying the arr.
* Compatible with Mybatis queries (`IN (:ids)` gets a List); Array has to use `toList()

---



##### `@Value` 

当 `Component` 中存在一些 `member variable` ，可以声明`@Value` ，并在  `yml`  中进行配置

```yml
#阿里云OSS
aliyun:
  oss:
    endpoint: https://oss-cn-beijing.aliyuncs.com
    bucketName: java-ai
    region: cn-beijin
```



```java
		@Value("${aliyun.oss.endpoint}")
    private String endpoint;
    
    @Value("${aliyun.oss.bucketName}")
    private String bucketName;
    
    @Value("${aliyun.oss.region}")
    private String region;
```

但如果注解变量过多，则可以利用Spring提供的简化版.



##### `@ConfigurationProperties`

* 需要创建一个实现类，且实体类中的属性名和配置文件当中key的名字必须要一致
  * 比如：配置文件当中叫endpoint，实体类当中的属性也得叫endpoint，另外实体类当中的属性还需要提供 getter / setter方法
* 需要将实体类交给Spring的IOC容器管理，成为IOC容器当中的bean对象
* 在实体类上添加`@ConfigurationProperties`注解，并通过 `prefix` 属性来指定配置参数项的前缀

```java
@ConfigurationProperties(prefix = "aliyun.oss")
public final class AliyunOSSProperties {
    private final String instanceVariable;
  	...

    public AliyunOSSProperties(String instanceVariable, ...) {
        this.instanceVariable = instanceVariable;
      	...
    }

    public String getInstanceVariable() { return instanceVariable; }
  	...
}
```

Since this is a property class, all instance variables should be declared with `final`

Don't use `@Data` , `@Component` , `@AllArgsConstructor` with `@ConfigurationPorperties`. Don't let beans to constrain properties, because it should be flexible. 
Also, since using `final`   and `@ConfigurationProperties` , in `WebApplication` add `@ConfigurationPropertiesScan` to let it works. 

###### (Still need to figure out why? ......to be continued)

---



##### `@RestControllerAdvice`

全局异常处理

> @RestControllerAdvice = @ControllerAdvice + @ResponseBody
>
> 处理异常的方法返回值会转换为json后再响应给前端

* @RestControllerAdvice  //表示当前类为全局异常处理器
* @ExceptionHandler  //指定可以捕获哪种类型的异常进行处理



##### `@Data` vs `@Component`



##### `@NoArgConstructor`

NEED NoArgConstructor:

* Classes used in MyBatis resultType 
* Entities mapped to DB
* Classes used with frameworks that instantiate via reflection:
  * Redis serialization
  * RabbitMQ messages
  * JPA entities
  * MyBatis result maps





##### `@AllArgConstructor`

Only using this one when manually construct the a new Object with full params.

```java
Object object = new Object([EVERY_PARAM]);
```

In Mybatis, if you are creating DTO using `resultType` , it actually creates the data using setter, like setId().

Example Code:

```java
public StudentCountDTO fetchStudentCount() {
		//...
		return new StudentCountDTO(clazzList, dataList);
}
public List<StudentDegreeDTO> fetchStudentDegree() {
    return reportMapper.fetchStudentDegree();
}
```

The first one needs `@AllArgConstructor` ; while the second one only uses `setter()` for each variable

```xml
<select id="fetchStudentDegree" resultType="com.franklin.dto.StudentDegreeDTO">
```



---



### - Useful Java method:



```
if (!CollectionUtils.isEmpty(exprList)) {}
//the same as
if (collection != null && !collection.isEmpty()) {}
```

To avoid `NullPointerException` and `useless logics for empty list`



---



### - `Mapper` interface

NO `;` at the end of the query.



##### `@MapKey`

@MapKey("pos")

This let Mapper know which one you want to set as `Key` , if you want to use Map as returned value.



##### Basic Query

`SELECT`

```sql
SELECT * FROM dept WHERE
```

`INSERT INTO`

```sql
INSERT INTO dept(column1, colume2) VALUES (#{entityName1}, #{entityName2})
```

`UPDATE`

```sql
UPDATE dept SET column1 = '#{entityName1}', column2 = '#{entityName2}' WHERE id = #{id}
```

```xml
<set>
    <if test="salary != null">salary = #{salary},</if>
    <!--auto remove comma in the last-->
    <if test="deptId != null">dept_id = #{deptId},</if> 
</set>
```

The same as:

```sql
SET name = ?, salary = ?, dept_id = ?
```



`DELETE FROM` 

```sql
DELETE FROM dept WHERE id IN (#{id1}, #{id1}, #{id1})
```



##### 模糊查询

```sql
e.name LIKE CONCAT('%', #{name}, '%') -- case insensitive
```



### - `mapper.xml`

⚠️ It doesn't allow `""` inside `<mapper>`



##### Mybatis Dynamic SQL

`<set>`

`<trim prefix="(" suffix=")" suffixOverrides=",">`

`<where>`

`<foreach>`

`<where>`：根据查询条件，来生成where关键字，并会自动去除条件前面多余的and或or。



##### `<if>`

判断条件是否成立，如果条件为true，则拼接SQL。

```xml
			<where>
            <if test="name != null and name != ''">
                AND e.name LIKE CONCAT('%', #{name}, '%')
            </if>
            <if test="gender != null">
                AND e.gender = #{gender}
            </if>
            <if test="begin != null">
                AND e.entry_date &gt;= #{begin}
            </if>
            <if test="end != null">
                AND e.entry_date &lt;= #{end}
            </if>
        </where>
```

**好处**：当某些值前端未输入，默认为null，不需要单独为该条件写一条SQL语句；否则 k 个param要写2^k 个SQL

> When filter `String` , you need to consider `''`
>
> But for `Integer`, no value inputs from front-end will auto be `null` 

```xml
<if test="name != null and name != ''">name = #{name},</if>
<if test="salary != null">salary = #{salary},</if>
```

Column 带逗号；像where中不需要，因为有and

##### `<for each>`

###### `Example 1:` 

```sql
insert into emp_expr() values (?, ?, ?, ?), (?, ?, ?, ?), (?, ?, ?, ?), (?, ?, ?, ?)
```

xml Code

```xml
<foreach collection="exprList" item="expr" separator="," >
  (#{expr.empId}, #{expr.company}, #{expr.startDate}, #{expr.endDate})
</foreach>
```

> 1. collection：集合名称 --要和 mapper interface 中传入参数名称一致
> 2. item：集合遍历出来的元素/项 --要和 #{expr. } 的 pojo 名称相同
> 3. separator：每一次遍历使用的分隔符
> 4. open：遍历开始前拼接的片段
> 5. close：遍历结束后拼接的片段

Think of it as :

```java
for (EmpExpr expr : exprList) {
    ...
}
```



###### `Example 2: `

```
/emps?ids=1,2,3 
List<Integer> ids = List.of(1, 2, 3); -- Spring recieve
ids = [1, 2, 3] --mapper get
```

```sql
WHERE id IN (1,2,3) --sql syntax
-- correct form in xml
 <foreach collection="ids" item="id" open="(" close=")" separator=",">
    #{id}
 </foreach>
```





##### Use auto increases key and add into pojo

```xml
<insert id="insert" useGeneratedKeys="true" keyProperty="id">
    INSERT INTO emp (name, gender, dept_id, entry_date)
    VALUES (#{name}, #{gender}, #{deptId}, #{entryDate});
</insert>
```

> **useGeneratedKeys = true** → enable JDBC auto key retrieval
>
> **keyProperty = "id"** → write the generated key into `emp.id`



##### - `resultMap` 

在一对多的查询中，`resultMap`  可以仅查询一次DB就能返回结果，而不用写两次SQL语句查询

```xml
<!--自定义结果集ResultMap-->
<resultMap id="empResultMap" type="com...Emp">
    <id column="id" property="id" />
    <result column="username" property="username" />
		<!--...-->

    <!--封装exprList-->
    <collection property="exprList" ofType="com...EmpExpr">
        <id column="ee_id" property="id"/>
        <result column="ee_company" property="company"/>
        <!--...-->
    </collection>
</resultMap>

<!--根据ID查询员工的详细信息-->
<select id="getById" resultMap="empResultMap">
    select e.*,
        ee.id ee_id,
				<!--...-->
    from emp e left join emp_expr ee on e.id = ee.emp_id
    where e.id = #{id}
</select>
```

> Mybatis中封装查询结果，什么时候用 `resultType` ，什么时候用 `resultMap`  ？
>
> * 如果查询返回的字段名与实体的属性名可以直接对应上，用 `resultType`  。
> * 如果查询返回的字段名与实体的属性名对不上，或实体属性比较复杂，可以通过 `resultMap` 手动封装 。

发生在SQL query 完成之后，所以对于发生在SQL的分页操作;

同时也会放大 `JOIN` 的问题: 多次访问Java对象，多次去重（根据对象id）



##### - `Case`

`&lt;` means <

`&gt;` means >



> The select column as new_name must represent the DTO's variable name

```sql
		<select id="fetchStudentDegree" resultType="com.franklin.dto.StudentDegreeDTO">
        select (case degree
                    when 1 then '初中'
                    when 2 then '高中'
                    when 3 then '大专'
                    when 4 then '本科'
                    when 5 then '硕士'
                    when 6 then '博士'
                    else '其他'
                end) as name,
                count(*) as num
        from student
        group by degree
        order by num
    </select>
```



### - File Upload

前端：

Form表单：

* 表单必须有file域，用于选择要上传的文件
* 表单提交方式必须为POST：通常上传的文件会比较大，所以需要使用 POST 提交方式
* 表单的编码类型enctype必须要设置为：multipart/form-data：普通默认的编码格式是不适合传输大型的二进制数据的，所以在文件上传时，表单的编码格式必须设置为multipart/form-data

```html
		<form action="/upload" method="post" enctype="multipart/form-data">
        <label for="fileInput">Choose file:</label>
        <input type="file" id="fileInput" name="file" />

        <!-- 多文件上传用 multiple -->
        <!-- <input type="file" id="fileInput" name="files" multiple /> -->

        <br /><br />
        <button type="submit">Upload</button>
    </form>
```

后端：

controller 

```java
public void upload(String username, Integer age, @RequestParam("file") MultipartFile file)
```



Always use `getParentFile()` when you want to save the file. To avoid

```java
File dir = new File("/upload/photo.jpg");
dir.mkdirs();
```

  

```java
File targetFile = new File(uploadFolder, newFileName);

// ensure folder exists
File parent = targetFile.getParentFile();
if (!parent.exists()) {
    parent.mkdirs();
}

// save file
file.transferTo(targetFile);
```

> **MultipartFile 常见方法：** 
>
> * `String  getOriginalFilename();`  //获取原始文件名
> * `void  transferTo(File dest);`` `   //将接收的文件转存到磁盘文件中
> * `long  getSize();`   //获取文件的大小，单位：字节
> * `byte[]  getBytes();`` `   //获取文件内容的字节数组
> * `InputStream  getInputStream();`    //获取接收到的文件内容的输入流



配置 yml 文件大小限制

```yaml
spring:
  servlet:
    multipart:
      max-file-size: 10MB
      max-request-size: 100MB
```



### - 云服务

> **云服务**指的就是通过互联网对外提供的各种各样的服务，比如像：语音服务、短信服务、邮件服务、视频直播服务、文字识别服务、对象存储服务等等。



### - SDK

> **SDK**：Software Development Kit 的缩写，软件开发工具包，包括辅助软件开发的依赖（jar包）、代码示例等，都可以叫做SDK。
>
> 简单说，sdk中包含了我们使用第三方云服务时所需要的依赖，以及一些示例代码。我们可以参照sdk所提供的示例代码就可以完成入门程序。



### - 分页逻辑

后端 + 数据库

* 数据量大，前端不能一次性加载所有数据
* 获得最新数据
* 安全性：前端不能看到全部数据
* 性能：后端查询比前端处理更高效

```sql
# 开始索引 = (当前页码 - 1)  *  每页显示条数
SELECT * FROM emp  LIMIT 0,10; -- get front-end data
```

```java
// PageResult send .json back to front-end
@Data
@NoArgsConstructor
@AllArgsConstructor
public class PageResult {
        private Long total; //总记录数
        private List rows; //当前页数据列表
}
```



##### `PageHelper`

```sql
PageHelper.startPage(1, 10)
     ↓
ThreadLocal 存下分页参数

empMapper.getAll()
     ↓
PageHelper 拦截 SQL → 自动改成 count + limit 语句
     ↓
返回 Page 类型（不是普通 List）
     ↓
new PageInfo(Page)
     ↓
PageInfo 从 Page 中读取分页元数据（total、pageNum、pageSize）
     ↓
返回给你完整分页结果
```



### - 1. `Controller` 

`GET` - get
`POST` - add
`PUT` - update
`DELETE` - delete



@ModelAttribute StudentQueryParamDTO param

create new Object, so it won't be null





##### Integer / Object

> 遇到复杂情况，需要多个字段，使用DTO（object）
>
> 简单情况如 id，直接使用基本类型

⚠️ `Integer` 可以为 `null` ；`int` 不能为 `null`; 所以接口一定要用包装类



##### QueryParam

1. 当前端返回 `queryString` 时，后端一定要用 @RequestParam接收

It is used to handle the circum that there are many `params` in query

```java
@GetMapping
    public Result getAll(@RequestParam(defaultValue = "") String name,
                         @RequestParam(required = true) Integer gender,
                         @DateTimeFormat(pattern = "yyyy-MM-dd") LocalDate begin,
                         @DateTimeFormat(pattern = "yyyy-MM-dd") LocalDate end,
                         @RequestParam(defaultValue = "1")  Integer page,
                         @RequestParam(defaultValue = "10")  Integer pageSize) {}
```

2. 遇到多个 `params` ，为了让 `controller` 更为清晰简洁，推荐新建一个 `QueryParamDTO` 。
   * 对于Required的Params，利用 `@Valid` 注解，可以减少 service 和 mapper 中的filter
     * 要在controller `@RequestBody` 前加入 `@Valid` ，让注解生效
   * 可以加入分页逻辑。

```java
public class StudentQueryParamDTO {
  
  	@NotNull(message = "ID is required")
    private Integer id;

    @NotEmpty(message = "name is required")
    private String name;

    // optional
    private String name;
    private Integer degree;
    private Integer clazzId;
  
    // Pagination Default
    private Integer page = 1;
    private Integer pageSize = 10;
}
```

```xml
<!--Jakarta Validation-->
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

同时，要在GlobalExceptionHandler，增加Validation的异常抛出。否则不会抛出异常。

> 不使用 `@Valid` 就要在后面加很多逻辑判断

```xml
		<update id="update">
        update clazz
        <set>
            <if test="name != null and name != ''">name = #{name},</if>
            <if test="room != null and room != ''">room = #{room},</if>
            <if test="beginDate != null">begin_date = #{beginDate},</if>
            <if test="endDate != null">end_date = #{endDate},</if>
            <if test="masterId != null">master_id = #{masterId},</if>
            <if test="subject != null">subject = #{subject},</if>
            update_time = NOW()
        </set>
        where id = #{id}
    </update>
```





### - 2.  `Service`

##### 逻辑外键

通过service中手动插入逻辑，实现外键约束，很方便的解决fk的缺点

> 在现在的企业开发中，很少会使用物理外键，都是使用逻辑外键。 甚至在一些数据库开发规范中，会明确指出禁止使用物理外键 foreign key 

---

### ‼️Qestions, for repreated logic, should I create gernral methods that all classes could use it? 

`existsByName` , `existsById`

---



##### `delete`

> Ex: if you want to delete a class has students, then throw an error

**Design**: 

* Create a `existsByParentId` method in child service to use query to check existence.

  * `exist` or `count` in xml query? Ans: **Exist**. 

    ```sql
    SELECT EXISTS (subquery);
    SELECT EXISTS(
        SELECT 1 FROM student WHERE clazz_id = #{clazzId}
    );
    ```

    * 1 or * or count(*) all work the same in EXISTS.
    * stops scanning at **first match**.

* check in `delete` method in parent service



##### Transactional（事务）

```java
@Transactional(rollbackFor = Exception.class)
```

> 事务是一组操作的集合，会把所有操作当做一个整体 向系统提交或撤销请求，要么同时成功要么同时失败。

具体流程：

```SQL
-- 开启事务
start transaction; / begin;

-- 1. 保存员工基本信息
insert into emp values (39, 'Tom', '123456', '汤姆', 1, '13300001111', 1, 4000, '1.jpg', '2023-11-01', 1, now(), now());

-- 2. 保存员工的工作经历信息
insert into emp_expr(emp_id, begin, end, company, job) values (39,'2019-01-01', '2020-01-01', '百度', '开发'),                                                                                                       (39,'2020-01-10', '2022-02-01', '阿里', '架构');

-- 提交事务(全部成功)
commit;

-- 回滚事务(有一个失败)
rollback;
```



###### - ACID四大特性

* Atomicity ：事务中的所有操作要么全部成功，要么全部失败 -- 回滚
* Consistency： 事务前后，数据库必须从一个合法状态到另一个合法状态。不能破坏约束（pk，fk）
  * 如果事务成功的完成，那么数据库的所有变化将生效。
  * 如果事务执行出现错误，那么数据库的所有变化将会被回滚(撤销)，返回到原始状态。
* Isolation：多个用户并发的访问数据库时，一个用户的事务不能被其他用户的事务干扰，多个并发的事务之间要相互隔离。一个事务的成功或者失败对于其他的事务是没有影响。
* Durability：一个事务一旦被提交或回滚，它对数据库的改变将是永久性的，哪怕数据库发生异常，重启之后数据亦然存在。



###### - `@Transactional` 

**作用：**就是在当前这个方法执行开始之前来开启事务，方法执行完毕之后提交事务。如果在这个方法执行的过程当中出现了异常，就会进行事务的回滚操作。

**位置：**业务层的方法上、类上、接口上

* 方法上：当前方法交给spring进行事务管理
* 类上：当前类中所有的方法都交由spring进行事务管理 
* 接口上：接口下所有的实现类当中所有的方法都交给spring 进行事务管理

> **默认情况下，只有出现RuntimeException(运行时异常)才会回滚事务。**其他Exception不会抛出异常

```yml
#spring事务管理日志
logging: 
  level: 
    org.springframework.jdbc.support.JdbcTransactionManager: debug
```



###### - `rollbackfor `

```
Class<? extends Throwable>[] rollbackFor() default {};
```

继承 `Throwable` ，可指定任何 `Throwable` 子类

`@Transactional(rollbackFor = Exception.class)` 



###### - `propagation` 

事务的**传播**行为: 当一个事务方法被另一个事务方法调用时，这个事务方法应该如何进行事务控制。

```java
REQUIRED(0), //默认值，有事务，新事务就加入；没有，则创建新的
SUPPORTS(1),
MANDATORY(2),
REQUIRES_NEW(3),//无论是否有事务，都创建新的
NOT_SUPPORTED(4),
NEVER(5),
NESTED(6);
```

`@Transactional(propagation = Propagation.REQUIRES_NEW)`



适用情况：

* **REQUIRED：**大部分情况下都是用该传播行为即可。
* **REQUIRES_NEW：**当我们不希望事务之间相互影响时，可以使用该传播行为。比如：下订单前需要记录日志，不论订单保存成功与否，都需要保证日志记录能够记录成功。



---



### - 3. `Entity`

> All DTOs, VOs, Entities, Params are POJOs.

Database tables (POJO mapped to DB)

实体类可以包含数据库没有的字段（很常见！）

```java
public class Emp {
    private Integer id;
    private Integer deptId;

    // 扩展字段（数据库里没有）
    private String deptName;
}
```

* 扩展字段 / 非持久化字段（transient field）
* VO（View Object）字段
* 仅用于返回给前端的展示字段

> 这些字段：
>
> * 不会插入数据库
> * 不会更新数据库
> * 不会出现在 emp 表里
> * 不会被 ORM 自动持久化



##### 构造方法

| 构造器类型       | 是否需要 | 用途                     |
| ---------------- | -------- | ------------------------ |
| **无参构造**     | ⭐ 必需   | ORM、JSON 解析           |
| **全参构造**     | 可选     | 测试、DTO/VO 常用        |
| **Builder 模式** | 强烈推荐 | 安全、可读性好、企业常用 |

```java
//@NoArgsConstructor
Emp emp = new Emp();
emp.setName("Franklin");
emp.setDeptId(3);

//with builder
@Builder
@NoArgsConstructor
@AllArgsConstructor
@Data
public class Emp { ... }

Emp emp = Emp.builder()
             .name("Franklin")
             .deptId(3)
             .salary(10000)
             .build();
```



### - 4. GlobalExceptionHandler

* Business Logic Handler -- all service logic exception should use this one
* @Valid Handler
* Front-end Input error Handler
* Other Exception Handler





### - DTO

dto → Data Transfer Objects

组合封装（Composition）；

```java
public class EmpDto {
    private Long id;
    private String name;
    private Long deptId;
    
    //组合封装
    List<WorkExperience> experiences;
}
```

提升可维护性，扩展性



##### DTO/Entity

For create/update services, use createDTO/updateDTO to accept json data. For createTime, updated in mapping. Without coping DTO to entity, let query handle it, using NOW().

For get/getPage, use entity to receive the data getting from db. Don't used DTO to receive it.



@NotNull
@NotEmpty
@NotBlank







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



### - Login



##### Jwt Token Verify

To make sure Front-end call api with valid authorization, the user must maintain a valid login status. Since Http is a stateless proxy that every request is independent from each other. So when using apis, the web does not know whether this user has logged in or not. Jwt token gives a way to store the login status.

Tech:

* Session Management: 会话技术

  > is the technology used to let the server remember the same user across multiple HTTP requests, despite HTTP being stateless.
  >
  > no need for a persistent connection

  * Session tracking: 
    * It solved the prob of Http **stateless**, allows sharing data between requests
    * Help server distinguish if the requests come from same web

* Global Filter / Interceptor: 统一拦截技术



##### Session Management

> **Cookie** 
>
> `cons`:
>
> * 移动端APP(Android、IOS)中无法使用Cookie
> * 不安全，用户可以自己禁用Cookie
> * Cookie不能跨域: 
>   * 协议 http/https
>   * IP 
>   * 端口

> **Session**
>
> Session 底层是基于Cookie实现的会话跟踪，如果Cookie不可用，则该方案，也就失效了。
>
> `Pros`：
>
> 存储在服务器，安全
>
> `Cons`：
>
> * 服务器集群环境无法使用 
>   * (负载均衡服务器会将前端请求分发给不同服务器，可能该服务器未存JSESSIONID)
>   * Solution: redis / JWT
> * Cookie全部缺点

> **JWT**
>
> JSON Web Token: 
>
> * Header: 记录令牌类型、签名算法等
> * Payload: 自定义信息（不能包含敏感信息）
> * Signature: 防止Token被篡改
>
> `Pros`:
>
> * 可在token中共享信息
> * 支持PC端、移动端
> * 解决集群环境下的认证问题
> * 减轻服务器的存储压力（无需在服务器端存储）
>
> `Cons`: 
>
> * 需要自己实现（包括令牌的生成、令牌的传递、令牌的校验）
> * 退出登陆，token可能仍然生效



##### Global Filter

JavaWeb三大组件(Servlet、Filter、Listener)之一

```java
@WebFilter(urlPatterns = "/*") //配置过滤器要拦截的请求路径（ /* 表示拦截浏览器的所有请求 ）
public class DemoFilter implements Filter {}

@ServletComponentScan //开启对Servlet组件的支持
@SpringBootApplication
public class WebAiApplication {}
```



##### Global Interceptor

拦截器是Spring框架中提供的，用来动态拦截控制器方法的执行







<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251202124947982.png" alt="image-20251202124947982" style="zoom:20%;" />

> Tomcat并不识别所编写的Controller程序，但是它识别Servlet程序，所以在Spring的Web环境中提供了一个非常核心的Servlet：DispatcherServlet（前端控制器），所有请求都会先进行到DispatcherServlet，再将请求转给Controller。



##### 两者对比

| 特性               | Filter                            | Interceptor                  |
| ------------------ | --------------------------------- | ---------------------------- |
| 所属               | Servlet 规范                      | Spring MVC                   |
| 执行位置           | Tomcat 容器层                     | DispatcherServlet 前后       |
| 拦截范围           | **所有请求（静态 + 动态）**       | **只有 Spring MVC 请求**     |
| 是否拦静态资源     | ✔ 会拦截                          | ✘ 不会拦截                   |
| 是否有 Spring Bean | ✘ 不能 @Autowired（除非特殊处理） | ✔ 可以用 Spring 的 IOC       |
| 典型用途           | 登录过滤、编码处理、XSS过滤       | 登录校验、权限校验、业务拦截 |



##### Tips

Must use **POST** instead of GET

* Most of the time, GET's json body will be ignored. Using url path more often.
* GET should never update data, based on RESTful rules. It is created with function of just get the data.
* For security reason, never use GET for Login. If putting password into url, website may cached these info.

Why return "username or password is wrong" instead of telling user which part is wrong.

> Short answer: This prevents enumerated attacks. If telling user which part is wrong, it gives attackers info for username or password.





### - AOP(面向切面)

Aspect Oriented Programming 

AOP (Aspect-Oriented Programming) is a programming paradigm used to modularize cross-cutting concerns such as logging, security, and transactions. Instead of writing duplicate code in every method, AOP allows injecting additional behavior at specific points in the program (called join points) through aspects and pointcuts. In Spring, AOP is commonly used for logging, permissions, and transaction management.

AOP adds cross-cutting functions on OOP

**AOP usage:** 

* 记录任务耗时
* 记录系统的操作日志
* 权限控制
* 事务管理：Spring事务管理，底层其实也是通过AOP来实现的，只要添加@Transactional注解之后，AOP程序自动会在原始方法运行前先来开启事务，在原始方法运行完毕之后提交或回滚事务

**AOP Pros：**

* 代码无侵入：没有修改原始的业务方法，就已经对原始的业务方法进行了功能的增强或者是功能的改变
* 减少了重复代码
* 提高开发效率
* 维护方便

##### **AOP核心概念**：

* **连接点：JoinPoint**：可以被aop控制的方法，如service中的每一个方法
* **通知：Advice**：将重复的逻辑封装成一个方法，如统计方法执行耗时

```java
		public Object recordTime(ProceedingJoinPoint pjd) throws Throwable {
        long begin = System.currentTimeMillis();
        Object result = pjd.proceed();
        long end = System.currentTimeMillis();
        log.info("Dept Service Methods take times: {}ms", end - begin);
        return result;
    }
```



* **切入点：PointCut**：匹配连接点的条件，通过切入点表达式联系哪些方法能调用

```java
//所有DeptService下的方法都可执行
("execution(* com.franklin.service.impl.DeptServiceImpl.*(..))")
```

* **切面：Aspect**：通知+切入点
* **目标对象：Target**：通知所应用的对象

Spring AOP：

> Spring的AOP底层是基于动态代理技术来实现的，也就是说在程序运行的时候，会自动的基于动态代理技术为目标对象生成一个对应的代理对象。在代理对象当中就会对目标对象当中的原始方法进行功能的增强。



##### **AOP进阶**

###### 1. 通知类型 

|                 |                     Spring AOP 通知类型                      |
| --------------- | :----------------------------------------------------------: |
| @Around         |    环绕通知，此注解标注的通知方法在目标方法前、后都被执行    |
| @Before         |       前置通知，此注解标注的通知方法在目标方法前被执行       |
| @After          | 后置通知，此注解标注的通知方法在目标方法后被执行，无论是否有异常都会执行 |
| @AfterReturning | 返回后通知，此注解标注的通知方法在目标方法后被执行，有异常不会执行 |
| @AfterThrowing  |        异常后通知，此注解标注的通知方法发生异常后执行        |

```java
//后置通知
@After("execution(* com.itheima.service.*.*(..))")

//返回后通知（程序在正常执行的情况下，会执行的后置通知）
@AfterReturning("execution(* com.itheima.service.*.*(..))")

//异常通知（程序在出现异常的情况下，执行的后置通知）
@AfterThrowing("execution(* com.itheima.service.*.*(..))"
```

`@PointCut` : Spring提供的注解，将公共切入点提取出来，减少重复

```java
		//切入点方法（公共的切入点表达式）
    @Pointcut("execution(* com.itheima.service.*.*(..))")
    private void pt(){}

    //前置通知（引用切入点）
    @Before("pt()")
    public void before(JoinPoint joinPoint){
        log.info("before ...");
    }
```





###### 2. 通知顺序

默认按照切面名称字母排序：

* 目标方法前的通知方法：字母排名靠前的先执行
* 目标方法后的通知方法：字母排名靠前的后执行

`@Order(k)` : 切面类的执行顺序; （前置通知：数字越小先执行; 后置通知：数字越小越后执行）



###### 3. 切入点表达式

常见形式：

* execution(……)：根据方法的签名来匹配

```java
//？可省略
execution(访问修饰符?  返回值  包名.类名.?方法名(方法参数) throws 异常?)
```



* @annotation(……) ：根据注解匹配

> 自定义注解

```java
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface LogOperation{
}
```

> Controller

```java
		@Override
    @LogOperation //自定义注解（表示：当前方法属于目标方法）
    public void delete(Integer id) {
        //1. 删除部门
        deptMapper.delete(id);
    }
```

> 切面类

```java
@Slf4j
@Component
@Aspect
public class MyAspect6 {
    //针对list方法、delete方法进行前置通知和后置通知

    //前置通知
    @Before("@annotation(com.itheima.anno.LogOperation)")
    public void before(){
        log.info("MyAspect6 -> before ...");
    }
    
    //后置通知
    @After("@annotation(com.itheima.anno.LogOperation)")
    public void after(){
        log.info("MyAspect6 -> after ...");
    }
}
```



##### 实操

> Design an Audit Log system save create, update, delete log info into database.
>
> Requirements: 操作人、操作时间、执行方法的全类名、执行方法名、方法运行时参数、返回值、方法执行时长
>
> Which advice type? 	`@Around` . 
>
> Why not `@Before + @After` ? 
>
> *  `@After` cannot obtain return value. 
> * Hard to capture exceptions. 
> * Log becomes spilt and duplicated.

###### - 1. Aspect

```java
@Aspect
@Component
public class OperationLogAspect {

    @Autowired
    private OperateLogMapper operateLogMapper;

    // 环绕通知
    @Around("@annotation(log)")
    public Object around(ProceedingJoinPoint joinPoint, LogOperation log) throws Throwable {
        // 记录开始时间
        long startTime = System.currentTimeMillis();

        Object result = null;
        Exception exception = null;

        try {
            result = joinPoint.proceed();    // If throws, jumps to catch
            return result;
        } catch (Exception ex) {
            exception = ex;                  // Record exception
            throw ex;                        // Re-throw so controller handles it
        } finally {
            // 当前时间
            long endTime = System.currentTimeMillis();
            // 耗时
            long costTime = endTime - startTime;

            // 构建日志对象
            OperateLog operateLog = new OperateLog();
          
          	// set variables
            operateLog.setOperateEmpId(getCurrentUserId()); //需要实现 getCurrentUserId 方法
            if (exception != null) {
                operateLog.setException(
                    exception.getClass().getSimpleName() + ": " + exception.getMessage()
                );
            }
            operateLog.setCostTime(costTime);

            // 插入日志
            logService.writeLogAsync(operateLog);
        }
    }
    
    // 示例方法，获取当前用户ID
    private int getCurrentUserId() {
        // 这里应该根据实际情况从认证信息中获取当前登录用户的ID
      	// 因为增删改都可以从token中获取当前用户操作ID，所以可以直接从ThreadLocal中调用
        return 1; // 示例返回值
    }
}
```



###### - 2. ThreadLocal

> It is a local variable of Thread
>
> ThreadLocal为每个线程提供一份单独的存储空间，具有线程隔离的效果，不同的线程之间不会相互干扰。
>
> Every request leads to a thread

<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251202172801854.png" alt="image-20251202172801854" style="zoom:20%;" />

```java
public class CurrentHolder {
    private static final ThreadLocal<Integer> CURRENT_LOCAL = new ThreadLocal<>();
    
    public static void setCurrentId(Integer employeeId) {
        CURRENT_LOCAL.set(employeeId);
    }
    
    public static Integer getCurrentId (){
        return CURRENT_LOCAL.get();
    }
		//清理ThreadLocal数据
    public static void remove() {
        CURRENT_LOCAL.remove();
    }
}
```

1)  Set ID inside preHolder in the interceptor
2) Remove data in ThreadLocal when this method is complete

> prevent data leak; since the Thread is reusable.

```java
		// Don't remove in postHolder; even a method has finished, it may throw an exception.
		@Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        System.out.println("afterCompletion .... ");
        CurrentHolder.remove();
    }
```

Add getID in `OperationLogAspect.java`

```java
		private int getCurrentUserId() {
        return CurrentHolder.getCurrentId();
    }
```

###### - 3. ThreadLocal in Filter

A **Filter** intercepts requests **before they reach a servlet/controller** and can also process responses **after the servlet executes**.

```java
// Filter
    try {
            chain.doFilter(request , response);
        } finally {
            // clear ThreadLocal data
            System.out.println("Current holder data: " + CurrentHolder.getCurrentId());
            CurrentHolder.remove();
            System.out.println("Current Holder stored data has been removed.");
        }
```

Better process:

* Parse Jwt token in Filter and put userId in ThreadLocal
* Validate userId in Interceptor
* AOP get userId and save to Audit Log
* Clear data from ThreadLocal in `finally` in Filter





### - Bugs in development

1. Use `.equals()` instead of `!=` when comparing two objects, and with their variable.

   ```java
   if (updateName != originName && this.existsByName(updateName)) {
   		throw new BusinessException("Name already in use");
   }
   if (updateName.equals(originName) && this.existsByName(updateName)) {
   		throw new BusinessException("Name already in use");
   }
   ```

   > It is because two names coming from two different objects.

2. Problem Example:

   ```java
   //1. front end without 'subject'
   {
     "name": "test-1",
     "room": "107",
     "beginDate": "2024-06-01",
     "endDate": "2025-01-25",
     "masterId": 10
   }
   
   //2. AllArgsConstructor set subject to null
   @Data
   @NoArgsConstructor
   @AllArgsConstructor
   public class ClazzDTO {
     private Integer subject; //学科
   }
   
   //3. mapper.xml update 'subject' requires NOT NULL in database
   update clazz
   	<set>
   		<if test="subject != null">subject = #{subject},</if>
   	</set>
   where id = #{id}
   
   //4.
   /**
   * However, output error
   * Caused by: 
   * java.sql.SQLIntegrityConstraintViolationException: Column 'subject' cannot be null
   */
   ```

   > The reason for this error happened is not due to the `<update>` query. The root cause is from  `<insert>` 
   >
   > Sometimes, the last error doesn't represent the true problem. You need to check more above.

3. Error

   ```java
   ### Error updating database.  Cause: org.apache.ibatis.executor.ExecutorException: Error getting generated key or setting result to parameter object. Cause: org.apache.ibatis.executor.ExecutorException: No setter found for the keyProperty 'id' in 'com.franklin.dto.EmpCreateDTO'.
   
   ### The error may exist in com/franklin/mapper/EmpMapper.xml
   
   No setter found for the keyProperty 'id' in 'com.franklin.dto.EmpCreateDTO'.
   ```

   This error is due to EmpCreateDTO doesn't have the field of id.

   ```xml
   <insert id="insert" useGeneratedKeys="true" keyProperty="id">
           insert into emp(user_name, name, gender, phone, job, salary, image, entry_date, dept_id, create_time, update_time)
           values (#{username},#{name},#{gender},#{phone},#{job},#{salary},#{image},#{entryDate},#{deptId},#{createTime},#{updateTime})
   </insert>
   ```

   `userGeneratedKeys` : “After inserting, go back to the database, get the newly generated primary key, and put it into the Java object you passed into the mapper.”

   

   MyBatis process:

   * Read the object I send to mapper with getters 
   * Replace values in query
   * execute query and got the generate id back using userGeneratedKeys
   * Use setter to set the id into the **same** object
   
   Here is the problem: if the object I gave to mapper does not have that column, Mybatis don't know where to set that key value, and this cause the not found error.



4. GET method cannot receive .json with requestBody; only POST/PUT/Delete can receive json

```java
error: "Required requestBody missing"
```



5. {{}} json format is not correct always leads to NullPointException

```java
NullPointerException: Cannot invoke "java.lang.Integer.intValue()" because "minutes" is null
```



##### MySQL

1. The insert() returned always value = 1 instead of the user.id generated using `useGeneratedKeys= true` 

```java
@Options(useGeneratedKeys = true, keyProperty = "id")
```

useGeneratedKeys是通过获得接收mysql 返回的自增数值，更新到最初传入mapper的对象中；所以能从emp.getId()获得更新后的id数据。
useGeneratedKeys只适用于auto increment columns。

注意，MySQL的insert/update/delete 方法 return how many rows are affected.





Start with a leading `/`

```
action="/api/upload/avatar"
```





### - 项目部署

##### **Linux系统**

安装方式：物理/虚拟机部署

**虚拟机**（Virtual Machine）指通过软件模拟的具有完整硬件系统功能、运行在完全隔离环境中的完整计算机系统。常用虚拟机软件



**Linux Distribution** 

Created based on Linux

Distros:

* Ubuntu
* Debian
* Alphine



### Docker



##### Docker compose

How to rewrite current compose with `secrets` ...

How to set restart at the compose, rather than set it in the terminal

##### Dynamic vs Static

Is static page mobile user friendly?

Is it possible to develop based on both? 



##### Single page vs Multi page

