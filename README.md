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
owner = models.ForeignKey(User, on_delete=models.CASCADE, verbose_name='所有者')
```
##### help_text
在表单输入框旁边, 会显示help_text, html标签会原样保留; 也可以仅仅把它当成注释
```python
body = models.TextField('正文', help_text='博客的<em>正文</em>')
```
##### default
默认值, 可以是callable(lambda除外),可以是值,不能是可变对象(list,set...)
```python
is_staff = models.BooleanField(default=False)
# 错误 callable([]) = False
comments = models.JSONField(default=[])
# 正确 callable(list) = True, 每次新建一个list
comments = models.JSONField(default=list)
# 关系型Field的default 一般 是对方的pk
owner = models.OneToOneField(User, on_delete=models.CASCADE, default=1)
```
##### choices
选项(choices) 由一系列 两个元素的tuple 组成, 在Html页面上显示为`select`标签.
tuple的第一个元素是实际存储的值, 第二个元素是显示给用户看的
```python
class Task(models.Model):
    status = models.PositiveSmallIntegerField(default=1, choices=models.IntegerChoices('任务状态', '可接取 进行中 已完成').choices)
# get_FOO_display()
>>> Task().status
1
>>> Task().get_status_display()
'可接取'
```
##### null
默认为`False`; 如果为`True`, Django会在存`None`到数据库时使用`NULL`  
用`CharField`举例:  
&emsp;无论`null=True`还是`False`,如果`CharField`的值是空字符串`''`, 存到数据库也是空字符串`''`  
&emsp;如果 `null=False`: 如果`CharField`的值是`None`, 存到数据库会报错  
&emsp;如果 `null=True`: 如果`CharField`的值是`None`, 存到数据库是`NULL`
##### blank
默认为`False`; 如果为`True`, Django将允许用户输入空值  
`blank`仅仅跟表单校验有关, 为`True`时允许用户不填, 为`False`时要求用户必填  
开发者直接对Field赋值(如 `title=''`)不会受到`blank`的限制
##### primary_key
##### unique
