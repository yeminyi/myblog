---
layout: post
title: MySQL all in one
categories: sql 
tags: [MySQL,sql,chinese]
---
Export from Xmind in chinese, I will continue to update later.

## 数据库安装

### window系统安装
```
- 下载5.7 免安装版

	- https://dev.mysql.com/downloads/mysql/5.7.html#downloads

- 解压并创建my.ini在根目录

	- 编写my.ini内容

	  [client]
	  # 设置mysql客户端默认字符集
	  default-character-set=utf8
	  [mysqld]
	  #设置3306端口
	  port = 3306
	  # 设置mysql的安装目录 这块换成自己解压的路径
	  basedir=D:\\softnew\\MYSQL\\mysql-5.7.20-winx64
	  # 允许最大连接数
	  max_connections=200
	  # 服务端使用的字符集默认为8比特编码的latin1字符集
	  character-set-server=utf8
	  # 创建新表时将使用的默认存储引擎
	  default-storage-engine=INNODB
```
### Linux系统安装

## 数据库操作

### 创建数据库

- CREATE DATABASE db_name DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci

### 查询数据库

- 查询所有数据库

	- SHOW DATABASES

- 查询数据库建表时的sql

	- SHOW CREATE DATABASE db_name;

### 删除数据库

- DROP DATABASE db_name;

### 修改数据库

- 修改数据库的字符编码和排序方式

	- ALTER DATABASE db_name DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;

### 选择数据库

- USE db_name;

### 命令行设置之后操作的编码格式

- SET NAMES UTF8

## 数据库表操作

### 创建表

- SQL : CREATE TABLE tb_name (建表的字段、类型、长度、约束、默认、注释)
- 约束

	- 非空

		- NOT NULL

			- 指定列在插入数据时候必须有值

	- 非负

		- UNSIGNED 

			- 插入数字不能是赋值

	- 主键

		- PRIMARY KEY

			- 这个列值必须是唯一，不能重复

	- 自增

		- AUTO_INCREMENT

			- 只应用于整型的主键列

	- 默认

		- DEFAULT

			- 指定列默认值

	- 注释

		- COMMENT

			- 说明字段

- 常用类型

	- 极小整形

		- TINYINT

			- 非负最大值255
			- 1个字节

	- 小整形

		- SAMLLINT

			- 非负最大值65535
			- 2个字节

	- 整形

		- INT

			- 非负最大值4 294 967 295
			- 4个字节

	- 长整型

		- LONG

	- 单精度

		- FLOAT

			- 4个字节

		- decimal（6，3）

	- 定长字符串

		- CHAR

			- 最大保存255个字节
			- 如果值没有到给定长度用空格补充

	- 变长字符串

		- VARCHAR

			- 最大保存255个字节
			- 用多大占多大

	- 文本

		- TEXT

			- 最大保存65535个字节

	- 日期

		- Date
		- DateTime
		- Timestamp

- 表字段索引

	- 唯一索引

		- 添加

			- 创建索引

				- CREATE UNIQUE INDEX index_name ON tb_name (account);

			- 表字段修改

				- ALTER TABLE tb_name ADD UNIQUE index_name(field_name);

		- 删除

			- DROP INDEX 索引名称 ON 表名

	- 普通索引

		- 添加

			- 表字段修改

				- ALTER TABLE 表名 ADD INDEX 索引名称(字段名称);

			- 创建索引

				- CREATE INDEX Index_name ON tb_name(`account`);
				- CREATE INDEX 索引名称 ON 表名(字段名);

		- 删除

			- DROP INDEX 索引名称 ON 表名

	- 主键

		- 添加

			- ALTER TABLE tb_name ADD PRIMARY KEY (field_name);
			- ALTER TABLE 表名 ADD PRIMARY KEY (字段名称)

		- 删除

			- ALTER TABLE tb_name DROP PRIMARY KEY;

	- 联合索引

		- 添加

			- ALTER TABLE tb_name ADD index_name (field_name1,field_name2);

		- 删除

			- DROP INDEX 索引名称 ON 表名

	- 索引最左前缀原理：

### 修改表

- 表字段的增删改查

	- 字段添加

		- ALTER TABLE tb_name ADD address VARCHAR (100) NOT NULL DEFAULT '' COMMENT '地址';
		- ALERT TABLE tb_name ADD 添加字段 字段类型  非空约束  默认  注释

	- 字段类型修改

		- ALTER TABLE tb_name MODIFY address VARCHAR (50) NOT NULL DEFAULT '' COMMENT '地址';
		- ALERT TABLE tb_name MODIFY 字段名称 新的字段类型  非负  非空  默认 注释

	- 字段名称类型修改

		- ALTER TABLE tb_name CHANGE address addr VARCHAR (100) NOT NULL DEFAULT '' COMMENT '地址';
		- ALTER TABLE tb_name CHANGE 旧的字段名  新的字段名  新的类型  约束  默认  注释

	- 字段类型查询

		- DESC tb_name;

	- 字段删除

		- ALTER TABLE tb_name DROP addr;
		- ALTER TABLE 表名 DROP 删除的字段名

- 表修改

	- 表名修改

		- ALTER TABLE tb_name RENAME TO new_tb_name;
		- ALTER TABLE 旧表名 RENAME TO 新表名

	- 引擎修改

		- ALTER TABLE tb_name ENGINE = InnoDB;
		- ALTER TABLE 表名 ENGINE = 新的引擎名称

### 删除表

