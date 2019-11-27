### java自带的格式化字符串  

    String.format(template.replace("{}", "%s"), values);  

### eclipse中部分术语解释   

    重构，move的作用： 到其他package方便。
    重构，改方法签名的作用： 不用一个一个改方法名。
    抽取方法和inline： inline是把方法去掉，变成代码。
    抽取常量和变量： 必须选中字符串，双引号也要选中。
    抽取本地变量：  也是选中字符串
    pull up： 子类提取方法或者变量到父类
    push down：父类拉方法到子类（接口不能拉）
    抽取类：  将变量抽取到另外一个类
    merge jar file： 合并内容到jar


    search 和ctrl+shift+U： search是文本，可以工作空间。      ctrl+shift+u只能是变量。只能当前文件。
    ctrl+g 是获取声明，可以有多个（包括详细的位置）(和f3不一样，f3只是可以获取变量）
    ctrl+shift+g  是查看所选被引用了多少次，或者出现了多少次（显示的当前引用）
    remote search可以搜索不在eclipse中的文件。
    read access 获取哪里用到这个变量(只能是变量，本地变量或者成员变量)  相当于ctrl+shift+g

### 几天后的时间：  

    Date date = new Date();
    Calendar calendar = Calendar.getInstance();
    calendar.setTime(date);
    calendar.add(Calendar.DAY_OF_YEAR, -3);
    System.out.println(calendar.getTime());


### mysql查询条件的分析  

    介于条件如果缺少条件:(不考虑空的情况，数据库为null的话，那么会过滤掉)
    缺少左边的条件      只查出小于右边的数据，左边无限了，因为除了null任何值都>=''
    缺少右边的条件      查不出任何数据，因为任何值都不在''范围内，除了''，但是左边有个条件
    如果有null，那么null被过滤了
    1、期待结果是  <右边，或者>左边     左边为空设置''，右边为空设置null
    2、期待结果是  什么都查不出来     左边为空设置'null'（任意字母），右边为空设置''     (我们程序种采用的是这种)

    不管是数字还是时间，那么右边可以写成'null',因为字母一定大于数字
    如果要什么都查不出来，右边是'' 即可。

### 位运算：  (只对于一位,而且是位运算,不是逻辑运算)
置0        与0
置1         或1
按位取反        ~1（实际操作中没有意义，因为会连符号位也变了,结果值不是期望值）
取反      异或1（同或1也可，但是没有同或符号）
保留  异或0  但是没有意义,因为或1是跟简单的保留方式
保留字节  &oxff

### 源码，反码，补码  

    源码-->补码    取反加1 例如  -1是   000000000000000000，取反11111111111111111111110   +1     ffffffffffff
    补码-->源码    减1取反
    -1的补码  00000000000001 11111111111111111110 +1

### 异或进行交换：

    function swap( a, b)
    {
        a=a^b;
        b=b^a;
        a=a^b;
        console.log(a)
    console.log(b)
    }
    var a=3;
    var b=4;
    swap(a,b)

### split的几种情况  

    split("adf")和split("adfa",-1)：  最多匹配
    split("adfa",-3) 模式匹配将应用尽可能多的次数，而且数组的长度是任何长度。
    split("adfa",3)  模式匹配将被最多应用n-1次，数组的长度将不会大于n
    split("adfa",0)  相当于直接使用split("adf"),末尾空字符串丢弃

### console.log(10^1)为什么是11   

    不建议对0和1之外的数字用异或，不好控制
    1010
    0001
    1011   就是11
