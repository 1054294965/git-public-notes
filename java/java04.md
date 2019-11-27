### springboot测试：

    @SpringBootTest  
    @RunWith(SpringRunner.class)  如果不加这个注解，那么@SpringBootTest是无效的
    @RunWith(SpringRunner.class)
    @WebMvcTest(UserVehicleController.class)
    @ConditionalOnMissingBean   如果没有MyService类，就会自动创建这个类
    @Configuration
    public class MyAutoConfiguration {
        @Bean
        @ConditionalOnMissingBean
        public MyService myService() { ... }

    }
    @TestConfiguration的作用:  这样的类不会被自动扫描，需要用@import来注入到特定的类中,如：@Import(MyTestsConfiguration.class)

    如果用了 @ComponentScan ，那么是会包括@TestConfiguration的类的，如果不想要，可以配置TypeExcludeFilter来排除。

    测试的使用不同的端口：@SpringBootTest(webEnvironment=WebEnvironment.RANDOM_PORT)
    @JsonTest    测试json

### @controller是不是组合注解：  
是的，@controller包括@Component

### @value和@ConfigurationProperties:   
@value 从spring容器中注入属性到bean，或者属性。 @ConfigurationProperties 通过类将属性赋给spring容器。

### @component 和@configuration：  
@configuration是一种特殊的component，@configuration中的bean也会被作为bean注入到spring容器。

### @ServletComponentScan :   
扫描指定包中的@WebServlet, @WebFilter, and @WebListener
serverlet webfiletr weblistener

### @localserverPort获取当前的port，如：    
因为他是包含@Value("${local.server.port}")的
@LocalServerPort0
int port;

### @import和@importResource：   
2者作用相似，import是导入class，importResource是导入xml。

### @propertysource可以在其他类中使用@value么：    
可以的，会把值注入到environment中，所以其他类中也是可以使用的。

### spring-boot:run 和spring-boot:start：   
都是启动，但是run不会关闭进程，start执行完毕会关闭。

### boot启动之后为什么自动停止：   
如果没有引入web组件，本来就是个main程序。肯定要执行完毕呀。

### @EnableAutoConfiguration注解为什么可以自动扫描:   
是组合注解 ，包含@AutoConfigurationPackage

### @Autowired加在方法上是什么意思：  
表示方法中参数是通过自动注入 来的。


### 如果一个bean，有一个构造方法，那么构造起的参数不用加@autowired，也是可以自动注入的。

### 排除自动配置类：  

    @Configuration
    @EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})
    public class MyConfiguration {
    }