- DROP TABLE tb_name;

### 查询表

- 查询所有表

	- SHOW TABLES;

- 查询建表时的sql

	- SHOW CREATE TABLE tb_name;

## 表数据操作

### 增

- 添加单条

	- INSERT INTO tb_name(`field1`,`field2`,....)VALUES('value1','value2',.....);

- 添加多条

	- INSERT INTO tb_name(`field1`,`field2`,....)VALUES('value1','value2',.....),('value1','value2',.....),('value1','value2',.....),....;

### 改

- sql

	- UPDATE tb_name SET field1 = value1,field2 = value2,.....   WHERE  ....

- 注意

	- 修改时必须加where条件

### 删

- sql

	- DELETE FROM tb_name WHERE ...

- 注意

	- 删除时必须加where条件

### 查

- 基础的查询

	- SELECT * FROM tb_name

- where子句

	- 比较运算符

		- 大于、小于、等于、不等于、大于等于、小于等于
		- SELECT * FROM tb_name WHERE user_id &gt;10;

	- 逻辑运算符

		- 逻辑运算符是用来拼接其他条件的。用and或者or来连接两个条件，如果用or来连接的时候必须使用小括号
		- SELECT * FROM tb_name WHERE user_id &gt; 10 AND sex = '男'

	- LIKE模糊查询

		- 通配符

			- %（百分号）匹配零个或者多个任意字符
			- _（下划线）匹配一个任意字符

		- sql

			- SELECT * FROM tb_name WHERE username LIKE '张%';查找username开头是张的数据
			- SELECT * FROM tb_name WHERE username LIKE '%张%';查询username中含有张的数据
			- SELECT * FROM tb_name WHERE username LIKE '%张';查询username字段的数据以张结尾的
			- SELECT   *  FROM  tb_name WHERE username LIKE '张_';查询username以张开头后边有一个字符的数据

	- IN字段指定多个值查询

		- IN (value1,value2,value3,....)
		- SELECT   *   FROM   tb_name  WHERE   user_id  IN (1,3,5,7,9,11);查询user_id是1，3，5，7，9，11的所有数据

	- BETWEEN AND 区间查询

		- field  BETWEEN  value1  AND   value2
		- SELECT * FROM user WHERE user_id  BETWEEN  2 AND 9;查询user表中user_id大于等于2小于等于9的所有值

- GROUP BY 分组查询

	- 配合函数 

		- count(field)获取符合条件出现的非null值的次数
		- SUM(field)获取所有符合条件的数据的总和
		- AVG(field)或者平均值

	- SELECT  sex,COUNT(*)  count  FROM class  GROUP BY sex;获取class表中男生和女生的数量
	- group by会创建临时表

- ORDER BY 查询排序

	- 查询顺序

		- ORDER BY field DESC;降序查询
		- ORDER BY field ASC;升序查询

	- SELECT  *  FROM  tb_name  ORDER BY   id  DESC; 查询tb_name表中所有数据，按id的降序来查找
	- mysql有两种排序方式：通过有序索引顺序扫描直接返回有序数据，通过explain分析显示Using Index,不需要额外的排序，操作效率比较高。通过对返回数据进行排序，也就是Filesort排序，所有不是通过索引直接返回排序结果的都叫Filesort排序。Filesort是通过相应的排序算法将取得的数据在sort_buffer_size系统变量设置的内存排序中进行排序，如果内存装载不下，就会将磁盘上的数据进行分块，再对各个数据块进行排序，然后将各个块合并成有序的结果集order by 使用索引的严格要求：索引的顺序和order by子句的顺序完全一致索引中所有列的方向(升续、降续)和order by 子句完全一致当多表连接查询时order by中的字段必须在关联表中的第一张表中

- LIMIT 查询结果截取

	- 参数

		- LIMIT 后边可以跟两个参数，如果只写一个表示从零开始查询指定长度，如果两个参数就是从第一个参数开始查询查询长度是第二个参数的值，俩个参数必须是整形。

	- SELECT   *   FROM   tb_name   LIMIT   5;查询tb_name表中的所有数据，只要前边的5条数据
	- SELECT    *   FROM   tb_name   LIMIT   5,5;查询tb_name中所有的数据，返回的结果是从第五条开始截取五条数据
	- 分页查询一般会全表扫描，优化的目的应尽可能减少扫描；第一种思路：在索引上完成排序分页的操作，最后根据主键关联回原表查询原来所需要的其他列。这种思路是使用覆盖索引尽快定位出需要的记录的id，覆盖索引效率高些第二中思路：limit m,n 转换为 n之前分页查询是传pageNo页码, pageSize分页数量，当前页的最后一行对应的id即last_row_id，以及pageSize，这样先根据条件过滤掉last_row_id之前的数据，然后再去n挑记录,此种方式只能用于排序字段不重复唯一的列，如果用于重复的列，那么分页数据将不准确

