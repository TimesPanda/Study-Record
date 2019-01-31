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
