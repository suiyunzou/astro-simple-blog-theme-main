## 打开：

mysql -u root -p

### 配置：

创建data文件：目录：C:\Program Files\MySQL\MySQL Server 5.7   

​                          mysqld --initialize-insecure --user=root

### 开关闭服务：



1.停止服务：net stop mysql57

2.开始服务：net start mysql57





----

## ==数据库的增删改查==

----



### 创建数据库：(create)

1.create database 库名    charset=gbk；

2.create database  ·关键库名字·例如：database; 使用``框起来；

3.create database if not exists student; 如果student不存在则创建，存在则不创建；

### 删除数据库：（drop）

1.drop database 库名;

2.drop database if exists student/关键词数据库(database)；如果（关键词databse）/student存在则删除，若不存在则不删除；

3.drop database  ·database`;删除有关键词类型的数据库；

### 修改数据库：（alter）

alter database student charset=gbk;//修改数据库字符编码为gbk；

### 查看数据库：（show）

1.查看已建立的数据库

 show databases;

2.查看数据库中已有的表格：

前提：use 数据库;

show tables;

3.查看创建的数据库信息： 

show create database student ;//查看创建的指令以及所用的字符编码；



****

## 表格的增删改查

-----



###  前提：使用数据库： 

use student;  //使用student 数据库；

### 创建表格：（create）

首先要选择使用的数据

分行写能够更清晰；

1.

create table  mes(

id int , 

name varchar(30) ,

 age int （4）

) ;

2 .

create table if not exists teacher(

​	id int auto_increment primary key comment '主键id'，

> （id为整型，添加主键并且自动增加1，注释：‘主键id’）

name varcahr(30) not null comment '老师的名字' ，

> （名字为不超过30的字符型，不能够不填写，注释：老师的名字 ）

phone varchar(20 ) comment '电话号码',

> 定义长度不超过20 个字符的电话号码，注释为：老师的名字

address varchar (100) default '暂时未知'，comment‘ 住址’

> 定义长度不超过100个字符的电话号码，默认为“暂时未知”，注释：‘住址’

)engine=innodb;

> 数据库引擎为innodb;



### 删除表格：(drop)

drop table mes;//删除mes表格；

drop table mes，a,b;//删除mes,a,b表格；(删除多个表格用，隔开)

删除表格某一项：

alter tablle student drop gender ；//删除性别



### 修改表格：（alter）

alter table student add phone varchar（30）；//添加电话号码

> 在表格中,增加新字段 默认放到最后;

alter table student add gender  varchar（2）after name；//把性别gender放大name之后；after name 可替换为：first，放到最开始；

>在表格中,增加新增字段并放到指定位置之后；

alter tablle student change phone  tel int（20）；//把phone改为tel

> alter table  <表名>change <旧字段名> <新字段名> <新数据类型>;   //修改字段名称；

alter table student modify tel varcahr(20);// 修改数据类型为int（20）；

>修改表格中字段的数据类型;

alter table student rename to stu;//修改表格名字；

> 修改表格名称;

### 查看表格：（desc）

desc teacher;





----

## ==数据的增删改查==

****



### 增加数据：（insert）

 **按自己要求增加**

1.insert into game (id,image,name,price)values(1,1,'beiqioafeng','100');

> 插入内容到表格game，（id，image，name，price）要添加内容，值为（1,1,'beiqioafeng','100'）
>
> 

2.insert into game values(1,1,'beiqioafeng','100')；



**增加多条数据：**

3.insert into game values(1,1,'beiqioafeng','100'),(1,1,'nanmurong','101');



### 删除数据：（delete）

delete from game where id=1;

>删除id为1的数据

delete from game where age>32;

>删除表格中所有年龄> 32的数据 ； 

delete from game;

> 删除表格中所有的内容，---------通过循环遍历删除每一项数据，速度过慢，而且下一次会接着上次的id续加，删库paolu有点慢啊；

truncate table  game;

> 毁掉整张表格，并创建一个新表个没有任何的数据

### 修改数据：（update）

**修改该条数据的一个信息**

update game set name='daming'  where id=1;

> 修改id=1的数据姓名为daming；

**修改某条数据的多条信息**

update game set name='daming' ，phone=111111  where id=1;

> 修改id=1的数据姓名为daming 电话号码为111111；

**按照条件修改数据信息**

update game set name='daming'  where id=1 or id=2;

> 修改id=1或者id=2的数据姓名为daming；

### 查看数据：（select）

select*from game;

> 选择game表格的所有内容；

select id name from game；

> 只看id 与name；

## ELSE

### 数据库语言（DDL）

data defination language 数据库定义语言 create  drop alter  show；

### 数据语言（DML）

 data manipulation language 数据库控制语言 insert delete update  select



### 修改字符编码

show  variables like 'character_set_%';

set character_set_%=utf8；

> 设置所有字符编码为utf8；

## 数据类型

### 字符类型

char(定长,表示范围比varchar小,但是效率快);

 varchar(不定长,表示范围大,占用字节根据实际,多余空间会收回);

### 数值类型

tinyint :smallint ;mediumint ;int ;

bigint , float,double,decimal(用于存钱,因为精确);

### 日期与时间

| 类型     | 字节 | 范围                                    | 写法                | 解释             |
| -------- | ---- | --------------------------------------- | ------------------- | ---------------- |
| DATETIME | 8    | 1000-01-01 00:00:00/9999-12-31 23:59:59 | YYYY-MM-DD HH:MM:SS | 混合日期和时间值 |

### 枚举(取1个)与集合(取多个)

举例枚举:

假如在student表格之下;

create table t_1(

sex  enum ('man','woman','notsee');

);

举例集合:

insert into student values (1)/('man');//,两种写法,数字1表示取枚举类中第一个枚举类型;man表示自己写值;

create table t_1(

sex  set ('man','woman','notsee')；

);

insert into student values ('man,woman');  注意  **'  values1, values2 ,  ...  ' 用 ' , '隔开;**

## 键

## 主键(primary key )

**特点**：唯一，与其他表可相关。



### 增加主键：

alter table 名字  add primary key(字段名称);

### 删除主键：

alter table 名字  drop primary key;

### 查看主键：

desc <表名>；



## 唯一键(unique)

**特点**：唯一(可多字段都有唯一键)，可以与其他表不相关。



### 增加唯一键：

alter table 名字 add unique(字段名称);

### 删除唯一键：

alter table 名字 drop index <字段名称>；

### 查看唯一键：

desc <表名>;

----

## 数据库的完整性

实体完整性：有主键；

参照完整性；外码可以为空；

域完整性；

---



## 外键

### **增加外键**；

alter talbe stu   add  foreign key id references  mes(id)  on delete set NULL on update cascade ;

> 选择stu表，增加外键id参考mes表的id,删除的时候置空,更新的时候级联；

### **删除外键**；

show create table  stu; 

> 首先查找该表中外键的名称；

alter table stu drop foreign key "查找的名字";

>选择stu表删除外键“删除的名字”；

## 置空与级联

删除置空：如果主表的数据删了，则该字段所在外键的那张表数据字段也被置空；

更新级联：关联操作；修改主表的数据，则该字段所在外键的那张表数据字段也被修改；

----

## 实体

实体间的关系：一对一，一对多，多对多；

----

## CODD范式

第一范式：确保每列原子性（原子不可再分）；

第二范式：非键字段要依赖字段（表的字段要符合表）（）

第三范式：消息传递依赖；（高考总成绩【总分】与大学生考试成绩【不需要总分】）

（学号->系->系主任）主键：学号 其余为非主属性

## 模糊查询

select *from student where name like '张%' (%一个或多个字符)或 ‘张_’（一个字符）;

## 字段

### **select** 

1. select 2*7 as result；

| result |
| ------ |
| 14     |

2.select ‘stu’ as '学生'；as后面跟的是别名；

| 学生 |
| ---- |
| stu  |

### from

select * from stu，mes；（stu与mes两张表做笛卡尔积）

### dual(伪表名)

select 2*7 from dual

| 2*7  |
| ---- |
| 14   |

### where

条件

### in

select  age 

from mes

where name not in ('zhangsan');

> 选择名字不是zhangsan的所有学生的年龄；

### between

select age

from mes

where age not between 15 and 20 （包括15和20）；

> 选择年龄不在15到20 学生的年龄；

### is null

select name，address

from mes

where address is （not）null；

> 选择地址为空（非空）的名字与地址；

### 聚合函数





## 子查询

### 多表查询之in and not in

select  * from student where id in ( select stuid from score where score>=85); //查询学生成绩在>=85分以上的学生信息；

### 多表查询之exists与 not exists

select  * from student where   not EXISTS ( select stuid from score where score>=85);

## 视图

视图的作用：

将sql查询语句的结果保存起来，方便以后直接使用。能够起到保护别人隐私的作用。

例如：我只想知道学生的姓名和成绩，而不想显示它们的性别，身份证，手机号 等隐私性的信息，这个时候我们就可是使用视图。



增加视图：

create view vm_student_all as  select name,age,phone  from student inner join score on student.id = score.stuid

修改视图：

alter view vm_student_mes as select name  ,score from student inner join score on student.id = score.stuid;

作用：修改vm_student_mes视图字段为姓名，分数；

删除视图：

drop view vm_student_mes;    

作用：删除视图vm_student_mes；

查看视图：

select  * from vm_student_mes;  

作用：查看视图vm_student_mes；



## 事务

 事务：就比如你要商城买东西，怎么确保你购物时候，你的账户减少，商家的账户增加，怎么保证它们的一致性，这个时候就用到了事务的概念。

start transaction ; //开启事务

//事务的处理

 update balance set balance = balance - 1 where id =1;
 update balance set balance = balance + 1 where id =2;

//提交事务

 commit;



## 事务的ACID：

Atomicity：原子性  事务要修改就一起修改

Consistency：一致性 事务一旦修改，相应的数据就应该发生变化

Isolation：隔离性      ac的事务，bd不可能打乱

Durability:持久性   数据一旦修改，就会永久保存



## 索引(index)

索引：比如查字典，根据字母前缀去定位单词的位置

优缺点：方便查，不方便增删改



创建索引：

create index balance_index on balance(balance);//给balance表的balance字段添加索引

格式：create index index_name on tablename(column_name)



修改索引：

alter table student add index student_index(name);//选择表student并添加索引name；

格式：alter table tablename add index indexname(column_name)



删除索引：

drop index balance_index on balance//删除表索引

格式：DROP INDEX [indexName] ON mytable; 



查看索引：

格式：SHOW INDEX FROM table_name\G



## 定界符delimiter 与 

delemiter // 那么mysql结束就不是；而是//

## 存储过程procedure用途

用途：天猫双11，给每个用户+1.1，并且修改淘宝表name字段为MaBaBa；

1. 先修改分节符

delemiter // 

2. 在设置程序

mysql> create procedure double11()
    -> begin
    -> update balance set balance=balance+1.1;
    -> update taobao set name = 'MaBaBa';
    -> end //

3. 双11当天执行程序

执行：call double11()；

## number



有趣的函数：

抽奖：

select*from student order by rand() limit 3 ;

随机数：

select rand()；

向上取整

select ceil(3.1);  //4

向下取整

select floor(3.1);  //3

四舍五入

select round(3.1);  //3

取位数

select truncate(3.1415926,2); //3.14

## String

大写

select ucase('fuck');  //FUCK

小写

select lcase('Fuck'); //fuck

拼接

select concat('s','b'); //sb

截取

select substring('fuckyou',1,4); //从1开始截取四位，fuck；

## other

获取当前时间

select now();

获取unix时间戳

select UNIX_TIMESTAMP();

获取当前时间年月日分

select year(now())year, month(now())month,day(now())day,MINUTE(now())minute; 

![image-20240331204752350](mysql.assets/image-20240331204752350.png)

加密字符串 

select sha('123456');#7c4a8d09ca3762af61e59520943dc26494f8941b

## 规范

### 库表字段约束规范

1. 对于判断类型：比如vip  字段名称为 ：is_vip，而且必须是无符号 短整型(unsigned tinyint);

2. 对于表名称：不能是复数；不能是关键字

3. 字段名称多个单词用“__”分开；

4. 小数不用float，double，用decimal；

5. uk_XXX （唯一键名称）, pk_XXX（主键名称）,idx_XXX（索引键名称）；

6. 对于字符串：5000以上用text，以下varchar；

7. id，create_time，update_time；

   **id必须**是**bigint**，必须**无符号**，必须**自增**；

   create_time，update_**time必须是datatime**；

8. 年龄：tinyint ；

9. 库大于2g，分库；

### SQL开发约束

1. count(*)，count(XXX,XXX)有区别：

   count()可以统计空字段，count(XXX)不能够；

2. 判断某个字段是不是空用函数 isnull()；

3. 不要使用存储过程操作。

   因为你不知道你的sql语句的问题，当不用事务时候会出现有的数据会出现不一致性，就算使用事务也不能保证。

4. 当执行更新或删除操作时候要先查询，查询后再去修改，插入，删除。

5. 避免使用in

6. 避免使用外键，级联。