- 关联查询

	- 外关联

		- 左关联

			- SELECT  *   FORM  tb_name1   LEFT  JOIN  tb_name2  ON  tb_name1.t2_id  =  tb_name2.t2_id;用表一的t2_id和表二的t2_id来关联，查询所有的值。 
			- FROM 之后的表是主表

		- 中关联

			- SELECT   *    FORM  tb_name1  JOIN   tb_name2   ON   tb_name1.t2_id  =  tb_name2.t2_id;用表一的t2_id和表二的t2_id来关联，查询所有的值。 
			- 中关联没有主表

		- 右关联

			- SELECT   *    FORM  tb_name1   RIGHT  JOIN   tb_name2   ON   tb_name1.t2_id  =  tb_name2.t2_id;用表一的t2_id和表二的t2_id来关联，查询所有的值。 
			- 在ON后边的表是主表

	- 内关联

		- 内管理的关联条件是用where来说关联的，多张表之间用AND来拼接where条件
		- SELECT   *   FROM   tb_name1,tb_name2,....   WHERE   tb_name1.t2_id = tb_name2.t2_id   AND  ...

	- 外关联的说明

		- 主表关联副表，如果副表数据不够用NULL来补全，但是中关联的时候，如果不够了，左边的数据或者右边的数据不会显示。直接去掉

	- 横向连接：两个表字段一样，数据合并

		- union会去重，union all不会

## MySQL函数

### 1.数学函数

- ABS()绝对值
- PI()  π值
- RAND()返回０到１内的随机值,可以通过提供一个参数(种子)使RAND()随机数生成器生成一个指定的值。
- ROUND(x,y)返回参数x的四舍五入的有y位小数的值
- MOD(x,y)                 返回x/y的模（余数）

### 2.聚合函数

- AVG(col)返回指定列的平均值
- COUNT(col)返回指定列中非NULL值的个数
- SUM(col)返回指定列的所有值之和

### 3.字符串函数

- UCASE(str)或UPPER(str) 返回将字符串str中所有字符转变为大写后的结果
- TRIM(str)去除字符串首部和尾部的所有空格
- RTRIM(str) 返回字符串str尾部的空格
- LTRIM(str) 从字符串str中切掉开头的空格
- LENGTH(s)返回字符串str中的字符数
- ASCII(char)返回字符的ASCII码值

### 4.日期和时间函数

- CURDATE()或CURRENT_DATE() 返回当前的日期
- CURTIME()或CURRENT_TIME() 返回当前的时间
- FROM_UNIXTIME(时间戳) 格式化传入的时间戳，转成日期格式
- UNIX_TIMESTAMP()获取系统当前的时间戳
- NOW()返回当前的时间的日期

### 5.加密函数

- MD5()    计算字符串str的MD5校验和
- PASSWORD(str)   返回字符串str的加密版本，这个加密过程是不可逆转的，和UNIX密码加密过程使用不同的算法。
- SHA()    计算字符串str的安全散列算法(SHA)校验和

### 6.控制流程函数

### 7.格式化函数

### 8.类型转化函数

### 9.系统信息函数

- DATABASE()   返回当前数据库名
- USER()或SYSTEM_USER()  返回当前登陆用户名
- VERSION()   返回MySQL服务器的版本
- CONNECTION_ID()   返回当前客户的连接ID
- BENCHMARK(count,expr)  将表达式expr重复运行count次

## 数据库导入导出

### 数据库导出

- 1.打开cmd命令
- 2.打开到mysql文件夹下的bin目录
- 3.通过mysqldump来执行导出
- 4.命令：mysqldump -u root -p 数据库（class15） &gt;  要导出的文件名如：（test.sql）
- 5.导出之后的文件会出现在bin目录下

### sql文件导入

- 1.cmd打开到mysql的bin目录下
- 2.通过   mysql -uroot -p 输入密码的形式进入到数据库中
- 3.选择数据库   USE  db_name;
- 4.执行导入命令：   source d:\datafilename.sql   后边路径是sql文件存放的物理路径

## 数据库引擎

### innoDB

- innodb主键使用自增bigint效率比uuid高1.方便比较大小2.不会破坏B+TREE结构
- 聚集索引：索引和数据在同一张表非聚集索引：索引在一张表，数据在一张表
- innodb使用b+tree存索引和数据 不使用hash的原因：范围查找使用hash不合适，需要全表扫描，hash(主键)直接存储到位置，因此一般使用B+Tree

### show engines查看所有引擎

## 事务

### ACID属性

- 持久性(Durable)

	- 事务完成之后,它对于数据的修改是永久性的,即使出现系统故障也能够保持

- 原子性(Atomicity)

	- 事务是一个原子操作单元,其对数据的修改,要么全都执行,要么全都不执行

- 隔离性(Isolation)

	- 数据库系统提供一定的隔离机制,保证事务在不受外部并发操作影响的“独立”环境执行。这意味着事务处理过程中的中间状态对外部是不可见的,反之亦然

- 一致性(Consistent)

	- 在事务开始和完成时,数据都必须保持一致状态。这意味着所有相关的数据规则都必须应用于事务的修改,以保持数据的完整性;事务结束时,所有的内部数据结构(如B树索引或双向链表)也都必须是正确的

### 并发事务处理带来的问题

- 更新丢失（Lost Update）

	- 两个或多个事务选择同一行，然后基于最初选定的值更新该行时，由于每个事务都不知道其他事务的存在，就会发生丢失更新问题–最后的更新覆盖了由其他事务所做的更新

- 脏读（Dirty Reads）

	- 事务A读取到了事务B已经修改但尚未提交的数据，还在这个数据基础上做了操作。此时，如果B事务回滚，A读取的数据无效，不符合一致性要求

- 不可重读（Non-Repeatable Reads）

	- 一个事务在读取某些数据后的某个时间，再次读取以前读过的数据，却发现其读出的数据已经发生了改变、或某些记录已经被删除了！这种现象就叫做“不可重复读”。  一句话：事务A读取到了事务B已经提交的修改数据，不符合隔离性

