### split  
    split -b 10k a.txt   根据大小分割   名字为  xa+a xab  xac等
    split -l 10  a.txt   根据行数分割 (注意 这个10不是分成10个文件  而是每个文件10行 数据多的时候千万别这么用,肯定卡死   因为要创建无数个10行的文件)  
    split -l 500000  h5x.csv  


### 删除多个小文件的方法
如果有很多个小文件  rm  -rf /root/h5/*  是不行的,非常慢
使用awk的删除命令也不行
用以下方法可以很快的删除:
mkdir /root/blank       #创建一个空文件夹
rsync --delete-before -d /root/blank/ /root/h5/      #   h5是目标文件夹


### 压缩多个文件
zip -r h5total.zip xaa  xab  xac  xad  xae  xaf  

### 服务器和网卡型号
dmidecode -s system-serial-number        服务器型号  
lspci |grep Ethernet      网卡型号

### netstat
```
netstat -n | awk '/^tcp/ {++S[$NF]} END {for(a in S) print a, S[a]}'       并发数
netstat -n     numberic，默认显示域名   这里显示ip地址
netstat -l    listening  显示监控端口
netstat -p    显示程序名
netstat -t    tcp状态，不加这个参数也是一样的
```

### 查看所有命令   
按4下esc

### 随机显示用户手册
man $(ls /bin | shuf | head -1)     随机显示用户手册

### shuf
shuf a.txt  打乱文件           shuf是打乱行，不打乱列
shuf a.txt -o b.txt -n 30     -o是输出文件，-n是输出行数

### ls和stat:
stat a.txt  查看文件的详细信息
stat更加的详细,还可以用于文件夹

### 算数，计算
```
echo  $[1+1]      $[***]表示算术式
let a=5+4 b=9-3;echo $a $b;   let是算数命令
i=2;echo $((i*3+3));        #i前没有$符号        $((算数表达式))
expr 10-2    expr也是算术
```
