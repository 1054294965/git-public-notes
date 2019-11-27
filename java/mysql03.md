### mysql查看
desc crm_log;  或者 describe crm_log;  查看表结构
desc user '%name%';  #查看user表中所有包含name的列
show create table crm_log;   查看建表语句，带注释
show index from mobile;   或者 show index in mobile;  #查看索引(或者show create table也是可以的)
show columns from mobile; 或者show columns in mobile; #查看所有列
show full columns from crm_log;    查看表结构，带注释和auto_increment等

show columns语法:
help show columns;
show columns from user;
show columns from test.user;
show columns from user from test;
show columns from user like '%username%';
show columns from user where field like '%username%';


### mysql导出
    这种导出的效率和create table as select * from user; 差不多
    select * from user into outfile 'c:/fff.txt';  导出查询结果   into outfile      （导出文件）（命令行） 默认在这个目录下 /var/lib/mysql
    load data local infile 'c:/fff.txt' into table user character set utf8;    导入文件（mysql命令行）
    select uid,lid from test into outfile '/tmp/datasets.csv' fields terminated by ',' lines terminated by '\n';  　#指定行列分隔符

    select * from user into outfile './result2.txt' fields terminated by ',' ;

### mysql结果输出到指定文件:
    pager cat > /tmp/test.txt;   #(sql结果不会显示在控制台上了,而是输出到文件)覆盖到test文件   目录最好用tmp,其他目录可能有权限问题
    pager cat >> /tmp/test.txt;  #追加到test文件
    vim /tmp/test.txt; # 查看导出的结果

### mysql导出数据库结构
    导出数据库结构：
    mysqldump -u root -p -d --add-drop-table [databasename]>[database].sql          -d 没有数据 --add-drop-table 在每个create语句之前增加一个drop table

### mysql
    source sss.sql     运行sql文件(在mysql中执行)

    show table status;    查看所有表(schema形式的，可视效果不好)
    show function status like '%sub2%';    #查看所有自定义函数

    show processlist; 显示前100个连接  processlist 中间没有空格
    相当于select * from information_schema.processlist where stage='0';

    show full processlist;  显示所有连接     看哪些语句正在执行,看time即可,如果time很长,表示执行了很长的时间

    show variables;
    show variables like '%charset%';
    show status like 'Threads_connected';   查看所有连接   和show processlist一样
    show status like 'uptime';   工作了多少秒
    system uname; 系统名称   #system 后面跟shell命令   其实就是相当于uname

    show variables like '%profiling%';   是否开启性能显示
    set profiling=1; 是开启
    show variables like 'datadir';     数据库文件位置

    mysql不支持top的语法，要用limit。
### mysql报错：order by
    报错解决：
    如果有分页的话，order by应该在分
    报错:Can't create/write to file '/user.txt' (Errcode: 13)  默认是mysql用户，不能向其他目录写文件

### 查询出哪个id数据条数最多
    select g.g1,g.g2 from (select count(member_id) as g1,max(member_id) as g2 from month_sales group by member_id order by g1 desc limit 100  ) as g


### mysql乱码处理
    1、jdbc连接中添加useUnicode=true&amp;characterEncoding=UTF-8
    2、show variables like 'character_set%';
    发现character_set_server 是latin1。
    打开linux中/etc/my.cnf文件(这是mysql的配置文件)
    进行如下配置：
    [mysql]中添加
    default-character-set=utf8
    [mysqld]中添加
    character-set-server=utf8
    然后运行service mysqld restart(重启使配置生效)
    show variables like 'character_set%';再次查看发现character_set_server是utf8了
    插入数据，发现不乱码了。

### 导入很多数据的时候报错: Lost connection to MySQL server during query    
    导入大量的数据,如果再执行其他的查询语句会出现这个问题  
    show variables like '%max_allowed_packet%'    #查看是否太小  
    set global max_allowed_packet=2*1000*1000*1000   #这个数值还可以更大 最大是  1073741824  
    systemctl restart mariadb;  
    show variables like '%max_allowed_packet%';   #如果数值大了 表示设置生效  
    再次导入可以导入了.   如果文件还是太大,先分割成小文件再说.  
    set  max_allowed_packet=2*1000*1000*1000