- 幻读（Phantom Reads）

	- 个事务按相同的查询条件重新读取以前检索过的数据，却发现其他事务插入了满足其查询条件的新数据，这种现象就称为“幻读”

- 脏读是事务B里面修改了数据,幻读是事务B里面新增了数据

### 事务隔离级别

- 分类

	- 读未提交(Read uncommitted)

		- 脏读/不可重复读/幻读都可能

	- 读已提交(Read uncommitted)

		- 脏读不可能，不可重复读/幻读都可能

	- 可重复读(Repeatable read)

		- 不可重复读/脏读不可能，幻读都可能

			- 可重复读的隔离级别下使用了MVCC机制，select操作不会更新版本号，是快照读（历史版本）insert、update和delete会更新版本号，是当前读（当前版本）
			- 要避免幻读可以用间隙锁在Session   _1下面执行update  acc  ount se t name  ='zhuge'where i d&gt; 10and id&lt;= 20;，则其他Session没法插入这个范围内的数据

	- 可串行化(Serializable)

		- 脏读/不可重复读/幻读都不可能

			- mysql中事务隔离级别为serializable时会锁表，因此不会出现幻读的情况，这种隔离级别并发性极低，开发中很少会用到

- 查看事务隔离级别

	- show variables like 'transaction_isolation';
	- select @@transaction_isolation;

- 默认的事务隔离级别(Repeatable read)

## 优化

步骤：
1.开启慢查询日志,设置阈值,比如超过5秒钟的就是慢SQL,并将它抓取出来;
2.EXPLAIN+慢SQL分析;
3.SHOW profile,查询SQL在MySQL服务器里面的执行细节和生命周期情况
4.具体优化

### explain

- 语法explain select * from xxl_job_log l where l.job_id in (select id from xxl_job_info)
- 字段说明

	- id：表示查询中执行select子句或操作表的顺序

		- id相同,执行顺序由上至下;id不同,如果是子查询,id的序号会递增,id值越大优先级越高,越先被执行;id相同不同,都存在

	- select_type：表示查询的类型，主要用于区别普通查询，联合查询，子查询等复杂查询https://www.cnblogs.com/danhuangpai/p/8475458.html

		- SIMPLE:简单的select查询，查询中不包括子查询或者UNION
		- PRIMARY：查询中若包括任何复杂的子部分，最外层查询则被标记为PRIMARY
		- SUBQUERY:在select或where列表中包含了子查询
		- DERIVED: 在FROM列表中,包含的子查询被标记为DERIVED(衍生),MySQL会递归执行这些子查询,把结果放在临时表里
		- UNION: 若第二个SELECT出现在UNION之后,则被标记为UNION;若UNION包含在FROM子句的子查询中,外侧SELECT将被标记为 DERIVE
		- UNION RESULT: 从UNION表获取结果的SELECT

	- table：查询的表
	- type：在表中找到所需行的方式  ALL、index、range、 ref、eq_ref、const、system、NULL（从左到右，性能从差到好）

		- ALL：全部扫描，效率低
		- index：Full Index Scan，index与ALL区别为index类型只遍历索引树explain select * from film; file中有name字段为索引
		- range：只检索给定范围的行，使用一个索引来选择行explain select * from employee where rec_id &lt; 3其中rec_id为主键
		- ref：表示上述表的连接匹配条件，即哪些列或常量被用于查找索引列上的值查找条件列使用了索引而且不为主键和unique。其实，意思就是虽然使用了索引，但该索引列的值并不唯一，有重复。这样即使使用索引快速查找到了第一条数据，仍然不能停止，要进行目标值附近的小范围扫描。但它的好处是它并不需要扫全表，因为索引是有序的，即便有重复值，也是在一个非常小的范围内扫描。下面为了演示这种情形，给employee表中的name列添加一个普通的key（值允许重复）explain select * from film where name = "film1" ref name是film中的普通索引
		- eq_ref：类似ref，区别就在使用的索引是唯一索引，对于每个索引键值，表中只有一条记录匹配，简单来说，就是多表连接中使用primary key或者 unique key作为关联条件eq_ref 与 ref相比牛的地方是，它知道这种类型的查找结果集只有一个？什么情况下结果集只有一个呢！那便是使用了主键或者唯一性索引进行查找的情况，比如根据学号查找某一学校的一名同学，在没有查找前我们就知道结果一定只有一个，所以当我们首次查找到这个学号，便立即停止了查询。这种连接类型每次都进行着精确查询，无需过多的扫描，因此查找效率更高，当然列的唯一性是需要根据实际情况决定的explain select * from film_actor left join film on film_actor.film_id= film.id eq_ref 根据主键或唯一索引查询film
		- const、system：当MySQL对查询某部分进行优化，并转换为一个常量时，使用这些类型访问。如将主键置于where列表中，MySQL就能将该查询转换为一个常量，system是const类型的特例，当查询的表只有一行的情况下，使用systemselect 1 from actor where id =1 constexplain extended select * from (select * from film where id =1) tmp 临时表中只有一条记录，system
		- NULL： MySQL在优化过程中分解语句，执行时甚至不用访问表或索引，例如从一个索引列里选取最小值可以通过单独索引查找完成explain select min(id) from film id是主键

	- possible_keys：指出MySQL能使用哪个索引在表中找到记录，查询涉及到的字段上若存在索引，则该索引将被列出，但不一定被查询使用（该查询可以利用的索引，如果没有任何索引显示 null），可能出现 possible_keys 有列，而 key 显示 NULL 的情况，这种情况是因为表中数据不多，mys   ql认为索引对此查询帮助不大，选择了全表查询
	- key：显示MySQL实际决定使用的键（索引)
	- key_len：表示索引中使用的字节数，可通过该列计算查询中使用的索引的长度（key_len显示的值为索引字段的最大可能长度，并非实际使用长度，即key_len是根据表定义计算而得，不是通过表内检索出的）不损失精确性的情况下，长度越短越好key_len计算规则如下：字符串	char(n)：n字节长度	varchar(n)：2字节存储字符串长度，如果是utf-8，则长度3n   + 2   数值类型	tinyint：1字节	smallint：2字节	int：4字节	bigint：8字节    时间类型 	date：3字节timestamp：4字节	datetime：8字节 如果字段允许为 NULL，需要1字节记录是否为 NULL索引最大长度是768字节，当字符串过长时，mysql会做一个类似左前缀索引的处理，将前半部分的字符提取出来做索引。
	- ref：列与索引的比较，表示上述表的连接匹配条件，即哪些列或常量被用于查找索引列上的值
	- rows：估算出结果集行数，表示MySQL根据表统计信息及索引选用情况，估算的找到所需的记录所需要读取的行数
	- filtered：一个半分比的值，rows * filtered/100 可以估算出将要和 explain 中前一个表进行连接的行数（前一个表指 explain 中的id值比当前表id值小的表）
	- Extra

		- Using where:不用读取表中所有信息，仅通过索引就可以获取所需数据，这发生在对表的全部的请求列都是同一个索引的部分的时候，表示mysql服务器将在存储引擎检索行后再进行过滤
		- Using temporary：表示MySQL需要使用临时表来存储结果集，常见于排序和分组查询，常见 group by ; order by;distinct
		- Using filesort：当Query中包含 order by 操作，而且无法利用索引完成的排序操作称为“文件排序”
		- Using join buffer：改值强调了在获取连接条件时没有使用索引，并且需要连接缓冲区来存储中间结果。如果出现了这个值，那应该注意，根据查询的具体情况可能需要添加索引来改进能
		- Impossible where：这个值强调了where语句会导致没有符合条件的行（通过收集统计信息不可能存在结果）
		- Select tables optimized away：这个值意味着仅通过使用索引，优化器可能仅从聚合函数结果中返回一行
		- No tables used：Query语句中使用from dual 或不含任何from子句

