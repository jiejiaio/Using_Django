Django默认使用本地操作系统的文件系统API来操作文件, 我们也可以自己实现一些其他的存储方式, 如OSS, CDN, FTP

Django的文件存储方式由`DEFAULT_FILE_STORAGE`决定, 默认为`django.core.files.storage.FileSystemStorage`

##### Storage 对象
Storage:存储, 并非对应某种具体的文件存储方式(本地文件存储, 网络文件存储, 对象存储...), 而是统一抽象出来的接口  
通常使用`File`对象便已足够, `File`对象会调用合适的`Storage`(存储方式); 我们也可以直接使用`Storage`API

```python
>>> from django.core.files.base import ContentFile
# 全局默认文件存储
>>> from django.core.files.storage import default_storage
# 保存文件
>>> path = default_storage.save('path/to/file', ContentFile(b'new content'))
>>> path
'path/to/file'
>>> default_storage.size(path)  # 文件大小
11
>>> default_storage.open(path).read()  # 读取文件
b'new content'
>>> default_storage.delete(path)  # 删除文件
>>> default_storage.exists(path)  # 是否存在
False
```

##### FileSystemStorage - Django默认的文件系统存储
`FileSystemStorage`是`Storage`的一个具体实现, 实现了针对**本地文件系统**的文件相关操作  
我们可以在使用`FileField`,`ImageField`时指定`storage`, 
```python
from django.core.files.storage import FileSystemStorage
from django.db import models

# FileSystemStorage的location默认使用MEDIA_ROOT的设置, 我们也可以自己定义
fs = FileSystemStorage(location='/media/photos')

class Car(models.Model):
    ...
    photo = models.ImageField(upload_to='cars', storage=fs)  # 文件将会存储至'/media/photos/cars'
```
---
我们也可以自定义实现其他存储方式, 参见[自定义存储系统](https://docs.djangoproject.com/en/3.0/howto/custom-file-storage/)
