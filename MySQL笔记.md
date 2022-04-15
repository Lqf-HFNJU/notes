# MySQL

##### *LQF*

[TOC]

------



## 卸载

1. 打开驱动软件，选`remove`
2. 删掉相关数据文件
   * exe程序
   * 数据文件（可能在C盘隐藏文件夹下`C:\ProgramData`）

* 但是已经将数据文件和exe程序放在同一包下
* 直接删掉D盘目录`D:\MySQL\mysql-5.7.34`即可

------



## SQL基础知识

* #### 数据库，数据库管理系统和SQL

  * **数据库：**
    * DataBase，即DB
    * 按照一定格式存储数据的一些文件的组合
    * 顾名思义：存储数据的仓库，实际上就是一堆文件。这些文件中存储了具有特定格式的数据
  * **数据库管理系统：**
    * DataBaseManagement，简称DBMS
    * 是用来管理数据库中数据的，可以对数据库当中的数据进行增删改查
  *   **SQL：结构化查询语言**
    * 通过编写SQL语句，然后DBMS负责执行SQL语句，最终来完成数据库中数据的增删改查操作
    * SQL是一套标准
  * **三者之间的关系**
    * DBMS--> 执行--> SQL --操作--> DB

* #### MySQL的端口号

  * 默认是3306

* #### 账号和密码

  * **账号：**
    * 超级管理员用户名不能改
    * 一定是：`root`
  * **密码：**
    * XXXXXX

* #### **计算机上MySQL的服务在哪**

  * 此电脑-->右键-->管理-->服务和应用程序-->服务-->找MySQL服务
  * 已经设置为手动启动

* #### 在windows操作系统，如何使用命令来启动和关闭MySQL服务

  * net stop 服务名称;
  * net start 服务名称;

* #### 如何使用客户端登录MySQL数据库

  * 使用管理员身份的DOS指令打开MySQL的bin目录下的程序
  * `cd D:\MySQL\mysql-5.7.34\bin `

* #### 两种输入密码的方式

  * 直接`MySQL -uroot -pxxxxxx`
  * 输入`MySQL -uroot -p`，再在提示下输入密码

* #### 语句结尾的方式

  * 语句用`;`结尾，**不见`;`不执行**
  * 也可以用`\c`来终止命令的输入

* #### 数据库当中最基本的单元

  * **表，table**
  * 数据库当中是以表格的形式表示数据的，表比较直观
  * 任何一张表都有**行**和**列**：
    	* **行（row）**：被称为数据/记录
    * **列（column）**：被称为**字段**
      * 每一个字段都有**字段名**、**数据类型**、**约束**等属性
  
* #### SQL语句的分类

  * **DQL：**
    		
    * 数据查询语言
    
    * `select`，凡是带有select关键字的都是查询语句
  
* **DML：**
    		
    * 数据操作语言
    
  * 凡是对表当中的数据进行**增删改**的都是DML
  * `insert` `delete` `update`
  * **DDL：**
       * 数据定义语言
       * 凡是带有`create`、`drop`、`alter`的都是DDL
       * 这个增删改和DML不同，DDL主要操作的是表的**结构**，不是表中的数据
  * **TCL：**
       * 事务控制语言
       * 事务提交：`commit;`
       * 事务回滚：`rollback;`
  * **DCL：**
       * 是数据控制语言。
       * 授权`grant;`
       * 撤销权限`revoke;`
  
* #### SQL语句的大小写

  * **不区分**
  
* #### 字符串的表示

     * 用`''`括起来
     
* #### sql脚本文件

     * xxxx.sql格式的文件
     * 我们执行sql脚本文件的时候，该文件中所有的sql语句会全部执行
     * 可以用`source 绝对路径;`导入

------



## MySQL常用语句

* #### 导入提前准备好的数据：

  * `source 该数据的绝对路径`

* #### 退出MySQL：

  * `exit`

* #### 查看MySQL中的数据库：

  * ​	`show databases; `

* #### 选择使用某个数据库：

  * `use xxx;`
  * xxx是要选择使用的数据库名

* #### 查看某个数据库下的表：

  * `show tables;`

* #### 查看MySQL数据库的版本号：

  * `select version();`

* #### 查看当前使用的数据库：

  * `select database();`

* #### 查看表中的数据：

  * `select * from 表名;`
  * `*`是通配符
  
* #### 不看表中的数据，只看表的结构：

  * `desc xxx;`
  * xxx是表名
  * `desc`是`describe`的简写（都可以用）

------



## 查询

### 简单查询

* #### 查询一个字段

  * `select 字段名 from 表名;`
    * `select`和`from`都是关键字
    * 字段名和表名都是**标识符**
    * 对于SQL语句来说是**通用的**

