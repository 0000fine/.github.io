## **1.项目名称：基于Arduino UNO开发板的童车倒车报警系统**
## 开发环境：Arduino UNO开发板+HC-SR04模块+LCD1602+光敏电阻+蜂鸣器+LED灯+马达驱动器
项目描述：该项目主要利用Arduino软件编写HC-SR04（超声波模块）、LCD1602、蜂鸣器、LED灯、马达驱动器和光敏电阻的代码，将已完成的代码烧录到Arduino UNO开发板中，HC-SR04（超声波模块）会检测车后方的实时距离并显示在LCD1602屏幕上，当距离小于20厘米时，蜂鸣器、LED（红）灯、会发出警报并且由马达驱动器驱动的车轮也会停止转动以保证童车的安全。光敏电阻检测到亮度为暗时，自动打开车LED（白）灯。
<br>如图所示：
![](https://github.com/0000fine/1032303971-qq.com/blob/Photos/%E4%BB%BF%E7%9C%9F%E5%9B%BE.png) 

<br><br>

## **2.mysql服务设置远程连接 解决1251 client does not support ..问题**
## 一、前期准备
1、虚拟机/物理机    mysql环境（非本机）
<br>2、本机 navicat软件（验证远程连接）
## 二 、mysql配置
1、在远程主机的本机   使用root用户连接mysql
* 命令：mysql -u root -p
* 备注 ： mysql -u 最高权限用户名 -p   再输入密码进入
<br>2、设置用户配置项
<br>(1) 查看用户信息
* select host,user,plugin,authentication_string from mysql.user;
* 备注：host为 % 表示不限制ip   localhost表示本机使用    plugin非mysql_native_password 则需要修改密码
<br>(2)修改用户密码
* ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'newpassword'; 
* 备注：更新一下用户的密码 root用户密码为newpassword

<br><br>

## **3.mysql数据库学习笔记**

### 数据库：
数据库对象：如：表、视图、存储过程、事件、查询、函数、报表和触发器等...
RDBMS 关系数据库管理系统:     
* 表（table）
* 数据库（database）
* 列（字段）
* 行（记录）
* 主键（唯一）
* 外键（关联两个表）
* 索引（目录）<br><br>

### 基础命令：
* create database 数据库名;  创建
* drop database 数据库名； 删除
* show databases； 查看数据库
* use 数据库名； 使用数据库
* show tables； 查看表<br><br>

### 字符集：（因为计算机只能识别二进制）
* ASSCII: 文字符号.（ANSI 20世纪60年代） ISO-646
* Unicode: (全世界语言、文字和符号) ISO-10646
* UTF-16
* UTF-8
* 汉字常见字符集：GB2312 GB13000 GBK GB18030<br><br>

### 存储引擎：（5.5版本）分类：
* MYISAM：不支持事务、外键，但是访问速度快;
* INNODB:支持事务提交、回滚和崩溃恢复，但是占空间大（保留数据与索引） 5.5版本默认选择
* MEMORY:使用内存存储 * *.frm*  优点：访问速度快  缺点：服务器关闭，数据丢失，表存在.
* **事务：是指作为单个逻辑单元执行的一系列操作，要么完全执行，要么完全不执行.**
* **扩展名：*.frm*:存储表定义 *MYD*:（MYData，存储数据）*MYI*:(MYIndex，存储索引)**<br><br>

### SQL：（结构化查询语言）数据库语言 分类：
* **DDL（数据定义语言）：定义数据库对象，创建库、表、列等.**
* ++ 创建数据库：create database 数据库名 character set utf8;
* ++ 创建表：create table 表名（
* 列名1 列的数据类型 [约束],
* 列名2 列的数据类型 [约束],
* ...... .......    .....
* 列名N 列的数据类型 [约束]
* ）;
* ++ 添加一列：Alter table 表名 add 列名 数据类型；
* ++ 修改字段类型：Alter table 表名 modify 字段名 数据类型；
* ++ 删除列： Alter table 表名 drop 字段名；
* ++ 修改表名：Alter table 原表名 to 新表名；
* ++ 查看字段信息：desc 表名；
* ++ 查看表的创建细节：show create table 表名；
* ++ 修改字符集：Alter table 表名 character set 字符集；
* ++ 修改表的列名：Alter table 表名 change 原列名 新列名 数据类型；
* ++ 删除表:drop 表名；
<br>———————————————————————————————————————————
* **DML（数据操作语言）：操作表中的记录.**
* ++ 查询表中的所有数据：select * from 表名；or select * from 表名\G；
* ++ 增加表的记录：insert into 表名（字段名1，字段名2，...） values（列值1，列值2，...）；
* ++ 改表的记录：update 表名 set 列名1=值1，列名2=值2，... where 列名1=值1，列名2=值2，...；
* ++ 修改数据库密码(1)：
*   use mysql；
*  **(5.7版本以前)** update user set password=password('新密码') where user='root';
*  **(5.7版本以后)** update user set authentication_string=password('新密码') where user='root' and Host='localhost';
*  **刷新MySQL的系统权限相关表** flush privileges;
* **修改数据库密码（2）：**
*  mysqladmin -u root -p password 新密码;
* ++ 删除表的记录:
*  delete from 表名 [where 列名=[值]]；
* truncate table 表名；
* **deleted 和 truncate 的区别** ：deleted[表结构还在，数据可找回]，truncate[删除表，建新表，数据库不可找回]
<br>———————————————————————————————————————————
* **DQL（数据查询语言）：查询数据库.**
* ++ 查询所有列：select * from 表名；
* ++ 结果集：内存中，虚拟表.
* ++ 查询指定的列：select 列1，列2，...  from 表名；
* ++ 查询条件：【where】
*  运行符以及关键字：
* *  ____ =、！=、<>(不等于)、<、>、<=、>=
* *  ____ Between......and.......
* *  ____ IN(set):固定范围值
* * ____ is null:(为空) 、 is not null(不为空)
* *  ____ and:与
* * ____ or:或
* *  ____ not:非
* **++ 模糊查询:(关键字【like】)**
*  **通配符：**
*  _ :任意一个字符；
*  % :任意0~N个字符； 例：包含 ： %s%
*  **字段控制查询：**
*  去重：distinct   格式：select distinct name from 表名；
*  结果运算，数值类型： select * ,age+score from 表名；
* select * ,ifnull(age,0)+ifnull(score,0) as 别名 from 表名；
*  **排序：**【order by】 类别：asc：升序（小——>大） desc：降序（大——>小）
*  **聚合函数：**
* count:不为null的行数；
* MAX：最大值；
* MIN: 最小值；
* SUM: 求和，如果不是数值型，结果为0；
* AVG: 平均值，如果不是数值型，结果为0；
* **分组查询(将查询的结果按照1个或者多个字段进行分组，字段值相同的为一组)**
* 分组使用：select gender,gruop_concat(name) from employee gruop by gender;
* gruop by + 聚合函数：select department,gruop_concat(salary) from employee gruop by department;
* gruop by + having: 分组查询后指定一些条件来输出结果.
* **having 和 where 的区别**
* having在分组后对数据进行过滤；
* where在分组前对数据进行过滤；
* having后面可以使用分组函数（统计函数）；
* where后面不可以使用分组函数；
* where是对分组前记录的条件，如果某行记录没有满足where子句的条件，那么这行不参加分组；而having是对分组后的数据的约束.
* **书写顺序：select->from->where->gruop by->having->order by->limit**
* **执行顺序：form->where->gruop by->having->select->order by->limit**
<br>———————————————————————————————————————————
* DCL（数据控制语言）：用来定义访问控制权限和安全级别.
<br>———————————————————————————————————————————

<br>
### SQL数据分类：
* 数值   decimal:高精度小数
* 字符串 
* 日期和时间   timestamp(时间戳): 格林威治时间1970年01月01日00时00分00秒(北京时间1970年01月01日08时00分00秒)起至现在的总秒数.——2038年
<br>

### 常用数据类型:
* double(浮点型)：double(5,2)[最多5位，2小数位] MAX: 999.99
* char(固定长度)：char(10) 'abc_ _ _ _ _ _ _'
* varchar(可变长度)：varchar(10) 'abc'
* text(文本)
* blob(二进制)
* data(日期)： yyyy-MM-DD
* time(时间)： hh:mm:ss
* datatime(日期和时间)： yyyy-MM-DD hh:mm:ss

