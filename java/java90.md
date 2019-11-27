
### java报错：Missing artifact jdk.toolsjdk.tools  

    <dependency>
        <groupId>jdk.tools</groupId>
        <artifactId>jdk.tools</artifactId>
        <version>1.8</version>
        <scope>system</scope>
        <systemPath>${JAVA_HOME}/lib/tools.jar</systemPath>
    </dependency>


### freemarker报错： 找不到页面    

    application.properties 中配置 spring.freemarker.template-loader-path=classpath:/templates/

### spring-boot:repackage报错：  
repackage failed: Source file must be provided    
解决方案：直接使用mvn package或者mvn package spring-boot:repackage，避免直接使用spring-boot:repackage


### 注入date时，400错误：  继承baseController即可  

    @InitBinder
    public void convertDate(WebDataBinder binder) {
        binder.registerCustomEditor(Date.class, new CustomDateEditor(new SimpleDateFormat("yyyy-MM-dd HH:mm"), true));
    }

### 404报错：The origin server did not find a current representation for the target resource or is not willing to disclose that one exists.   
说明没有找到index


### 报错invlid byte tag 1.9        
tomcat版本太低了，tomcat7换成tomcat8即可


### eclipse错误关闭,svn图标不见了(重新拷贝svn插件)??   
1、eclipse svn图标不见了。应该是eclipse强制关闭造成的。
打开preference，svn选项没了，说明插件有问题。去dropins下面删掉，从新复制一个即可。（问题成功解决）
2、如果还不行，就删掉.metadata,重新导入项目即可。