- 缺点：• EXPLAIN不会告诉你关于触发器、存储过程的信息或用户自定义函数对查询的影响情况• EXPLAIN不考虑各种Cache• EXPLAIN不能显示MySQL在执行查询时所作的优化工作• 部分统计信息是估算的，并非精确值• EXPLAIN只能解释SELECT操作，其他操作要重写为SELECT后查看执行计划

### SHOW WARNINGS 在explain执行后执行，查看翻译后的sql

### 最佳左前缀法则

- 如果索引了多列，要遵守最左前缀法则。指的是查询从索引的最左前列开始并且不跳过索引中的列

### 索引优化规则

- 不在索引列上做任何操作（计算、函数、（自动or手动）类型转换），会导致索引失效而转向全表扫描EXPLAIN SELECT * FROM employees WHERE name = 'LiLei'; 使用索引EXPLAIN SELECT * FROM employees WHERE left(name,3) = 'LiLei'; 未使用索引
- 存储引擎不能使用索引中范围条件右边的列EXPLAIN SELECT * FROM employees WHERE name= 'LiLei' AND age = 22 AND position ='manager'; 使用索引EXPLAIN SELECT * FROM employees WHERE name= 'LiLei' AND age &gt; 22 AND position ='manager'; 未使用索引
- 尽量使用覆盖索引（只访问索引的查询（索引列包含查询列）），减少select *语句EXPLAIN SELECT name,age FROM employees WHERE name= 'LiLei' AND age = 23 AND position ='manager'; 只查询索引不用查询具体的数据，效率更高EXPLAIN SELECT * FROM employees WHERE name= 'LiLei' AND age = 23 AND position ='manager';
- mysql在使用不等于（！=或者&lt;&gt;）的时候无法使用索引会导致全表扫描
- is null,is not null 也无法使用索引
- like以通配符开头（'$abc...'）mysql索引失效会变成全表扫描操作
- 字符串不加单引号索引失效EXPLAIN SELECT * FROM employees WHERE name = '1000';EXPLAIN SELECT * FROM employees WHERE name = 1000;
- or 只有两边都有索引才走索引，如果都没有或者只有一个是不走索引的
- in操作能避免则避免，若实在避免不了，需要仔细评估in后边的集合元素数量，控制在1000个之内
- union all 不去重复，union去重复，union使用了临时表，应尽量避免使用临时表
- order by如果根据多个值进行排序，那么排序方式必须保持一致，要么同时升续，要么同时降续，排序方式不一致不走索引

### 优化方式

- 优化数据库表结构的设计

	- 字段的数据类型

		- 不同的数据类型的存储和检索方式不同，对应的性能也不同，所以说要合理的选用字段的数据类型。比如人的年龄用无符号的unsigned tinyint即可，没必要用integer

	- 数据类型的长度

		- 数据库最终要写到磁盘上，所以字段的长度也会影响着磁盘的I/O操作，如果字段的长度很大，那么读取数据也需要更多的I/O, 所以合理的字段长度也能提升数据库的性能。比如用户的手机号11位长度，没必要用255个长度

	- 表的存储引擎

