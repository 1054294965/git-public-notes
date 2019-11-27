### union 和union all         
union去重，union all不去重

### 2个表的交集和差集:
    join是交集
    (left join)    union   (right join ) 是差集

### mysql查看慢查询语句
show variables like '%slow%';

### mysql 列=列：   
只能查出非空数据
SELECT * FROM `user` where del_flag=del_flag ;


### navicat使用
```
navicat选中整个格子：  右键即可      或者 shift+上箭头下箭头各一次
f8 显示主窗口
ctrl+h  navicat历史记录
navicat  查找数据 ，会高亮显示(浅粉色，不容易看出来)
navicat 查询中修改数据： 只有select *才可以修改， select 某个字段是不行的。
navicat 运行快捷键：
ctrl+r 运行全部
ctrl+shift+r  运行已选择的
f7   从这里运行一个语句
navicat 表的模糊查询是可以跨越所有打开的数据库的
```

### mysql in和exists：
in是在内存中查询    in跟的是结果集
exists是去数据库中查询    exists跟的是true or false

### 删除重复列：
    DELETE FROM table WHERE
    id IN (
     SELECT id FROM (
    SELECT id,COUNT(*) FROM table
    GROUP BY id
    HAVING COUNT(*) > 1
     ) AS a
    ) LIMIT 1;


### 添加唯一索引：
    alter table group_portray_analysis add unique(group_portray_name);   //首先  数据库中要没有重复列

### mybatis什么情况返回0：  
    如果是批量  操作成功多少条，就返回几个
    例如删除一个不存在的id
    update一条记录，但是id不存在
    delete from group_portray_analysis where group_portray_name='adjfasdjadsf';

### 修改列的位置：2种用法(first或者after某个列名)
alter table ttt2 modify chushiyun varchar(32) first;
alter table ttt2 modify chushiyun varchar(32) after id;

### change和modify的区别:
    如果列名需要修改,那么就需要用change, 否则用modifiy即可.  change语法如: change column column_new
    列定义最少要有2个：
    column_name column_definition ...

### 去重:
```
delete from table where key in(
            select t.key from(
                elect key from table group by key having count(*)>1
            ) t
        )and id not in(
            select t.id from(
                select max(id) as id from table group by id having count(*)>1
            ) t
        )
```
