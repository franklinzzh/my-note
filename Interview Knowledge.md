# Interview Knowledge

## ⭐ SDE 面试总体要考什么

SDE 面试几乎都包含 5 大部分：

1. **Coding（算法）** → LeetCode 中等 50–150 题
2. **System Design（系统设计）** → 初级小系统设计，高级大规模架构
3. **Behavioral（行为面试）** → STAR 故事
4. **Project Deep Dive（项目深挖）** → 任意语言都必须
5. **CS 基础（操作系统、网络、数据库、并发）**

## ✅ 1. Coding（算法）

这个你已经知道了：

* LeetCode（中等为主、少量 hard）
* 考察：数据结构、算法、时间复杂度、边界情况
* 通常现场 coding + follow up

------

## ✅ 2. System Design（系统设计）

即使是初级 SDE 也会逐渐考这部分，尤其是后端方向。

考察内容一般包括：

### ⭐ 2.1 小系统设计（Junior / New Grad 常考）

* 设计一个 Rate Limiter
* 设计一个 URL Shortener
* 设计一个文件上传系统
* 设计一个简单登录系统 + Session/JWT
* 聊清楚：数据流、数据库模型、扩展性、瓶颈点

### ⭐ 2.2 大系统设计（Mid/高级）

* 设计高并发服务：比如订单系统、Feed 流、消息队列
* 设计电商库存系统
* 设计聊天系统（支持群聊、在线状态、消息同步）

重点考：

* 架构拆解
* 数据库选择
* 读写扩散、缓存、MQ、负载均衡
* 扩展性、高可用
* CAP、事务、幂等性、限流

------

## ✅ 3. OOD（面向对象设计）

前 Amazon、Uber、Meta 都爱问。

面试内容：

* 设计一个电梯系统
* 设计停车场
* 设计一个通知系统
* 怎么设计一个游戏类（扑克牌、黑杰克）

考察点：

* 类的职责划分
* 抽象、继承、接口
* 可扩展性
* 代码的可维护性

------

## ✅ 4. Behavioral / Leadership（行为面试）

所有大厂都极其重视，尤其是 Amazon 的 LP（Leadership Principles）。

常见问题：

* 讲一次你处理冲突的经历
* 讲一个你推动某个项目落地的例子
* 讲你遇到最大困难的经历
* 讲一个你如何快速学习新技术的例子
* 为什么离开上一份工作
* 失败经历、成功经历、团队合作经历

准备方法：

* STAR 模型（Situation / Task / Action / Result ）
* 列出 10 个项目故事轮流使用

------

## ✅ 5. Project Deep Dive（深入项目聊技术）

尤其针对你写在简历上的 Java/SpringBoot 项目。

面试官会问：

* 为什么要用这个技术？权衡是什么？
* 系统结构能画一个架构图吗？
* 最大的挑战是？你怎么解决？
* 你的服务怎么保证高可用？
* 如何做并发？如何做缓存？
* 如何处理数据一致性（最终一致、分布式锁、MQ 重试）？
* 如果流量暴涨 10 倍怎么办？
* 是否有遇到过性能瓶颈？

这块**是决定你是否“像个工程师”**的关键。

------

## ✅ 6. 基础知识：CS Fundamentals

后端方向常考这些：

### ⭐ 6.1 操作系统

* 线程 vs 进程
* 死锁
* 上下文切换
* 内存分配、GC
* 同步/互斥

### ⭐ 6.2 网络

* TCP vs UDP
* 三次握手
* HTTPS 原理
* DNS 解析
* CDN
* HTTP/1.1 vs HTTP/2 vs HTTP/3

### ⭐ 6.3 数据库

* 索引结构（B+ 树）
* 事务（ACID）
* 隔离级别
* 锁
* 乐观/悲观并发
* SQL vs NoSQL
* 如何做分页、模糊搜索、高并发写入

------

## ✅ 7. 工程能力（现实开发能力）

LeetCode 考不出这些，但企业非常看重：

* Git 熟练程度
* 阅读 API 文档能力
* 日志、监控、排错能力
* 如何写单元测试
* 如何调优代码
* CI/CD（GitHub Actions、Jenkins）
* Docker、容器化、部署
* Linux 基本命令

很多公司在 Onsite 会让你做：

* Code Review
* Debugging
* 网上写一段 clean code

------

# 总结：SDE 面试的七大模块

| 类别              | 是否必考           | 难度 |
| ----------------- | ------------------ | ---- |
| Coding 算法       | ✔️必考              | ⭐⭐⭐  |
| System Design     | 初级少、中高级必考 | ⭐⭐⭐⭐ |
| OOD               | 看公司             | ⭐⭐⭐  |
| Behavior          | ✔️必考              | ⭐⭐   |
| Project Deep Dive | ✔️必考              | ⭐⭐⭐⭐ |
| CS Fundamentals   | 高度相关           | ⭐⭐⭐  |
| 工程能力          | 看公司             | ⭐⭐⭐  |





# 学习路径

## ✅ 1. **操作系统（OS）基础**

你必须掌握（但不需要极深），这些面试必考：

