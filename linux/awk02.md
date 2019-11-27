### awk  jpg批量重命名
    #!/bin/sh
    ls |grep .jpg|while read name;do
    s_fn=$(echo $name|tr -d ' ','\(','\)');
    echo $s_fn
    mv "$name" $s_fn;
    done

### awk  jpg批量重命名2
    #!/usr/bin/gawk -f
    {
        ori=$0;
        gsub(/[\(\)\[\]]/,"");
        printf ori"\n";
        printf $0"\n";
        cmd="mv '"ori"' '"$0"'";
        printf cmd"\n";
        system(cmd)
    }

### awk 脚本:       
    如果不用begin的话,会需要输入一行,然后提示一行
    vim test.awk
    输入:
    #!/usr/bin/awk -f
    BEGIN{}
    {printf 1234}
    END{}
    然后: chmod -x test.awk
    ./test.awk a.txt 执行即可(不要忘记传参a.txt)

### awk 合并2个文件的列:
    NR==FNR{
      a[FNR]=$0;
      next;
    }
    NR>FNR{
        for(i in a){
            if(FNR==i){
                print a[i],$0
            }
        }
    }

### awk match函数:  
    返回值是匹配的个数
    echo "chushiyun" | awk '{result=match("chushiyun",/u/);print result}'

### gsub函数:   
    和sub类似,只是变成了全局查找
    gensub函数:  不同点是 不修改原始字符串,返回值是原始字符串.
    echo "chushiyun" | awk '{result=gensub(/chu/,"hello",$0);print result}'  #gensub 返回的替换后的字符串
### awk
    awk '$0 !~ /chushiyun/{print 122}' a.txt

    awk '1111{print 2};111;111{print 2}' a.txt  #一个分号表示一个单独的语句, 1111表示的是true.

### awk的内置(built-in))函数:
    gsub, index, length, match, printf, split, sprintf,substr, tolower, toupper, atan, cos, exp, int, log, rand, sin,sqrt, srand, system

### awk
    awk '!a[$1]++{print}' h5_utf8.csv >h5_utf82.txt    对第一列去重      但是因为内存的问题 会被kill掉      !表示如果有重复记录，只显示一条

    awk -F "," '{a[$3]++}END{for(j in a) print j,a[j] > "hhh.txt"}' h5.txt         根据第3列进行统计
    awk -F "," '{a[$2]++}END{for(j in a) print j,a[j] > "hhh.txt"}' h5.txt
### awk 多条件:  (这2种写法都是对的)
    FNR >= 23 && FNR <= 28 { print "     " $0 }
    可改写为
    FNR == 23 , FNR == 28 { print "     " $0 }

### awk自定义变量(调用自定义变量不需要加$):
    str  print str;    例如  str=1234; print $str; (这样是错的)

awk里面执行shell命令: system("echo hello")
### awk自定义数组:
    arr[0]= "chu";
    arr[1]="zhangfei"
    arr[2]="guanyu"
    for(i  in  arr){
      print arr[i]
    }

### awk默认会输出么：
不会的  awk是在所在的流里面进行操作

### awk命令输入多行:     后面加个  右斜杠即可
    awk \
    'BEGEN{} \
    {printf $0}  \
    END{}   \
    ' \
    a.txt

### awk报错:fatal: NF set to negative value      
是因为空行执行NF-=1的操作

### awk
    ,    {    ?    :    ||    &&    do    else    #awk忽略新行
    awk 'BEGIN {print "Name            Belt\n---------------------------"}> {print $1"\t"$4}' grade.txt
    awk 打印所有列： awk '{print $0}' grade.txt
    awk 打印多列： awk '{print $1,$4}' grade.txt
    awk 检索并打印： awk '$4~/brown/ {print $0}' ;        ---      $4表示第4列，~表示后面跟正则表达式来筛选，/brown/表示内容中包含brown的。然后打印$0，打印
    所有列。
    awk '{ x += $0 } END { print x }' a.txt     求和
    awk '{$1="";print $0 > "b.txt"}' b.txt      awk结果重定向
    awk '{print $2}' a.txt  >c.txt      awk结果重定向2    awk不能重定向到  自己这个文件
    awk -F "," '{print $NF}' a.txt    #打印最后一列   NF是最后一列的编号,$NF是最后一列的值
    awk -F "," '{print $(NF-1)}' a.txt    #打印倒数第1列的数据   $(NF-1)
    awk -F '[:\s]' '{print $1}' a.txt   # awk多个分隔符

### awk
    cat a.txt |awk 'BEGIN{sum=0}NF>0 { sum+=1}END{print sum}'   #awk统计非空行
    cat a.txt |awk 'BEGIN{sum=0}NF<1 { sum+=1}END{print sum}'   #awk统计空行
    awk 'NF-=2' a.txt;   #awk过滤掉最后2列
    awk '!a[$0]++' a.txt  # 过滤掉重复行(a[$0] 是0, a[$0]++之后a[$0]变成1,但是判断的时候是0  再次出现相同$0的时候 a[$0]是1  而!a[$0]是0 )

    awk '{"cat a.txt" | getline;print $0}' a.txt
    awk 'NR==1' a.txt      #打印第一行


### getline:  
    从shell脚本获取内容,如果直接getline,就是定位到下一行.
    awk '{print $0;getline;print $0}'    #依次打印,最后一行重复, 当n=1,打印row1.   getline 到n=2, 打印row2,getline到n=3,打印row3, getline,没有下一行了,打印row3
    awk '{print $0;"date"| getline;;print $0}' a.txt

### awk打印奇数行
    awk 'a=!a' a.txt   #打印奇数行
    分析:
    a=!a  第一行的时候  !a=1  a=1

    awk '/zhangsan/{print $1}' a.txt    #正则和printf一起使用
    第二行的时候   !a=0 a=0

### awk打印单引号:  `\47`
    awk 'BEGIN { print "Don\47t Panic!" }'