* #### 查询两个或者多个字段

  * 使用逗号隔开`,`
  * `select 字段名1,字段名2 from 表名;`

* #### 查询所有字段

  * 可以把每个字段都写上
  * 或者使用通配符`*`
    * 但是效率低，且可读性差，不建议使用

* #### 给查询的列起别名

  * 使用`as`关键字起别名
  * 只是将显示的查询结果列名显示为别名，原表列名还是不变
  * select语句是**永远都不会进行修改操作的**
  * `select 字段名 as 别名 from 表名;`
  * `as`可以省略，使用**空格**代替
    * `select 字段名 别名 from 表名;`
    * 不建议使用
  * 起的别名里面有**空格**：
    * 使用双引号或者单引号括起来
    * 一般建议使用单引号（所有SQL都适用）
    * `select 字段名 '别 名' from 表名;`
  * 起的别名是**中文**
  * 使用单引号括起来

* #### 字段可以使用数学表达式

  * 只需要数据类型符合即可
  * `select 字段名*num from 表名;`
  * 与此同时也可以给这个字段起别名

------

### 条件查询

* #### 语法格式：

  * select

    ​	字段1,字段2,字段3....

  * from 

    ​	表名

  * where

    ​	条件;

* #### 条件：

  * 大部分同Java

  * ##### 新内容：

    * ###### 不等于：

      * **`<>`**或`!=`

    * ###### 两个值之间：

      *  `between … and …` 等同于 `>= and <=`

    * ###### 是否为 null ：

      * `is null `，`is not null` 

    * `and`和`or`使用时带上括号

    * ###### 包含：

      * `in` 
      * 相当于多个 `or` 
      * `where in (3000,4000,80);`
      * `not in` 不在这个范围中

------

### 模糊查询

* 关键字：`like`
* `%`匹配任意多个字符
* 下划线`_`：任意一个字符
* 加在关键字`where`后面
* `select 字段... from 表名 where 条件 like '_lqf_2333%';`

------

### 排序

* 关键字：`order by 字段名`  
* 默认升序排序
* 降序：要排序的字段名后加上 ` desc`
* 升序：要排序的字段名后加上 ` asc`
* `select 字段... from 表名 where 条件 order by 字段1 desc, 字段2 asc, ... ;`
  * 只有字段1的排序顺序相等时，才会用第二种排序顺序
* 根据字段的位置也可以排序
  * `select ename,sal from emp order by 2;`
  * 根据`sal`排序

------

### 注意

* 关键字顺序**不能改变**
  1. `from`
  2. `where`
  3. `select`
  4. `order by`
* 排序总是在**最后执行**

------

### 数据处理函数

* 又称为**单行处理函数**
  * 一个输入对应一个输出
* 常见的单行处理函数
  * `lower('str')` 转换小写
  * `upper('str')` 转换大写
  * `substr('str',st,len)` 取子串   (被截取的字符串, 起始下标,截取的长度)
  * `concat('str1','str2')`函数进行字符串的拼接
  * `length('str')` 取长度
  * `trim('str')` 去空格
  * `case 字段 when..then..when..then..else..end` 条件语句
  * `round(num,args)` 四舍五入
    * args为1：保留1个小数
    * args为2：保留2个小数
    * args为0：保留0个小数
    * args为-1：保留到十位
    * ......
  * `rand()` 生成**0到1**之间随机数
  * `ifnull(数据，被当成的值)` 可以将 `null` 转换成一个具体值
    * 空处理函数

------



### 分组函数（多行处理函数）

* 输入多行，最终输出一行

* ##### 使用前提：

  * 分组函数在使用的时候**必须先进行分组**，然后才能用
  * 如果你没有对数据进行分组，整张表**默认为一组**

* ##### 5个：

  * `count()`
  * `sum()`
  * `avg()`
  * `max()`
  * `min()`

* ##### 注意：

  1. 分组函数**自动忽略NULL**，你不需要提前对NULL进行处理
  2. `count(*)`和`count(具体字段)`
     * `count(具体字段)`：表示统计该字段下所有不为NULL的元素的总数
     * `count(*)`：统计表当中的**总行数**
       * 因为每一行记录不可能都为NULL，一行数据中有一列不为NULL，则这行数据就是有效的
  3. 分组函数不能够直接使用在`where`子句中
     * 因为分组的执行顺序在条件过滤之后
     * 使用`having`代替，分组后再过滤，可在`having`使用分组函数

------

### 分组查询

* 分组查询和分组函数紧密相关

* 根据需要的字段进行分组

  * `group by 要分组的字段` 

* ```mysql
  select
  	...
  from
  	...
  where
  	...
  group by
  	...
  order by
  	...
  	having ...
  ```

