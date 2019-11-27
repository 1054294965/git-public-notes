### isAssignableFrom()   
例子： a是否是b类的同类或者父类或者父接口(不要用反了)
System.out.println(Iterable.class.isAssignableFrom(List.class));
System.out.println(List.class.isAssignableFrom(List.class));

### 26个字母：  
abcdefghijklmnopqrstuvwxyz0123456789

### jms和 jmx :       
java message service和  java management extensions(管理扩展)  

### spring.factories 是定义默认加载的class，提升效率  
additional-spring-configuration-metadata.json  配置一些默认参数  

### getAsText()和setAsText()以及getValue() setValue() ：  

    都是操作的value， getValue和setValue都是操作的原对象。
    java操作的时候是obj，网络间传递的时候是string。
    主语是属性值。 setAsText是set the property value 根据传来的string。 getAsText是Gets the property value根据value传出。
    代码：
    public String getAsText() {
           return (this.value != null)
                   ? this.value.toString()
                   : null;
       }
    public void setAsText(String text) throws java.lang.IllegalArgumentException {
       if (value instanceof String) {
           setValue(text);
           return;
       }
       throw new java.lang.IllegalArgumentException(text);
    }

### instance of和isassignableFrom：     

    instance of是对象和class， isAssignableFrom是class和class
    手动校验validator:
    Foo foo = new Foo();
    foo.setAge(22);
    foo.setEmail("000");
    ValidatorFactory vf = Validation.buildDefaultValidatorFactory();
    Validator validator = vf.getValidator();
    Set<ConstraintViolation<Foo>> set = validator.validate(foo);
    for (ConstraintViolation<Foo> constraintViolation : set) {
        System.out.println(constraintViolation.getMessage());
    }

### logback中的springProfile标签：  

    设置profile并且以及引入几个appender，并配置细粒度的appender。  
    <springProfile name="dev">
      <root level="info">
        <appender-ref ref="STDOUT"/>
        <appender-ref ref="SAVE-TO-FILE"/>
      </root>
      <logger name="com.lankydan.service.MyServiceImpl" additivity="true" level="debug">
        <appender-ref ref="STDOUT"/>
        <appender-ref ref="SAVE-TO-FILE"/>
      </logger>
    </springProfile>

### logback中的fileAppender和rollingFileAppender：  
rollingFileAppender更加的高级，  文件满足多大就新建一个文件。
