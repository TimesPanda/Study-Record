### 1.如何修改maven项目中JDK原始版本信息
- 在POM中修改
```xml
<build>  
        <plugins>  
            <plugin>  
                <groupId>org.apache.maven.plugins</groupId>  
                <artifactId>maven-compiler-plugin</artifactId>  
                <version>3.1</version>  
                <configuration>  
                    <source>1.8</source>  
                    <target>1.8</target>  
                </configuration>  
            </plugin>  
        </plugins>  
</build>
```
- 在maven配置中心修改
```xml
<profile>    
    <id>jdk-1.8</id>    
     <activation>    
          <activeByDefault>true</activeByDefault>    
          <jdk>1.8</jdk>    
      </activation>    
<properties>    
<maven.compiler.source>1.8</maven.compiler.source>    
<maven.compiler.target>1.8</maven.compiler.target>    
<maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>    
</properties>    
</profile>
```
### 2.新建的项目遇到未知错误
```xml
主要原因是jar的问题导致，一般是采用将jar版本换取即可，本文记录的原因是因为采用了spring-boot的2.1.5的版本导致出现这个问题，修改版本为2.1.2即可。这个问题衍生的问题导致查询：
有一种说法是删除仓库中所有下载失败的文件：
linux下

~/.m2 -name "*.lastUpdated" -exec grep -q "Could not transfer" {} \; -print -exec rm {} \;

window下

cd %userprofile%\.m2\repository
for /r %i in (*.lastUpdated) do del %i

然后右击你的工程，Maven->"Update Project ..."，即可解决
```