- 分库分表
- 数据库参数配置优化
- 主从复制，读写分离
- 数据库编码: 采用utf8mb4而不使用utf8
- 字段名

	- MySQL 在 Windows 下不区分大小写，但在 Linux 下默认是区分大小写。因此，数据库名、 表名、字段名，都不允许出现任何大写字母，避免节外生枝。一般所有表都要有id, id必为主键，类型为bigint unsigned,单表时自增、步长为1; 有些特殊场景下(如在高并发的情况下该字段的自增可能对效率有比价大的影响)id是通过程序计算出来的一个唯一值而不是通过数据库自增长来实现的。一般情况下主键id和业务没关系的，例如订单号不是主键id，一般是订单表中的其他字段，一般订单号order_code为字符类型一般情况下每张表都有着四个字段create_id,create_time,update_id,update_time, 其中create_id表示创建者id，create_time表示创建时间，update_id表示更新者id，update_time表示更是时间，这四个字段的作用是为了能够追踪数据的来源和修改最好不要使用备用字段(个人观点), 禁用保留字，如 desc、range、match、delayed 等表达是与否概念的字段，必须使用 is_xxx 的方式命名，数据类型是 unsigned tinyint (1 表示是，0 表示否), 任何字段如果为非负数，必须是unsigned。表达逻辑删除的字段名 is_deleted，1 表示删除，0 表示未删除如果某个值能通过其他字段能计算出来就不需要用个字段来存储，减少存储的数据为了提高查询效率，可以适当的数据冗余，注意是适当强烈建议不使用外键, 数据的完整性靠程序来保证单条记录大小禁止超过8k， 一方面字段不要太多，有的都能上百，甚至几百个，另一方面字段的内容不易过大像文章内容等这种超长内容的需要单独存到另一张表

- 字段类型

	- 字符类型

		- 不同存储引擎对char和varchar的使用原则不同，myisam:建议使用国定长度的数据列代替可变长度。innodb：建议使用varchar，大部分表都是使用innodb，所以varchar的使用频率更高

	- 数值类型

		- 金额类型的字段尽量使用long用分表示，尽量不要使用bigdecimal，严谨使用float和double因为计算时会丢失经度如果需要使用小数严谨使用float，double，使用定点数decimal，decimal实际上是以字符串的形式存储的，所以更加精确，java中与之对应的数据类型为BigDecimal如果值为非负数，一定要使用unsigned，无符号不仅能防止负数非法数据的保存，而且还能增大存储的范围不建议使用ENUM、SET类型，使用TINYINT来代替

	- 日期类型

		- 根据实际需要选择能够满足应用的最小存储日期类型。如果应用只需要记录年份，那么仅用一个字节的year类型。如果记录年月日用date类型, date占用4个字节，存储范围10000-01-01到9999-12-31如果记录时间时分秒使用它time类型如果记录年月日并且记录的年份比较久远选择datetime，而不要使用timestamp,因为timestamp表示的日期范围要比datetime短很多如果记录的日期需要让不同时区的用户使用，那么最好使用timestamp, 因为日期类型值只有它能够和实际时区相对应datetime默认存储年月日时分秒不存储毫秒fraction，如果需要存储毫秒需要定义它的宽度datetime(6)timestamp与datetime两者都可用来表示YYYY-MM-DD HH:MM:SS[.fraction]类型的日期。都可以使用自动更新CURRENT_TIMESTAMP对于TIMESTAMP，它把客户端插入的时间从当前时区转化为UTC（世界标准时间）进行存储。查询时，将其又转化为客户端当前时区进行返回。而对于DATETIME，不做任何改变，基本上是原样输入和输出。timestamp占用4个字节：timestamp所能存储的时间范围为：’1970-01-01 00:00:01.000000’ 到 ‘2038-01-19 03:14:07.999999’datetime占用8个字节 ：datetime所能存储的时间范围为：’1000-01-01 00:00:00.000000’ 到 ‘9999-12-31 23:59:59.999999’总结：TIMESTAMP和DATETIME除了存储范围和存储方式不一样，没有太大区别。如果需要使用到时区就必须使用timestamp，如果不使用时区就使用datetime因为datetime存储的时间范围更大注意：禁止使用字符串存储日期，一般来说日期类型比字符串类型占用的空间小，日期时间类型在进行查找过滤是可以利用日期进行对比，这比字符串对比高效多了，日期时间类型有丰富的处理函数，可以方便的对日期类型进行日期的计算也尽量不要使用int来存储时间戳

	- 是否为null

		- MySQL字段属性应该尽量设置为NOT NULL，除非你有一个很特别的原因去使用 NULL 值，你应该总是让你的字段保持 NOT NULL 。在MySql中NULL其实是占用空间的，“可空列需要更多的存储空间”：需要一个额外字节作为判断是否为NULL的标志位“需要mysql内部进行特殊处理”， 而空值”“是不占用空间的。含有空值的列很难进行查询优化，而且对表索引时不会存储NULL值的，所以如果索引的字段可以为NULL，索引的效率会下降很多。因为它们使得索引、索引的统计信息以及比较运算更加复杂。你应该用0、一个特殊的值或者一个空串代替null。联表查询的时候，例如SELECT user.username, info.introduction FROM tbl_user user LEFT JOIN tbl_userinfo info ON user.id = info.user_id; 如果tbl_userinfo.introduction设置的可以为null, 假如这条sql查询出了对应的记录，但是username有值，introduction没有值，那么就不是很清楚这个introduction是没有关联到对应的记录，还是关联上了而这个值为null，null意思表示不明确，有歧义注意：NULL在数据库里是非常特殊的，任何数跟NULL进行运算都是NULL, 判断值是否等于NULL，不能简单用=，而要用IS NULL关键字。使用 ISNULL()来判断是否为 NULL 值，NULL 与任何值的直接比较都为 NULL。1) NULL&lt;&gt;NULL的返回结果是NULL，而不是false。2) NULL=NULL的返回结果是NULL，而不是true。3) NULL&lt;&gt;1的返回结果是NULL，而不是true。

