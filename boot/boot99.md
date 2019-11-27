### jpa报错---The server time zone value 'й' is unrecognized or represents more than one time zone. You
    报错信息：
        The server time zone value '?й???????' is unrecognized or represents more than one time zone. You must configure either the server or JDBC driver (via the serverTimezone configuration property) to use a more specifc time zone value if you want to utilize time zone support.

    原因：
    在使用mysql的jdbc驱动最新版（6.0+）版本时，数据库和系统时区差异引起的问题。
    解决办法：
    1.一种是降版本，并不推荐，如果需要降版本5.5版本可以满足基本需要；
    2.还有一种是在jdbc连接的url后面加上`serverTimezone=UTC`或GMT即可，如果需要指定使用gmt+8时区，需要写成GMT%2B8，不然可能会报错误，解析为空

    示例如下：
    jdbc.url=jdbc:mysql://localhost:3306/demo?serverTimezone=UTC&characterEncoding=utf-8

    有时会出现一种情况：就是有的url可以不用加，有的用加。 例如服务器的url不用加，localhost的用加，这是因为服务器已经有了时区的设置，localhost却没有。


### springboot直接引入spring-boot-starter的坑
pom.xml是这样的:   
```
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter</artifactId>
</dependency>  
```
注意这个 spring-boot-starter 会自动装备很多东西，如果对springboot不是很熟悉，很容易出问题，建议用到什么添加什么比较好。
