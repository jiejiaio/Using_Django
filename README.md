当项目配置了这两个app(`django-admin startproject`默认配置): django.contrib.admin 和 django.contrib.auth, 我们便可以通过admin后台来管理用户, 权限 和 组. 

在admin后台可以创建用户, 权限 和 组, 可以把权限添加到组, 可以把权限赋予给用户, 可以给用户分配多个组.

Django会记录下每个用户 **在admin后台**的 对model的操作(User, Group, Permission 都是Model), **超级管理员**(superuser)可以查看所有历史记录, **员工**(staff)可以查看自己的历史记录.

#### 创建用户
注意事项: 如果你希望一个用户能够在admin创建新用户, 那么ta必须同时具有**新增用户**和**修改用户**的权限. 因为: 如果仅靠**新增用户**权限就允许你创建新用户, 那么ta可以通过创建一个超级管理员来间接地获取所有特权.

[给予某个用户**修改用户**的权限]这个动作请三思而后行. 这样做相当于把ta变成超级管理员.  

#### 修改密码
用户的密码不会显示在admin(也不会在数据库存储明文), 但是相关加密方法会显示在admin, 并且可以修改密码
