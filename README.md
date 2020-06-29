Django默认将(用户上传)文件存放在`MEDIA_ROOT`, 访问时以`MEDIA_URL`作为根路径

在Model中, 可以使用`FileField`或`Imagefield`来代表用户上传的文件,并提供了一系列文件操作API

```python
from django.db import models

class Car(models.Model):
    name = models.CharField(max_length=255)
    price = models.DecimalField(max_digits=5, decimal_places=2)
    # 保存到 MEDIA_ROOT + 'cars/' + 文件名
    photo = models.ImageField(upload_to='cars/')
    # 保存到 MEDIA_ROOT + 'cars/2020/07/04/' + 文件名
    photo = models.ImageField(upload_to='cars/%Y/%m/%d/')
```

```python
>>> car = Car.objects.get(name="57 Chevy")
>>> car.photo  # FieldFile 对象
<ImageFieldFile: cars/chevy.jpg>
>>> car.photo.name  # FieldFile.name 文件相对于 MEDIA_ROOT的 路径 
'cars/chevy.jpg'
>>> car.photo.path  # 文件在操作系统中的绝对路径 FieldFile.path
'/media/cars/chevy.jpg'
>>> car.photo.url  # 可访问该图片的url
'http://media.example.com/cars/chevy.jpg'
```

Django会在保存Model到数据库的同时保存文件; 重命名已保存的文件 示例:
```python
>>> import os
>>> from django.conf import settings
>>> initial_path = car.photo.path  # 原路径
>>> car.photo.name = 'cars/chevy_ii.jpg'  # 相对于MEDIA_ROOT的路径
>>> new_path = settings.MEDIA_ROOT + car.photo.name  # 新绝对路径
>>> os.rename(initial_path, new_path)  # 移动文件
>>> car.save()  # 重新保存
>>> car.photo.path  # 保存后的绝对路径
'/media/cars/chevy_ii.jpg'
>>> car.photo.path == new_path
True
```

对于`ImageField`, 它的宽`width`,高`height`,文件大小`size`可以直接得到, 实际图片数据则需要`open()` 
```python
>>> from PIL import Image
>>> car = Car.objects.get(name='57 Chevy')
>>> car.photo.width  # 宽
191
>>> car.photo.height  # 高
287
>>> image = Image.open(car.photo)  # 打不开
# Raises ValueError: seek of closed file.
>>> car.photo.open()  # 调用open()才能打开
<ImageFieldFile: cars/chevy.jpg>
>>> image = Image.open(car.photo)
>>> image
<PIL.JpegImagePlugin.JpegImageFile image mode=RGB size=191x287 at 0x7F99A94E9048>
```