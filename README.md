#### Web 请求的认证
Django使用 [session](https://docs.djangoproject.com/en/3.0/topics/http/sessions/) 中间件来关联 认证系统 和 [request](https://docs.djangoproject.com/en/3.0/ref/request-response/#django.http.HttpRequest) 对象

每个请求都有`request.user`属性, 如果用户尚未登录, 这个属性会被设为 [AnonymousUser](https://docs.djangoproject.com/en/3.0/ref/contrib/auth/#django.contrib.auth.models.AnonymousUser) 实例; 如果已登录, 则是 [User](https://docs.djangoproject.com/en/3.0/ref/contrib/auth/#django.contrib.auth.models.User) 实例.

```python
if request.user.is_authenticated:
    # 已登录, 已认证的用户    
    ...
else:
    # 未登录 未认证的 匿名用户
    ...
```

#### 如何实现登录
登录的过程就是验证用户证明(Credentials), 然后将已认证用户绑定到session的过程  
##### 使用`login(request, user, backend=None)`
通常我们会在view函数中使用`login()`方法, 该方法会把用户的id保存到session中. 用户登录前保存在session中的数据, 登录后依然保留.

下列代码同时使用了`authenticate()`和`login()`:
```python
from django.contrib.auth import authenticate, login

def my_view(request):
    user = authenticate(request, username=request.POST['username'], password=request.POST['password'])
    if user is not None:
        login(request, user)
        # 可以返回一个重定向(Redirect), 到登录成功页面
        ...
    else:
        # 返回错误信息或错误页面
        ...
```

#### 选择 authentication backend
用户登录后, 用户 id 和用来验证用户的 backend 会被存到 session 中, 这样允许使用多种方式来认证用户, 不同方式认证的用户的数据从对应的 backend 中取.

Django 按照如下顺序选择 authentication backend:
1. 如果`login(request, user, backend=None)`中的 backend 非空, 使用该 backend.
2. 如果`user.backend`属性存在, 则使用它. `authenticate()`方法会设置该属性. 如此便可将`authenticate()`和`login()`连起来使用.
3. 如果`AUTHENTICATION_BACKENDS`(settings.py)中仅包含一个元素, 使用它.
4. 若上述都没有, 抛异常

在1和2中, backend应是字符串, 例如:`backend='django.contrib.auth.backends.ModelBackend'`, 而非
```python
from django.contrib.auth.backends import ModelBackend
backend=ModelBackend
```