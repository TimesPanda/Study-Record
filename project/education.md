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

### 2.数据库结构与TopJUI菜单图标适配问题
```
在TopJUI框架中，二级图标默认的时iconCls,且是默认获取json数据对象中的此属性，当我们从数据库取出来字段时，必须严格按照此格式。
因为原数据库中的图标字段为icon，因此不适配，所以需要修改TopJUI中核心的Js文件。查看css代码后，发现字段，于是找到核心文件进行修改‘topjui.core.min.js’
（在3146行已经标注）修改如下：
=======================================================================
/**自定义修改：适配iconCls图标，因为数据库中取出来的数据为icon，与原始框架的数据不符合，因此添加一个选项:'<span class="tree-icon tree-file ' + (k.iconCls ? k.iconCls: "") +" "+ (k.icon ? k.icon: "") +'"></span>'**/
                    if ("closed" == k.state ? (h.push('<span class="tree-hit tree-collapsed"></span>'), h.push('<span class="tree-icon tree-folder ' + (k.iconCls ? k.iconCls: "") + '"></span>')) : k.children && k.children.length ? (h.push('<span class="tree-hit tree-expanded"></span>'), h.push('<span class="tree-icon tree-folder tree-folder-open ' + (k.iconCls ? k.iconCls: "") + '"></span>')) : (h.push('<span class="tree-indent"></span>'), h.push('<span class="tree-icon tree-file ' + (k.iconCls ? k.iconCls: "") +" "+ (k.icon ? k.icon: "") +'"></span>')), this.hasCheckbox(b, k)) {
                        var m = 0;
                        i && "checked" == i.checkState && g.cascadeCheck ? (m = 1, k.checked = !0) : k.checked && a.easyui.addArrayItem(f.tmpIds, k.domId),
                        k.checkState = m ? "checked": "unchecked",
                        h.push('<span class="tree-checkbox tree-checkbox' + m + '"></span>')
                    }
多添加一个适配选项即可！
=========================================================================
*****由图标引申到另外一个对象打印问题：
var property = ""; 
for (var item in k) {
    property += "属性：" + item + "数值：" + k[item] + "\n";
}
console.info("k:"+k.icon);
```

### 3.数据库数据
```
【Question】Cause: java.sql.SQLException: Zero date value prohibited
【cause&method】
jdbc:mysql://yourserver:3306/yourdatabase?zeroDateTimeBehavior=convertToNull
设置zeroDateTimeBehavior 属性，当遇到DATETIME值完全由0组成时，最终的有效值可以设置为，异常(exception)，一个近似值(round)，或将这个值转换为null(convertToNull)。
出现0000-00-00 属于一个无效日期，用convertToNull属性即可
```
