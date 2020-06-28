#### 关于Field
- 在Model类中, Field就是类的属性, 对应数据表的字段
- Field属性的命名不能与Django API冲突, 例如`save`, `clean`, `delete`
- 不同种类的Field对应不同类型的数据库字段, 如`CharField`对应`VARCHAR`, `IntegerField`对应`INT`
- Field的class也会影响Html表单的渲染, 不同的Field对应不同的`input`标签
- Field有一些基本的校验规则,例如默认`null=False`,`blank=False`;`CharField`要求指定`max_length`

#### Field 常用参数
##### verbose_name
在前端页面(如admin界面,表单等)显示时, 会自动使用verbose_name
```python
# 对于普通Field, 第一个参数就是 verbose_name
title = models.CharField('标题', max_length=100)
# 对于关系型Field, 第一个参数必须是关联的Model
owner = models.ForeignKey(User, verbose_name='所有者')
```
##### help_text
在表单输入框旁边, 会显示help_text, html标签会原样保留; 也可以仅仅把它当成注释
```python
title = models.CharField('标题', max_length=100, help_text='博文的<em>标题</em>')
```
##### default
默认值, 可以是callable(lambda除外),可以是值,不能是可变对象(list,set...)
```python
title = models.CharField(max_length=100, default='Hello World')
# 错误 callable([]) = False
comments = models.JSONField(default=[])
# 正确 callable(list) = True, 每次新建一个list
comments = models.JSONField(default=list)
# 关系型Field的default 一般 是是对方的pk
owner = models.ForeignKey(User, default=1)
```
##### choices
##### null
##### blank
##### primary_key
##### unique
