### su和sudo：   
su是切换用户  sudo是以其他身份来执行命令

### chmod和chown：   

    chmod 是设置文件权限  chown是改变文件所属的用户和组      chmod 是change modify,chown 是change owner的意思
    chmod u+x a.txt  给user添加执行权限
    chmod u-x a.txt  给user去掉执行权限
    chmod +x a.txt  给user,group,others添加执行权限
    chmod 644 a.txt   设置a.txt权限为644
    chmod u=rwx a.txt 使用等号设置权限
    chmod a+x a.txt 所有都添加x权限(a=u+g+o)
    chmod u+x,g+x a.txt    多个权限用都好分隔

    umask     查看默认的权限   文件的x权限默认丢弃
    umask -S    查看默认的权限(字符形式)

### linux为什么安全??  

    新建的文件权限是rw-r--r--(644),都是没有执行权限的,所以病毒没有生存空间。
    644和755???
    644用户rw，其他r(一般是新建文件的状态)。755 用户可rwx 其他用户rw.


### sort   

    cat a.txt |cat   管道原样输出
    cat b.txt | sort   通过管道排序
    sort a.txt  对文件内容进行排序
    sort -u a.txt  或者uniq a.txt           --- 排序并去重
    sort -n a.txt 根据数字来排序(默认是按照字符串排序的)     如 100 2000 30  按照大小和按照string排序不一样
    sort -r a.txt 倒序排序
    ls -l |sort -k4   -k是--key根据第几列进行排序
    sort -k2 -u mail-list       # sort 根据某一列去重

    sort -t: a.txt   -t指定分隔符      如111:aaa  如果不指定：  那么会认为只有一列
    cat a.txt | sort -k 6,6  -k9,9r    第6列和第9列排序，r在后面表示只对9列进行反转
    cat a.txt | sort -k 6.1,6.2  -k9,9r  6列第一个字段进行排序，注意不要写6.1，6.1这个查询结果不正确

### uniq  

    uniq -c a.txt     count统计 统计每种各有多少行
    uniq a.txt -c |grep ddd    统计某行的行数
    uniq -d a.txt     repeat  只显示重复行
    uniq -u a.txt     unique 只显示不重复的行

    cat a b | sort| uniq> c           # c is a union b 并集
    cat a b | sort| uniq -d > c           # c is a intersect b 交集
    cat a b b | sort| uniq -u > c           # c is set difference a - b 差集
    cat a.txt b.txt b.txt | sort| uniq -u > c.txt

### getconf   

    getconf PAGESIZE     获取block的大小，一般是4096
    getconf -a        获取所有的变量
    getconf -a ./     path参数可选
