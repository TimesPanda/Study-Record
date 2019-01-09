> 【引言】 对于初学者，在使用数据库连接时，总是不能很好的把握连接工具类的使用，本文将从最开始的搭建到后续不断的完善，结合基础知识的内容来进行对应的处理，使之工具类更加完善，使之java基础知识学到的内容得到广泛应用，涉及到注解、反射等机制
# 编码实现
## 一、普通方式：第一种实现方式
#### 1.用户登录
使用ajax技术传输数据

#### 2.登录的servlet
在后端对数据进行获取，采用```request.getParameter("");```

#### 3.编写数据库连接工具类
  - 3.1 注册驱动，通过反射机制来注册驱动。```Class.forName("驱动全名称");```

  - 3.2 通过驱动管理器获得数据库连接。```DriverManager.getConnection(url,user,password);```
    - 3-2-1 通过配置文件存取相关的```driverName,user,password.```
       ``` InputStream in = JDBCUtils.class.getClassLoader().getResourceAsStream("jdbc.properties");```

  - 3.3 通过```Connction```对象执行预编译语句。```conn.prepareStatement("sql");```

  - 3.4 动态填充值。

  - 3.5 执行查询语句。 ```pstm.executeQuery();```

  - 3.6 获得结果集。```ResultSet```

  - 3.7 根据结果集通过```rs.next()```方法，获取每一条数据内容

    > 以下步骤表示最原始的写法
    >
    > 存在的不足有：
    >
    > （1）方法不能够完全通用，第一个参数无法动态传输，在此基础经过改良，传递了Map<String,Object> ma进来，里面存放的是需要填充的值
    >
    > （2）对rs返回的值不能方便、快速的去进行处理
    >
    > 综上原因，我们开始改良这个数据库工具类 

## 二、不带注解：第三步的改良版本A版本
#### 大致的思路：
- （1）利用反射机制获取对象的属性
- （2）利用注解的方式与数据库字段进行匹配，其目的是防止数据库字段或者实体的字段发生改变后，会程序产生致命性的错误

#### 具体步骤：
- (1)在方法上面新增一个传递参数，为：```Class clz```

- (2)获取所有对象属性
  ```Field[] fields = clazz.getDeclaredFields();```

- (3)通过rs对象获得数据库数据的元数据及其数量
        字段数据：```ResultSetMetaData rsmt = rs.getMetaData();```
        数量：```int column = rsmt.getColumnCount();```

- (4)开始获取数据。```rs.next()```

```java
  while(rs.next()) {
   //操作逻辑
  }
```

- (5)将clz进行实例化，采用```newInstance()```的方式进行实例化

```java
  while(rs.next()) {
   Object obj = clazz.newInstance();
  }
```

- (6)遍历数据库所有的字段信息

```java
  while(rs.next()) {
   Object obj = clazz.newInstance();
   for(int i = 1;i<=column;i++){
      //操作逻辑
   }
  }
```

- (7)在遍历体1里面获取字段所对应的value，比如：userName --- 》 admin

```java
  while(rs.next()) {
   Object obj = clazz.newInstance();
   for(int i = 1;i<=column;i++){
      Object value = rs.getObject(i);
   }
  }
```

- (8)在遍历体1里面再遍历对象的属性

```java
  while(rs.next()) {
   Object obj = clazz.newInstance();
   for(int i = 1;i<=column;i++){
      Object value = rs.getObject(i);
      for(int j=0;j<fields.length;j++){
         //操作数据
      }
   }
  }
```
- (9)获取Field

```java 
   while(rs.next()) {
   Object obj = clazz.newInstance();
   for(int i = 1;i<=column;i++){
      Object value = rs.getObject(i);
      for(int j=0;j<fields.length;j++){
         Field f = fields[j];
         //操作数据
      }
   }
  }
```

- (10)通过field与第3步获取的rsmt的字段进行比较

```java
  while(rs.next()) {
       Object obj = clazz.newInstance();
       for(int i = 1;i<=column;i++){
          Object value = rs.getObject(i);
          for(int j=0;j<fields.length;j++){
             Field f = fields[j];
             if(f.getName().equalsIgnoreCase(rsmt.getColumnName(i))){}
             //操作数据
          }
        }
  }
```

- (11)如果不相同，则不设置值，否则设置值
   通过filed的set方法设置obj和value

```java 
   f.setAccessible(true);
    f.set(obj, value);
    f.setAccessible(flag);
```
代码如下：
```java
 Object obj = clazz.newInstance();
   for(int i = 1;i<=column;i++){
      Object value = rs.getObject(i);
      for(int j=0;j<fields.length;j++){
         Field f = fields[j];
         if(f.getName().equalsIgnoreCase(rsmt.getColumnName(i))){
            boolean flag = f.isAccessible();
	        f.setAccessible(true);
	        f.set(obj, value);
	        f.setAccessible(flag);
         }
      }
   }
}
```

- (12)在rs.next()每次结束前，要将Obj放置到list中，供外部调用

 ```java 
 while(rs.next()) {
   Object obj = clazz.newInstance();
   for(int i = 1;i<=column;i++){
      Object value = rs.getObject(i);
      for(int j=0;j<fields.length;j++){
         Field f = fields[j];
         if(f.getName().equalsIgnoreCase(rsmt.getColumnName(i))){
            boolean flag = f.isAccessible();
	        f.setAccessible(true);
	        f.set(obj, value);
	        f.setAccessible(flag);
         }
      }
   }
   list.add(obj);
}
 ```

