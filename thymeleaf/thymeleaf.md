## 1.在使用thymeleaf模板的时候，采用了easyUI的表格渲染，这个是否发现字段无法解析的情况
>  org.thymeleaf.exceptions.TemplateProcessingException: Could not parse as expression:
```
采用的处理方式：
1、[[]]是thymeleaf的内联表达式，可以在cols的后面换行
2、在script标签里 th:inline="none" （我采用第二种方式解决）
```
