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
