### printf 和echo：    

    echo换行，printf 不换行
    print和printf:  print只是单纯的打印,printf是格式化输出(例如: '{print "%s",111}')
    创建文件 touch  grade.txt
    touch -a "2016-05-04 12:00:00" a.txt       -a表示修改创建时间
    touch -m "2016-05-04 12:00:00" a.txt      -m修改修改时间
    touch -d "2016-05-04 12:00:00" a.txt      -d 2个时间都修改为这个值
    touch -t 201803041212.59 a.txt   修改文件的时间，可以用全量的format字符串  或者  毫秒值字符串
    touch abc`date +%Y%m%d%H%M%S`.txt    创建一个当前时间的文件
    %6s  如果长度不够6,那么在左边补空格到指定长度.


### bash case例子:  
```
num=2;
case $num in
  1 )
    echo 1
    ;;
  2 )
    echo 2
  ;;
  *)
    echo "default"
  ;;
esac
```

### test1.sh内容:  

    var1="变量1";
    echo "脚本1的pid是: " $$;
    case $1 in
      sh )
      echo "用sh执行脚本2"
      sh ./test2.sh
        ;;
      source )
      echo "用source执行脚本2"
      source ./test2.sh
        ;;
      exec )
      echo "用exec执行脚本2"
      exec ./test2.sh
        ;;
    esac
    echo "执行完脚本2之后返回";

### test2.sh内容:  

    var2="变量2";
    echo "脚本2的pid是: " $$;
    echo "变量1是: " $var1

sh ./test.sh sh  #sh新打开一个shell,所以不共享变量  pid也是不同的  
sh ./test.sh source  #source 用一个shell执行2个脚本,变量共享   pid相同  
sh ./test.sh exec  #exec 和source类似,只是执行完子shell不返回  

### join命令  

    join a.txt b.txt   2个文件第一列相同，就把行拼接到一起
    join -j 1 a.txt b.txt  拼接的列，默认是1
    join -j 2 a.txt b.txt  第二列为拼接识别列
    join -1 2 -2 3 a.txt b.txt  以多列为识别列

### paste命令  

    paste a.txt b.txt
    paste -s a.txt b.txt    -s serial文件合并成行输出，不是列输出
    paste -d ":" a.txt b.txt   2个文件之间的列的分隔符
    cat a.txt | paste -d"" -

### copy命令  

    cp a.txt b.txt 目标是文件
    cp a.txt zzz   目标是文件夹，如果文件夹不存在，会当作  复制为的文件
    cp -r zzz yyy  递归复制
    cp -a zzz yyy    -a是-r,-p,-d的集合  一个顶3个

    -r 的几个意思：   verbose详情,  invert反转, reverse反转，  recursive

### Linux中有以下三个标准设备：  
标准输入(stdin)、标准输出(stdout)、标准错误输出(stderr) 对应的文件描述符分别为：0、1、2  
2>&1   #错误输出  重定向到标准输出  

### 清空缓存   
echo 1 > /proc/sys/vm/drop_caches;     