* 执行顺序：

  1. `from`
  2. `where`
  3. `group by`
  4. `select`
  5. `order by`

* 分组后，`select`后面的字段必须是**被分组的字段**或者是**分组函数**

* 分组可以多个字段联合分组：

  * `group by 字段1，字段2，...`

* 使用`having`可以对分完组之后的数据进一步过滤

  * `having`不能单独使用，`having`不能代替`where`，`having`必须和`group by`联合使用

* 先分组后选择的效率较低

  * 优化策略：
    * 优先选择`where`，`where`实在完成不了了，再选择`having`

------



### distinct关键字

* 把查询结果去除重复记录

* `distinct`只能出现在所有字段的最前方，表示根据这些字段联合去重

* ```mysql
  select distinct 字段1,字段2，... from ...;
  ```

* `distinct`可以作为参数传入分组函数里

  * ```mysql
    select count(distinct ...) from ...;
    ```

------



### 连接查询

* 跨表查询，多张表**联合起来**查询数据，被称为连接查询

* ##### 连接查询的分类

  * **内连接：**
    * 等值连接
    
      * 非等值连接
       * 自连接
    
    * **外连接：**
  * 左外连接（左连接）
  
  * 右外连接（右连接）
  
  * **全连接：**
  
* 表的链接原理是**笛卡尔积**

  * 为了避免此现象，可以加条件筛选  

  * 表应该起别名，可以提高效率

  * 表的连接次数越多效率越低，尽量避免表的连接次数 

  * **SQL99语法：**

  * ```mysql
    	select 
    		e.ename,d.dname
    	from
    		emp e
    	join
    		dept d
    	on
    		e.deptno = d.deptno;
    ```

    

  * sql99优点：表连接的条件是独立的，连接之后，如果还需要进一步筛选，再往后继续添加`where`

* **内连接：**（A和B连接，AB两张表没有主次关系，平等的）

* **外连接：**两张表连接，产生了主次关系

* 带有`right`的是右外连接，又叫做右连接，带有`left`的是左外连接，又叫做左连接

* 任何一个右连接都有左连接的写法，任何一个左连接都有右连接的写法

     * **SQL99语法：**

     * ```mysql
       	select 
       		e.ename,d.dname
       	from
       		emp e
       	left join
       		dept d
       	on
       		e.deptno = d.deptno;
       ```

       * `left join `表示以左边的表为主表
       * `right join`表示以右边的表为主表

* ##### 多张表连接：

  * 一直继续`join ... on ...`即可

------



### 子查询

* `select`语句中嵌套`select`语句，被嵌套的`select`语句称为子查询

* ##### 可以出现的地点：

  * `select`后面
    * 对于`select`后面的子查询来说，这个子查询只能一次返回1条结果，多于1条，就报错了
  * `from` 后面
  * `where`后面

------



### union合并查询结果集

* `union`可以将查询的两个表进行连接，使查询结果合并

* `union`的效率要高一些

  * 对于表连接来说，每连接一次新表，则匹配的次数满足笛卡尔积
  * `union`可以减少匹配的次数

* ##### 使用注意事项：

  * `union`在进行结果集合并的时候，要求两个结果集的列数相同
  * 结果集合并时列和列的数据类型也要一致

------



### limit用法

* 将查询结果集的一部分取出来，通常使用在**分页查询**当中

* ##### 用法：

  * **完整用法：**`limit startIndex, length;` 起始下标从0开始
  * **缺省用法：**`limit num;` 这是取前num个查询结果

* MySQL当中`limit`在`order by`之后执行

------



### DQL总结

* ##### 写法顺序：

```mysql
	select 
		...
	from
		...
	where
		...
	group by
		...
	having
		...
	order by
		...	limit
		...
```

* ##### 执行顺序:

  1. `from`
  2. `where`
  3. `group by`
  4. `having`
  5. `select`
  6. `order by`
  7. `limit..`

------



## 建表,删表和表结构的修改

### ~~直接用图形化界面一键搞定~~

### 1. 建表

#### 普通建表：

* 属于DDL语句，包括 `create` `drop` `alter` 

* ##### 语法：

  ```mysql
  create table 表名(
  		字段名1 数据类型, 
  		字段名2 数据类型 default ... , 
  		字段名3 数据类型 
  	);
  ```

* **表名：**建议以`t_` 或者 `tbl_`开始

* 表名和字段名都属于**标识符**

* 可以用`default`关键字指定默认值

------



#### 特殊建表：

* ##### 表复制：

  * `create table 表名 as select * from 原表;`

------



### 2. MySQL的数据类型

1. **varchar(最长255)**
   * 可变长度的字符串
   * 会根据实际的数据长度动态分配空间
   * **优点：**节省空间
   * **缺点：**需要动态分配空间，速度慢
