### grep
```
ID=`ps -ef | grep "$NAME" | grep -v "$0" | grep -v "grep" | awk '{print $2}'`
fgrep: 就是不支持RE(正则表达式)
cat a.txt | fgrep "\w"   #这样不行, 应该用awk "zhangsan" a.txt;
cat a.txt | egrep "zh?*"
=============================================
杀掉grep： ps -aux |grep grep ; 然后kill -9 端口
ps -aux |grep mysqld
cat a.txt | grep -v aaa       找到不包含aaa的内容
cat a.txt | grep -n aaaa     显示匹配的行号        -n 是单参，后面不用跟任何参数
cat a.txt | grep -c aaaa     -c表示统计行数
echo aaabbb |grep -i AAA     忽略大小写
echo abcddf |grep -o 'dd'    只获取匹配，不获取整行
grep -q asdfasdf a.txt;echo $?;    0表示成功  1表示失败
grep "a\+"  a.txt       正则转义(grep中的限制符等都需要转义)
grep -A 3 aaa a.txt   匹配行和之后的n行都会显示  a可以小写  A是after
grep -B 3 aaa a.txt   匹配行和之前的n行都会显示  b可以小写  B是before
grep -C 2 aaa a.txt   匹配行和前后各n行显示    c可以小写
grep -w "bcd" a.txt  或者 grep "\bbcd\b" a.txt    只匹配单词    \b是单词分界符,  左斜杠也行，区分是否是单词，看是否是在[0-9a-zA-Z]
grep -r "aaa" *      递归搜索,否则忽略文件夹
grep "aaa" *.zzz     在后缀文件中搜索
grep "bcd\|efg" a.txt   搜索多个单词，注意转义\|
grep -l bcd *    只显示匹配文件的文件名，不加-l只是显示匹配的内容(注: 是显示的时候只显示文件名,过滤还是根据内容过滤)
color bbb a.txt  匹配结果彩色显示
grep "aaa\|bbb" a.txt   或者 grep aaa a.txt |grep bbb b.txt    grep多条件查询，注意|需要转义
netstat -nltp |grep "8080.*java"     获取端口和java
grep -R 'adsfadsfa' ./    搜索当前目录下所有的文件，查找字符串
man ls |grep "list"  -c    -c 有多少匹配的行
man ls |grep -E "list|file" 匹配多个需要-E，或者使用egrep
grep -r "aaa" ./     -r在某个目录下查找
grep -r "aaa"       -r在某个目录下查找，不写路径默认是当前目录
```

### grep
grep "hello" --include=*.{sh} -r .
grep "a*" --include=*.{txt} -r .
egrep "aaaa" a.txt b.txt     多文件查找，空格分开文件
egrep "aaaa" *     表示当前目录下的所有文件来查找
egrep "aaaa" ./*     表示当前目录下的所有文件来查找

### 查看所有不是我运行的程序:   
ps aux | grep -v `whoami`  

### 查看最占用时间的10个程序：   
ps aux--sort=-%cpu | grep -m 11 -v `whoami`  

### ~和/区别：  

    /是根目录   ~或者~/是用户目录   如果是root用户，那么是/root   如果是其他用户，要看用户的目录
    cd -     切换到上个目录
    cd ~chushiyun  切换到其他用户的家目录

### pushd和popd   

    pushd /etc   pushd压入一个目录，并切换到该目录，再次pushd，即可在所有压入的目录进行切换  
    popd  会弹出最顶层的目录，并打印出来  
    dirs -v  #查看压入的目录,带有序号
    dirs #

### perl  

    perl -i -pe 's/Windows/Linux/;' a.txt  替换a.txt中的windows为linux
    perl -i -pe 's/Windows/Linux/;' a.txt b.txt  替换a.txt中的windows为linux     ---多文件可以用空格分隔，或者用通配符aaaa*.txt文件
    find . -name '*.txt' -print | xargs perl -pi -e's/Windows/Linux/ig' *.txt     替换当前目录以及下层所有目录
    find -type f -name '*.txt' -print0 | xargs --null perl -pi -e 's/Windows/Linux/'    只作用于普通文件


### 系统  

    cat /etc/redhat-release  查看系统版本
    cat /etc/issue
    cat /etc/issue.net
    uname -a     查看系统内核和系统版本等信息
    uname  `查看系统内核和系统版本等信息`


### head和tail  

    head -n -3 a.txt         head只有-     -是末尾   从开头，到末尾n       不包括n
    tail -n +3 a.txt         tail只有+    +是开头   从开头n,到结尾
    head和tail 如果带有+ -号，          tail只有+

### ln   

    ln a.txt a.lnk   
    创建硬连接,如果存在硬连接,那么即使删除源文件,也是可以访问的
    ln -s a.txt a.lnk2      -s  symbolic(符号连接,就是软连接)

### tree   

    tree -L 1   #展示一级目录
    tree -L -a  # -a展示所有   太多了不实用(非常推荐使用-L)
    tree -L -d  # -d只显示目录的内容
