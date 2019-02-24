#### 1.springboot实现热部署
- 在pom文件中添加依赖
```xml
<dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <optional>true</optional>
</dependency>
```
- 设置项目为自动发布
```
以eclipse为例：project-->build Automatically
intellij编辑器：File -> Settings -> Build,Execution,Deplyment -> Compiler，选中打勾 “Build project automatically” 
```

#### 2、在使用springboot集成包的一些问题
描述：今日在使用maven多项目管理时，因为父工程依赖了‘mybatis-spring-boot-starter’包等其他依赖包，而这些包中存在JDBC链接，新建一个web项目时，因为无需链接数据库，在启动的时候会存在DataSource无法找到的问题
```
解决此类问题
（1）需要严格看清依赖包中所有的依赖项，否则将导致启动的时候，因为依赖了JDBC，所以springboot项目会去寻找配置文件中的DataSource属性
（2）如果涉及到多个工程，记得把非相关的依赖放置到对应的项目中，不要作为全局
（3）依赖包时，多看依赖项，不要盲目的多添加jar进来
```