- 实例

	- EXPLAIN SELECT * FROM tbl_user LIMIT 100000,2;EXPLAIN SELECT * FROM tbl_user u INNER JOIN (SELECT id FROM tbl_user ORDER BY id ASC LIMIT 10000,2) temp ON u.id = temp.id;id为主键，性能高于第一条全表扫描
	- where中如果有多个过滤条件，在没有索引的情况下将过滤多的写在前面，过滤少的写在后面

- 禁止使用select *，需要什么字段就去取哪些字段
- 不要使用count(列名)或 count(常量)来替代 count()，count()是SQL92定义的标准统计行数的语法，跟数据库无关，跟 NULL和非NULL无关。 说明:count(*)会统计值为NULL 的行，而count(列名)不会统计此列为NULL值的行
- 禁止使用存储过程，存储过程难以调试和扩展，更没有移植性。避免使用存储过程、触发器
- 除了 IO 瓶颈之外，SQL优化中需要考虑的就是 CPU 运算量的优化了。order by, group by,distinct … 都是消耗 CPU 的大户（这些操作基本上都是 CPU 处理内存中的数据比较运算）。当我们的 IO 优化做到一定阶段之后，降低 CPU 计算也就成为了我们 SQL 优化的重要目标

## 分区

### 分区方式

- Range

	- 基于属于一个给定连续区间的列值，把多行分配给分区。这些区间要连续且不能相互重叠，使用VALUES LESS THAN操作符来进行定义

		- CREATE TABLE employees (	id INT NOT NULL,	NAME VARCHAR ( 30 ),	hired DATE NOT NULL DEFAULT '2018-12-01',	job VARCHAR ( 30 ) NOT NULL,	dept_id INT NOT NULL 	) 	PARTITION BY RANGE ( dept_id )(	PARTITION p0 VALUES LESS THAN ( 6 ),	PARTITION p1 VALUES LESS THAN ( 11 ),	PARTITION p2 VALUES LESS THAN ( 16 ),	PARTITION p3 VALUES LESS THAN ( 21 ) );

			- 1）、当需要删除一个分区上的"旧的"数据时,只删除分区即可。如果你使用上面最近的那个例 子给出  的分区方案，你只需简单地使用"ALTER TABLE employees DROP PARTITION p0；"来删除所有在1991年前就已经停止工作的雇员相对应的所有行。对于有大量行的表，这比 运行一个如“DELETE FROM employees WHERE YEAR (separated) &lt;= 1990；”这样的一个DELETE查询要有效得多。2）、想要使用一个包含有日期或时间值，或包含有从一些其他级数开始增长的值的列。3）、 经常运行直接依赖于用于  分割 表的 列的查询。例如，当执行一个如“SELECT COUNT(*) FROM employees WHERE YEAR(separated) = 2000 GROUP BY dept_id；”这样的查询时，MySQL可以很  迅速地确定只有分区p2需要扫描 ，这是因为余下的分区不可能包含有符合该WHERE子句的任何记录。

- List

	- 设置若干个固定值进行分区，如果某个字段的值在这个设置的值列表中就会被分配到该分区。适用于字段的值区分度不高的，或者值是有限的，特别是像枚举这样特点的列

		- CREATE TABLE employees (          id INT NOT NULL,          NAME VARCHAR ( 30 ),          hired DATE NOT NULL DEFAULT '2015-12-10',         job_code INT,          store_id INT ) PARTITION BY LIST ( store_id )(	PARTITION pQY VALUES IN ( 3, 5, 6, 17 ),	PARTITION pJN VALUES IN ( 1, 10, 11, 19 ),	PARTITION pCH VALUES IN ( 4, 12, 14, 18 ),	PARTITION pJJ VALUES IN ( 2, 9, 13, 16 ),	PARTITION pGX VALUES IN ( 7, 8, 15, 20 ));

- range columns

	- create table rc3 (	a int,	b int)partition by range columns(a, b) (	partition p01 values less than (0, 10),	partition p02 values less than (10, 10),	partition p03 values less than (10, 20),	partition p04 values less than (10, 35));insert into rc3(a, b) values(1, 10);

- hash分区

	- 常规hash分区

		- 常规hash分区使用的是取模算法，对应一个表达式expr是可以计算出它被保存到哪个分区中，N = MOD(expr, num)

	- 线性hash分区

		- 线性hash分区使用的是一个线性的2的幂运算法则

			- 常规hash分区在管理上带来了的代价太大，不适合需要灵活变动分区的需求。为了降低分区管理上的代价，mysql提供了线性hash分区，分区函数是一个线性的2的幂的运算法则。同样线性hash分区的记录被存在那个分区也是能被计算出来的。线性hash分区的优点是在分区维护(增加、删除、合并、拆分分区)时，mysql能够处理的更加迅速，缺点是：对比常规hash分区，线性hash各个分区之间数据的分布不太均衡

