- 一个Model类*通常*对应数据库中的一张表
- 一个Model实例对应数据表的一行记录
- Model中的每个属性*通常*对应数据表的一个字段(列名)
- Django给每个Model提供了增删改查的API

Django代码

```python
from django.db import models

class Question(models.Model):
    text = models.CharField(max_length=200)
    pub_date = models.DateTimeField()
```

建表SQL
  - 表名称是app_label + '_' + model类名(小写,下划线分词)
  - id是Django自动帮我们加上的

```mysql
CREATE TABLE `polls_question` (
  `id` int NOT NULL AUTO_INCREMENT,
  `text` varchar(200) NOT NULL,
  `pub_date` datetime(6) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
```

![Question表](01.png)
