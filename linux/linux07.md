### 调用其他shell的脚本:  

    sh ./date3.sh   #
    exec ./date3.sh   #
    source ./date3.sh   #父shell中的函数和变量会被子shell集成

### date "+%j"    

    如果是连续的不用加双引号   但是如果有其他符号 会认为是多参,所以最好加双引号(单引号也一样)
    date +'%Y-%m-%d %H:%M:%S'  标准格式化

### manpath  查看man命令的位置

### wget  

    wget www.baidu.com    下载命令，这样就会下载到index.html
    wget -c www.baidu.com        -c是断点续传，不会重复下载  只对ftp和支持range的http服务有效
    wget www.baidu.com  -O ./index2.html        -O  --output-document=file
    wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo    -O如果在最前面，那么第一个参数为下载到的文件
    wget  -P /root/downloads www.baidu.com  #  下载到某个目录

### linux的5种常见状态：  

    R（运行）：进程正在运行或在运行队列中等待。
    S（中断）：进程处于休眠中，当某个条件形成后或者接收到信号时，则脱离该   状态。
    D（不可中断）：进程不响应系统异步信号，即便用kill命令也不能将其中断。
    Z（僵死）：进程已经终止，但进程描述符依然存在, 直到父进程调用wait4()系统函数后将进程释放。
    T（停止）：进程收到停止信号后停止运行。

### ps的标题头例子：  
    USER	PID	%CPU	%MEM	VSZ	RSS	TTY	STAT	START	TIME	COMMAND
    进程的所有者	进程ID号	运算器占用率	内存占用率	虚拟内存使用量(单位是KB)	占用的固定内存量(单位是KB)	所在终端	进程状态	被启动的时间	实际使用CPU的时间	命令名称与参数
    root	1	0.0	0.4	53684	7628	?	Ss	07:22	0:02	/usr/lib/systemd/systemd

### top和pid  

    top   列出正在执行的进程的内容的占用情况，第一个字段是pid   每2秒执行一次
    top   状态下按shift+m，切换到按照内存排序    默认是根据cpu排序的
    pidof mysqld       pidof 根据进程名来获取，pid,可以有多个pid，例如pidof java
    pid是什么:  processId 进程id

### pid找进程的路径   
ls -l /proc/116792/exe       

### 单引号和双引号：   
aaa=111; echo '$aaa'; echo "$aaa";      单引号中不解析$,是单纯的字符串。   双引号中可以解析$变量


### linux10个重要的环境变量:  

    变量名称	作用
    HOME	用户的主目录（即家目录）
    SHELL	用户在使用的Shell解释器名称
    HISTSIZE	输出的历史命令记录条数
    HISTFILESIZE	保存的历史命令记录条数
    MAIL	邮件保存路径
    LANG	系统语言、语系名称
    RANDOM	生成一个随机数字    #如  echo $RANDOM
    PS1	Bash解释器的提示符
    PATH	定义解释器搜索用户执行命令的路径
    EDITOR	用户默认的文本编辑器

### bash脚本赋值语句  变量和=  不能有空格    

    例如 arr=(111 222)是对的  arr =(111 222)会报错 ( syntax error near unexpected token `(' ) ,这是因为  如果有空格,会当作是2个命令