2. **char(最长255)**
   * 定长字符串
   * 不管实际的数据长度是多少，分配固定长度的空间去存储数据
   * **优点：**不需要动态分配空间，速度快
   * **缺点：**使用不当可能会导致空间的浪费
3. **int(最长11)**
   * 数字中的整数型

4. **bigint**
   * 数字中的长整型
5. **float(有效数字，小数位)和double（有效数字，小数位）**
   * 可以选定有效数字和小数位
6. **date**
   * 短日期类型，年月日
   * mysql中默认可以将`YYYY-MM-dd`的格式的日期字符串传换成`date`类型
   * 或者使用`str_to_date`和`date_format`函数
7. **datetime**
   * 长日期类型，年月日时分秒
   * 可以通过`now()`函数获取当前日期
   * mysql中默认可以将`YYYY-MM-dd HH:mm:ss`的格式的日期字符串传换成`datetime`类型
8. **clob**
   * Character Large OBject
   * 字符大对象
   * 最多可以存储4G的字符串
   * 超过255个字符的都要采用CLOB字符大对象来存储
9. **blob**
   * Binary Large OBject
   * 二进制大对象
   * 专门用来存储图片、声音、视频等流媒体数据
   * 往BLOB类型的字段上插入数据时，需要使用IO流

------



### 3. 删除表

* `drop table 表名;`
  * 当这张表不存在的时候会报错
* `drop table if exists 表名;`
  * 表不存在时**不会报错**

------



### 4. 表结构的修改

* 添加，删除或修改一个**字段**
* 对表结构的修改需要使用`alter`

------



## 插入数据：insert（DML）

* `insert`

* **语法格式：**

  * `insert into 表名(字段名1,字段名2,字段名3...) values(值1,值2,值3);`
  * **字段名和值要一一对应**
  * `insert`语句但凡是执行成功了，那么必然会多一条记录
  * 没有给其它字段指定值的话，默认值是NULL
  * `insert`语句中的字段名可以省略
    * 但此时默认全部都已**按顺序写上**

* 可以一条`insert`语句插入多条数据：

  * ```mysql
    insert into 表名(字段名1,字段名2,字段名3...) values
    (值1,值2,值3),
    (值1,值2,值3),
    (值1,值2,值3),
    ...;
    ```

* 将查询结果插入到一张表当中：
  * `insert into 表名 select * from ...;`
  * 很少用

------



## 修改和删除

### 修改：update

* **语法格式：**
  * `update 表名 set 字段名1=值1,字段名2=值2,字段名3=值3... where 条件;`
* **注意：**
  * 没有条件限制会导致所有数据全部更新

------



### 删除：

#### 1. delete(DML)

* **语法格式：**
  * `delete from 表名 where 条件`
* **注意：**
  * 没有条件，整张表的数据会**全部删除**
* `delete`语句删除数据的原理:
  * 表中的数据被删除了，但是这个数据在硬盘上的真实存储空间不会被释放
  * **缺点：**删除效率比较低
  * **优点：**支持回滚可以再恢复数据

#### 2. truncate(DDL)

* **语法格式：**
  * `truncate table 表名;`
* `truncate`是删除表中的**全部数据**，表还在
* truncate语句删除数据的原理
  * 这种删除效率比较高，表被一次截断，物理删除
  * **缺点：**不支持回滚
  * **优点：**快速

------



## 约束

* 约束对应的英语单词：**constraint**
* 在创建表的时候，我们可以给表中的字段加上一些约束，来保证这个表中数据的完整性、有效性
* 在创建表的时候，在字段后添加相应的约束即可

