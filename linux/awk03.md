### awk 的参数们:   第一个参数是命令名   然后是传入的文件名
    awk 'BEGIN {
           for (i = 0; i < ARGC; i++)
               print ARGV[i]
         }' inventory-shipped mail-list
    结果为:
    awk
    inventory-shipped
    mail-list

### awk -v A=1 -f showargs.awk B=2 /dev/null
    结果为:
    A=1, B=0
          ARGV[0] = awk
          ARGV[1] = B=2
          ARGV[2] = /dev/null
    A=1, B=2

### awk 打印行数最大值:
    awk '{ if (length($0) > max) max = length($0) }
         END { print max }' data

### awk
    awk -f  后面可以跟任意的文件,不一定是.awk后缀
    gawk 'BEGIN{$string="";}  {$string=$string""$0;}     END{printf $string}' b.txt
    awk 'BEGIN{FS="2018-01-01"}$1>"07:00:00"{print RS,$0}' date.txt  # 日期是2018-01-01  7点之后的数据
    awk 'BEGIN{print strftime("%Y-%m-%d",systime())}'     #时间戳转为str
    awk 'BEGIN {printf("%d\n",mktime(2006" "8" "5" "15" "09" "0))}'   # 将str转换为时间戳
    awk -F "/s" '{print $1}' a.txt  # 空格分隔符 注意是左斜杠  /s 或者是" "

    awk遇到这些符号,忽略新行:   ,    {    ?    :    ||    &&    do    else
    awk中的~   后面跟正则表达式,  如 awk '$1 ~ /chu/{print $0}' mail-list;    那么 awk '/chu/{print $3}' mail-list; 全列的话是不需要的
    awk '/edu/ && /li/' mail-list  # awk 使用逻辑与
    awk '/edu/ || /li/' mail-list   # awk使用逻辑或

    awk '$1 == "on", $1 == "off"' myfile

### awk
    awk 'BEGIN { for (i = 1; i <= 7; i++) print int(101 * rand()) }'  #打印7个  100内的随机数
    ls -l a.txt | awk '{ x += $5 } END { print "total bytes: " x }'   #总的字节数  注意前面的ls
    awk -F: '{ print $1 }' /etc/passwd | sort    #打印登录用户的名字 并排序
    awk 'END{print NR}' a.txt       # awk统计行数
    awk 'NR % 2 == 0' data         # 统计偶数行    也可以用  a=!a
    awk '/12/ { print $0 }   /21/ { print $0 }' mail-list inventory-shipped   # 多个正则表达式分别作用
    ls -l | awk '$6 == "Nov" { sum += $5 } END { print sum }'      #统计11月的   文件尺寸

### awk
    cat a.txt | awk  '$0~/aaa/ {print $0}'    从行中搜索匹配项
    less a.txt b.txt |awk '$0~/lisi/ {print $0}'       awk多文件搜索
    cat a.txt | awk -F "," '{print $1}'            -F指定分隔符
    cat a.txt | awk -F "," '{print FS}'            FS表示分隔符，注意不要用$FS， FS是key,$FS相当于value
    echo -e "line1 f2 f3nline2 f4 f5nline3 f6 f7" | awk '{print NF  " "  NR}';      ---语句中的字符串需要用双引号
    echo -e "line1 f2 f3nline2 f4 f5nline3 f6 f7" | awk '{print  NF}';      ---NF 最后元素的下标     NF要大写
    NF和$NF:  nf是最后元素的位置，$nf是最后一个元素
    NR和NF: nr是number of records，表示行数(即时行数，相当于行号)。  nf是nuber of final ，总列数
    echo -e "line1 f2 f3n line2 f4 f5" | awk '{print $(NF-1)}'    ---$(NF-1)    倒数第几个元素        -e 允许backslash转义
    echo -e "line1 f2 f3n line2 f4 f5" | awk '{print $2,$3}'        ---打印第二和第三个字段
    awk 'BEGIN {count=0;print "[start] user count is ",count} {count=count+1;print $0} END{print "[end] user count is ",count}' a.txt     begin和end,总共有3个大括号，begin和end只对这2行有用

### awk
```
awk '{a=!a}' a.txt       #a 是一个undifined的变量, !a是true,也就是1  然后会在1,0之间来回循环
awk '{b=a[$0]++;print b}' a.txt   #awk a[$0]++   a是一个map,以$0(每行的数据)为key,如果出现一次,value就+1   ++2个作用(使变量右值,自增1)
awk -F "," 'BEGIN{ORS=" "}{print $0}' a.txt    #ORS   输出记录分割符（默认是以\n,这里使用空格）
awk -F "," 'BEGIN{OFS="***"}{print $1,$2}' a.txt    #OFS   输出FIELD分割符（默认是以\n,这里使用空格）  一定要用$1,$2的形式  如果$1$2其实已经制定了输出的格式了
awk  '/aaa/{print $0}' a.txt;  #打印包含 aaa的行
awk '{print $2}' a.txt   # 默认的分割符  是空格
awk -F "," 'BEGIN{OFS=" "}{print $1,$2}' a.txt   #分隔符 逗号-->空格
awk  'BEGIN{OFS=","}{print $1,$2}' a.txt   #分隔符  空格-->逗号
```

### awk
    cat a.txt | awk -F "," 'BEGIN{sum=0}{sum+=NR}END{print FS}'
    cat a.txt | awk -F ","  'BEGIN{sum=0; OFS="-";}{sum+=NR}END{print OFS}'  # OFS不能写在前面   不能用-OFS,只能在{}语句中定义
    cat a.txt | awk -F ","  'BEGIN{}NF>0{if($1==0){print "stdin"}else if($1==1){ print "stdout"}else{print "stderr"}}END{}'  # 注意判断是2个==   一个=是赋值符号
    cat a.txt | awk -F ","  'BEGIN{}{print NR"行,"NF"列"}END{}'      #打印行列

### awk
    awk  -F "," '{print $1 >"a.txt"}' a.txt   # awk直接修改文件   >"fileName"
    awk  -F "," '$2>80{printf $1}' a.txt   #  列条件判断
    awk  -F "," '$2~80{print $1}' a.txt   #条件判断   ~ 表示  等于
    awk  -F "," '$2!~80{print $1}' a.txt   #条件判断   !~ 表示 不等于
    awk 'NR==1' a.txt      #只显示第一行   n 只显示第n行
    awk 'NR >1 && NR <4' a.txt   #几行到几行之间的数据
    awk 'END{print $0}' a.txt   #打印最后一行
    awk 'NR != 1' a.txt  #不显示第一行
    awk '{print $NF}' a.txt   #只显示最后一列
    awk '{for(i=1;i<NF;i++){print $i}}' a.txt
    awk 'NF--{print NF}' a.txt  #不显示最后一列    实测不对
    awk -F "," '{for(i=1;i<NF;i++){print $i}}' a.txt   #不显示最后一列   i<NF 所以最后一列显示不出来
