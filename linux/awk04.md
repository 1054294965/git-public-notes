### awk sub函数:   第三个参数可以省略(那么用默认的$0,推荐最好写上最后一个参数)  sub会直接修改原来的字符串,返回值是匹配的个数
    echo "chushiyun" | awk '{sub(/chu/,"hello");print $0}'
    echo "chushiyun" | awk '{sub(/chu/,"hello",$1);print $1}'          #也可以使用& 匹配之前的内容
    echo "chushiyun" | awk '{result=sub(/chu/,"hello");print result}'  #匹配个数

### begin有什么用: 如果指定RS=":",那么写在一个{}中无法即时生效,写在begin中就有效. begin后的左括号要紧挨着.
    awk 'BEGIN{a="11";if(a>=9){print "ok"}}'    无输出 字符串和数字无法比较
    awk 'BEGIN{a="b";print a++,++a}'      打印多个参数
    awk 'BEGIN{a="b";print a=="b"?"ok":"err"}'    三目运算符
    awk -F [[:space:]+] '{print $1,$2,$3,$4,$5}' space.txt   多个空格     :space是空格   :是分号
    awk -f awk.txt a.txt        执行awk文件     -f 是awk脚本文件    脚本为：  #!/bin/awk       {print $0}  脚本中不用外边的单引号了
    ls -ls |awk  'BEGIN{OFS="#"} {print $1,$2}'         指定输出分隔符   不能在前面使用-OFS


###awk内置参数
    awk '{print ARGV[0]}' a.txt b.txt   #不能直接用ARGV,需要加下标,ARGV[0]=awk ,ARGV[1]=a.txt,ARGV[2]=b.txt
    awk '{print ARGC}' a.txt b.txt   # 参数个数 这里返回3  awk也算是个参数

    awk '{print ENVIRON }' a.txt b.txt   # 文件名 只是最后一个文件
    BEGIN和END和后面的左括号不要换行.  否则会报错.
    awk '{print ARGIND}' a.txt b.txt   # 被处理文件ARGV标识符   例如a.txt是1  b.txt是2

    awk BEGIN 代码块  并不能获取FILENAME属性,但是END可以

    awk '{printf ARGV}' a.txt b.txt   #ARGV是参数数组,不能直接需要printf,需要加下标

### awk split 函数:
    4个参数是 split(string,arr,sepreg,seps)  seps是匹配到的分隔符
    echo 1 | awk '{result=split("chu shi yun",arr," ",seps); print seps[1]}'
    echo 1 | awk '{result=split("2018-12-12",arr,"-",seps); print seps[1]}'
    echo 1 | awk '{result=split("2018-12-12",arr,/-/,seps); print seps[1]}'

    echo 1 | awk '{pival = sprintf("pi = %.2f (approx.)", 22/7);print pival}'

    pival = sprintf("pi = %.2f (approx.)", 22/7)
