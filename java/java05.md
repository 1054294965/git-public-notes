### 远程debug参数：

    更多参数细节：
    -XDebug               启用调试。
    -Xnoagent             禁用默认sun.tools.debug调试器。
    -Djava.compiler=NONE  禁止 JIT 编译器的加载。
    -Xrunjdwp             加载JDWP的JPDA参考执行实例。
    transport             用于在调试程序和 VM 使用的进程之间通讯。
    dt_socket             套接字传输。
    dt_shmem              共享内存传输，仅限于 Windows。
    server=y/n            VM 是否需要作为调试服务器执行。
    address=3999          调试服务器的端口号，客户端用来连接服务器的端口号。
    suspend=y/n           是否在调试客户端建立连接之后启动 VM 。


### boot重新启动和重新加载：  
重新启动最慢，重新加载快，因为boot提供了2个classloader，jar等基类放在一个classloader中，需要重启的类放在另外一个classloader中。

### boot设置不重新启动：  

    public static void main(String[] args) {
        System.setProperty("spring.devtools.restart.enabled", "false");
        SpringApplication.run(MyApp.class, args);
    }

### boot设置不重新加载：

    spring.devtools.livereload.enabled=false
    devtools默认的文件名： .spring-boot-devtools.properties

### violate  值修改的时候会立刻更新到内存，读取的时候会重新重内存中读取。所以不会有线程的问题。

### 打印100以内的乘法：

    for (int j= 100; j >0 ; j--) {
    	System.out.println();
    	for (int i = 1; i < 101; i++) {
    		int num=i*j;
    		String string=String.format( "% 5d", num);
    		System.out.print(string);
    	}
    }

### 100以内的乘法共有多少个数：2906个      去掉重复的   

    HashMap<Integer, Integer> map=new HashMap<Integer,Integer>();
    for (int i = 1; i < 101; i++) {
    	for (int j = 1; j < 101; j++) {
    		int num=i*j;
    		if(map.get(num)==null){
    			map.put(num, 1);
    		}else{
    			int count=map.get(num);
    			map.put(num,++count);
    		}

    	}
    }
    System.out.println(map.entrySet().size());

### 比较运算符为什么要把null放在前面：  
null==a和a==null:     如果少写一个=， null=a会报错。


### 格式化补0（补零）   
String string=String.format( "% 5d", num);

### 占位符格式化：  

    String format = String.format("[{}] [{}] asdflajf".replace("{}", "%s"), "111","222");
    System.out.println(format);

### 参数格式化： 大括号中要有数字，如果没有参数会保留{2}这样的输出  

    String format = MessageFormat.format("{0} is first,{1} is second,{2} is third", "aaa","bbb","ccc");
    System.out.println(format);      //messageformat在字符串中有单引号的时候不要用，因为会把单引号吃掉，可以用多次StringUtils来替换，
    如：String replace = StringUtils.replace(sql, "{0}", "111").replace("{1}", "222");
