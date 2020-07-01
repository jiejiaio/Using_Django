#### **User** 对象的主要属性:
- username - 用户名
- password - 密码
- email - 邮箱
- first_name - 名字
- last_name - 姓氏

还有其他属性, 详见 [User](https://docs.djangoproject.com/en/3.0/ref/contrib/auth/#django.contrib.auth.models.User)

#### 创建用户
```python
>>> from django.contrib.auth.models import User
# create_user() 会创建User对象 并立刻保存到数据库
>>> user = User.objects.create_user('用户名', '邮箱', '密码')
# 修改姓氏
>>> user.last_name = 'Lennon'
# 再次保存到数据库
>>> user.save()
```

#### 创建超级用户
交互式创建超级用户
```shell script
# 会要求输入用户名 邮箱 密码
python manage.py createsuperuser
# 会要求输入密码
python manage.py createsuperuser --username=joe --email=joe@example.com
```
编程式创建超级用户, 参见[懒人运行manage.py的方法](https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C-%E6%87%92%E4%BA%BA%E8%BF%90%E8%A1%8Cmanage.py%E7%9A%84%E6%96%B9%E6%B3%95)

#### 修改密码
Django不存储明文密码, 直接修改数据库密码是不方便的, 除非你知道[Django的加密机制](https://docs.djangoproject.com/en/3.0/topics/auth/passwords/#how-django-stores-passwords)  
修改密码的几种方式:
- 交互式: `python manage.py changepassword 用户名`可以修改用户密码, 会提示你输入密码和确认密码
- 编程式
```python
>>> from django.contrib.auth.models import User
>>> u = User.objects.get(username='用户名')
>>> u.set_password('新密码的明文')
>>> u.save()
```
- 在 admin 管理后台修改
- 使用Django提供的 [views](https://docs.djangoproject.com/en/3.0/topics/auth/default/#built-in-auth-views) 和 [form](https://docs.djangoproject.com/en/3.0/topics/auth/default/#built-in-auth-forms)

修改密码后将会自动登出用户session

#### 对登录用户进行认证(Authenticate)
**authenticate(request=None, \*\*credentials)**  

要想验证你是我的网站的注册用户, 你需要提供一些**证明(credentials)**, 例如 Django默认组合:用户名+密码, 手机号+短信验证码, 邮箱+密码

Django会把这些证明交给**Authentication Backend**去验证(如ModelBackend会去匹配数据库记录), 如果匹配, 则认证成功, 返回User对象

如果没有匹配,或抛出`PermissionDenied`(权限不足)异常, 会返回`None`

```python
from django.contrib.auth import authenticate
user = authenticate(username='用户名', password='密码明文')
if user is None:
    # 认证失败
else:
    # 认证成功
```

`authenticate(...)`是底层API, 通常只有在你自定义 **Authentication Backend** 时才需要用到.
如果你只想实现登录, 可以使用 [LoginView](https://docs.djangoproject.com/en/3.0/topics/auth/default/#django.contrib.auth.views.LoginView)