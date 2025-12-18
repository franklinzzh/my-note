# ⭐ 方案 A：JOIN 一次查完（但数据量多要小心）

SQL：

```
SELECT e.id, e.name, ex.company, ex.position 
FROM emp e
LEFT JOIN emp_expr ex ON e.id = ex.emp_id
WHERE e.id = #{id}
```

Mapper 返回 **扁平结构**，比如：

```
Emp 1 | name="Jack" | company="Alibaba" | position="Engineer"
Emp 1 | name="Jack" | company="Tencent" | position="PM"
```

你再在 Java 里手动组装：

```
EmpDetailVO detail = new EmpDetailVO();
Emp emp = new Emp();
List<EmpExpr> exprList = new ArrayList<>();

// 遍历结果，把重复 emp 去掉，把 empExpr 塞进去……
```

### ✔ 优点

* 只查询一次数据库
* 返回的数据里已经包含两张表的信息

### ❌ 缺点

* JOIN 后有重复行 → Java 必须自己去重
* 如果 emp_expr 表很大（成千上万条经历）JOIN 会变慢
* MyBatis 处理多对一、多对多结构比较麻烦
* 不适合分页（分页 JOIN 是噩梦）

------

# ⭐ 方案 B：MyBatis 的多结果映射（resultMap + collection）

MyBatis 可以帮你自动把 JOIN 的结果转换成：

```
Emp {
  id: 1,
  name: "Jack",
  exprList: [
    {company="Alibaba"}, 
    {company="Tencent"}
  ]
}
```

mapper.xml 写法类似：

```
<resultMap id="empDetailMap" type="Emp">
    <id property="id" column="emp_id" />
    <result property="name" column="emp_name" />

    <collection property="exprList" ofType="EmpExpr">
        <result property="company" column="company" />
        <result property="position" column="position" />
    </collection>
</resultMap>

<select id="getEmpDetail" resultMap="empDetailMap">
    SELECT ...
    FROM emp LEFT JOIN emp_expr ...
</select>
```

### ✔ 优点

* 只查一次数据库
* MyBatis 自动把关联 List 填好
* Controller 返回 VO 即可

### ❌ 缺点

* MyBatis XML 比较复杂
* 分页时很难处理（会重复数据）
* 不适合大数据 JOIN

**大公司内部基本只在“单个详情页”使用这种方式。**

------

# ⭐ 方案 C：写 DTO 并让 Mapper 直接返回组合数据（推荐）

定义一个 DTO：

```
@Data
public class EmpDetailDTO {
    private Long id;
    private String name;
    private String gender;
    private String company;  // 工作经历字段
    private String position;
}
```

SQL JOIN 查询：

```
SELECT e.id, e.name, ex.company, ex.position
FROM emp e
LEFT JOIN emp_expr ex ON e.id = ex.emp_id
WHERE e.id = #{id}
```

Mapper 返回 List<EmpDetailDTO>：

```
[
  {id=1, name=Jack, company=Alibaba, position=Engineer},
  {id=1, name=Jack, company=Tencent, position=PM}
]
```

Service 中再拼成 VO：

```
EmpDetailVO vo = new EmpDetailVO();
List<EmpDetailDTO> list = empMapper.getDetail(id);

vo.setId(list.get(0).getId());
vo.setName(list.get(0).getName());

List<EmpExprVO> exprList = list.stream()
                    .map(x -> new EmpExprVO(x.getCompany(), x.getPosition()))
                    .collect(Collectors.toList());

vo.setExprList(exprList);
```

### ✔ 优点（最灵活）

* 只查询一次 DB
* 不会导致 Entity 变脏
* DTO 字段可以随意加、随意组合
* 分页时依然灵活（DTO 不会重复结构）

### ✔ 企业里最常用的方法

大厂通常不让实体类承担过多责任，因此这种 **DTO 承担 JOIN 结果的方式**最灵活。

------

# 🟩 最终总结（让你100%清楚）

| 方法                             | 查询次数 | 说明                                               |
| -------------------------------- | -------- | -------------------------------------------------- |
| **2 次查询（你现在用的）**       | 2        | 逻辑清晰、安全、维护性最强（ 推荐用于列表、分页 ） |
| **JOIN + resultMap（一次查完）** | 1        | 适合“单个详情页”，不适合分页                       |
| **DTO 承担组合结果（一次查完）** | 1        | 大厂最常用、灵活性最高（推荐）                     |



# resultMap



### resultMap 是如何识别“哪些属于同一个父对象”的？

父对象必须有 `<id>` 标签（唯一标识）

 子对象（collection）必须有 `<id>` 标签

### 自动拼接 List 的原理（非常重要）

MyBatis 遵循如下算法：

**遍历每一行 JOIN 结果**

假设共 3 行：

**行 1：**

* emp_id=1 → 当前没有父对象，就 new Emp
* expr_id=101 → exprList 新增一条

**行 2：**

* emp_id=1 → 已存在同一个父对象（通过 `<id>` 判断） → 不 new
* expr_id=102 → exprList 再追加一条

**行 3：**

* emp_id=1 → 依旧是同一个 Emp
* expr_id=103 → exprList 再追加一条





### 为什么 resultMap 分页时很难处理（会重复数据）？