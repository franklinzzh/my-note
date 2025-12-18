# Database

### Basic

##### Concepts:

* **数据库管理系统 (Database Management System - DBMS):** 科学地组织和存储数据、高效地获取和维护数据；为我们屏蔽了底层文件操作的复杂性，提供了一套标准接口（如 SQL）来操纵数据，并负责并发控制、事务管理、权限控制等复杂问题。如 MySQL。
* **数据库 (Database - DB):** 按照一定数据模型组织、描述和储存起来的、可以被各种用户共享的结构化数据的集合。
* 

##### DBMS 功能

1. **数据定义**：
2. **数据操作**：
3. **数据控制**：包含并发控制、事务管理、完整性约束、权限控制、安全性限制等功能
4. **数据库维护**： 数据的导入导出、数据库的备份与恢复、性能监控与分析、以及系统日志管理等。



##### DBMS 分类

* 关系型数据库（RDBMS）*(ACID)*
  * 严格的表结构和 SQL，非常适合结构化数据和需要事务保证的场景，例如银行交易、订单系统。如Mysql、PostgreSQL、Oracle。
* NoSQL数据库 *(BASE)*
  * 键值数据库：Redis
    * **特点：**Map，通过 Key 来存取 Value。内存操作，性能极高。
    * **适用场景：** 非常适合做缓存、会话存储、计数器等对读写性能要求极高的场景。
  * 文档数据库：MongoDB
    * **特点：** 它存储的是半结构化的文档（比如 JSON/BSON），结构灵活，不需要预先定义表结构。
  * 列式数据库：HBase
    * **特点：** 数据是按列族而不是按行来存储的。这使得它在对大量行进行少量列的读取时，性能极高。
    * **适用场景：** 专为海量数据存储和分析设计，非常适合做大数据分析、监控数据存储、推荐系统等需要高吞吐量写入和范围扫描的场景。
  * 图形数据库：Neo4j
    * **特点：** 数据模型是节点（Nodes）和边（Edges），专门用来存储和查询实体之间的复杂关系。
    * **适用场景：** 在社交网络（好友关系）、推荐引擎（用户-商品关系）、知识图谱、欺诈检测（资金流动关系）等场景下，表现远超关系型数据库。

* NewSQL数据库: 分布式存储+SQL+事务



##### ACID vs BASE

* Atomicity：roll back if one failed
* Consistency: data, constraints, rules, and invariants must hold
* Isolation
* Durability



##### Relational DB: 

* tuple
* key
* Candidate key
* pk
* fk
* uk
* nn

##### ER diagram

* 实体
* 属性
* 联系



##### 删除

* drop:  `drop table <tablename>` remove data and table.
* delete: `delete from <tablename> where`, without where, similar to truncate.
* truncate: `truncate table <tablename>` remove data in table, autoincrement start reset to 1.

> `truncate` 和 `drop` 属于 DDL(数据定义语言)语句，操作立即生效，原数据不放到 rollback segment 中，不能回滚，操作不触发 trigger。而 `delete` 语句是 DML (数据库操作语言)语句，这个操作会放到 rollback segment 中，事务提交之后才生效。



##### DDL & DML

* DML 是数据库操作语言（Data Manipulation Language）的缩写，是指对数据库中表记录的操作，主要包括表记录的插入、更新、删除和查询，是开发人员日常使用最频繁的操作。
* DDL （Data Definition Language）是数据定义语言的缩写，简单来说，就是对数据库内部的对象进行创建、删除、修改的操作语言。它和 DML 语言的最大区别是 DML 只是对表内部数据的操作，而不涉及到表的定义、结构的修改，更不会涉及到其他对象。DDL 语句更多的被数据库管理员（DBA）所使用，一般的开发人员很少使用

##### Database design

1. **需求分析** : 分析用户的需求，包括数据、功能和性能需求。
2. **概念结构设计** : 主要采用 E-R 模型进行设计，包括画 E-R 图。
3. **逻辑结构设计** : 通过将 E-R 图转换成表，实现从 E-R 模型到关系模型的转换。
4. **物理结构设计** : 主要是为所设计的数据库选择合适的存储结构和存取路径。
5. **数据库实施** : 包括编程、测试和试运行
6. **数据库的运行和维护** : 系统的运行与数据库的日常维护。













