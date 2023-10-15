# Ki1z's MySQL学习笔记

`更新时间：2023-10-15`

注释解释：

- `<>`必填项，必须在当前位置填写相应数据

- `{}`选择必填项，必须在当前位置选择一个给出的选项

- `[]`可选项，可以选择填写或忽略

# 数据库介绍

## 数据库概念

数据库是按照数据结构来组织，存储和管理数据的建立在计算机存储设备上的仓库

## 数据库分类

**网络数据库**

借助于网络，将数据存储在网络上进行有效管理，并实现用户与网络中的数据库进行实时动态数据交互

**层级数据库**

层次模型实质上是一种有根节点的定向有序树

*在数学中“树”被定义为一个无回的连通图*

**关系数据库**

关系数据库是建立在关系模型上的数据库，借助于集合代数等数学概念和方法来处理数据库中的数据

**其他方式**

数据库的另外一种分类方式，通过存储介质分类，即硬盘和内存

- 关系型数据库：存储在硬盘中

- 非关系型数据库：存储在内存中

## 关系型数据库

**基本概念**

关系型数据库，建立在关系模型上的数据库，借助于集合代数等数学概念和方法来处理数据库中的数据。现实世界中的各种实体以及实体之间的各种联系均用关系模型表示。关系模型是由埃德加·科德于1970年首先提出的并配合“科德十二定律”。现如今虽然对此模型有一些批评意见，但它还是数据存储模型的传统标准，关系模型由`关系数据结构`、`关系操作集合`、`关系完整性约束`三部分组成

- 关系数据结构：指数据以什么方式来存储，是一种二维表的形式存储
  
> 本质：二维表
> <img src="https://github.com/Ki1z/PHP-Study-Notes/blob/main/Image/0OD_PV~9)JE6%7D4OBEXUB)VM.png?raw=true">

- 关系操作集合：如何来关联个管理对应的存储数据，SQL指令。

> 获取张三的年纪，已知条件为姓名
> ```php
> select 年龄 from 二维表 where 姓名 = 张三
> ```

- 关系完整性约束：数据内部有对应的关联关系，以及数据与数据之间也有对应的关联关系。

  - 表内约束：对应的具体列只能放对应的数据（不能乱放）

  - 表间约束：自然界各实体间都是有着对应的关联关系（外键）

**典型的关系型数据库**

Oracle , DB2 , Microsoft SQL Server , Microsoft Access , MySQL , SQLite

- 小型关系型数据库：Microsoft Access , SQLite

- 中型关系型数据库：Microsoft SQL Server , MySQL

- 大型关系型数据库：Oracle , DB2

*MySQL当前跟Oracle是一个公司，隶属于Oraccle*

---

# SQL介绍

## SQL基本介绍

Structured Query Language，结构化查询语言，简称SQL，是一种特殊目的的编程语言，是一种数据库查询和程序设计语言，用于存取数据以及查询、更新和管理关系数据库系统，同时也是数据库脚本文件的扩展名

*SQL就是专门为关系型数据库而存在的*

## SQL分类

**数据查询语言** `Data Query Language`

其语句，也称为“数据检索语句”，用以从表中获得数据，确定数据是怎样在应用程序给出。保留字 `SELECT` 是DQL（也是所有SQL）使用最多的动词，其他DQL常用的保留字有 `WHERE` , `ORDER BY` , `GROUP BY` 和 `HAVING` 。这些DQL保留字常与其他类型的SQL一起使用。

*专门用于查询数据*

**数据操作语言** `Data Manipulation Language`

其语句包括动词 `INSERT` , `UPDATE` 和 `DELETE` 。它们分别用于修改和删除表中的行。也成为动作查询语句。

*专门用于写数据*

**事务处理语言** `Transaction Control Language`

它的语句能确保被DML所影响的表的所有行及时得以更新。TPL语句包括 `BEGIN` , `TRANSACTION` , `COMMIT` 和 `ROLLBACK` 。（不是所有的关系型数据库都提供事务安全处理）

*专门用于事务安全处理*

**数据控制语言** `Data Control Language`

它的语句通过 `GRANT` 和 `REVOKE` 获得许可，确定单个用户和用户组对数据对象的访问。它的某些RDBMS可用 `GRANT` 和 `REVOKE` 控制对表单个列的访问。

