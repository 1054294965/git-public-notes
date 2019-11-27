### Array可以被new么:   
不可以，他是一个私有的构造方法

### map的get()和containsKey():  

    HashMap<String, String> map = new HashMap<String,String>();
    map.put("aaa", "111");
    map.put("bbb", "222");
    map.put("ccc", null);
    System.out.println(map.get("ccc")==null); //用get值的方法来判断对象是否为空不一定对，因为value可能为null
    System.out.println(map.containsKey("ccc"));

### for还是while：  

    int i=0;        //for可以当作while，退出条件写再代码里面
    for(;;){
    	i++;
    	if(i>10)break;
    }
    while(i<10){

    }

### lambda表达式:       (java中的:: 表示方法引用)  

    List<Integer> list = new ArrayList<Integer>();
    list.add(111);
    list.add(222);
    list.add(333);
    list.forEach(System.out::println);
    list.forEach(e -> System.out.println("方式二：" + e));

### date格式化：  

    LocalDateTime now = LocalDateTime.now();
    DateTimeFormatter pattern = DateTimeFormatter.ofPattern("yyyyMMddHHmmss");
    String format = now.format(pattern);
    System.out.println(format);

### 日期加减：  

    LocalDateTime now = LocalDateTime.now();
    LocalDateTime plusDays = now.plusDays(3);    //不是add，是plus
    LocalDateTime minusDays = now.minusDays(3);
    System.out.println(plusDays);
    System.out.println(minusDays);

### 日期获取年月  

    LocalDateTime now = LocalDateTime.now();
    System.out.println(now.getYear());
    System.out.println(now.getMonthValue());      //getMonth()返回的是英文月
    System.out.println(now.getDayOfMonth());
    System.out.println(now.getHour());
    System.out.println(now.getMinute());
    System.out.println(now.getSecond());

### 设置时间：  

    LocalDateTime now = LocalDateTime.now();
    LocalDateTime result = now.withYear(2017)
    		.withMonth(12)
    		.withDayOfMonth(12)
    		.withHour(12)
    		.withMinute(12)
    		.withSecond(12);
    System.out.println(result);

### 时间转毫秒值,时间转天数：  

    Date date = new Date();
    System.out.println(date.getTime()/1000);  //除以1000是秒      时间戳
    System.out.println(date.getTime()/1000/86400*86400);  //获取天数 相当于先去掉小数，再乘回来         java中的除是只要整数部分的