## 三、带注解：第三步的改良版本B版本
#### 大致的思路：
- （1）利用反射机制获取对象的属性
- （2）利用注解的方式与数据库字段进行匹配，其目的是防止数据库字段或者实体的字段发生改变后，会程序产生致命性的错误

#### 具体步骤：
- (1)在方法上面新增一个传递参数，为：```Class clz```
- (2)获取所有对象属性
  ```java Field[] fields = clazz.getDeclaredFields();  ```
- (3)通过rs对象获得数据库数据的元数据及其数量
        字段数据：```ResultSetMetaData rsmt = rs.getMetaData();```
        数量：```int column = rsmt.getColumnCount();```
- (4)开始获取数据。```rs.next()```
```java
while(rs.next()) {
   //操作逻辑
}
```
- (5)将clz进行实例化，采用```newInstance()```的方式进行实例化
```java
while(rs.next()) {
   Object obj = clazz.newInstance();
}
```
- (6)遍历数据库所有的字段信息
```java
while(rs.next()) {
   Object obj = clazz.newInstance();
   for(int i = 1;i<=column;i++){
      //操作逻辑
   }
}
```
- (7)在遍历体1里面获取字段所对应的value，比如：userName --- 》 admin
```java
while(rs.next()) {
   Object obj = clazz.newInstance();
   for(int i = 1;i<=column;i++){
      Object value = rs.getObject(i);
   }
}
```
- (8)在遍历体1里面再遍历对象的属性
```java
while(rs.next()) {
   Object obj = clazz.newInstance();
   for(int i = 1;i<=column;i++){
      Object value = rs.getObject(i);
      for(int j=0;j<fields.length;j++){
         //操作数据
      }
   }
}
```
- (9)获取Field
```java
while(rs.next()) {
   Object obj = clazz.newInstance();
   for(int i = 1;i<=column;i++){
      Object value = rs.getObject(i);
      for(int j=0;j<fields.length;j++){
         Field f = fields[j];
         //操作数据
      }
   }
}
```
- (10)通过field与第3步获取的rsmt的字段进行比较  (B版本改良的地方在此处)
  通过注解的属性来与数据库字段名称进行匹配
  改良的地方主要是：原来是通过反射机制获取对象的属性，现在是通过注解的方式+反射机制来获取对象属性的注解（标签），注解类我们在下面讲到
```java
while(rs.next()) {
   Object obj = clazz.newInstance();
   for(int i = 1;i<=column;i++){
      Object value = rs.getObject(i);
      for(int j=0;j<fields.length;j++){
         Field f = fields[j];
         if(f.getName().equalsIgnoreCase(rsmt.getColumnName(i))){}
        //获得注解， FieldDate就是我们自定义注解类
FieldDate fielddate =f.getAnnotation(FieldDate.class);
if(fielddate !=null) {
               	if(fielddate.name().equalsIgnoreCase(rsmt.getColumnName(i))) {
		      boolean flag = f.isAccessible();
		      f.setAccessible(true);
		      f.set(obj, value);
		      f.setAccessible(flag);
		 }
}
         //操作数据
      }
   }
}
```
- (11)如果不相同，则不设置值，否则设置值
   通过filed的set方法设置obj和value
   ```java
    f.setAccessible(true);
    f.set(obj, value);
    f.setAccessible(flag); 
   ```
     代码如下：
```java
while(rs.next()) {
   Object obj = clazz.newInstance();
   for(int i = 1;i<=column;i++){
      Object value = rs.getObject(i);
      for(int j=0;j<fields.length;j++){
         Field f = fields[j];
         if(f.getName().equalsIgnoreCase(rsmt.getColumnName(i))){
            boolean flag = f.isAccessible();
	        f.setAccessible(true);
	        f.set(obj, value);
	        f.setAccessible(flag);
         }
      }
   }
}
```
- (12)在rs.next()每次结束前，要将Obj放置到list中，供外部调用
 ```java
 while(rs.next()) {
   Object obj = clazz.newInstance();
   for(int i = 1;i<=column;i++){
      Object value = rs.getObject(i);
      for(int j=0;j<fields.length;j++){
         Field f = fields[j];
         if(f.getName().equalsIgnoreCase(rsmt.getColumnName(i))){
            boolean flag = f.isAccessible();
	        f.setAccessible(true);
	        f.set(obj, value);
	        f.setAccessible(flag);
         }
      }
   }
   list.add(obj);
}
 ```
#### 关于第三步的改良版本的B版本，注解的使用：
- （1）创建一个注解类，该类名称叫做：FieldDate
```java
@Target({ElementType.FIELD})
@Retention(RetentionPolicy.RUNTIME)
public @interface FieldDate {
	 String name() default "";
}
```
 ```@Target``` 表示注解应用到什么地方，比如：方法、属性、类
 ```@Retention``` 表示在什么时间点启动这个注解，也就是使之生效
- （2）要在对象属性上面标记注解： ```@FieldDate(name=”你的数据库字段名”)```

总结：实现注解很简单，难点在于怎么结合反射机制来对注解的属性赋予新的含义。
案例说明：把FieldDate --- > name 属性与数据库字段进行结合，有效的防止字段改动或者对象属性改动导致数据库数据无法与实体匹配。通过我们之前学到的```@WebServlet```，我们应该联想到servlet的url，也是对注解场景进行深层次处理。
（mybatis注解方式）	
```java
  @Select("select * from mybatis_Student")
	@Results({
		@Result(id=true,property="id",column="id"),
		@Result(property="name",column="name"),
		@Result(property="age",column="age")
	})
	public List<Student> getAllStudents();
```
