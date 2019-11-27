### diff  

    diff命令比较文本：  diff -c a.txt b.txt     不同的行首会加！
    diff a.txt b.txt -y   并排显示结果, |表示结果不同  <表示左边比右边少   >表示右边比左边多

### vimdiff  

    vimdiff a.txt b.txt; #左右分屏
    vimdiff a.txt b.txt -o; #上下分屏
    ]c; #跳到上一个不同
    [c; #跳到下一个不同
    ctrl+ww; #左右切换
    :diffu     #手动的刷新比较
    do  #把不同复制到本文件
    dp  #把不同复制到另外文件

### comm  

    comm a.txt b.txt        comm命令必须要先排序
    comm -1 a.txt b.txt     -1：不显示在第一个文件出现的内容；
    comm -2 a.txt b.txt     -2：不显示在第二个文件中出现的内容；
    comm -3 a.txt b.txt     -3：不显示同时在两个文件中都出现的内容。


### tar  

    tar cvf a.txt.rar a.txt      压缩，注意第一个是rar，             -v verbose    -f是file   无论如何都带上

    tar xvf a.txt.rar          vf(v是查看过程，f是指定文件)  如果是gz格式就用z,否则不加
    tar xvf a.txt.rar  -C zzz     C是解压到某个目录
    tar cvf a.txt.rar a.txt b.txt c.txt    压缩多个文件
    tar tvf a.txt.tar        查看压缩包内容    -t
    tar uvf a.txt.tar b.txt   追加内容      -u   追加压缩包内容
    tar -vf a.txt.tar --delete b.txt   删除某文件   -d是diff，所以只能用--delete了

### telnet的4步操作：  

    telnet localhost 8080; #一定要有端口  
    提示：Escape character is '^]'.    意思是 输入ctrl+] 可以唤起telnet的命令行   
    输入 ?  
    输入quit   


### 配置zookeeper环境变量：  

    export ZOOKEEPER_HOME=/root/zookeeper-3.3.6
    export PATH=$ZOOKEEPER_HOME/bin:$PATH
    然后 source /etc/profile     生效文件


### 报错：Starting zookeeper ... ./zkServer.sh: line 103: /root/zookeeper-3.3.6/data/zookeeper_server.pid: No such file or directory   
FAILED TO WRITE PID             是因为datadir没有配置对 找不到文件造成的

### uptime查看系统负载：   
uptime      后面3个参数是统计最近1，5，15分钟的系统平均负载  

### linux查看date的详细用法: info coreutils 'date invocation'  

    date "+%Y-%m-%d %H:%M:%S"  格式化日期，注意前面必须有+号
    date用法:  -d 是--date=String的意思  后面跟描述时间的字符串
    支持的格式有: 年月日  月日  日期之间一定要有分隔符,否则会认为是时间
    date -d '2018'   注意这不是2018年,因为这是表示时间的  所以是20:18
    date -d '2018-11-19'  年-月-日 时分秒默认是00:00:00
    date -d '11-19'   月-日   年默认是今年
    date -d 'day' 不写数字,默认是一天
    date -d '1 day'  一天之后
    date -d '-1 day'  #一天之前
    date -d 'yesterday' 昨天
    date -d 'tomorrow' 明天
    date -d 'month'  一个月
    date -d和 + 的位置可以互换的  也就是前后并没有关系

    date --date 'yesterday'  昨天
    date --date 'today'   今天
    date --date 'tomorrow'    明天
    echo `date -d "yesterday" +%Y-%m-%d`  获取昨天的日期


### shell脚本实现date求上月相同日期:
#!/bin/bash
function get_lastmonth_date(){
    local date=$1;
    local month=${date:5:2};
    echo "传入的日期是: " $date;
    local lastmonth_date=`date -d "$date -1 month" "+%Y-%m-%d"`;
    local lastmonth_month=${lastmonth_date:5:2};
    echo "上个月日期是: " $lastmonth_date;
    while(( $lastmonth_month >= $month && ${lastmonth_date:0:4} == ${date:0:4}))   # 如果上月>=当年前月,   年相等是考虑到2018-01-31这样上月跨年的情况,因为1月和12月都是31天,跨年其实不用考虑
    do
        lastmonth_date=`date -d "$lastmonth_date -1 day" "+%Y-%m-%d"`;
        lastmonth_month=${lastmonth_date:5:2};
        echo "上个月的日期减去一天,为: "  $lastmonth_date;
    done
    echo "最终上个月日期是: "  $lastmonth_date;
    lastmonth_date_result=$lastmonth_date;  #全局变量, 调用完函数,需要立刻获取$result_date值,因为下次调用会改变他的值
    return 1;
}
get_lastmonth_date 2018-03-31;
echo $lastmonth_date_result;
