# MySQL基础 - 数据类型

> MySQL 支持多种类型，大致可以分为三类：数值、日期/时间和字符串(字符)类型。

[[toc]]

# 数值

> MySQL 支持所有标准 SQL 数值数据类型。
> 这些类型包括严格数值数据类型(TINYINT, SMALLINT, MEDIUMINT, INT, BIGINT、DECIMAL 和 NUMERIC)，以及近似数值数据类型(FLOAT、REAL 和 DOUBLE PRECISION)。

![MySQL数值类型](/_images/database/mysql/basic/MySQL数值类型.png)

## 整型

TINYINT, SMALLINT, MEDIUMINT, INT, BIGINT 分别使用 8, 16, 24, 32, 64 位存储空间，一般情况下越小的列越好。

INT(11) 中的数字只是规定了交互工具显示字符的个数，对于存储和计算来说是没有意义的。

## 浮点数

FLOAT 和 DOUBLE 为浮点类型，DECIMAL 为高精度小数类型。CPU 原生支持浮点运算，但是不支持 DECIMAl 类型的计算，因此 DECIMAL 的计算比浮点类型需要更高的代价。

FLOAT、DOUBLE 和 DECIMAL 都可以指定列宽，例如 DECIMAL(18, 9) 表示总共 18 位，取 9 位存储小数部分，剩下 9 位存储整数部分。

## 日期和时间类型

> 表示时间值的日期和时间类型为DATETIME、DATE、TIMESTAMP、TIME和YEAR。
> 每个时间类型有一个有效值范围和一个"零"值，当指定不合法的MySQL不能表示的值时使用"零"值。

![MySQL日期和时间类型](/_images/database/mysql/basic/MySQL日期和时间类型.png)

MySQL 提供了两种相似的日期时间类型：DATETIME 和 TIMESTAMP。

### DATETIME

能够保存从 1001 年到 9999 年的日期和时间，精度为秒，使用 8 字节的存储空间。

它与时区无关。

默认情况下，MySQL 以一种可排序的、无歧义的格式显示 DATETIME 值，例如“2008-01-16 22:37:08”，这是 ANSI 标准定义的日期和时间表示方法。

### TIMESTAMP

和 UNIX 时间戳相同，保存从 1970 年 1 月 1 日午夜（格林威治时间）以来的秒数，使用 4 个字节，只能表示从 1970 年 到 2038 年。

它和时区有关，也就是说一个时间戳在不同的时区所代表的具体时间是不同的。

MySQL 提供了 FROM_UNIXTIME() 函数把 UNIX 时间戳转换为日期，并提供了 UNIX_TIMESTAMP() 函数把日期转换为 UNIX 时间戳。

默认情况下，如果插入时没有指定 TIMESTAMP 列的值，会将这个值设置为当前时间。

应该尽量使用 TIMESTAMP，因为它比 DATETIME 空间效率更高。

## 字符串

> 字符串类型指CHAR、VARCHAR、BINARY、VARBINARY、BLOB、TEXT、ENUM和SET。该节描述了这些类型如何工作以及如何在查询中使用这些类型。

![MySQL字符串类型](/_images/database/mysql/basic/MySQL字符串类型.png)

主要有 CHAR 和 VARCHAR 两种类型，一种是定长的，一种是变长的。

VARCHAR 这种变长类型能够节省空间，因为只需要存储必要的内容。但是在执行 UPDATE 时可能会使行变得比原来长，当超出一个页所能容纳的大小时，就要执行额外的操作。MyISAM 会将行拆成不同的片段存储，而 InnoDB 则需要分裂页来使行放进页内。

VARCHAR 会保留字符串末尾的空格，而 CHAR 会删除。

# 选择优化的数据类型 

* 数据类型的选择：更小的通常更好；更小的数据类型通常更快，因为它们占用更少的磁盘、内存和CPU缓存，并且处理时需要的CPU周期也更少； 
* 简单原则: 整形比字符串操作代价更低；实用内建类型而不是字符串来存储日期和时间；用整形存储IP地址等； 
* 尽量避免NULL: 如果查询中包含可为NULL的列，对MySQL来说更难优化，因为可为NULL 的列使得索引、索引统计和值比较都更复杂。尽管把可为NULL的列改为NOT NULL带来的性能提升比较小，但如果计划在列上创建索引，就应该尽量避免设计成可为NULL的列； 

# 选择表示符（identifier） 

* 整数类型通常是标识列的最佳选择，因为它们很快并且可以使用AUTO_INCREMENT。
* 尽量避免使用字符串类型作为标识列，因为它们很耗空间，并且比数字类型慢。
* 完全随机的字符串需要多加注意，例如MD5(),SHA1()或者UUID()产生的字符串。这些函数生成的新值会任意分布在很大的空间内，这会导致INSERT以及一些SELECT语句变得很慢。
* 因为插入值会随机的写入到索引的不同位置，所以使得INSERT语句更慢。这会导致叶分裂、磁盘随机访问。 
* SELECT语句会变的更慢，因为逻辑上相邻的行会分布在磁盘和内存的不同地方。 
* 随机值导致缓存对所有类型的查询语句效果都很差，因为会使得缓存赖以工作的局部性原理失效。

## 示例

* 选择合适的数据类型，例如，
  * 年龄不会出现负数、而且不会太大，选择 `tinyint unsigned`
  * 用户名长度不定，但是应该限制不超过一定值，选择 `varchar(20)`, 
  * 入职时间只需准确到日期，选择 `DATE`
  * 考试成绩，最多出现一位小数，选择 `double(4,1)`
  * 手机号，固定为11位长度，选择 `char(11)`
  * 性别，存储男或女，选择 `char(1)`

* String类型的数据定义一个数据库的数据库类型，一般参考的都是char或者varchar，两者的区别如下：

    * char的长度是不可变的，而varchar的长度是可变的，也就是说，定义一个char[10]和varchar[10]，如果存进去的是‘json’，那么char所占的长度依然为10，除了字符‘json’外，后面跟六个空格，而varchar就立马把长度变为4了。

    * char的存取速度还是要比varchar要快得多，因为其长度固定，方便程序的存储与查找；但是char也为此付出的是空间的代价，因为其长度固定，所以难免会有多余的空格占位符占据空间，可谓是以空间换取时间效率，而varchar是以空间效率为首位的。

    * char的存储方式是，对英文字符（ASCII）占用1个字节，对一个汉字占用两个字节；而varchar的存储方式是，对每个英文字符占用2个字节，汉字也占用2个字节。