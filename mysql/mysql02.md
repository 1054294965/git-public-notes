### mysql
    select coalesce(1,2,null,null);  # 第一个非null字符
    select coalesce(null,2,null,null); #
    select interval(5,1,2,3,7,4);  #返回第一个比5大的数据的位置-1
    select least(3,1,2); #   最小值
    select greatest(2,1,3);  # 最大值

    is null和isNull:       * is null   和isNull(0)
    SELECT 1 IS NULL, 0 IS NULL, NULL IS NULL;    # 0 0 1      是null返回1，否则是0
    SELECT ISNULL(1+1);     #  是null返回1  否则返回0  mysql中没有nvl,所以要用ifnull
    如何过滤掉null,0,''      length(ifnull(member_id,''))> 1   不要写>0  因为0的长度=1


### 分组后取分组内的时间最大值:    
    先根据时间排序,再根据用户分组
    select username,password
    from
    (select * from user10 where length(ifnull(username,''))> 1 order by password desc ) as a
    group by username;

### group_concat用来连接组
```
select *,GROUP_CONCAT(uname,umonth separator ':') from t_access group by uname;   #group_concat用来连接组
```

###mysql操作字符串
    string functions:        substring的下标是从1开始的
    select substring('abcdefg',2); #
    select substring('abcdefg',-2); # 倒数第2个到最后
    select substring('abcdefg',2,3);  #从2开始往后的3个
    select substring('abcdefg',-2,3);  # 倒数从2开始往后的3个

    select substring('abcdefg' from 2);  #from 是上面的繁写形式 意思是一样的
    select substring('abcdefg' from -4 for 2);
    select mid('abcdefg',2,6);   #mid函数 类似java中string  2个坐标之间的内容

    select right('abcdefg',2); # right从右边开始几个字符 和substring -2一样
    select left('abcdefg',2);  #左边开始几个字符
    select trim('   abcdefg   '); # trim 去掉左右空格
    select rtrim('   abcdefg   '); # rtrim去掉空格 rtrim是remove trim
    select ltrim('   abcdefg   '); #  去掉左边的空格
    select reverse('abcdefg'); # reverse 反转

### mysql操作字符串2
    select ucase('abcdefg');
    select lcase('ABCDEF');

    select SUBSTRING_INDEX('ABCDEF');   #实测没有这个函数
    select strcmp('text','text');  # 相同为0
    select strcmp('text','text2');  # -1 左边的参数 和右边的类似
    select strcmp('text2','text'); # 1 所有其他的情况

    select repeat('text',3); #重复
    select replace('www.baidu.com','w','W');  #替换
    select insert('abcdefg',3,4,'www'); #指定位置之间替换为 www
    select insert('abcdefg',-1,4,'www'); # 不替换，找不到-1
    select insert('abcdefg',3,100,'www'); # abwww
    select position('baidu' in 'www.baidu.com'); #下标
    select locate('efg','abcdefg');  # 位置 下标
    select length('text');  #长度
    select OCTET_LENGTH('text');  #和length 一样

    select rpad('baidu',10,'?'); #  向右补充符号到某个长度
    select lpad('baidu',10,'?'); #  向左补充符号到某个长度
    select quote('don\'t!'); #给字符串加引号

### mysql操作字符串
    select concat('aaa','bbb','ccc')   -- 直接连接
    select concat_ws('-','江苏省','南京市','玄武区','徐庄软件园');      -- 以'-'作为分隔符连接
    select regexp_replace('www.tuniu.com','tuniu','jd');  -- 替换
    select repeat('ab',3); -- 重复n次字符串
    select lpad('ab',7,'k'); -- 如果不够长度，用某字符补位到长度(左补位)
    select rpad('ab',7,'k'); -- 如果不够长度，用某字符补位到长度(右补位)
    select trim(' adf bbb  ')
    select to_date('2017-01-16 09:55:54'); -- 字符串转换为日期    mysql是没有这个方法的
    select datediff('2017-01-16', '2017-01-10');  -- 日期差(左-右)
    select date_add('2017-01-10', 7); -- 几天后的日期
    select last_day('2017-01-16 09:55:54');  -- 当前日期  所在月的最后一天
### mysql
SELECT FIELD('fo', 'Hej', 'ej', 'Heja', 'hej', 'foo'); #第一个在后面list中完全相同的坐标值-1
SELECT ELT(1, 'ej', 'Heja', 'hej', 'foo');  #elt是field的补充  获取数组中的某个下标的值
select make_set(4,'a','b',null,'c'); # null不会算在其中 所以认为只有3个值 4是获取不到的
select make_set(1,'a','b',null,'c'); # 集合中的第一个值

### mysql数字函数
```
select rand();  # rand(10)  也是没有用的  照样是0-1的随机数a
select round(rand()*10);  # 0-10的随机整数

select substring(md5(rand()),1,20); #生成随机字符串
select * from user2 order by rand() limit 3;   #获取随机数据
```

### mysql UpdateXML函数：
    用来替换xml内容   第2个是什么情况下替换(中间不能有干扰的标签，如<a><a><a/>,a中间还有a)，第三个是替换成什么,
    SELECT
    UpdateXML('<a><b>ccc</b><d></d></a>', '/a', '<e>fff</e>') AS val1,
    UpdateXML('<a><b>ccc</b><d></d></a>', '/b', '<e>fff</e>') AS val2,
    UpdateXML('<a><b>ccc</b><d></d></a>', '//b', '<e>fff</e>') AS val3,
    UpdateXML('<a><b>ccc</b><d></d></a>', '/a/d', '<e>fff</e>') AS val4,
    UpdateXML('<a><d><b>ccc</b></d></a>', '/a/d', '<e>fff</e>') AS val5