* ##### 约束的划分：

  * 非空约束：`not null`

    * 约束的字段不能为NULL

  * 唯一性约束: `unique`

    * 约束的字段不能重复，但是可以为NULL

    * **列级约束：**

      * 直接添加到字段的后面，每个字段都具有唯一性：

        * ```mysql
          create table t(
          			id int,
          			name varchar(255) unique,  // 约束直接添加到列后面的，叫做列级约束
          			email varchar(255) unique
          		);
          ```

          

    * **表级约束：**

      * 没有添加到字段的后面，两个或者多个字段联合起来具有唯一性：

        * ```mysql
          create table t(
          				id int,
          				name varchar(255),
          				email varchar(255),
          				unique(name,email) // 约束没有添加在列的后面，这种约束被称为表级约束
          			);
          ```

          

  * 主键约束: `primary key` （简称PK）

    * `unique` 和`not null`联合约束
    * 主键约束的相关术语
      * **主键约束：**一种约束
      * **主键字段：**添加了主键约束的字段
      * **主键值：**主键字段中的每一个值
    * 主键值是每一行记录的唯一标识
    * **任何一张表都应该有主键，没有主键，表无效**
    * 可以表级约束添加主键，称为复合主键，但不建议使用
    * 一张表，主键约束**只能有1个**
    * 还能分类成**自然主键和业务主键：**
      * **自然主键：**主键值是一个自然数，和业务没关系
      * **业务主键：**主键值和业务紧密关联
      * 一般使用**自然主键**多一些，不和业务挂钩
    * 在mysql中有一种机制，可以帮助我们自动维护一个主键值：
      * `主键字段 int primary key auto_increment ...`
      * `auto_increment`表示自增，从1开始

  * 外键约束：`foreign key`（简称FK）

    * 外键约束涉及到的相关术语：

      * **外键约束：**一种约束（foreign key）
      * **外键字段：**该字段上添加了外键约束
      * **外键值：**外键字段当中的每一个值

    * 子表中的外键引用的父表中的某个字段，被引用的这个字段**不一定是主键**，但至少具**有`unique`约束**

    *  使用时在声明完字段之后加上` foreign key(外键字段) references 父表(被引用的字段)`

    * ```mysql
      mysql> create table t_school(
          -> sid bigint,
          -> sname varchar(255),
          -> foreign key (sid) references t_user(id)
          -> );
      ```

    * 外键值可以为NULL

  * 检查约束：`check`（mysql不支持，oracle支持）

    * 略

------



## 存储引擎

* 存储引擎是MySQL中特有的一个术语，其它数据库中没有
* 实际上存储引擎是一个**表存储/组织数据的方式**
* 不同的存储引擎，表存储数据的方式不同

* ##### 查看建表信息：

  * `show create table 表名;`
  * 可能因为屏幕太小放不下

* ##### 建表时指定存储引擎(和默认字符集等内容)：

  * 在建表的时候可以在最后小括号的")"的右边使用：

    * `ENGINE=InnoDB AUTO_INCREMENT=11 DEFAULT CHARSET=utf8`

    * ```mysql
      	create table t_product(
      		id int primary key,
      		name varchar(255)
      	)engine=InnoDB default charset=gbk;
      ```

* ##### 查看mysql支持的存储引擎

  * `show engines \G;`

* ##### 常见的存储引擎

  1. ###### MyISAM存储引擎

     * 它管理的表具有以下特征：
       * 使用三个文件表示每个表：
         * 格式文件 — 存储表结构的定义（mytable.frm）
         * 数据文件 — 存储表行的内容（mytable.MYD）
         * 索引文件 — 存储表上索引（mytable.MYI）
       * MyISAM存储引擎特点：
         * 可被转换为压缩、只读表来节省空间
         * MyISAM不支持事务机制，安全性低

  2. ###### InnoDB存储引擎

     * 这是mysql默认的存储引擎，同时也是一个重量级的存储引擎
     * InnoDB**支持事务**，支持数据库崩溃后自动恢复机制
     * InnoDB存储引擎最主要的特点是：**非常安全**
     * 它管理的表具有下列主要特征：
       * 每个 InnoDB 表在数据库目录中以.frm 格式文件表示
       * InnoDB 表空间 tablespace 被用于存储表的内容（表空间是一个逻辑名称，表空间存储数据+索引）
       * 提供一组用来记录事务性活动的日志文件
       * 用 `COMMIT`(提交)、`SAVEPOINT` 及`ROLLBACK`(回滚)支持事务处理
       * 提供全 ACID 兼容
       * 在 MySQL 服务器崩溃后提供自动恢复
       * 多版本（MVCC）和行级锁定
       * 支持外键及引用的完整性，包括级联删除和更新

  3. ###### MEMORY存储引擎

     * 使用 MEMORY 存储引擎的表，其数据存储在内存中，且行的长度固定，这两个特点使得 MEMORY 存储引擎非常快
     * MEMORY 存储引擎管理的表具有下列特征：
       * 在数据库目录内，每个表均以.frm 格式的文件表示
       *  表数据及索引被存储在**内存**中（目的就是快，查询快！）
       *  表级锁机制
       * 不能包含 TEXT 或 BLOB 字段
     * MEMORY 存储引擎以前被称为HEAP 引擎
     * MEMORY引擎优点：**查询效率最高**，不需要和硬盘交互
     * MEMORY引擎缺点：**不安全**，关机之后数据消失，因为数据和索引都是在内存当中

------



## 事务

* 一个事务其实就是一个完整的业务逻辑，一个最小的工作单元，不可再分

* 只有**DML**语句才会有事务这一说，其它语句和事务无关

  * `insert` `delete` `update`
  * 只有以上的三个语句是数据库表中数据进行增、删、改
  * 只要你的操作涉及到数据的增、删、改，那么就一定要考虑安全问题

