### springboot排除默认数据库
在使用2.2.1版本的时候，默认会有2个数据库，如果不配置会报错，添加一个配置类，排除掉默认的数据库配置即可:

    @Configuration(proxyBeanMethods = false)
    @EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})
    public class MyConfiguration {

    }


### springboot集成devtools
pom.xml添加:  
```
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-devtools</artifactId>
	<scope>runtime</scope>
	<optional>true</optional>
</dependency>
```
关闭热部署,application.properties中设置：
spring.devtools.restart.enabled=false #默认是true  restart包含livereload
spring.devtools.livereload.enabled=false #只livereload（重新加载类）而不restart


### springboot排除默认的数据库
在使用2.2.1版本的时候，默认会有2个数据库，如果不配置会报错，添加一个配置类，排除掉默认的数据库配置即可:

    @Configuration(proxyBeanMethods = false)
    @EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})
    public class MyConfiguration {

    }
