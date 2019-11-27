### vim缩进  

    > 右缩进
    >> 右缩进
    << 左缩进
    < 左缩进
    4>> 多行缩进 (不要用visual-block模式)
    =% 缩进括号内的内容
    如果要首选多行缩进,也可以用visual模式


### vim  

    :r c.txt       r和r!的区别是:   r后面接文件名   r!后面加命令
    :r!date  执行命令并将结果插入到文件中     r是read
    :r!ls   插入 目录文件列表到文件
    :read  !ls   #和r !ls一样
    G=gg  跳转到某行
    gg  # 首行  2gg  表示跳转到第二行
    G  # 尾行   2G 表示跳转到第二行
    :%y  复制所有,只是在vim中复制,按p粘贴
    :1,3y  多行复制
    :r!date      插入日期
    a,i,o:       a 当前字符后插入文本 ，i当前字符前插入文本，o 下一行添加文本,O 上一行添加文本
    A,I,O          I 单词前插入   A  单词后插入  O  行前插入
    ZZ  保存并退出，相当于wq  注意大写
    less：
    :read a3.txt   读取a3.txt内容并插入到当前文件
    R   替换模式
    guu   行小写
    gUU   行大写
    ~  转换大小写
    ga 查看字符ascii码
    gu 查看字符utf8码
    gf 查看引用的文件 例如在.sh文件中  source ./date.sh
    - 上一行开头
    + 下一行开头
    v 进入vi编辑器
    h 显示帮助
    :%s/\s+//g    替换空格为空     %s会匹配所有行
    :%s/cccc//gn  vim 显示匹配的个数
    u 是撤销
    ctrl+r  撤销
    g;  最近一次编辑的位置
    set nu  或者set number        显示行号
    set textwidth=10  #一行10个字符  多个单词才会换行
    set nonu  或者 set nonumber     不显示行号
    set ignorecase
    set noignorecase
    set list         显示不可见字符SDDDDDD  要隐藏的话使用  set nolist

### vim  

    搜索: / 输入字符，enter   n向前 N 向后
    ?  输入字符，enter   n向后，N向前

    开头输入内容： :s/^/sadfsafsa               s表示替换 %表示当前行
    结尾输入内容： :s/$/adfadfasdf
    全局查找替换： :%s/aaa/ccc/g     # 百分号是全局查找替换
    当前行查找替换： :s/aaa/ccc/g
    linux 总是在光标前插入  总是在光标前插入 linux 总是在光标前插入
    shift +insert   开头插入
    .  点号  重复上次操作
    &  重复上次替换操作
    @a 重复宏 @@  重复上次宏
    :h . 查看.号的用法

### vim  

    25s/ddd/ccc    25行  替换内容     语法为ns/ddd/ddd  n是第几行
    1,10s/ddd/ccc/g  1-10行  替换内容       并不是从当前行开始  是绝对行数
    %s/datetime/ccc/g     所有行替换内容
    撤销  u    撤销的尽头是already at oldest change       是最老的版本
    重做 ctrl+r     恢复的尽头是already at newest change    是最新的版本
    :! 外部命令  执行结束之后,  再次按enter即可回到  vim
    m,nw !cmd           如  1,2w ! echo
    yum -y install vim-enhanced         vim扩展
    :x 和 :wq     :x 在内容没有改变的情况下不会修改时间
    vim使用鼠标：   :set mouse=a      a表示所有模式
    永久使用鼠标:   用户目录下新建.vimrc  文件,输入 ::set mouse=a 保存
    vim自定义tag长度: 编辑/etc/.vimrc 输入 set tabstop=4  并且 set shiftwidth=4

    vim全选   ggVG   VG是大写  这个是全选  但是如何复制出来啊 ??
    visual,visual-line,visual-block    v可以用光标选，V可以选行，ctrl+v可以选行和列
    X(删除光标前,同backspace，backspace不能在普通模式下使用) x(删除光标所在位置，同delete)   删除单个字符
    d和x和退格?       d是通用删除命令，最慢   x同delete      退格必须编辑模式才可以用
    :e  a2.txt      vim中进入其他文件
    :wq! a3.txt        另存为其他文件
    :saveas new.txt    #另存为其他文件
    p和P    p是光标后粘贴       P 光标前粘贴

### vim宏定义  

    宏定义的例子:
    qa   出现recording,表示开始录制宏,
    按dd,再按dd    执行2次删除行的操作
    q    退出宏,recording消失  表示录制完毕
    然后  @a  可以发现删除了2行

### vim多行插入

    ctrl+v    # 块模式
    10j       #向下选择10行
    I       # 行前插入
    --      # 插入2个--
    esc   　#多行插入

### vim -c rm a2.txt a.txt

### 报错： Swap file ".aaa.sql.swp" already exists!  [O]pen Read-Only, (E)dit anyway, (R)ecover, (Q)uit, (A)bort:    
删除swp即可： rm -rf .\*.swp 或者rm -rf .\*.\*.swp       点号不能用*代替
