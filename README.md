#### 如何实现登出
##### 使用`logout(request)`
在view函数中的使用示例:
```python
from django.contrib.auth import logout

def logout_view(request):
    logout(request)  # logout()没有返回值
    # 重定向 到 登出成功页面
```
如果用户并未登录, `logout()`不会抛异常

登出后, 用户的session将会被清空. 如果你想在session中保存**登出后也可用**的数据, 放在`logout()`后面去保存
