# 项目记录
## 进展记录
### 1.2019.03.28

```
1.完成education项目搭建工作
2.完成education项目的讲师列表、讲师表、枚举表定义、银行账户字典表的定义
```

## 问题记录
### 1.模板无法找到的问题
> template might not exist or might not be accessible by any of the configured Template Resolvers
```
可能的原因是：在控制器层没有找到对应的解析快，请检查是否标注注解，@Controller或者@RestController，如果使用@Controller返回json时，需要添加@RequestMapper
```
