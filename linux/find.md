### file相关
```
mkdir -p a/b/c/d/e 循环创建文件夹      注意这个创建的是文件夹  不是文件
touch ./dir/{b.txt,c.txt} 创建多个文件
find ./ -type d    查找文件类型 是目录的
find ./ -type l    类型为链接的
find ./ -name "*.txt" 或者find . \*.name         ---  查找后缀名为txt的文件,需要加双引号
find ./ -type f -empty   查找空文件
find -type f \( -newermt '2018-04-01 00:00' -a -not -newermt '2018-05-01 23:59' \)        查找时间段-根据时间字符串
ls -l `(find -type f \( -newer a.zzz -a -not -newer a.txt \))`        查找时间段-根据2个文件
ls -l `(find -type f \( -newermt '2018-04-23 00:00:00' -a -not -newermt '2018-04-23 23:59:59' \) )`    查找时间在某天的文件  (左右一定要有空格)
find . -name "*" -maxdepth 1       不查找子目录
find . -maxdepth 1       当前目录为1         如果是0表示 当前文件夹  0没有什么用
find . -size +200M  #  +200M 是大于200M   -200M是小于200M   M是大写，不要小写  不写加减号就是等于
find . -maxdepth 1 -size +200M   #-maxdepth 1最好在最前面
find . -maxdepth 1 -type f -size 200M
-mtime +2 一天以前的数据
-mtime -2 一天内的数据
-mtime 2  2天前那一天的数据
-mmin +2 2分以前的数据
-mmin -2 2分钟以内的数据
-min 2 2分钟这分钟内的数据
```


### file相关  

    ls -l `(find -type f \( -newermt '2019-05-01 00:00:00' -a -not -newermt '2019-06-01 23:59:59' \) )`  #这个命令会把符合条件的一级文件夹也打印出来

    ls -l `(find -type f \( -newermt '2019-05-01 00:00:00' -a -not -newermt '2019-06-01 23:59:59' \) )`
    find -type f \( -newermt '2018-04-01 00:00' -a -not -newermt '2018-05-01 23:59' \)  -maxdepth 1
    -mindepth 4 至少要4层目录以上的才行
    \( -newermt newermt newermt  '2018-04-01 00:00:00' -a -not -newermt '2019-06-01' \)
    find -type f \( -newermt '2018-04-01 00:00' -a -not -newermt '2018-05-01 23:59' \)        查找时间段-根据时间字符串


### file相关
```
find ./  -regex  ".*aaa.*"     find使用正则表达式
find . -maxdepth 1 -name *.
find . -maxdepth 1 -name *.jpg -print -exec convert "{}" -resize 80x60 "thumbs/{}" \; batch resize files in the current directory and send them to a thumbnails directory (requires convert from Imagemagick)

ls -l a.txt 查看name，size，date等
file a.txt   查看文件类型
file zzz  查看文件类型
file a.txt b.txt 多个文件类型
file -z a.txt.tar  探测压缩文件的类型
file -v  无用
file grep ccc  探测没有后缀名的文件类型，文件夹无效，多媒体文件无效
find a.txt -ok  rm {} \;     find后面可以添加 -ok  或者-exec

find . -maxdepth  1 -type d -name "其他文本"
find ./ -depth a.txt ; #-depth 后面不用加内容   不用参数,是先显示目录本身,再显示子内容

find a.txt -delete;  # -delete 直接加在find后面比较高效
```
