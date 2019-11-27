### ls多列排序  

    ls -l的6个标题头：3个用户权限  大小  时间  文件名
    ls根据时间排序：  ls -ls  s默认是时间倒序排序
    .: 是什么意思     .是当前目录  冒号就是冒号
    ls -R 查看子目录
    ls -lS  根据大小排序
    ls --sort=time; #时间排序     或者 ls -t
    ls --sort=none;
    ls --sort=version; #
    ls --sort=size; #大小排序    或者  ls -s
    ls --sort=extension; #扩展名排序
    默认是根据name排序的

### ls -a和ls -l的区别：   

    维度不一样  -a是是否显示隐藏文件等   -l是控制多列输出
    ls -lt    根据时间排序
    ls -ln    根据name排序

### ls  

    ls -l | head -10    ls列出前10条
    ls -l /dev/sda*   ls后面的模糊匹配
    ls -l | grep "^-" | wc -l      统计文件数目
    ls -l | grep "^d" | wc -l      统计目录数目
    ls | grep aaa -c       -c是显示数目
    ls | grep -E "awk|a.txt"      -E expression  根据正则来查询,不加 -E 的话表示字符串，加了之后表示是正则
    ls -lSrh   找到最大的文件
    ls -t       -t sort by modify time   根据时间排序
    ls -lr    # -r倒序(reverse)
    ls和ls- l: ls只返回文件名， ls -l返回详细列
    ls -lU       U是不排序
    ls -u    -l（根据name排序，显示access type）  -lt（根据access排序，显示access）  其他情况都是根据access
    ls -ld /root        查看目录的详细信息

### ls括号来执行组合命令   

    (cd ../;ls -l)  括号来执行组合命令
    ls xxx >ls.txt 2>&1     重定向到标准输出,xxx文件不存在是个错误的命令
    这句相当于 ls xxx 1>ls.txt 和2>ls.txt
