### mysql查看数据库状态
    mysqladmin -uroot -p1234 extended-status ;   # 显示数据库状态
    mysqladmin -uroot -p1234 flush-hosts ; #清空错误连接数    在mysql命令中,是flush hosts;

### 短索引例子:
    explain SELECT count(1) from mobile8; --
    create index idx_sbt3_c on mobile8(id(1));  -- 创建短索引
    select count(1) from mobile8 ;  --  600万数据40多秒   直接用主键是260多秒


### rolluup 对分组的数据统计之后,再进行求和.
    select username,sum(deal_number),count(1) from user10 group by username with rollup ;

### group_conat设置
    SET  group_concat_max_len=102400;  -- group_conat默认是1024
    SET  group_concat_max_len=-1;  如果要最大值,那么就设置为-1

### 当月1号 ,当年1号
    -- 月
    DATE_ADD(curdate(),interval -day(curdate())+1 day)
    -- 年
    DATE_SUB(CURDATE(),INTERVAL dayofyear(now())-1 DAY)

### 查看某个表是否存在某个字段:
describe user10 username;  如果没有返回记录,就是没有这个字段
