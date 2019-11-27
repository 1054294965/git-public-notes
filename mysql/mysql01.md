### mysql报错(the server has gone away)
    执行2句话即可：
    show global variables like 'max_allowed_packet';
    set global max_allowed_packet=268435456;

### mysql手册
    help Account Management
    help Administration
    help Compound Statements
    help Data Definition
    help Data Manipulation
    help Data Types
    help Functions
    help Functions and Modifiers for Use with GROUP BY
    help Geographic Features
    help Help Metadata
    help Language Structure
    help Plugins
    help Procedures
    help Table Maintenance
    help Transactions
    help User-Defined Functions
    help Utility

### mysql
help date and time functions      时间函数  日期函数
help '%concat%';  #help 可以使用通配符

### 天数：  
date_add和add_date是一样的
SELECT DATE_ADD('2008-01-02', INTERVAL 31 DAY) '2008-02-02'; # 整数表示之后天数
SELECT DATE_ADD('2008-01-02', INTERVAL -31 DAY) '2008-02-02'; # 负数表示之后天数
时间: 最多只能加天
SELECT ADDTIME('2007-12-31 23:59:59', '1 1:1:1') ;  #时分秒
SELECT ADDTIME('2007-12-31 01:01:01', '0:0:1') ;  # 只要秒

### 当前时间:
    select CURDATE(); 和select CURRENT_DATE(); 一样  # 当前天
    select CURTIME(); 和select CURRENT_TIME(); 一样  # 只是时间
    select CURRENT_TIMESTAMP();  #整个时间戳

### utc时间
    utc 时间比+时区时间  =当前时间  例如utc是2点 本地就是10点(8区)
    select UNIX_TIMESTAMP(); #
    select UTC_DATE(); #
    select UTC_TIME();
    select UTC_TIMESTAMP();
    例如:
    utc +8  =utc8
    要3:55跑   那么coordinator时间设置为每日19:55

    utc=utc8-8
    utc=3:55-8=  27:55-8=19:55

    我要6:00 那么就是 6-8=30-8=22:00
