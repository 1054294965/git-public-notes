### sitemesh用法

    1、加入jar和配置web.xml  filter。
    2、配置decorators.xml,
    defaultdir="/WEB-INF/views"
    被装饰的页面需要加<meta name="decorator" content="default"/>
    content="default"对应<decorator name="default" page="layouts/default.jsp" />  的name="default"
    然后用default.jsp装饰。
    把请求页面head中的所有内容，替换掉<sitemesh:head/>
    把请求页面body中的所有内容，替换掉<sitemesh:body/>


    页面引入sitemesh标签的前缀是可以自由指定的，
    <%@ taglib prefix="sitemesh" uri="http://www.opensymphony.com/  sitemesh/decorator" %>
    这个prefix指定为什么，就是什么。

### factoryBean和beanFactory

    主要方法是getObject()，xml中的bean，其实就是factoryBean。
    通过id引用，调用的是他的getObject()方法。
    beanFactory：
    spring容器其实就是个beanFactory，有getBean()等方法来管理bean。


### 始终是多的一方来维护关系。(多的一方就是子表)  

    子表添加父表对象,用@JoinColumn(name="parent_id")指定用哪个字段来关联父表。
    父表添加子表列表，用mappedBy="parent"表示Son对象的parent属性来表示映射。
    一对一，哪方都行。
    多对多，
    @ManyToMany(fetch = FetchType.LAZY)
       @JoinTable(name = "sys_role_menu", joinColumns = { @JoinColumn(name = "role_id") }, inverseJoinColumns = { @JoinColumn(name = "menu_id") })
    @ManyToMany(mappedBy = "menuList", fetch=FetchType.LAZY)
    如果拆分的话：
    Student 设置多对多
       @ManyToMany(cascade = CascadeType.PERSIST, fetch=FetchType.LAZY)
       @JoinTable(name="teacher_student",joinColumns={@JoinColumn(name="s_id")},inverseJoinColumns={@JoinColumn(name="t_id")})
       private Set<Teacher> teachers;
    Teacher 设置多对多
       @ManyToMany(cascade = CascadeType.PERSIST, fetch=FetchType.LAZY)
       @JoinTable(name="teacher_student",joinColumns={@JoinColumn(name="t_id")},inverseJoinColumns={@JoinColumn(name="s_id")})
       private Set<Student> students;
    维护方，用joinTable name属性指定中间表。joinColumns和inverseJoinColumns分别指定关联字段。
    只要有关联，就肯定是2个表的事情，即使是最简单的一对一，也要在2个class中都进行设置。
    private List<User> userList = Lists.newArrayList();
    只要看到实体中有list就表示，这个类是User的父表，也就是user表外键关联该表(也可能是多对多)
    其实实体比较麻烦，一个外键就需要2个关联。
    一对一，子表引入父表对象。父表引入子表对象。
    多对一，子表引入父表对象,父表引入子表列表。
    多对多，其实就是2个多对一。

### RequestMappingHandlerAdapter类的getModelAndView方法:  

    isRequestHandled()表示如果参数有response,可能已经处理完毕请求了，就不需要继续处理了，返回null
    isViewReference()表示如果是String类型的view，那么需要手动的设置View。
    model instanceof RedirectAttributes如果是redirectAttributes请求，那么需要从flashMap中取参数

### ResponseEntity有4种:(不能为空)  

    1、ResponseEntity(HttpStatus status)
    2、ResponseEntity(T body, HttpStatus status)---这个T只能和泛型一致，否则报错。
    3、ResponseEntity(MultiValueMap<String, String> headers, HttpStatus status)
    4、3个参数都有。

### modelandview添加参数有2种方式：  

    modelAndView.addObject("param", "chushiyun");或modelAndView.getModel().put("param", "chushiyun");
    设置页面的方式: modelAndView.setViewName("param");
    return modelAndView;

### hadoop笔记：  

    D:\hadoop-2.7.4到d盘
    如果没有winutils.exe和hadoop.dll需要下载之后添加过去。  最好hadoop\bin和c:/windows/system32/下都有一份(尤其是hadoop.dll)
    环境变量配置：
    HADOOP_HOME hadoop目录
    classpath中添加
    path添加 ;%HADOOP_HOME%\bin;
    注意hadoop.dll等文件不要与hadoop冲突。为了不出现依赖性错误可以将hadoop.dll放到c:/windows/System32下一份。

### c标签属性：  

    status.index: ${status.index }
    status.current: ${status.current}
    status.count: ${status.count }
    status.first: ${status.first }
    status.last: ${status.last }
    status.begin: ${status.begin }
    status.end: ${status.end }
    status.step: ${status.step }

### @modelAttribute用法:   

    字符串是属性的key，返回的值是value。  相当于把一个键值对放进model中了。
    @ModelAttribute("student")
    public Student getStudent(@RequestParam(value = "id", required = false) String idStr, Map<String, Object> map) {
        Student student = null;
        try {
            Integer id = Integer.parseInt(idStr);
            System.out.println("student id: " + id);
            student = new Student(1, "lisi", 23);
        } catch(NumberFormatException ignored) {
        }
        return student;
    }

### spring自带几个httpmessageconverter:  

    requestmappinghandler构造方法自带：
    public RequestMappingHandlerAdapter() {
    		StringHttpMessageConverter stringHttpMessageConverter = new StringHttpMessageConverter();
    		stringHttpMessageConverter.setWriteAcceptCharset(false);  // see SPR-7316

    		this.messageConverters = new ArrayList<HttpMessageConverter<?>>(4);
    		this.messageConverters.add(new ByteArrayHttpMessageConverter());
    		this.messageConverters.add(stringHttpMessageConverter);
    		this.messageConverters.add(new SourceHttpMessageConverter<Source>());
    		this.messageConverters.add(new AllEncompassingFormHttpMessageConverter());
    	}
