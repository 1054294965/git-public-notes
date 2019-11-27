### sed

    sed -n '2,3p' a.txt   #2-3行的内容    bbb,ccc
    sed -n '2,+3p' a.txt   #2行,之后3行的内容  bbb,ccc,ddd,eee

    sed 's/^/HEAD/g' a.txt   #行首添加
    sed 's/$/END/g' a.txt   #行尾添加

    sed '/^$/d' a.txt   #删除所有空行
    sed '/^$/!d' a.txt   #删除所有非空行 用!
    sed 's/[0-9]//g' a.txt  #删掉所有的数字(不要忘掉g)
    sed '/a/d' a.txt   #删除包含内容的行
    sed '3d;5d;7d' a.txt  #删除3,5,7行

    sed  -n 'p;n' a.txt  #奇数行
    sed  -n 'n;p' a.txt  #偶数行
    sed -n '=' a.txt   #打印行号

    sed 's/aaa/(&)/' a.txt  # 给匹配的内容添加括号
    sed 's/^..//' a.txt    #删掉前2个字符


### sed  
```
sed -i 's/yyyy/zzz/' a.txt            -i直接修改
sed -e '/com/s/baidu/sina/g' a.txt     含有com的行中，baidu替换为sina  -e是正则表达式脚本(不写也是)
sed -e '5c\hello world!!!' a.txt        5行替换为hello world!!!
sed -e '/^ *$/d' a.txt         删除空行  注意空格          或者 sed -ie '/^\s$/d' a.txt    ie不能ei   e后面必须跟 正则
cat a.txt | tr -s '\n' >a.txt; #tr删除空行
grep -v '^$' a.txt   #grep 删除空行
sed -n '/second/p' a.txt
sed -n '/bbbb/,/77777/p' a.txt   #或的条件  用逗号分隔或者写2个语句都可以  sed -n '/bbbb/p;/77777/p' b.txt 或者用 sed -n '/bbbb\|77777/p' b.txt,记住|符号需要加右斜杠
sed -n '1,2!p' a.txt       本来取得是1行     这样取得是除了1之外得所有行
sed -n '5p' a.txt  打印第几行
sed -n '/b\{1,3\}/p' a.txt  含有1，3个b字符的行
sed中分号 ;  多个命令
sed中的大括号        在定位行执行的命令组，用分号隔开
sed中的q    匹配第一个就退出
sed -n '/^#/p' a.txt  所有注释（#开头）
sed -n '/^#/!p' a.txt  所有非注释
sed -n '/^#/!{/^$/!p}' a.txt     双重否定
sed -i '1 i\sed command start' a.txt    第一行插入内容      2个i不一样    -i直接修改文件  i\ 在定位行号前插入新文本信息
sed -i '$ a\sed command end' a.txt     $是末行   a是append
sed -i '3d' a.txt  删除第3行
sed -i '1d' a.txt; # 删除第一行      vim删除一行?   :1,1d
sed -i '$d' a.txt; # 删除最后一行   不要用双引号，会把$d认为是变量，所以删除不了
sed -i '1,$d' a.txt; #删除1到$行
sed -i '1,2d' a.txt; #删除1到2行     都是闭区间
sed -i '/a\|b/ d' a.txt    sed或    中间的| 要有斜杠\|
sed '/c/s/$/ LI/' a.txt       c行尾添加Li
sed '1,2s/a*/bbbb/g' a.txt; # 1-2行的  a*替换为bbbb
sed '1,2c newnew asdadf' a.txt; #1-2行的数据 用newnew替换(2行替换为一行)      c后面的所有内容都当作替换的字符串
sed '1,2c asdfjkasjdfk2 \n    sadfa1' a.txt; # 取代内容  中间使用\n
sed -e 4a\newLine a.txt; # a表示在下面新增 4a表示第4行下面新增
sed -e '1a chushiyun \n > chushixiao'  a.txt;
sed -i '/ggg/d' a.txt;  #搜索并删除所在行
sed -n '/ggg/p' a.txt; #  -n表示只显示匹配的
sed -n '/chu/{s/yun/xiao/;p;q}'  a.txt;  #找到匹配行   并将行内的内容进行替换
sed -i '/chu/{s/yun/xiao/;q}'  a.txt;  #找到匹配行  替换a为b  并直接在文件中修改
sed -n 's/yun/xiao/gp'  a.txt;    #g表示全局替换，否则第一个   一行里面有2个    chushiyun  chushiyun
sed -e '1d' -e '2d' a.txt;    #多点编辑
sed  '1d' '2d' a.txt;  #  这样不对   只会第一个1d
sed -f sed.sh a.txt; # 文件内容为2p（删除第二行）    文件中的内容不用双引号
```

### sed 中的s是什么意思： 替换操作：s命令   

    echo sksksksksksk | sed 's/sk/SK/'    不加g表示只匹配第一个
    echo sksksksksksk | sed 's/sk/SK/g'    g表示全局匹配
    echo sksksksksksk | sed 's/sk/SK/2'    n表示匹配第几个
    echo sksksksksksk | sed 's/sk/SK/2g'    n表示从第2个开始匹配
    sed -n '1,3p' b.txt      sed  -n来查看几行之间的内容
    sed -n '3p' b.txt     -n  查看某行的内容
    sed 's/^/HEAD/g' a.txt   #行首添加
    sed 's/$/END/g' a.txt   #行尾添加
    sed -n '1~2p' a.txt   #奇数行 从第一行开始,每2行打印
    sed -n '0~2p' a.txt   #偶数行 从第0行开始,每2行打印
    sed -n '2~4p' a.txt   #从2行开始每隔4行打印
    sed -n '2~4!p' a.txt   # !是对选取的行进行取反处理

### sed中的n和N:  
n是read,也可以理解为overwrite 所以用n只有一行内容  
N是append   所以用N可以有多行内容  


### sed过程分析  

    sed 'n;n;n;p' a.txt        #过程分析
    默认读入第一行,打印  aaa
    n; 读入下一行,打印   bbb
    n; 读入下一行,打印   ccc
    n; 读入下一行,打印   ddd
    p  打印当前pattern space内容  ddd

### sed过程分析详细  

    sed 'N;N;N;p' a.txt
    打印第一行内容,并读入aaa到pattern
    N;  打印bbb,并append bbb到pattern
    N;  打印ccc,并append ccc到pattern
    N;  打印ddd,并append ddd到pattern
    p   打印pattern内容 aaa,bbb,ccc,ddd

### 故意保留换行的：  

    sed -e '1,2c\
    How are you?\
    my name is feige.
    ' a.txt

### sed命令之后出现右箭头           因为引号不对称  

    sed -n -s '1' a.txt
    sed -n -s '1' a.txt           -i(inplace) 原文件替换
    sed -n '/bbb /ccc /ddd' a.txt   #结果是cc /ddd, 这句话翻译含有bbb的行,c表示替换为, cc /ddd是替换的内容

### sed例子  

    echo 192.168.0.1  | sed 's/^192.168.0.1/&localhost/'            &是已匹配字符串标记，表示之前匹配到的  
    echo this is digit 7 in a number | sed 's/digit \([0-9]\)/\1/'            \1 \2 \n 子串匹配标记\1  
    字串匹配的时候有个注意点，就是匹配到的结果是整个的， 但是\1是获取结果的子匹配。  