### 要点：

* 线程 vs 进程
* 同步、互斥、锁、死锁
* Context Switching
* CPU 调度
* 虚拟内存、分页
* 文件系统（非常常考）
* 并发模型（Java 线程池、Executor）

**为什么要学？**
 任何后端开发都离不开并发、线程池、性能问题，面试官会问：

> “Java 线程池是什么？为什么要用？线程之间怎么通信？”
>  “死锁是怎么产生的？怎么避免？”

------

## ✅ 2. **计算机网络（Networking）**

后端开发最重要的基础之一，你在学校几乎没学，但面试必考。

### 必备内容：

* TCP vs UDP
* 三次握手 / 四次挥手
* HTTP 1.1 / 2.0 / 3.0 区别
* HTTPS（TLS 握手、证书、非对称加密）
* DNS、CDN
* Cookie & Session、JWT
* REST、RPC
* CORS
* 负载均衡（面试常问）

### 面试常问例子：

* “为什么要三次握手？”
* “HTTPS 是怎么保证安全的？”
* “Cookie、Session、JWT 的区别？”

这部分是你*现在完全缺失但必须补*的。

------

## ✅ 3. **系统设计（System Design）基础（轻量级）**

你目前的课程完全没有涉及，但对于后端 SDE 是必须具备的。

不用深到高并发架构，但要懂这些：

### 初级必备系统设计：

* URL Shortener
* 登录系统（Session/JWT）
* Rate Limiter
* 聊天系统的基本原理
* 文件上传系统
* Cache（Redis）如何使用

### 核心知识点：

* 缓存（Redis）
* 消息队列（Kafka/RabbitMQ）
* 分布式锁
* 数据一致性
* 水平扩展 vs 垂直扩展
* 读写分离

你现在有 Java/SpringBoot 项目背景，很适合补这块。

------

## ✅ 4. **工程能力（Software Engineering Skills）**

学校不会教，但公司非常看重；你要补的内容包括：

### 4.1 Linux 基本命令

* cd、ls、grep、tail、curl
* top、df、du
* 日志分析（日志太重要了）

### 4.2 Git

* branching
* merge / rebase
* code review 习惯

### 4.3 Docker（你现在已经在用，继续深入）

* Dockerfile
* Volume
* 容器间网络
* 本地 + 服务器部署

### 4.4 Spring Boot 基础（你已经在做项目）

继续提升：

* Spring MVC 工作流
* AOP（Logging、Security）
* Spring Security + JWT
* MyBatis/JPA
* 全局异常处理
* 缓存（Redis）
* 线程池
* 分页、事务、锁、并发问题

------

## ⭐ 综合能力图（你现在的位置 vs SDE 要求）

| 能力           | 你目前        | SDE 要求     | 差距                      |
| -------------- | ------------- | ------------ | ------------------------- |
| 数据结构与算法 | ✔             | ✔            | ✅OK                       |
| 数据库         | ✔             | ✔            | 小差距（索引/事务需要补） |
| 机器学习       | ✔             | ⚠️ irrelevant | 不重要                    |
| 操作系统       | ❌             | ✔            | 要补                      |
| 计算机网络     | ❌             | ✔            | 要补（重点）              |
| 系统设计       | ❌             | ✔            | 要补（轻量级就够）        |
| Java 工程能力  | ✔（但可加强） | ✔            | 继续提升                  |
| Docker/Linux   | ✔（基础）     | ✔            | 继续提升                  |

# 

# ⭐ 给你一个最适合你现在背景的学习路线（2–3 个月版）

🚀 总体策略

每个月专攻一个主方向：

* **第 1 月：补 CS 基础（Networking + OS）**
* **第 2 月：补工程能力（部署、Linux、Docker、Git、CI/CD）**
* **第 3 月：系统设计 + 项目加强 + 面试准备**



## ⭐ 第 1 个月：补 CS 基础（必须补齐）

你现在最缺、也是所有面试都会问的，就是：

* 网络
* 操作系统
* 并发（尤其 Java）

这部分补齐后，就能回答 70% 的基础知识面试题。

------

### 📌 Week 1–2：计算机网络（Networking）

目标：能答出所有高频面试题。

#### 必学主题（SDE 必考）：

* TCP / UDP 区别
* 三次握手 / 四次挥手
* 拥塞控制（Reno、Cubic）
* HTTP 1.1 / 2.0 / 3.0
* HTTPS 是如何加密的（TLS 握手）
* Cookie / Session / JWT（你做 Java Web 项目用得上）
* DNS / CDN / 反向代理（Nginx）
* REST vs RPC
* CORS 原理

#### 面试会问：

* 为什么要三次握手而不是两次？
* HTTPS 怎么保证数据不被中间人篡改？
* 浏览器输入 URL 到页面显示经历了什么？
* JWT 为什么是无状态的？有什么缺点？

#### 推荐资源：

* 《计算机网络：自顶向下方法》前 5 章
* 1–2h YouTube CS144 Networking 课程精华

------

### 📌 Week 3：操作系统（OS）

面试重点不是实现 OS，而是理解线程与并发。

