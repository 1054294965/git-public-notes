### mysql修改列
      alter table city add column3 decimal(15,2); # column标识符是可选的
      alter table city add column column2 decimal(15,2); #列名和列定义
      alter table city add (column5 decimal(15,2),column6 decimal
      (15,2));   #多列用小括号()扩起来
      alter table city drop column3; #删除列只要有名字就行

### bash中执行mysql
    mysql --password=1234 -e "use test;select * from user limit 1" db_springboot_mobile;  #不要忘记-e(--execute="select * from user limit 1"  )
    mysql --password=1234 --execute="show variables" db_springboot_mobile;


### mysql报错：Access denied for user 'root'@'localhost' (using password: YES)
    mysql命令行:
    use mysql;
    update user set password=PASSWORD("1234") where user='root';  -- 重置密码
    flush privileges;

### mysql触发器例子:
    show triggers;  #查看所有触发器
    drop trigger trigger1;   #删除触发器
    create trigger trigger1 before insert on ttt for each row insert into one_table values(1); #创建触发器
    创建单列表：
    create table one_table(
      id int
    )default character set=utf8;
    给ttt新增一条数据，发现one_table自动插入一条数据。

### mysql引擎
    show engines; # 查看所有支持的引擎  support是default的那个就是
    select * from information_schema.engines where support='default';

### mysql information_schema
    information_schema 是一个数据库：
    use information_schema;  # 使用information_schema库
    select table_schema,table_name,table_comment from tables limit 1; # table_schema 表所在数据库名   table_name表名  table_comment表注释  table_type表类型(base table或者view)
    select table_schema,table_name,column_name,data_type,column_type,column_comment from columns limit 1;  #columns表没有table_type字段
    column_type和data_type区别：  column_type是 varchar(32)   data_type 是varchar

### mysql存储过程
```
存储过程：
show procedure status;  #查看所有存储过程
show create procedure doiterate;  #查看存储过程创建语句
delimiter //   # 这里不要加分号
delimiter ;    # 还原分隔符为";"

例子1:
delimiter //
CREATE PROCEDURE doiterate(p1 INT)
BEGIN
  label1: LOOP
    SET p1 = p1 + 1;
    IF p1 < 10 THEN
      ITERATE label1;
    END IF;
    LEAVE label1;
  END LOOP label1;
  SET @x = p1;
END;
select @x;

例2：
DROP TABLE IF EXISTS test.test;
CREATE TABLE test.test(
id int(10) not null auto_increment,
a int(10) not null,
b int(10) not null,
c int(10) not null,
PRIMARY key (`id`)
)ENGINE INNODB DEFAULT CHARSET utf8 COMMENT '测试表';
#清空数据
TRUNCATE table test.test;

#定义存储过程

delimiter //
DROP PROCEDURE IF EXISTS insert_test_val;
##num_limit 要插入数据的数量,rand_limit 最大随机的数值
CREATE PROCEDURE insert_test_val(in num_limit int,in rand_limit int)
BEGIN

DECLARE i int default 1;
DECLARE a int default 1;
DECLARE b int default 1;
DECLARE c int default 1;

WHILE i<=num_limit do

set a = FLOOR(rand()*rand_limit);
set b = FLOOR(rand()*rand_limit);
set c = FLOOR(rand()*rand_limit);
INSERT into test.test values (null,a,b,c);
set i = i + 1;
END WHILE;
END
//
#调用存储过程
call insert_test_val(100000,10); #call 只能跟存储过程

call doiterate(2);  #传参并调用存储过程
创建或替换一个存储过程：
create or replace A as
begin
...
end;
delimieter //;  #重置定界符  因为存储过程中需要用 ";" 作为定界符
```
