Django通过 [auth][1] 模块来处理用户的**认证**(你是谁?)和**授权**(你能做什么?)

[auth][1]模块包括:
- 用户
- 权限
- 权限组(角色)
- 密码加密解密
- 登录注册等功能的表单和视图
- 可替换的 Authentication Backend (存储并进行用户认证的方案, 例如数据库, 内存, LDAP, OAuth)


`django-admin startproject` 做了什么auth配置:
```python
# settings.py
INSTALLED_APPS = [
    ...
    # django 认证框架的核心, 包括 用户,权限,组 等Model
    'django.contrib.auth',
    # Django 的 content type 系统, 将 Model 与 权限 关联上
    'django.contrib.contenttypes',
]
MIDDLEWARE = [  # 中间件
    ...
    # 启用 session (客户端session或服务端session)
    'django.contrib.sessions.middleware.SessionMiddleware',
    # 借助 session 将用户绑到每个请求上
    'django.contrib.auth.middleware.AuthenticationMiddleware',
]
AUTH_PASSWORD_VALIDATORS = [  # 密码校验
    # 和其他属性相似
    {'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',},
    ... MinimumLength ... ,  # 太短
    ... CommonPassword ... ,  # 过于常见
    ... NumericPassword ... ,  # 纯数字
]
```

[1]: https://docs.djangoproject.com/en/3.0/ref/contrib/auth/