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



###### - DQL

The SQL engine works like this:

> 1. FROM + WHERE
> 2. GROUP BY
> 3. AGGREGATE (COUNT, SUM...)
> 4. HAVING (filters aggregated results)
> 5. SELECT
> 6. ORDER BY

<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251114165035470.png" alt="image-20251114165035470" style="zoom:40%;" />

* 



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



##### **分组查询**

```sql
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



##### `Delete table data with fk`

```sql
SET FOREIGN_KEY_CHECKS = 0;

TRUNCATE TABLE orders;
TRUNCATE TABLE users;

SET FOREIGN_KEY_CHECKS = 1;
```



##### 多表查询

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



##### `MyBatis` query



`SELECT`
`INSERT INTO`
`UPDATE`
`DELETE FROM` 

```sql
INSERT INTO dept(column1, colume2) VALUES(#{entityName1}, #{entityName2})

UPDATE dept SET column1 = '#{entityName1}', column2 = '#{entityName2}' WHERE id = #{id}
```



### `Controller` API

`GET` - get
`POST` - add
`PUT` - update
`DELETE` - delete

##### Integer / Object

> 遇到复杂情况，需要多个字段，使用DTO（object）
>
> 简单情况如 id，直接使用基本类型

⚠️ `Integer` 可以为 `null` ；`int` 不能为 `null`; 所以接口一定要用包装类



`@PathVariable`

`http://localhost:8080/depts/1`

```java
@GetMapping("/depts/{id}")
public Result getDept(@PathVariable Integer id) {}
```



`@RequestBody`

Recieve `.json` data

```
PUT - http://localhost:8080/depts 请求参数：{"id": 1, "name": "研发部"}
```

```java
@PutMapping("/depts")
public Result updateDept(@RequestBody Dept dept) {}
```



##### 分页逻辑

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



##### Entity

###### 实体类可以包含数据库没有的字段（很常见！）

```java
public class Emp {
    private Integer id;
    private Integer deptId;

    // 扩展字段（数据库里没有）
    private String deptName;
}
```

* 扩展字段 / 非持久化字段（transient field）
*  VO（View Object）字段
*  仅用于返回给前端的展示字段

> 这些字段：
>
> * 不会插入数据库
> * 不会更新数据库
> * 不会出现在 emp 表里
> * 不会被 ORM 自动持久化

###### 构造方法

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
