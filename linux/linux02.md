### su命令  

    su chushiyun;  #切换到  chushiyun用户
    su - chushiyun;   #切换到  chushiyun用户, - 表示连环境变量也切换过来
    su ;  # 没有用户表示切换到root用户
    su - ;  #没有用户 表示切换到root用户 -表示连环境变量也切换

### su和sudo：  
sudo用其他账号来执行命令,su是切换到其他账户，必须输入账号密码

### 查看当前用户               
id命令     其实shell  @前面就可以看，如root@hostname


### linux报错：is not in the sudoers file   

    因为没有在/etc/sudoers文件中添加.  如果添加了,那么该用户只有第一次执行sudo的时候,需要输出密码  
    输入：visudo 打开sudo配置文件  
    添加2行：  
    [[test]] ALL=(ALL) ALL  
    test2 ALL=(ALL) ALL  


### ls排序   

    默认是根据filename排序  
    根据时间降序排序  ls -lt     
    如果要反序，ls -lrt  


### cat命令   

    cat file |tail -n 100       显示最后100行           head -n 符号只有-号
    cat file |tail -n +100      显示100行之后的      tail -n 符号只有+号
    cat file |head -n 200 | tail -n +100        显示100行-200行(tail + 确定首行，head -n 确定尾行)      head和tail的先后顺序  会影响代码

    查看最后3行到最后5行:
    cat a.txt |tail -n  5| head -n -2
    cut -c 2-10 a.txt >c.txt  输出列数到列数
    cat a.txt |cut -b 1-3    1-3字节
    cat a.txt |cut -b 1-3，5-7    多段字节逗号分隔
    cat a.txt |cut -c 1-3    c表示字符
    cat a.txt |cut -d ":" -f 2   -d分隔符，-f取某段(f是fields的意思)
    cat a.txt |cut -d ":" -f 2,4   某段之间，会连分隔符一块显示
    cut -d :  -f 1,2< /root/a.txt;  多列 用-f 2,3这样的形式显示


### du和df   

    df是查看磁盘占用空间大小。如： df -h。 du是查看目录及子目录文件夹大小，如：du -hs最下面的.号是当前文件夹的大小。    u是 usage 磁盘的使用

    df -h
    df -ahl
    du -s   --summarize
    du -h   --human-readable
    du -a   默认只计算文件，-a表示也显示文件
    du -sh ./     目录大小
    du -sh a.txt  文件大小      du -c -d 0;  -c是文件夹分别计数(-s是总计数)   -d 0是当前文件夹的意思
    du -sh ./*   # 查看目录下各个文件夹的大小

### zmodem是什么?   

    是文件传输协议,rz,sz都是遵循这个协议
    rz 上传，sz下载
    rz: receive Zmodem   接受和发送都是对于linux来说的。  所以从linux接收文件是rz，从linux发送文件到window是sz。
    sz: Send Zmodem        多个文件用空格分隔
    sz 空文件的时候为什么会失败,其实是传递过去了,只是因为没有大小所以提示传输失败.
    rz传输失败： 如果文件重复  就会失败 ，解决方案  rz -y        -y --overwrite
    rz -e aaa.tar.gz  #rz的时候出现乱码   -e 是escape的意思
