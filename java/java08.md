### mybatis !=0: < if test="overdueDayTypes!=null and overdueDayTypes!='' or overdueDayTypes == '0'.toString()">为什么要加!=''   

    因为在为""的时候会，认为这不是空，查询的时候会出现 column='' 这样的条件。
    0 在判断!=''  的时候会出错，  因为会把0当作''
    如果这样写： 传0  不会进入条件
    <if test="data.isSent != null and data.isSent!='' ">
        and is_sent=#{data.isSent,jdbcType=INTEGER}
        </if>
    例如del_flag  传0，表示查未删除的数据，如果这样写就错了。  所以加上一个 ==''.toString()就可以成功的筛选了。
    如果只是一个null，也是可以的。

### mybatis 新增数据自动返回主键：  

    <insert id="add" parameterType="com.ehaier.crmbusiness.domain.analysis.GroupPortrayAnalysisBean" useGeneratedKeys="true" keyProperty="id" >
    //如果是dto，记得给dto赋值id，因为返回id只返回给bean
    this.groupPortrayAnalysisDAO.add(groupPortrayAnalysisBean);
    groupPortrayAnalysisDTO.setId(groupPortrayAnalysisBean.getId());

### mybatis查询的返回值：  

    如果是单个对象，没有查询到返回null。
    如果是list，返回一个size为0的list。不是null。
    mybatis queryCount如果查询不出来任何数据,那么默认返回0

    什么时候会有errorMessages,逻辑错误的时候可以添加这个。
    如果有了errorMessages如何处理?? 如果有了错误   建议直接返回错误信息。

    getResult!=null 那么表示返回了数据
    list结果为0不能算错，因为条件可能筛掉全部。
    但是queryById是一定要求返回结果的，因为后面很可能要用到。

### dubbo服务的传参：
如果是一个方法内，传的是对象的引用，如果跨越了dubbo，传递的是序列化之后的对象，只是值，所以并不能起到修改原内存地址的作用。

### java日志级别值：  类似于权重，如果高于级别值就打印  

    System.out.println(Logger.TRACE_INT);  低
    System.out.println(Logger.DEBUG_INT);
    System.out.println(Logger.INFO_INT);
    System.out.println(Logger.WARN_INT);
    System.out.println(Logger.ERROR_INT);  高

### 服务器异常：   
服务端的异常一定要抛出的，否则调用方接收不到。  和用户的交互接口不要直接抛异常，会500很难看。但是需要反馈，服务端和web端都是需要日志来记录的。
web端，需要有返回，以便其他位置的逻辑处理。
异常可以有： 日志一定要记录，返回的结构中一定要有体现。

### 定义为null和定义为new：   
定义为new其实很不错，因为如果先null，但是赋值的时候报错了，那么就会返回null。

### 异常处理之后还可以返回是因为没有抛出新异常。  
这个很重要，有了异常一定要抛出，否则找不到错误在哪里

### 打印异常内容：  

    StackTraceElement[] stackTrace = e.getStackTrace();
    stackTrace.getClass();
    System.out.println(stackTrace.getClass());
    for (StackTraceElement stackTraceElement : stackTrace) {
    	  String className=stackTraceElement.getClassName();
        String methodName=stackTraceElement.getMethodName();
        String fileName=stackTraceElement.getFileName();
        int lineNumber=stackTraceElement.getLineNumber();
        System.out.println(className);
        System.out.println(methodName);
        System.out.println(fileName);
        System.out.println(lineNumber);
        System.out.println("StackTraceElement数组下标 i="+"fileName="
                +fileName+",className="+className+",methodName="+methodName+",lineNumber="+lineNumber);
    }

### 整数的范围： 超过范围会计算不准确  

    Integer integer=Integer.MIN_VALUE;
    Integer integer2=integer-1;
    System.out.println(integer2); //没有报错,但是结果显然不对   最小值-1  反而成为正数了

### 网页打开慢:  
1、ping
2、查看服务器内存
3、查看磁盘空见大小，日志大小

### mns: message service 短信服务

### 术语：  
pv: 页面浏览量   每打开一次  或者刷新一次  
uv （unique visitor独立访客）: 独立访客数量  
IP: 有多少个ip访问了该页面，如果是一个局域网内的各个电脑，只算是一个IP。  
