### 查看某个数据库的改动时间：
    SELECT
    	TABLE_NAME,
    	UPDATE_TIME
    FROM
    	INFORMATION_SCHEMA. TABLES
    WHERE
    	TABLE_SCHEMA = '' order by update_time;

### mysql命令行：
    help      #客户端命令
    help contents   #服务端命令
    \g  #执行语句
    \s  #查看服务器状态   ip、当前用户等
    \! ls 　　#　 \! 后面跟shell命令
    \r   #重新连接 connection id会改变

### explain分析语句
    explain SELECT id FROM `user` limit 1; -- 索引
    explain SELECT type FROM `mobile3` limit 1; -- 不使用索引
      -- 查看性能
    analyze table mobile3; -- 分析表
    check table mobile3; -- 检查表

### mysql是否使用缓存：
    show variables like '%query_cache%'; -- 是否开启缓存
    show status like 'Qcache%';
    Select password from user where id='1';
    Select password from user where id='1';
    show status like 'Qcache%';  -- 按道理应该有缓存数  实测没有


### mysql创建用户并授权：
    mysql --password; #默认是root
    create user 'springuser'@'localhost' identified by 'ThePassword'; -- Creates the user
    grant all on db_example.* to 'springuser'@'localhost'; -- 给db_example库授权
    grant all on *.* to 'springuser'@'localhost'; -- 授权为所有库


    create user aaa;
    create user aaa@localhost; #也是可以的
    create user aaa@localhost identified by '1234';
    drop user aaa;
    drop user aaa@localhost;

    create user ggg@localhost identified by '1234';

    create user ggg identified by '1234';
    grant use,select on *.* to ggg@localhost;

    rename user aaa  to  bbb  #重命名
    rename user aaa@localhost to  bbb@localhost #

    set password=password('1234');
    set password for aaa=password('1234');
    set password for bbb@localhost=password('1234')

    set password for bbb=password('1234');
    grant all privileges on *.* to aaa@local;    #privileges  可以不写的
    grant all privileges on *.* to bbb@localhost identified by "1234" ;

    一句可以分解为3句：
    create user ddd@localhost;
    set password for ddd@localhost=password('1234');
    grant all privileges on *.* to ddd@localhost;

    grant select on *.* to ggg@localhost;  # 查询权限
    grant insert on *.* to ggg@localhost;  # 插入权限


    revoke insert on *.* from ggg@localhost;  #移除insert权限
    revoke all privileges on *.* from ggg@localhost;  #溢出所有权限
    grant和revoke??  grant是on库表to用户  revoke是on库表from用户

    revoke privileges on *.* from ddd@localhost;  #revoke是撤销权限


    SELECT DISTINCT CONCAT('User: ''',user,'''@''',host,''';') AS query FROM mysql.user;   #查看所有用户      不能直接user，
    select host,user from mysql.user; #查看所有用户

    create user eee;
    grant all privileges on test.* to eee@localhost identified by "1234" ;  #只开通某个库
    create user fff;
    grant all privileges on test.city to fff@localhost identified by "1234" ;  #只开通某个表的权限
