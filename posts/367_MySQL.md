# MySQL

作为前端，你可以把 **MySQL** 理解为 **后端专门用来存“正式数据”的超级 Excel 表格**，只不过它存在服务器上，支持无数人同时读写，而且查询速度极快。

### 1. 核心概念翻译（Excel 类比法）

| MySQL 概念              | 前端/Excel 类比                          | 通俗解释                                                     |
| :---------------------- | :--------------------------------------- | :----------------------------------------------------------- |
| **数据库（Schema）**    | 一个 **Excel 工作簿文件**                | 你们项目里的 `weique-lowcode` 就是一个“大文件”，里面装了所有业务数据（用户表、案件表、流程表等）。 |
| **表（Table）**         | Excel 里的 **Sheet（工作表）**           | 比如 `sys_user` 表专门存用户信息，`case_info` 表专门存案件信息。互不干扰。 |
| **行（Row/Record）**    | Excel 里的 **一行数据**                  | 代表一条具体记录，比如“张三”的账号信息就是一行。             |
| **列（Column/Field）**  | Excel 里的 **表头（列名）**              | 比如 `username`、`password`、`create_time`。**关键区别**：MySQL 的列在创建时必须指定数据类型（比如 `VARCHAR(50)` 代表最长 50 个字符的字符串，`INT` 代表整数），不能像 Excel 那样随意乱填类型。 |
| **主键（Primary Key）** | 每一行的 **“身份证号”**                  | 通常是 `id` 字段，唯一且不能重复，用来快速锁定某一行数据。   |
| **SQL 语句**            | 对着 Excel 做的 **“高级筛选 + VLOOKUP”** | 比如 `SELECT * FROM sys_user WHERE age > 18`，就是“把年龄大于 18 岁的用户全部筛出来”。 |

### 2. 针对你这个项目的“特殊背景”

- **Schema 名字叫 weique-lowcode**：说明这套数据库专门服务于你们“微企/微权”的低代码业务。Jeecg-Boot 的底层代码会自动根据这个库名生成增删改查（CRUD）的 SQL。
- **你有 93 个 Mapper**：这些 Mapper 就是负责**写 SQL 语句**的 Java 文件。你可以把它们想象成 **“93 个专门负责操作不同 Sheet 的脚本”**。
  - 比如 `UserMapper.java` 里定义了一个 `selectByUsername()` 方法，底层执行的 SQL 就是 `SELECT * FROM sys_user WHERE username = ?`。
- **版本是 MySQL 5.7**：这是个很成熟稳定的老版本（相当于 Vue 2）。虽然 MySQL 8.0 已经出了，但 5.7 依然在大量企业项目中使用。**需要注意**：5.7 默认不支持 `WITH` 递归查询等新语法，如果你在日志里看到复杂的 SQL 报错，基本可以排除是 MySQL 版本太低导致的语法不支持。

### 3. 前端联调时，你和 MySQL 的“间接关系”

作为前端，**你永远不直接操作 MySQL**（你不会在后端代码里写 SQL）。你的交互路径是：

> **你的浏览器（Vue/React）** → 调用接口（如 `/api/user/list`）→ **后端 Controller** → **Service（业务逻辑）** → **Mapper（执行 SQL）** → **MySQL（返回数据）** → 逐层返回给你 JSON。

**但你得留意这几个点**：

1. **时间/日期格式乱码**：MySQL 5.7 对时区敏感。如果后端返回给你的时间（`create_time`）比实际少了 8 小时或多了 8 小时，**不是后端代码错了**，是 MySQL 连接的 `serverTimezone` 没设成 `Asia/Shanghai`。让后端在数据库连接串（`jdbc:mysql://...`）后面加上 `?serverTimezone=Asia/Shanghai` 即可。
2. **中文变成问号（???）**：这是编码问题。MySQL 5.7 建表时如果不指定 `CHARACTER SET utf8mb4`，存中文就会乱码。如果遇到，让后端运维执行 `ALTER DATABASE weique-lowcode CHARACTER SET utf8mb4;`。
3. **慢接口排查**：如果你发现某个列表接口加载花了 3 秒，大概率是 MySQL 里对应的表**没有建索引**（相当于 Excel 没有做“筛选器”导致全表扫描）。后端的 Mapper.xml 里如果 SQL 复杂，你可以让后端在 Navicat（MySQL 图形化管理工具，相当于后端的“Robo 3T”）里跑一遍 `EXPLAIN` 看执行计划。

### 4. 给你的“入门级”工具推荐（方便查数据）

后端联调时，如果你需要自己看一眼数据库里的真实数据（比如确认某个字段有没有存进去），别用黑乎乎的终端（命令行），装一个**图形化工具**：

- **Navicat Premium**（付费，但公司一般会买）：界面像 Excel，点点点就能看表数据、写测试 SQL。
- **DBeaver**（免费开源）：社区版完全够用，功能也很强大。
- **DataGrip**（JetBrains 全家桶，和 IDEA 同厂）：如果你习惯 IDEA 的快捷键，这个最顺手。

**一句话总结**：把 MySQL 当成**后端的“巨型 JSON 数据库”**，表结构就是固定的 `interface`（TypeScript 里的类型约束），Mapper 就是封装好的 API 查询函数。只要接口返回的 JSON 格式没问题，MySQL 那边就基本不用你操心。如果接口报 500 且日志里出现 `SQLException`，那就是 MySQL 这张表或者 SQL 语句出问题了。