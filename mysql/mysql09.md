### mysql查询主外键关系:
    SELECT C.TABLE_SCHEMA            拥有者,
              C.REFERENCED_TABLE_NAME  父表名称 ,
              C.REFERENCED_COLUMN_NAME 父表字段 ,
              C.TABLE_NAME             子表名称,
              C.COLUMN_NAME            子表字段,
              C.CONSTRAINT_NAME        约束名,
              T.TABLE_COMMENT          表注释,
              R.UPDATE_RULE            约束更新规则,
              R.DELETE_RULE            约束删除规则
         FROM INFORMATION_SCHEMA.KEY_COLUMN_USAGE C
         JOIN INFORMATION_SCHEMA. TABLES T
           ON T.TABLE_NAME = C.TABLE_NAME
         JOIN INFORMATION_SCHEMA.REFERENTIAL_CONSTRAINTS R
           ON R.TABLE_NAME = C.TABLE_NAME
          AND R.CONSTRAINT_NAME = C.CONSTRAINT_NAME
          AND R.REFERENCED_TABLE_NAME = C.REFERENCED_TABLE_NAME
         WHERE C.REFERENCED_TABLE_NAME IS NOT NULL ;

### mysqluuid更新策略:
插入更新策略,只会插入更新,但是不会删除之前的数据.  
解决办法: 添加一个uuid字段,任务执行完毕之后,delete from TABLE_NAME where uuid !='';

### 多条件关联:
不要用on了   用where 就好了

### mysql没有insert overwrite table语法

### 开窗函数的排序函数:  
    很多函数都是有参数的,如果是
    over()可以没有任何内容,表示对所有内容进行排序
    rank()  非连续排序(例如并列第一,后面只能跟第三了)   1,1,2,3,4
    dense_rank()  密集排序(连续排序),有多个并列值,后面依然一样.    1,1,3
    row_number()  组内记录的行号,可以用于分页   就是1,2,3,4,5
    ntile()  将所有结果尽量平均分配到为长度为n的集合的每个区间中
    lead()  下几个
    lag()  前几个
    first_value()  当前组第一个值
    last_value()  当前组最后一个值

### 自定义函数while:
    create function udf_while()
    returns int
    begin
        declare i int;
        set i=0;
        while i<5 do
        set i=i+1;
        end while;
        return i;
    end;

### 自定义函数if:
    create function udf_if(a int)
    returns int
    BEGIN
      if a=0 then return 0;
      end if;
      return 2;
    end;

### 自定义函数case:
    create function udf_case(a int)
    returns int
    BEGIN
        case
        when a=0 then return 0;
        when a=1 then return 1;
        else return 2;
        end case;
    end;


### 存储过程定义减法函数:
    DELIMITER //
    create function sub2(a int ,b int )
    returns int
    BEGIN
    DECLARE c int DEFAULT 10;
    RETURN (a-b+c);
    END//

    然后:    select sub2(3,2) \\     #因为已经delimiter \\了,所以要用\\表示分号

### 存储过程set 设置变量的值,必须先用declare声明.
set @aaa=1;   #加@表示设置全局变量

### mysql开启自动补全
rehash       #开启自动补全
