### 阿里云  
阿里云设置远程登录---更多---重置实例密码---就可以远程登录了  
阿里云创建安全组:  
控制台---网络与安全---安全组---这里就是安全组的列表了  

阿里账号：chushiyun001
阿里密码：al通用


### ssl key生成：  

    -certreq            生成证书请求
    -changealias        更改条目的别名
    -delete             删除条目
    -exportcert         导出证书
    -genkeypair         生成密钥对
    -genseckey          生成密钥
    -gencert            根据证书请求生成证书
    -importcert         导入证书或证书链
    -importpass         导入口令
    -importkeystore     从其他密钥库导入一个或所有条目
    -keypasswd          更改条目的密钥口令
    -list               列出密钥库中的条目
    -printcert          打印证书内容
    -printcertreq       打印证书请求的内容
    -printcrl           打印 CRL 文件的内容
    -storepasswd        更改密钥库的存储口令


### 查看程序：   

    ps -aux |grep dubbo
    ps -lu root  查看某个 用户的进程
    ps aux | sort -k4nr | head -n 10    内存前10     -k 第几列   n 按照数值大小(不加-n的话 8会大于111显然不对)   r反序
    ps aux | sort -k3nr | head -n 10    cpu前10
    sort多列排序:
    ll | sort -k5n -k8n ;    #现根据敌5列size排序,再根据第8列时分排序   n最好写在后面  前面先写k

    ls -l | awk '{print $5}' | sed -n '2p'

    4列是内存 3列是cpu

### ps列的含义  

    1）USER: 行程拥有者
    2）PID: 进程的ID
    3）%CPU: 占用的 CPU 使用率
    4）%MEM: 占用的记忆体使用率
    5）VSZ: 占用的虚拟记忆体大小
    6）RSS: 占用的记忆体大小
    7）TTY: 终端的次要装置号码 (minor device number of tty)
    8）STAT: 该行程的状态:
            D: 不可中断的静止
            R: 正在执行中
            S: 静止状态
            T: 暂停执行
            Z: 不存在但暂时无法消除
            W: 没有足够的记忆体分页可分配
            <: 高优先序的行程
            N: 低优先序的行程
            L: 有记忆体分页分配并锁在记忆体内
    9）START: 行程开始时间
    10）TIME: 执行的时间
    11）COMMAND:所执行的指令

### cat,more,less??  

    cat一次显示全部  
    more显示一屏，空格换屏,退出      more或者less中输入v进入编辑模式       less一定可以进入vi模式，more小文件直接读取完毕了  
    less显示一屏，支持pageup，pagedown，冒号下输入q是退出  
    less标记   ma 表示用a字母标记     用的时候输入'a 调用即可  
    look a a.txt    以字母a开头的行  
    look -t a a.txt    以字母a结尾的行  

### 转换编码   
iconv -f gb2312 -t utf-8 a.txt -o b.txt   
或者  iconv -f gb2312 -t utf-8 a.txt >> b.txt      -f from -t to  -o  output

### linux清空文件  

    cat /dev/null >a2.txt   
    echo "" > a2.txt    清空文件
    > a2.txt      清空文件

### more：  
空格  向下滚屏  
ctrl+b 向上滚屏  

### java环境变量：
用户目录下   添加.bash_profile环境变量  
profile文件中添加 export  aaa=111;然后  source 该profile即可。  
或者执行export aaa=111;  直接执行表示添加到环境变量中  
export用法    export key=value;  


### sudo命令的坑：sudo后面不要使用*通配符， 关闭tomcat不要用shutdown，因为如果有守护进程，那么shutdown杀不掉    
