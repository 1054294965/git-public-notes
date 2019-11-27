### awk传参  

    传入参数1：
    num=1000;
    echo| awk -v num=$num '{print num}';    -v 传入参数
    传入参数2：
    var1="aaa"
    var2="bbb"
    echo | awk '{ print v1,v2 }' v1=$`var1` v2=$var2
    传入混合参数：
    var1="aaa"
    echo | awk '{ print v1,v2 }'  v2=$var2 a.txt

### awk 一定要有文件么,不一定:
    awk 'BEGIN{print "chuasdf"}'

### awk的输入模式:
awk '/chu/'  直接回车,如果输入带有'chu'的字符串,就会输出, 否则不打印

### awk模拟wc -l:
    awk 'BEGIN{print NR}' a.txt     #注意不要用BEGIN 否则是0

### awk自定义函数:
    function f1(){
      printf 1;
      return 1;
    }

### awk if用法:    注意不是elseif
    i=1;
    if(i==0){
      printf 0;
    }else if(i=1){
      printf 2;
    }

### awk简单写法
    'BEGIN{FS=""}{}END{}'/

### awk
    awk '{size=0;size=size+1;print size}' a.txt

### awk 判断是否包含中文:
    echo "asdf我是国人" | awk '/[^!-~]/'      # !-~  是ascii中 33-126的字符,   32是apace,127是delete  [^!-~] 表示除了这些字符范围之外的

### awk重置行号:
    echo '1
    2
    3
    4' | awk 'NR == 2 { NR = 17 }
    { print NR }'

### awk字符类：
```
echo ",.//" | awk '/[[:punct:]]/'  #匹配所有标点符号
echo "xff" | awk '/[[:xdigit:]]/'   #是否包含16进制字符   也就是0-9 a-f

echo "_" | awk '/[[:punct:]]/'

字符类:
[:alnum:]  Alphanumeric characters.(所有字母和数字)
echo "121234" | awk '/[[:alnum:]]/'
[:alpha:]  Alphabetic characters.(任何字母)
echo "asasdf" | awk '/[[:alpha:]]/'
[:blank:]  Space or tab characters.(空格和tab)
echo " \n" | awk '/[[:blank:]]/'
[:cntrl:]  Control characters.(控制字符)
awk '/[[:cntrl:]]/' a.txt
[:digit:]  Numeric characters.(任何数字)
[:graph:]  Characters that are both printable and visible.  (A space is printable, but not visible, while an a is both.)   (可以打印而且可见)
[:lower:]  Lowercase alphabetic characters.
[:print:]  Printable characters (characters that are not control characters.)
[:punct:]  Punctuation characters (characters that are not letter, digits, control characters, or space characters).
[:space:]  Space characters (such as space, tab, and formfeed, to name a few).
[:upper:]  Uppercase alphabetic characters.
[:xdigit:] Characters that are hexadecimal digits.
```
