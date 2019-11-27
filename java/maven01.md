### maven
    mvn verify      #验证包有效性   如果没有会下载     相当于先package再验证
    mvn clean  # 会把target 文件夹也删掉
    mvn compile #编译  没有jar文件
    mvn test #编译并测试
    mvn package #有jar文件  生成target目录，编译、测试代码，生成测试报告，生成jar/war文件
    mvn eclipse:eclipse #  构建eclipse结构,然后ls -a查看（因为.project .classpath是隐藏的）
    mvn idea:idea # 构建idea结构
    mvn archetype:generate #构建结构 例如web     这个命令如果不是pom文件，那么无效(例如jar就无效)
    mvn dependency:tree     #打印依赖树
    mvn help:effective-pom  # 看这个“有效的 (effective)”POM，它暴露了 Maven的默认设置
    mvn help:describe -Dplugin=exec -Dfull   # 列出所有 Maven Exec 插件可用的目标
    mvn help:describe -Dplugin=help #使用 help 插件的  describe 目标来输出 Maven Help 插件的信息
    mvn help:describe -Dplugin=compiler -Dmojo=compile -Dfull #获取单个目标的信息,设置  mojo 参数和  plugin 参数。此命令列出了Compiler 插件的compile 目标的所有信息
    mvn checkstyle:check #检查  即使失败  也不一定是错   加上-e -X可以打印 详细的信息
    mvn help:effective-settings      #查看仓库位置  默认是~/.m2/repository

### maven常用命令:
    maven查看依赖tree命令：dependency:tree
    maven生成结构命令：mvn archetype:generate -DgroupId=com.chushiyun -DartifactId=mavendemo -Dversion=1.0.0 -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    maven查看profile命令：mvn -help
    maven插件的help命令：mvn javadoc:help (语法是mvn pluginname:goal，javadoc自己就有help这个goal，所以这样写)
    maven查看插件所有参数：mvn war:help -Detail(或者-Ddetail=true)
    maven查看插件某个goal的参数：mvn war:help -Detail -Dgoal=war
    maven通用查看插件的方法：mvn help:describe -Dplugin=org.apache.maven.plugins:maven-war-plugin
    maven通用查看插件的方法(因为是自带的插件，所以可以直接写一个war)：mvn help:describe -Dplugin=war

### maven手动添加jar：
    mvn install:install-file    -Dfile=functions-1.1.2.jar  -DgroupId=jp.sf.amateras.func  -DartifactId=functions       -Dversion=1.1.2                -Dpackaging=jar


### maven中optional和exclusions的区别
    Optional和Exclusions都是用来排除jar包依赖使用的，两者在使用上却是相反。

    Optional定义后，该依赖只能在本项目中传递，不会传递到引用该项目的父项目中，父项目需要主动引用该依赖才行。

    Exclusions则是主动排除子项目传递过来的依赖。

### runtime和provide的区别
provide在编译，测试阶段用到，但是不打包。 runtime在test和runtime的时候用到，也是不打包。

### 查看一个插件下有多个少goal，就看有多少mojo类即可。
查看compiler插件下有几个goal??  使用命令行可以，去类里面看也可以。
查看compiler的compile(这个goal)可以使用哪些参数??   命令列出的都是可以使用的，去类里面也是可以的。如果没有，就去父类找。AbstractCompilerMojo是主要抽象类，基本属性从这里看即可。

### maven报错：Failed to execute goal org.apache.maven.plugins:maven-compiler-plugin:3.1:compile
9成是jdk问题，很有可能是run configuration中的jre，在jdk修改之后没有再改，造成的，重新配置下即可。

### maven报错:org.apache.maven.archiver.MavenArchiver.getManifest(org.apache.maven.project.MavenProject
org.apache.maven.archiver.MavenArchiveConfiguration)
其实是spring-boot-starter-parent  版本不对。

### maven顶级元素：
```
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                          https://maven.apache.org/xsd/settings-1.0.0.xsd">
  <localRepository/>
  <interactiveMode/>
  <usePluginRegistry/>
  <offline/>
  <pluginGroups/>
  <servers/>
  <mirrors/>
  <proxies/>
  <profiles/>
  <activeProfiles/>
</settings>
```

### 安装mvnw:
    mvn -N io.takari:maven:wrapper;
    mvn -N io.takari:maven:wrapper -Dmaven=3.3.3; #表示使用maven 3.3.3版本

### maven下载源码：
    mvn:dependency:sources
    或者
    <profiles>
    <profile>
        <id>downloadSources</id>
        <properties>
            <downloadSources>true</downloadSources>
            <downloadJavadocs>true</downloadJavadocs>
        </properties>
    </profile>
    </profiles>

    <activeProfiles>
      <activeProfile>downloadSources</activeProfile>
    </activeProfiles>

### maven下载doc：
mvn dependency:resolve -Dclassifier=javadoc
