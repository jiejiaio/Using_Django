Django处理请求的步骤:
1. request中有没有`urlconf`属性(`HttpRequest.urlconf`)?  
&nbsp;&nbsp;有: 使用指定的`urlconf`  
&nbsp;&nbsp;无: 使用settings.py中的`ROOT_URLCONF`  
2. 导入`urlconf`中的`urlpatterns`变量  
&nbsp;&nbsp;`urlpatterns`通常是个`list`  
&nbsp;&nbsp;`urlpatterns`中的元素是django的`path`或`re_path`    
3. 遍历`urlpatterns`, 逐个匹配URL  
&nbsp;&nbsp;请求的url存放在`HttpRequest.path_info`属性中  
&nbsp;&nbsp;匹配到之后即停止遍历  
4. 匹配成功后, Django会调用相应的视图(view)来处理请求, 两种数据会传递给view:  
&nbsp;&nbsp;`HttpRequest`实例  
&nbsp;&nbsp;匹配了urlpattern中的正则的参数, 包括有名字的参数和没名字的参数  
5. 如果第3步没有匹配到, 或第4步抛出了异常, Django会调用特定的视图(views), 这些视图专门用于处理异常

```python
def year_archive(request, num):
    pass
def month_archive(request, **kwargs):
    pass
urlpatterns = [
    path('articles/2003/', views.special_case_2003),
    # 会给view传递一个位置参数(Positional Argument)
    re_path(r'^articles/([0-9]{4})/$', views.year_archive),
    # 会给view传递两个关键字参数(Keyword Argument)
    path('articles/<int:year>/<int:month>/', views.month_archive),
    path('articles/<int:year>/<int:month>/<slug:slug>/', views.article_detail),
]
```