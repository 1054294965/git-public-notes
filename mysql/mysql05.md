### 唯一索引加在2个字段上：
    alter TABLE re_field_sql add CONSTRAINT uqfield UNIQUE(sql_field,del_flag)
    添加和删除外键约束：
    alter TABLE re_field_sql add CONSTRAINT uqfield UNIQUE(sql_field,del_flag);
    alter TABLE re_field_sql drop constraint uqfield;

### 查看表和视图
    show tables ; -- 查看所有表（不包含view）
    show full tables; --  查看所有表(包含view)
    show full tables where table_type ='view';  -- 查看所有视图
    show full tables where table_type !='view';  -- 查看非视图表
    show full tables where table_type ='base table';  -- 查看非视图表2
    show tables in db_springboot_jpa; -- 查看某个数据库的所有表  in

### mysql报错：Results have expired, rerun the query if needed.     
查询结果已经过期，如果需要结果重新运行sql


### mysql
    select if(length('abcd')=5,'yes','no')  -- if语句
    select length(nickname)  from dual_2018;   -- length
    select greatest(100,200,150)   -- 最大值
    select least('2016-01-01','2017-01-01'); -- 最小值
    select rand(); -- 随机值
    select split('a-b-c','-'); -- 分隔字符串
    select "2311443" rlike '^\\d*$' ;    -- 正则        r是reg的意思
    select map('100','tom','101','mary')   -- map 构建（必须是偶数）
    select size(map(1,3))  -- map size

    SELECT nvl(null,'0')   -  如果为空就用后面的值,否则使用前面的值.
    SELECT nvl(1,'is null')
    SELECT ifnull(age,'0') from user where id='7';

    select array(11,2222)[0]

    select find_in_set('bb','aabbcc,bb,aa')  -- 集合中出现的位置
    select ascii('a')   -- 字符的ascii码
    select concat('aaa',space(7),'b')   -- 7个长度的空格
    SELECT  COALESCE(NULL, 111, NUll,222)     -- 返回第一个非空的值,如果全为null，返回null
    SELECT cast('12.3456' AS DECIMAL (5,2))   --  类型转换函数

### case when
    CASE
    WHEN cast(auth.auth_sex AS INT) = 1 THEN
    '男'
    WHEN cast(auth.auth_sex AS INT) = 2 THEN
    '女'
    ELSE '未知'
    END AS sex,

### GROUPING SETS相当于多个group by 结果的union all
    select name, work_space[0] as main_place, count(employee_id) as emp_id_cnt
    from employee
    group by name, work_space[0]
    GROUPING SETS((name,work_space[0]), name, ());
    // 上面语句与下面语句等效
    select name, work_space[0] as main_place, count(employee_id) as emp_id_cnt
    from employee
    group by name, work_space[0]
    UNION ALL
    select name, work_space[0] as main_place, count(employee_id) as emp_id_cnt
    from employee
    group by name
    UNION ALL
    select name, work_space[0] as main_place, count(employee_id) as emp_id_cnt
    from employee;

### mysql去掉2边的双引号
    select TRIM(BOTH '"' FROM id), type,area,volte from mobile3;     去掉两边的双引号


### 连接数据库的另外一种方法
mysql --user=root --password=1234 db_springboot_mobile -A   连接数据库的另外一种方法
mysql的语句分隔符(; \g \G)
mysql --user=root --password=1234 db_springboot_mobile -A  < sss.sql > out.txt  执行脚本    将结果输出到out.txt(是带列名的)
mysql -u root -p1234


### mysql profile
    set profiling=1;
    show profiles ; 查看之前执行的语句
    show profile;    查看最近一条语句的详细信息
    show variables like '%prof%';
    set profiling_history_size=15;  默认是15条
    select @@profiling;      查看某个参数值
    show profile for query 2;     查看某个序号的语句  性能分析
    show profile cpu,swaps  for query 2;查看其他性能指标
