### 统计行数：  

    wc -l catalina.out    
    或者  cat catalina.out | wc -l   
    或者 wc- l < a.txt  

### more中的按键：  
enter下一行，空格  翻页，b 上翻，h 显示帮助信息，q 退出  


### history  

    最近100命令记录  history 100  直接数字，不用'-'，也不用-n
    !1226      ！+数字表示  调用history中对应的命令
    history中  ctrl+r    然后输入命令中的任意字符串，继续按ctrl+r会在所有匹配记录中切换

    export HISTTIMEFORMAT="%F %T `whoami` "         history 中使用时间戳
    echo 'export HISTTIMEFORMAT="%F %T `whoami` "' >> /etc/profile          history中使用时间戳(永久)

    ctrl+g  退出历史记录
    ctrl+g  显示文件名称,行数,当前位置比例
    :args 查看文件名
    ctrl+p  上一条历史
    ctrl+n  下一条历史
    ctrl+o  同于回车
    ctrl+m  同于回车
    ctrl+y  粘贴或者复制上一次删除的命令
    alt+p
    alt+>
    !-n    前n条命令, !-1是上一条
    !!      上一条命令
    !* 或者alt+.号  上条命令的所有参数
    !#   引用目前输入的字符串     如  echo 1 !#
    history |tail -n 10   最后的10条命令


### cp  

    cp a.txt !#:1.bak   --- cp a.txt a.txt.bak      !#:n   n是命令的第几个 引用当前的命令行
    cp a.txt !#:0.bak   --- cp a.txt cp.txt
    cp -n a.txt.bak a.txt       -n不提示（但是不会覆盖）

### cp直接覆盖   

    cp -rf a.txt.bak a.txt     cp直接覆盖
    vim ~/.bashrc;
    注释掉cp这一行。
    source ~/.bashrc; #生效


### tr是单字符逐个操作，所以不存在正则什么的:  

    cat a.txt | tr [a-z] [A-Z]  或者  echo "abc" | tr [:lower:] [:upper:] 注意这个不修改原始文件  小写-->大写
    cat a.txt | tr [A-Z] [a-z]  或者 echo  "ABC" | tr [:upper:] [:lower:]  大写-->小写
    echo "abc1234" |tr -d "0-9" 或者 echo "afbc13432" |tr -d [:digit:]    这里不能使用中括号
    cat a.txt | tr '\t' ' '     \t制表符
    echo "thissss is      a text linnnnnnne." | tr -s ' sn'    -squeeze-repeats压缩重复为单个
    echo aa.,a 1 b#$bb 2 c*/cc 3 ddd 4 | tr -d -c '0-9 \n'      删除补集中的所有字符 -c是补集的意思
    echo 1 2 3 4 5 6 7 8 9 | xargs -n1 | echo $[ $(tr '\n' '+') 0 ]    tr数字相加
    cat file | tr -s "\r" "\n" > new_file  或    cat file | tr -d "\r" > new_file    删除^M字符
    -t ???

    cat和tac: tac是反向显示，相当于行数对调了。

    tr可以使用的字符类:
    [:alnum:]：字母和数字
    [:alpha:]：字母
    [:cntrl:]：控制（非打印）字符
    [:digit:]：数字
    [:graph:]：图形字符
    [:lower:]：小写字母
    [:print:]：可打印字符
    [:punct:]：标点符号
    [:space:]：空白字符
    [:upper:]：大写字母
    [:xdigit:]：十六进制字符
    uid和gid:  userId和groupId