* 一个事务其实就是多条DML语句**同时成功，或者同时失败**

* 只有使用`innoDB`存储引擎才支持事务

* **mysql当中默认的事务行为：**

  * 支持自动提交事务，每执行一条DML语句，则提交一次
  * 因此需要手动开启事务

* ##### 事务的过程：

  * **开启**
    * `start transaction;`
  * **提交**
    * 在多条DML语句结束后（该事务结束后）执行
    * ` commit;`
  * **回滚**
    * `rollback;`
    * 在提交前都可以回滚达到撤销的效果
    * 可以回滚至上一次提交点

* ##### 事务的特性（ACID）：

  1. **原子性(A)**
     * 事务是最小的工作单元，不可再分
  2. **一致性（C）**
     * 在同一个事务当中，所有操作必须同时成功，或者同时失败，以保证数据的一致性
  3. **隔离性（I）**
     * A事务和B事务之间具有一定的隔离
  4. **持久性（D）**
     * 事务最终结束的一个保障
     * 事务提交，就相当于将没有保存到硬盘上的数据保存到硬盘上

* ##### 事务的隔离性：

  * ###### 分为四个级别:

    1. **读未提交：**`read uncommitted`（最低的隔离级别）

       * 没有提交就读到了

       * 事务A可以读取到事务B未提交的数据
       * 存在脏读现象(Dirty Read)

    2. **读已提交：**`read committed`

       * 提交之后才能读到
       * 解决了脏读的现象
       * 但是**不可重复读取数据：**
         * 在事务开启之后，第一次读取数据，当前事务还没有结束，可能第二次再读取的时候两次读取的数据不同，称为不可重复读取
       * oracle数据库默认的隔离级别是：read committed

    3. **可重复读：**`repeatable read`

       * 提交之后也读不到，永远读取的都是刚开启事务时的数据
       * 可重复读取
         * 事务A开启之后，不管是多久，每一次在事务A中读取到的数据都是一致的。即使事务B将数据已经修改，并且提交了，事务A读取到的数据还是没有发生改变
         * 可重复读**解决了不可重复读取数据**
         * 可重复读存在的问题是可以会出现**幻影读**
           * 每一次读取到的数据都是幻象，不够真实
       * mysql中默认的事务隔离级别就是这个

    4. **序列化/串行化：**`serializable`（最高的隔离级别）

       * 这是最高隔离级别，效率最低，解决了所有的问题
       * 每一次读取时其他线程会**堵塞**，**直到当前线程结束**才会继续
       * 这种隔离级别表示事务排队，**不能并发**
       * synchronized，线程同步（事务同步）
       * 每一次读取到的数据都是最真实的，并且**效率是最低的**

* ##### 查看隔离级别

  * `SELECT @@tx_isolation`

* ##### 设置隔离级别

  * `set global transaction isolation level xxx;`

* ##### 模拟

  * 可以通过开多个命令行来验证隔离级别

------



## 索引

* 索引是在数据库表的字段上添加的，是为了提高查询效率存在的一种机制

* 类似**B-Tree**的查找机制

* **主键字段**会被自动添加为索引

* 在任何数据库当中主键上都会自动添加索引对象，另外在mysql当中，一个字段上如果有`unique`约束的话，也会自动创建索引对象

* 在任何数据库当中，任何一张表的任何一条记录在硬盘存储上都有一个硬盘的物理存储编号

* 在mysql当中，索引是一个单独的对象，不同的存储引擎以不同的形式存在，在`MyISAM`存储引擎中，索引存储在一个.MYI文件中。在`InnoDB`存储引擎中索引存储在一个逻辑名称叫做`tablespace`的当中。在`MEMORY`存储引擎当中索引被存储在内存当中。不管索引存储在哪里，索引在mysql当中都是一个树的形式存在

* **唯一性比较弱的字段上添加索引用处不大**

* ##### 添加索引的原因

  * 数据量庞大
  * 该字段经常出现在where的后面，以条件的形式存在，也就是说这个字段总是被扫描
  * 该字段很少的DML(`insert` ` delete ` `update`)操作（因为DML之后，索引需要重新排序）
  * 但是建议**不要随意添加索引**，因为索引也是**需要维护的**，太多的话反而会降低系统的性能
  * 建议**通过主键查询**，建议**通过unique约束的字段进行查询**，效率是比较高的