- key分区

	- 按照key进行分区非常类似于按照hash进行分区，只不过hash分区允许使用用户自定义的表达式，而key分区不允许使用用于自定义的表达式，需要使用mysql服务器提供的hash函数，同时hash分区只支持整数分区，而key分区支持使用出blob or text类型外的其他类型的列作为分区键

		- partition by key(expr) partitions num;-- 不指定默认首选主键作为分区键，在没有主键的情况下会选择非空唯一键作为分区键partition by key() partitions num;-- linear keypartition by linear key(expr)

- 子分区

	- 是分区表中对每个分区的再次分割，又被称为复合分区，支持对range和list进行子分区，子分区即可以使用hash分区也可以使用key分区。复合分区适用于保存非常大量的数据记录

		- create table ts (	id int, 	purchased date) partition by range(year(purchased))subpartition by hash(to_days(purchased)) subpartitions 2 (	partition p0 values less than (1990),	partition p0 values less than (2000),	partition p0 values less than maxvalue);

### 管理分区

- -- 删除list或者range分区(同时删除分区对应的数据)alter table &lt;table&gt; drop partition &lt;分区名称&gt;;-- 新增分区-- range添加新分区alter table &lt;table&gt; add partition(partition p4 values less than MAXVALUE);-- list添加新分区alter table &lt;table&gt; add partition(partition p4 values in (25,26,28));-- hash重新分区alter table &lt;table&gt; add partition partitions 4;-- key重新分区alter table &lt;table&gt; add partition partitions 4;-- 子分区添加新分区，虽然我没有指定子分区，但是系统会给子分区命名的alter table &lt;table&gt; add partition(partition p3 values less than MAXVALUE);-- range重新分区ALTER TABLE user REORGANIZE PARTITION p0,p1,p2,p3,p4 INTO (PARTITION p0 VALUES LESS THAN MAXVALUE);-- list重新分区ALTER TABLE &lt;table&gt; REORGANIZE PARTITION p0,p1,p2,p3,p4 INTO (PARTITION p0 VALUES in (1,2,3,4,5));

### 优缺点

- 优点

	- 和单个磁盘或者文件系统分区相比，可以存储更多数据优化查询。在where子句中包含分区条件时，可以只扫描必要的一个或者多个分区来提高查询效率；同时在涉及sum()和count()这类聚合函数的查询时，可以容易的在每个分区上并行处理，最终只需要汇总所有分区得到的结果对于已经过期或者不需要保存的数据，可以通过删除与这些数据有关的分区来快速删除数据跨多个磁盘来分散数据查询，以获得更大的查询吞吐量

## 锁

### 分类

- 乐观锁和悲观锁

	- 乐观锁

		- 根据版本号控制

	- 悲观锁

		- 锁定表或者行，让其他数据操作等待

			- 读锁(共享锁)

				- 针对同一份数据，多个读操作可以同时进行而不会互相影响
				- 不能进行写操作

			- 写锁(排他锁)

				- 当前写操作没有完成前，它会阻断其他写锁和读锁

- 表锁和行锁

	- 表锁

		- 表锁偏向MyISAM存储引擎，开销小，加锁快，无思索，锁定粒度大，发生锁冲突的概率最高，并发度最低当前session对该表的增删改查都没有问题，其他session对该表的所有操作被阻塞 

			- lock table表名称 read(write)unlock tables

				- MyISAM在执行查询语句(SELECT)前,会自动给涉及的所有表加读锁,在执行增删改操作前,会自动给涉及的表加写锁。1、对MyISAM表的读操作(加读锁) ,不会阻寒其他进程对同一表的读请求,但会阻赛对同一表的写请求。只有当读锁释放后,才会执行其它进程的写操作。2、对MylSAM表的写操作(加写锁) ,会阻塞其他进程对同一表的读和写操作,只有当写锁释放后,才会执行其它进程的读写操作总结：简而言之，就是读锁会阻塞写，但是不会阻塞读。而写锁则会把读和写都阻塞

	- 行锁

		- 行锁偏向InnoDB存储引擎，开销大，加锁慢，会出现死锁，锁定粒度最小，发生锁冲突的概率最低，并发度也最高。InnoDB与MYISAM的最大不同有两点：一是支持事务（TRANSACTION）；二是采用了行级锁

### 行锁分析

- show status like'innodb_row_lock%';

	- Innodb_row_ lock_current_wait

		- 当前正在等待锁定的数量

	- Innodb_row_ lock_time

		- 从系统启动到现在锁定总时间长度

	- Innodb_row_ lock_time_avg

		- 每次等待所花平均时间

	- Innodb_row_ lock_time_max

		- 从系统启动到现在等待最长的一次所花时间

	- Innodb_row_ lock_waits

		- 系统启动后到现在总共等待的次数

### 死锁

- Session   _1执行：select *from account where i d= 1  for update;Session   _2执行：select *from account where i d= 2  for update;Session   _1执行：select *from account where i d= 2  for update;Session   _2执行：select *from account where i d= 1  for update;查看近期死锁日志信息：show engine inno   db  statu  s\G;

## 分表

### 横向：表字段相同，数据量太大

- union会去重，union all不会

### 纵向：一个表存基本信息，另外一个表存详情

- join

## 数据访问

### JDBC连接MySQL

### Mybatis连接MySQL

### Spring data Jpa
