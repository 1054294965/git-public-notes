###  命令在哪个目录下：  

    /bin(也可以是/usr/bin)， /usr/bin
    which 和whereis ： which只用于查看命令   whereis范围稍微大一些，除了sh命令后，还可以搜索到man说明文档
    whatis  find       查看命令的作用简介     whatis是查找文档的描述
    updatedb        更新linux数据库，配合locate使用
    updatedb -U /crmdata/crm-web/tomcat-crm/logs  更新指定位置的数据库
    updatedb -U /crmdata/crm-web/tomcat-crm/logs -v      ---    -v显示更新的详细情况, 要在最后

    locate awk.txt  查找awk.txt文件
    locate awk.txt -n 10 或者  locate -n 10 awk.txt    locate显示符合条件的前10条记录
    locate -r ".*/a.txt$"   -r表示正则，表达式加不加双引号都可      .*/a.txt  表示任意目录下的a.txt   ^a.txt$不行  因为是全路径（如:/asdf/asdfas/a.txt）
    locate bash_profile  没有任何结果，也就是说，不是所有的文件都可以用locate找到。      全局配置文件是/etc/profile
    locate是比find -name高效的多的一个命令，原因是它不直接搜索目录，而是搜索一个数据库。

###  type  

    type cd      自带命令
    type grep     外部命令
    type -p vim   结果为/usr/bin/vim，其实相当于which了

###  rev  

    echo "abc" |rev  翻转字符串
    rev a.txt     文件中所有行都翻转
    rev   #输入rev, 提示输入string,  回车后就是反转的字符

###  用户和目录相关   

    pwd    显示当前目录
    pwd -P  显示当前实际目录,例如/var/mail下执行  显示/var/spool/mail
    last   最近登陆次数
    lastlog    登陆日志
    lastb   登陆失败记录
    who  正在登陆
    who am i    和whoami    whoami  是只显示用户名   who am i 是详细信息
    w    登陆中的用户       推荐，会显示登陆的ip地址

###  hostname  

    hostname   是查看，后面带有内容是修改
    hostname asdfasdf    修改主机名
    hostname -i      名称改为'-i'  -不是参数前缀
    hostname 改名之后不生效??  新开一个窗口就生效了

    永久修改hostname:
    hostname -i    #查看ip
    vim /etc/hostname   改为  主机名
    vim /etc/hosts       添加  192.169.0.1 主机名
    vim /etc/sysconfig/network    HOSTNAME=主机名

###   ascii码  
    man ascii  查看所有的ascii码  (这个命令有点慢呀)
    echo 97 |awk '{printf("%c,$1)}'     #输出a   注意要用printf,  print是不行的
    printf "%d\n" "'a"   # ascii码和字符互相转换  输出97
    printf "\x`printf "%x" 97`\n"   # 97转换为a


### dd命令生成文件  

    dd if=/dev/zero of=sun.txt bs=1M count=10       dd命令生成文件,if 是输入，of是输出， bs(bytes)是大小  count是块数   文件总大小是   bs*count