*专门用于权限管理*

**数据定义语言** `Data Definition Language`

其语句包括动词 `CREATE` 和 `DROP` 。在数据库中创建新表或删除表，为表加入索引等。DDL包括许多与人数据库目录中获得数据有关的保留字。它也是动作查询的一部分。

---

# MySQL介绍

## MySQL基本介绍

MySQL是一个关系型数据库管理系统，由瑞典MySQL AB公司研发，目前属于Oracle旗下产品。MySQL是最流行的关系型数据库管理系统之一，在WEB应用方面，MySQL是最好的RDBMS（Relational Database Management System 关系数据库管理系统）应用软件。 

- MySQL是一款开源免费的产品

- MySQL对PHP的支持是最好的

*MySQL中用到的指令就是SQL指令*

## 启动和停止MySQL服务

MySQL是一种C/S结构：客户端和服务端

服务端对应的软件：Mysqld.exe

**命令行方式**

通过Windows下打开CMD控制台，然后使用命令进行管理

`Net start 服务(mysql)` ：开启服务
`Net stop 服务(mysql)`：停止服务

**系统服务方式**

*前提：在安装MySQL的时候将其添加到了Windows的服务中*

- 方式 1：进入服务

  > 右键此计算机 > 管理 > 服务和应用程序 > 服务 > 找到MySQL > 启动

- 方式 2：通过命令行

  > `Win` + `R` > 输入 `services.msc` > 找到MySQL > 启动

## 退出和登录MySQL系统

通过客户端（mysql.exe）与服务器进行连接认证，就可以进行操作

*通常：服务端与客户端不在同一台电脑上*

**登录**

1. 找到mysql.exe

  *通过cmd控制台，如果在安装的时候指定了mysql.exe所在的路径为环境变量，就可以直接访问；如果没有，就必须进入mysql.exe所在路径*

2. 输入对应的服务器地址 `-h`

  *-h代表host，举例：-h[IP地址/域名]*

3. 输入对应服务器中MySQL监听的端口 `-P`

  *-P代表port，举例：-P:3306，<b>此处的P必须大写</b>*

4. 输入用户名 `-u`

  *-u代表user，举例：-u:root*

5. 输入密码 `-p`

  *-p代表password，举例：-p:root，<b>此处的p必须小写</b>*

> <img src="https://github.com/Ki1z/PHP-Study-Notes/blob/main/Image/@A6(R6C{X]E4@@E2O$1(%EC.png?raw=true">

**连接认证基本语法**

```
Mysql.exe/mysql -h127.0.0.1 -P3306 -uroot -proot
```

注意事项

- 通常端口都可以默认，MySQL的默认监听端口通常都是3306

- 密码的输入可以先输入-p，直接换行，然后再以密文的方式输入密码

**退出**

断开与服务器的连接，通常MySQL服务器数量有限，一旦客户端用完，建议断开

- 建议方式：使用SQL提供的指令

  - `Exit;` *Exit后分号不能省略*
  - `\q;` *Quit的缩写*
  - `Quit;`
> <img src="https://github.com/Ki1z/PHP-Study-Notes/blob/main/Image/W0ZAXBR~%{HXE$0}]K{`@2N.png?raw=true">

- 其他方式：直接关闭cmd窗口

## MySQL服务端架构

MySQL服务端架构由以下几层构成：

- 数据库管理系统（最外层） `Database Management System` ，专门管理服务器端的所有内容

- 数据库（第二层） `Database` ，专门用于储存数据的仓库

- 二维数据表（第三层） `Table` ，专门用于存储具体实体的数据

- 字段（第四层） `Field` ，具体存储某种类型的数据（实际存储单元）

服务端常用关键字

- `Row` 行

- `Column` 列，对应 `Field`

---

# 数据库基本操作

数据库是数据存储的最外层（最大单元）

> DBMS（数据库管理系统） > DB（数据库） > Table（表） > Field（字段）

## 创建数据库

**基本语法**

> ```sql
> create database <databasename> [databaseoption];
> ```
> <img src="https://github.com/Ki1z/PHP-Study-Notes/blob/main/Image/8K7LY6@72GW@TU1XXBM`YSO.png?raw=true">

**库选项 DatabaseOption**

数据库的相关属性

- `charset` 字符集，代表着当前数据库下的所有表存储的数据默认的指定的字符集