* ##### 使用语法

  * ###### 创建：

    * `create index 索引名 on 表名(添加索引的字段);`

  * ###### 删除：

    * `drop index 索引名 on 表名;`

  * ###### 查看查询语句中是否使用索引检索：

    * `explain select ...`
    * 关注``type`一栏
      * `type=ALL`：没有使用索引
      * `type=ref`:使用索引

* ##### 索引的失效

  1. 使用模糊查询的时候以`%`开始
  2. 使用`or`的时候会失效，要求`or`两边的条件字段都要有索引，才会走索引，如果其中一边有一个字段没有索引，那么另一个字段上的索引也会失效
     * 一般不建议使用`or`,建议使用`union`
  3. 使用复合索引的时候，没有使用左侧的列查找，索引失效
     * 两个字段，**或者更多的字段联合起来添加一个索引**，叫做复合索引
  4. 在`where`当中索引列参加了运算或使用了函数，索引失效
     * 也就是对索引的值进行改变

------



## 视图

* **`view`:**站在不同的角度去看待同一份数据

* ##### 使用语法

  * ###### 创建：

    * `create view 视图名 as select ... ;`

  * ###### 删除：

    * `drop view 视图名;`

* 只有DQL语句才能以`view`的形式创建，`as`后面必须是DQL语句

* 可以面向视图对象进行增删改查，并且**会导致原表被操作**

* 将一个查询结果保存为视图来便于后续开发，便不需要每次都重新编写了

* 视图对应的语句只能是**DQL语句**，但是视图对象创建完成之后，**可以对视图进行增删改查等操作**

------



## DBA常用命令

* 重点只需了解**数据的导入和导出**（数据的备份）

* ##### 导出：

  *  **`mysqldump 数据库名 表名(可以不写)>D:\xxxx.sql -uroot -p123456`**

* ##### 导入：

  * 需要先登录到mysql数据库服务器上
  * 然后创建数据库：`create database 数据库名;`
  * 使用数据库：`use 数据库名;`
  * 然后初始化数据库：`source xxxx.sql`

------



## 数据库设计三范式

### 第一范式：

* **要求任何一张表必须有主键，每一个字段原子性不可再分**

### 第二范式：

* **建立在第一范式的基础之上，要求所有非主键字段完全依赖主键，不要产生部分依赖**

### 第三范式：

* **建立在第二范式的基础之上，要求所有非主键字段直接依赖主键，不要产生传递依赖**

### 表设计

#### 多对多：

* **三张表，关系表两个外键**

#### 一对多：

* **一对多，两张表，多的表加外键**

#### 一对一：

* 可能存在一张表字段太多，太庞大，这个时候要拆分表
* **一对一，外键唯一**

------



## 悲观锁和乐观锁

### 悲观锁：

* 又称为行级锁
* 用于锁定并查询记录，使得在**事务中**查询期间线程堵塞，其他线程无法进行修改
* 在DQL语句后面加上关键字`for update`便可以锁定

### 乐观锁：

* 同样可以保证查询的真实性
* 但在修改后会生成一个版本号，类比git的冲突

------

------

------



## JDBC

**说实话直接上mybatis更香（学完ssm和springboot回来考古 2021.10）**

### 连接步骤：

1. 加载驱动， 用配置文件
2. 用户信息和url `"jdbc:mysql://localhost:3306/hflqf?useUnicode=true&characterEncoding=utf8&useSSL=true"`
3. 连接成功，返回数据库对象
4. 执行sql对象
5. 执行sql
6. 释放连接

```java
package com.hflqf;

import java.sql.*;
import java.util.ResourceBundle;

public class myJdbc01 {
    public static void main(String[] args) {
        //使用资源绑定器绑定属性配置文件
        ResourceBundle bundle = ResourceBundle.getBundle("jdbc");
        String driver = bundle.getString("driver");
        String url = bundle.getString("url");
        String username = bundle.getString("username");
        String password = bundle.getString("password");

        Connection conn = null;
        Statement stmt = null;
        ResultSet rs = null;

        try { //1.加载驱动,固定写法
            Class.forName(driver);

            //2.用户信息和url,背下基本格式和参数

            //3.连接成功，返回数据库对象
            conn = DriverManager.getConnection(url, username, password);

            //4.执行sql对象
            stmt = conn.createStatement();

            //5.执行sql
            // String sql = "insert into c values('6','COMPUTING','fangchunrong')";
            //  String sql = "delete from c where CNAME='COMPUTING'";
            //   int i = stmt.executeUpdate(sql);
            //  System.out.println(i == 1 ? "成功" : "失败");

            String sql = "select ename as name,sal,deptno from emp";
            //返回结果集，封装了全部的查询结果
            rs = stmt.executeQuery(sql);

            while (rs.next()) {
                //jdbc中所有下标从1开始,第几列
                //getString()不管数据库中数据类型是什么，都已String类型取出来
                /*String ename = rs.getString(1);
                String sal = rs.getString(2);
                String deptno = rs.getString(3);*/

                //重命名之后要写重命名之后的字段
                String ename = rs.getString("name");
                String sal = rs.getString("sal");
                String deptno = rs.getString("deptno");
                System.out.println(ename + "," + sal + ',' + deptno);
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            //6.释放连接
            if (rs != null) {
                try {
                    rs.close();
                } catch (SQLException throwables) {
                    throwables.printStackTrace();
                }
            }
            if (stmt != null) {
                try {
                    stmt.close();
                } catch (SQLException throwables) {
                    throwables.printStackTrace();
                }
            }
            if (conn != null) {
                try {
                    conn.close();
                } catch (SQLException throwables) {
                    throwables.printStackTrace();
                }
            }
        }
    }
}
```

属性配置文件jdbc.properties内容如下：

```properties
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/hflqf?useSSL=false
username=root
password=123456
```

pom.xml文件导入mysql驱动依赖：

```xml
<dependencies>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.47</version>
    </dependency>
</dependencies>
```



### 手写jdbc工具类

```java
package com.hflqf;

import java.sql.*;
import java.util.ResourceBundle;

public class JdbcUtil {
    private JdbcUtil() {}