#### 要学：

* 进程 vs 线程
* 线程状态切换
* 锁（互斥锁、读写锁）
* 死锁（产生原因 + 预防 + 检测）
* 内存分页、虚拟内存
* CPU 调度（RR、优先级等）

#### Java 后端常问：

* 什么是线程安全？
* 什么情况下会发生死锁？
* synchronized 的底层原理？
* 线程池为何更高效？

------

### 📌 Week 4：Java 并发（你用 Java 项目必备）

Java Concurrency 是所有 Java SDE 必问。

#### 必学：

* Executor + 线程池
* CompletableFuture
* synchronized vs Lock
* volatile
* CAS
* ConcurrentHashMap 原理
* 生产者-消费者模型



## ⭐ 第 2 个月：工程能力（能让你从“学生”变“工程师”）

SDE 真正考的不是语言，而是工程能力。
 你已经有 Java Web、Docker 基础，这个月让你变成“能上线项目”的工程师。

------

### 📌 Week 5：Docker & Linux 深度使用

你会基础 Docker，但要补：

#### Docker：

* Dockerfile 优化（多阶段构建）
* Volume / bind mount 区别
* Docker 网络（bridge、host、overlay）
* 用 nginx + Docker 部署前后端
* docker-compose（非常重要）

#### Linux：

服务器必须会的命令：

* cd, ls, grep, tail -f
* top, htop
* systemctl
* journalctl
* curl
* scp/rsync
* ufw / firewall

------

### 📌 Week 6：数据库原理（你有基础，但要升维）

你只上过 database 课程，但远不够面试。

要补这些：

#### MySQL：

* 索引（B+树）
* 索引失效情况
* 事务隔离级别（RR、RC）
* 死锁
* 执行计划 explain
* SQL 优化

#### NoSQL：必须学 Redis 基础

* 字符串、哈希、Set、Sorted Set
* 缓存穿透/击穿/雪崩
* 分布式锁
* Redis 与数据库一致性策略

------

### 📌 Week 7：Git + CI/CD（现代工程必考）

Git（20% 的公司现场让你做 merge/rebase）：

* branch
* merge vs rebase
* cherry-pick
* conflict resolve
* PR review

CI/CD：

* GitHub Actions（最容易入门）
* 自动 build + test + deploy

------

### 📌 Week 8：Node.js / SpringBoot 工程化

你不局限于 Java，但你已经在 Java Web 项目上花时间了，可以继续深化：

#### 后端必备：

* 日志（logback / winston）
* 全局异常处理
* 安全（Spring Security）
* 中间件（Redis）
* Swagger 文档
* RESTful 规范
* 接口鉴权
* 文件上传、分页、事务、锁
* 单元测试（JUnit）

你的项目会变得非常专业。



## ⭐ 第 3 个月：系统设计 + 项目深挖 + 面试准备

------

### 📌 Week 9：系统设计（你完全缺，需要补）

目标：掌握 8~12 个小型设计题。

必须会的小系统设计：

* Login System（Session/JWT）
* Rate Limiter
* URL Shortener
* Cache + DB 架构
* Feed 流
* 聊天系统
* 文件上传系统

学习重点：

* 流量估算（QPS）
* 分区、分片
* 读写分离
* 缓存策略
* MQ 的使用场景
* 高可用架构

##### OOD

📌 **Day 1：复习 OOP 四大特性 + SOLID**

* 封装、继承、多态、抽象
* SOLID 原则（面试常问）

📌 **Day 2：核心设计模式**

重点会用的 6 个：

* Singleton
* Factory
* Strategy
* Observer
* Builder
* Decorator

面试能举例说明即可，不用死记硬背。

📌 **Day 3–5：刷 5–8 道 OOD 面试题**

重点题型：

1. **Parking Lot**（考试频率最高）
2. **Elevator system**
3. **Coffee maker / Vending machine**
4. **Online booking system**
5. **Blackjack game**
6. **File system**

只要你能：

* 正确拆类
* 讲清楚职责、扩展性
* 画出基本 UML
* 支持未来可扩展

------

### 📌 Week 10：强化你自己的项目（简历杀器）

你有 Java、Node、Vue3 项目，这周把它升级到“能面试拿出来讲”的级别：

让项目具备：

* 完整架构图
* 日志、限流、分页、缓存
* 增加 Redis 缓存一处
* 增加 MQ（可选）
* 加一个线程池任务
* 做性能优化
* 并发场景设计（例如库存扣减、并发更新）

然后准备项目 Deep Dive 问题：

* 为什么这样设计？
* 最大挑战？
* 数据一致性怎么保证？
* Redis 为什么加？
* 线程池怎么用？
* 如何应对高并发？

------

### 📌 Week 11：LeetCode 60 题 + Behavior（STAR）

每天 2 题 Medium
 加上准备以下 10 个 STAR 故事：

* 冲突处理
* 推动项目
* 失败经历
* 成功经历
* 性能优化
* 改善流程
* 从 0 到 1 做一个项目
* 时间管理
* 帮助团队
* 最难 Bug