```sql
create database <databasename> charset {charsetname};
```

- `collate` 校对集，代表着当前数据库下的所有表存储的数据默认的指定的校对集

```sql
create database <databasename> collate {collationname};
```

## 显示数据库

每当用户通过SQL指令创建一个数据库，系统就会产生一个对应的存储数据的文件夹

> <img src="https://github.com/Ki1z/PHP-Study-Notes/blob/main/Image/7MQY8ISC5$X]4ELTA92FXIR.png?raw=true">

每个文件下都有一个opt文件，保存的是对应的数据库选项

**基本语法**

- 显示全部库

  ```sql
  show databases;
  ```

  > <img src="https://github.com/Ki1z/PHP-Study-Notes/blob/main/Image/QH1}ZW}P]ES~$UUUA~{]{95.png?raw=true">

- 显示部分库

  ```sql
  show databases like {'matchmode'};
  ```

- <div id="match_mode">匹配模式（通配符） MatchMode</div>

  - `_`：匹配当前位置单个字符

  - `%`：匹配指定位置零个或多个字符

  > 匹配以my开头的多个数据 `'my%';`
  > 获取以m开头，第二个字符不确定，最后以database结尾的数据 `'m_database';`
  > 获取以database结尾的数据 `'%database';`
  >
  > <img src="https://github.com/Ki1z/PHP-Study-Notes/blob/main/Image/6ANE}$QLU4JIHA8JP1Y`7%R.png?raw=true">

## 显示数据库创建语句

**基本语法**

```sql
show create database <databasename>;
```

> <img src="https://github.com/Ki1z/PHP-Study-Notes/blob/main/Image/@YL)Q1TS{3IKI1M$I}E@%DW.png?raw=true">

## <span id="select_database">选择数据库</span>

*为社么要选择数据库？*

因为数据是存储在数据表，数据表存储在数据库下。如果要操作数据，那么必须进入对应的数据库中。

**基本语法**

```sql
use <databasename>;
```

> <img src="https://github.com/Ki1z/PHP-Study-Notes/blob/main/Image/B[KAU0$%}I2N93N0WJU@B1L.png?raw=true">

## 修改数据库

修改数据库库选项

*在MySQL5.5之前可以使用rename修改数据库名，之后被移除*

**基本语法**

```sql
alter database <databasename> {charset/collate} [=] {charsetname/collationname};
```

> <img src="https://github.com/Ki1z/PHP-Study-Notes/blob/main/Image/`3IQA)H`0}(%5Y~6R78R}P5.png?raw=true">

## 删除数据库

*删库跑路？*

**基本语法**

```sql
drop database <databasename>;
```

> <img src="https://github.com/Ki1z/PHP-Study-Notes/blob/main/Image/L%{PL]K1T(XNJPBYVF}NXT7.png?raw=true">

---

# 数据表操作

## 创建数据表

### 普通创建表

**基本语法**

```sql
create table <tablename>(<fieldname> <fieldtype> [fieldattribute],...) [tableoption];
```

> <img src="https://github.com/Ki1z/PHP-Study-Notes/blob/main/Image/SBOJI%BY494628IN_IZXI{O.png?raw=true">

错误信息：表必须放到对应的数据库下，有两中方式可以将表挂入到指定的数据库下

1. 在数据表前面加上数据库的名字，用 `.` 连接

```sql
create table <databasename>.<tablename>(<fieldname> <fieldtype> [fieldattribute],...) [tableoption];
```

