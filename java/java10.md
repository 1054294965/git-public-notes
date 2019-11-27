###  restTemplate模拟超时(Read timed out)(用代码实现)
HttpComponentsClientHttpRequestFactory httpRequestFactory = new HttpComponentsClientHttpRequestFactory();
            httpRequestFactory.setConnectionRequestTimeout(3000);
            httpRequestFactory.setConnectTimeout(3000);
            httpRequestFactory.setReadTimeout(3000);
        ResponseEntity forObject = new RestTemplate(httpRequestFactory).getForObject("http://localhost:8081/response/sleep", ResponseEntity.class);


### svn报错：Unable to connect to a repository at URL
很有可能是url地址不对，有可能是http地址写成了https地址。

### win7删除svn目录：
  C:\Users\Administrator\AppData\Roaming\Subversion\auth?
  红字处要换成对应的用户名。
  C:\Users\chushiyun\AppData\Roaming\Subversion\auth

### svn删除缓存信息：
    如果是javaHL删除C:\Users\chushiyun\AppData\Roaming\Subversion\auth
    如果是svnkit删除D:\eclipse\configuration\org.eclipse.core.runtime下的所有

### svn报错(文件夹已过期)：(eclipsesvn插件式site*.jar这些都是eclipse插件)
    最可能的原因是svn插件版本太低，下载对应版本的插件放到dropins下即可。
    版本是有对照关系的,例如安装的是tortoisesvn1.8,site最少需要1.10以上，低版本就会报错。
    svn比较合并选择CollabNet Desktop
    svn接口选择javaHL

    1、可能是文件夹确实不存在，
    2、更可能是密码错误
    退出eclipse 重新进入就会要求重新输入密码
    3、高级目录没有权限，但是低级目录正在被依赖，所以会报这个错
    解决方案，不要管高级目录，低级目录不影响使用即可。
