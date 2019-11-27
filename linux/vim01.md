### vim安装中文手册:  

    wget http://sourceforge.net/projects/vimcdoc/files/vimcdoc/1.8.0/vimcdoc-1.8.0.tar.gz
    tar -zxvf vimcdoc-1.8.0.tar.gz 解压然后 执行./vimcdoc.sh -i命令安装
    vim ~/.vimrc ,添加一行内容 set helplang=cn
    vim a.txt, :help ,然后输入 :set helplang=cn

    ./vimcdoc.sh -u  #卸载vim中文手册
    --------------------------------
    vim -p a.txt b.txt  # 打开2个文件
    :tabnew c.txt   # 新打开一个tab
    :tabn   # 下一个
    :tabp   # 前一个
    :tabc   # 关闭当前tab
    :tabo   # 关闭其他tab
    :tabs   # 查看所有打开的tab
    gt/gT   #切换下一个,上一个

### vim自定义缩进:   

    vim /root/.vimrc;  #用户目录的下的 .vimrc
    set tabstop=2
    set shiftwidth=2
    然后
    vim a.txt ;
    i进入输入模式, 发现tab是2格缩进
    或者v进入visual模式, > 也是缩进2格

### vim移动和定位:  

    j 下
    l 右
    h 左
    k 上
    0,$  行首  0和g0的区别: g0是回到屏幕的行首,不算折行
    ^ 行尾
    ( 句首
    ) 句尾
    { 段首,向上找空行
    } 段尾,向下找空行
    gg 首行    2gg 第二行
    G 尾行    2G 第2行
    w 下个单词词首
    W 下个长单词词首
    b 上个单词词首
    B 上个长单词词首
    e 下个单词词尾
    E 下个长单词词尾
    ge 上个单词词尾
    gE 上个个长单词词尾
    | 第几列  一般是字符  N
    f a 向前找某个字符 N
    F a 向后找某个字符 N
    t a 向前找某个字符之后的位置 N
    T a 向后找某个字符之后的位置 N
    ; 重复之前的fFtT查找 N
    , 反向重复之前的fFtT查找 N


    ctrl+b  向上翻页
    ctrl+f  向下翻页
    ctrl+u  上翻半页
    ctrl+d  下翻半页
    ctrl+e  上翻一行
    ctrl+y  下翻一行

### vim插入:  

    i 当前字符前插入      和y,c一起的时候表示符号内的所有内容
    a 当前字符后插入      和y,c一起的时候表示整个单词
    A 行首插入
    I 行尾插入
    o 向下插入新行
    O 向上插入新行

### 复制,粘贴,剪切,删除:  

    y 可视模式选中后按y  复制选中的内容
    yy 复制当前行   2yy 复制2行  注:yy 没有2,4yy这样的语法
    y+定位符 复制到某个位置  yw yb y0 y$  y2l(向右复制2个字符) y2j(向下复制2行,共3行)  y)不能用  y}(复制到段尾)
    yaw 复制光标所在单词
    p 当前位置后粘贴
    P 光标前粘贴



### 删除:  
    x
    X
    del
    d
    dd
    D
    J   合并行

### 其他  

    ctrl+] 查看光标处文档
    ctrl+t 跳回

    ctrl+w,w   切换窗口   :sp  水平切分窗格,  vsplit 垂直切分窗口    :q  关闭窗口
    Normal mode command      (nothing)   :help x
    Insert mode command	  i_	   :help i_<Esc>
    Command-line command	  :	   :help :quit
    Command-line editing	  c_	   :help c_<Del>
    Vim command argument	  -	   :help -r
    Option			  '	   :help 'textwidth'
    s  删除n并插入       3s     感觉c和s很像啊  区别是什么呢??
    R  替换模式
    :3d5     从3行开始  删除5行
    c  也是insert
    cc 删除行  并开启插入
    vi(vim)编辑器
    vi删除命令：  d其实是剪切命令
    dd删除当前行
    d$删除到行尾
    d^删除到行首
    nd删除几行(从当前行开始)
    dw删除光标之后的单词
    db删除光标之前的单词
    x向右删除一个字符           4x  删除多个
    X向左删除一个字符           5X  删除多个
    5x   删除5个字符
    5X     删除5个字符
    shell 经常卡死         ctrl+q解锁
    :ls  查看vim当前打开的文件
    ga  查看选中ascii码(注意,不用冒号)
    *   搜索光标所在单词(不是字母)  向下搜索
    #   搜索光标所在单词(不是字母)  向上搜索
    g8  查看utf8码