    static {//静态代码块，类加载的时候只执行一次
        try {
            Class.forName("com.mysql.jdbc.Driver");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }

    public static Connection getConnection() throws SQLException {

        ResourceBundle jdbc = ResourceBundle.getBundle("jdbc");
        String url = jdbc.getString("url");
        String username = jdbc.getString("username");
        String password = jdbc.getString("password");

        return DriverManager.getConnection(url, username, password);
    }

    public static void close(Connection conn, Statement stmt, ResultSet rs) {
        if (rs != null) {
            try {
                rs.close();
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            }
        }
        close(conn, stmt);
    }

    public static void close(Connection conn, Statement stmt) {
        if (stmt != null) {
            try {
                stmt.close();
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            }
        }
        if (conn != null) {
            try {
                conn.close();
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            }
        }
    }
}
```

### PreparedStatement和Statement

* ##### PreparedStatement

  * 可以解决sql注入的问题
  * 对sql代码预编译，可以提高执行速度
  * 用占位符`?`解决问题

* ##### Statement

  * 存在sql注入的问题，对需要sql注入的操作还是有存在的价值

```java
package com.hflqf;

import java.sql.*;

public class myJdbc02 {
    public static void main(String[] args) {

        Connection conn = null;
        PreparedStatement ps = null;
        ResultSet rs = null;

        try {
            conn = JdbcUtil.getConnection();

            //  String sql = "select ename as ?,?,? from emp";
            String sql = "insert into t_user values (?,?,?,?)";

            ps = conn.prepareStatement(sql);//编译sql语句

            /*ps.setString(1, "ename");         查询
            ps.setString(2, "sal");
            ps.setString(3, "deptno");*/
            ps.setInt(1, 4);
            ps.setString(2, "zl");
            ps.setString(4, "zhanglian");
            ps.setString(3, "456");

            int i = ps.executeUpdate();
            System.out.println(i);

           /*rs = ps.executeQuery();

            while (rs.next()) {
                String ename = rs.getString("ename");
                String sal = rs.getString("sal");
                String deptno = rs.getString("deptno");
                System.out.println(ename + "," + sal + ',' + deptno);
            }*/
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            //6.释放连接
            JdbcUtil.close(conn, ps, rs);
        }
    }
}
```

### jdbc处理事务

* jdbc中是自动提交的，只要执行任意一条dml语句，则自动提交一次

* 重点三行代码：
  1. `conn.setAutoCommit(false);`
  2. `conn.commit();`
  3. `conn.rollBack();`  写在 try catch 里

```java
package com.hflqf;

import java.sql.*;

public class myJdbc03 {
    public static void main(String[] args) {

        Connection conn = null;
        PreparedStatement ps = null;
        int cnt = 0;
        try {
            conn = JdbcUtil.getConnection();
            conn.setAutoCommit(false);//开启事务

            String sql = "update t_bank set balance=? where id=?";
            ps = conn.prepareStatement(sql);

            ps.setInt(2, 1);
            ps.setDouble(1, 10000);
            cnt = ps.executeUpdate();


            ps.setInt(2, 2);
            ps.setDouble(1, 10000);
            cnt += ps.executeUpdate();

            conn.commit();//提交事务

        } catch (Exception e) {
            if (conn != null) {
                try {
                    conn.rollback();
                } catch (SQLException t) {
                    t.printStackTrace();
                }
            }
            e.printStackTrace();
        } finally {
            System.out.println(cnt == 2 ? "转账成功" : "转账失败");
            JdbcUtil.close(conn, ps);
        }

    }
}
```
