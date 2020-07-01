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
Django默认会为所有已注册的app中的Model创建`add`(增),`delete`(删),`change`(改),`view`(查看) 四种权限

当你为新定义的Model执行`manage.py migrate`时, Django会为该Model创建默认权限

如果我注册了一个app叫做blogs (`app_label='blogs'`), 并在blogs app中定义了一个Blog Model, 那么我可以通过如下方法测试用户是否有权限:
- 增: `user.has_perm('blogs.add_blog')`
- 删: `user.has_perm('blogs.delete_blog')`
- 改: `user.has_perm('blogs.change_blog')`
- 查: `user.has_perm('blogs.view_blog')`

#### 权限组
`django.contrib.auth.models.Group`是Django提供的Model, 便于对用户权限进行分类, 换句话说:给用户不同的角色

属于某个权限组的用户,自动获得该组的所有权限; 一个用户可以属于多个权限组

常见应用: 网盘/视频/点餐等app的会员分级, 黄金,白银,普通会员的所享的权益不同; 后台管理系统的不同部门所能接触到的数据不同, 不同职务的操作权限不同

#### 编程式创建权限


#### 权限缓存
#### 代理Model