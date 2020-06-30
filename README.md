Django使用它自定义的 [django.core.files.File](https://docs.djangoproject.com/en/3.0/ref/files/file/#django.core.files.File) 而非Python的[file object](https://docs.python.org/3/glossary.html#term-file-object) 

一般情况下使用Django的`File`就足够了, 我们可以在Python的`file object`的基础上构造一个Django的`File`对象
```python
>>> from django.core.files import File

# 使用open()创建一个Python的file object
>>> f = open('/path/to/hello.world', 'w')
# 接着构造一个Django的File对象
>>> myfile = File(f)
```
上面这个方法构造的文件流是不会自动关闭的, 如果很多文件流没有被关闭, 可能会导致如下错误:
```shell script
OSError: [Errno 24] Too many open files```
```
所以推荐使用以下方法:
```python
>>> from django.core.files import File
# 使用 with 语句
>>> with open('/path/to/hello.world', 'w') as f:
...     myfile = File(f)
...     myfile.write('Hello World')
...
>>> myfile.closed  # with 语句结束后自动关闭文件流
True
>>> f.closed
True
```