2. 在创建数据表之前先进入到某个指定的数据库，用 `use` ，语法[点击参考上文](#select_database)

**表选项 TableOption**

与库选项类似，优先级大于库选项

```sql
create table <databasename>.<tablename>(<fieldname> <fieldtype>[fieldattribute],...) engine [=] {enginename} charset [=] {charsetname} collate [=] {collatename};
```

- `Engine` ：存储引擎，指MySQL提供的具体存储数据的方式，默认 `innodb` ，MySQL5.5以前默认 `myisam`

- `Charset` ：字符集

- `Collate` ：校对集

### 复制已有结构

从已经存在的表复制一份（只复制结构，不复制数据）

**基本语法**

```sql
create table [databasename.]<tablename> like [databasename.]<tablename>;
```

## 显示数据表

每当一张数据表被创建，那么就会在对应的数据库下创建一些文件（与存储引擎有关）

**基本语法**

- 显示所有表

  ```sql
  show tables;
  ```

  > <img src="https://github.com/Ki1z/PHP-Study-Notes/blob/main/Image/C6IWMFEFNF7MM~1HP3ZNUUR.png?raw=true">

- 显示部分表

  ```sql
  show tables like {'matchmode'};
  ```

- 匹配模式[点击参考上文](#match_mode)

  > <img src="https://github.com/Ki1z/PHP-Study-Notes/blob/main/Image/XS9JE(0ELNVH{EXCIW8TN(2.png?raw=true">

## 显示表结构

显示表中所包含的字段信息（名字，类型，属性等）

**基本语法**

```sql
{Describe/Desc/show columns from} <tablename>;
```

> <img src="https://github.com/Ki1z/PHP-Study-Notes/blob/main/Image/6_FV{TAH9LBT3XF7_P~Z%AL.png?raw=true">

**解释**

- `Field` ：字段名

- `Type` ：字段类型

- `Null` ：值是否允许为空

- `Key` ：索引名

- `Default` ：默认值

- `Extra` ：其他属性

## 显示表创建语句

查看数据表创建时的语句

**基本语法**

```sql
show create table <tablename>;
```

> <img src="https://github.com/Ki1z/PHP-Study-Notes/blob/main/Image/R2[UQDNI]_QUMP(IK0HKIZR.png?raw=true">


## 修改表结构

**基本语法**

- 修改表名

  ```sql
  rename <tablename> to <tablename>
  ```

- 修改表选项

  ```sql
  alter table <tablename> {engine/charset/collate} [=] {enginename/charsetname/collationname};
  ```

  *注：如果数据库已经确定，表中已经存在数据，不要轻易修改表选项*

- 新增字段

  ```sql
  alter table <tablename> add [column] <fieldname> {columntype} [columnattribute] [location];
  ```

- 修改字段名

  ```sql
  alter table <tablename> change <tablename> <newtablename> <fieldtype> [columnattribute] [location];
  ```

- 修改字段类型

  ```sql
  alter table <tablename> modify <fieldname> <fieldtype> [fieldattribute] [location];
  ```

- 删除字段

  ```sql
  alter table <tablename> drop <fieldname>;
  ```

**解释**

- `columntype` ：列类型，包含 `int` , `float` , `char(length)` 等

- `fieldattribute` ：字段属性，包含 `null` , `default` , `key` 等

- `location` ：字段位置，`first` 表示最前端， `after <fieldname>`表示在指定字段之后

## 删除表结构

**基本语法**

```sql
drop table <tablename>[,tablename,...];
```

> <img src="https://github.com/Ki1z/PHP-Study-Notes/blob/main/Image/2N{}9GOC5KX}W{99UK}L}6H.png?raw=true">

---

# 数据操作基础

## 插入操作

本质：将数据以SQL的形式存储到指定数据表的字段里

**基本语法**

```sql
insert into <tablename> [(fieldname,...)] values(value1,...)
```

> <img src="https://github.com/Ki1z/PHP-Study-Notes/blob/main/Image/}MXSOXSNFZ_3~0U6N@O@ISN.png?raw=true">

如果指定了 `fieldname` ，则每个 `value` 对应一个 `fieldname` ；若没有指定 `fieldname` ，则默认向所有字段插入一个 `value` ，且 `value` 结构必须与 `fieldname` 结构一致

> <img src="https://github.com/Ki1z/PHP-Study-Notes/blob/main/Image/3DJ(6V9A1@@B%KH8UK({WQY.png?raw=true">

## 查询操作

**基本语法**

- 查询全部数据（通配符'*'表示表中全部字段）

  ```sql
  select * from <tablename>;
  ```

- 查询表中部分字段

  ```sql
  select <fieldname>[,fieldname...] from <tablename>;
  ```

- 简单条件查询数据

  ```sql
  select <fieldname>[,fieldname...] from <tablename> where <fieldname> = <value>;
  ```

  > <img src="https://github.com/Ki1z/PHP-Study-Notes/blob/main/Image/L9@YAY{_2})USSF7{]%Q8]S.png?raw=true">

  *解释：获取表中满足条件fieldname = value数据的fieldname下的值*
