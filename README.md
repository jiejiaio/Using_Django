Django内置了权限系统

Django admin 管理后台用到了权限系统:
- 查看某类Model, 需要拥有该类Model的`view`或`change`权限
- 新增某类Model, 需要拥有该类Model的`add`权限
- 修改某类Model, 需要拥有该类Model的`change`权限
- 删除某类Model, 需要拥有该类Model的`delete`权限

权限通常针对每一个Model类进行设置. 若想针对某个Model实例, 可以重写`ModelAdmin`类提供的方法:
- `has_view_permission()`
- `has_add_permission()`
- `has_change_permission()`
- `has_delete_permission()`

User对象有两个多对多字段:`groups`(权限组)和`user_permissions`(权限列表):
```python
# 一个用户可以属于多个权限组
myuser.groups.set([group_list])
myuser.groups.add(group, group, ...)
myuser.groups.remove(group, group, ...)
myuser.groups.clear()
# 一个用户可以拥有多个权限
myuser.user_permissions.set([permission_list])
myuser.user_permissions.add(permission, permission, ...)
myuser.user_permissions.remove(permission, permission, ...)
myuser.user_permissions.clear()
```

#### 默认权限
当你为新定义的Model执行`manage.py migrate`时, Django会为该Model创建四种权限: `add`(增),`delete`(删),`change`(改),`view`(查看)

如果我注册了一个app叫做 myapp (`app_label='myapp'`), 并在 myapp 中定义了一个Model类`Blog`, 那么我可以通过如下方法测试用户是否有权限:
- 增: `user.has_perm('myapp.add_blog')`
- 删: `user.has_perm('myapp.delete_blog')`
- 改: `user.has_perm('myapp.change_blog')`
- 查: `user.has_perm('myapp.view_blog')`

#### 权限组
`django.contrib.auth.models.Group`是Django提供的Model, 便于对用户权限进行分类, 换句话说:给用户不同的角色

属于某个权限组的用户,自动获得该组的所有权限; 一个用户可以属于多个权限组

常见应用: 网盘/视频/点餐等app的会员分级, 黄金,白银,普通会员的所享的权益不同; 后台管理系统的不同部门所能接触到的数据不同, 不同职务的操作权限不同

#### 编程式创建权限
我们可以在Model的Meta类中通过`permissions`属性定义[自定义权限](https://docs.djangoproject.com/en/3.0/topics/auth/customizing/#custom-permissions), 也可以直接通过编程的方式创建自定义权限:
```python
from myapp.models import BlogPost
from django.contrib.auth.models import Permission
from django.contrib.contenttypes.models import ContentType

# 获取 BlogPost的 资源类型
blog_post_content_type = ContentType.objects.get_for_model(BlogPost)
# 给该 资源 创建自定义权限, 这个权限将会立刻存入权限表
permission = Permission.objects.create(
    codename='can_publish',  # 在程序中使用的权限名
    name='可以发布文章',  # 用户容易理解的权限名
    content_type=blog_post_content_type,  # 资源类型
)
```

#### 权限缓存
初次检查用户是否有某个权限时, 该用户的所有权限都会被获取到, 并且被ModelBackend缓存起来

如果你给用户增加了一个权限, 然后**马上**检查该用户是否有这个权限, 会发现没有(因为读的是缓存)

解决方案是(从数据库)重新加载该用户:

```python
from django.contrib.auth.models import Permission, User
from django.contrib.contenttypes.models import ContentType
from django.shortcuts import get_object_or_404

from myapp.models import BlogPost

def user_gains_perms(request, user_id):
    user = get_object_or_404(User, pk=user_id)
    # 任何权限校验, 都会导致该用户的所有权限被缓存下来
    user.has_perm('myapp.change_blogpost')

    # 创建一个新权限
    content_type = ContentType.objects.get_for_model(BlogPost)
    permission = Permission.objects.get(
        codename='change_blogpost',
        name='修改博文',
        content_type=content_type,
    )
    # 给用户添加权限
    user.user_permissions.add(permission)

    # 立刻检查用户是否获得了该权限
    user.has_perm('myapp.change_blogpost')  # 并没有

    # 重新查询该用户
    # 注意: user.refresh_from_db() 不会清空权限缓存
    user = get_object_or_404(User, pk=user_id)

    # 权限缓存重新生成了
    user.has_perm('myapp.change_blogpost')  # 有
```
#### 代理Model
代理model的权限机制和普通model是一样的.  
 注意: 普通model的 content type 和 代理model的 content type 不共享, 代理model也不继承普通model的权限
```python
class Person(models.Model):
    class Meta:
        permissions = [('can_change_name', '可以改名')]

class Citizen(Person):
    class Meta:
        proxy = True
        permissions = [('can_change_nationality', '可改变国籍')]

>>> # 要获取代理model的content type, 必须设置 for_concrete_model=False
>>> citizen_content_type = ContentType.objects.get_for_model(Student, for_concrete_model=False)
>>> citizen_permissions = Permission.objects.filter(content_type=citizen_content_type)
>>> [c.codename for c in citizen_permissions]  # 代理model的权限列表
['add_citizen', 'change_citizen', 'delete_citizen', 'view_citizen',
'can_change_nationality']
>>> for permission in citizen_permissions:  # 给用户添加代理model的权限
...     user.user_permissions.add(permission)
>>> user.has_perm('app.add_person')  # 不继承父model的 默认 权限
False
>>> user.has_perm('app.can_change_name')  # 也不继承父model的 自定义 权限
False
>>> user.has_perms(('app.add_citizen', 'app.can_change_nationality'))  # 只有代理model的权限
True
```