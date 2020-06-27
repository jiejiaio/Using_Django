```python
# ./settings.py
SECRET_KEY = os.getenv('SECRET_KEY', '7&1y4zwt45)!g0t1%p^*%1kmn3n6)t*-ertsns1*du72*www(1')
# 注意 bool('False') = True
DEBUG = os.getenv('DEBUG', 'True') != 'False'
ALLOWED_HOSTS = ['*']
INSTALLED_APPS = [
    ...
    'rest_framework',
]
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'dbname',
        'HOST': 'localhost',
        'PORT': 3306,
        'USER': 'root',
        'PASSWORD': os.getenv('MYSQL_PASSWORD', '123456'),
    } if os.getenv('PRODUCTION', 'False') == 'True' else {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
    # import platform
    # if platform.system() == 'Linux'
}
LANGUAGE_CODE = 'zh-hans'
TIME_ZONE = 'Asia/Shanghai'
STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'static/')
MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'media/')
# ./urls.py 开始
from django.conf import settings
from django.conf.urls.static import static
urlpatterns = [
    ...
] + static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
+ static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
# urls.py 结束
AUTH_USER_MODEL = 'users.User'
LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'formatters': {
        'verbose': {
            'format': '{asctime} {levelname:7} {name:18} {threadName:8} {message}',
            'style': '{',
        },
    },
    'handlers': {
        'console': {
            'class': 'logging.StreamHandler',
            'formatter': 'verbose',
        },
        'file': {
            'level': os.getenv('DJANGO_LOG_LEVEL', 'DEBUG'),
            'class': 'logging.FileHandler',
            'filename': os.path.join(BASE_DIR, 'myproject.log'),
            'formatter': 'verbose',
        },
    },
    'root': {
        'handlers': ['console', 'file'],
        'level': os.getenv('DJANGO_LOG_LEVEL', 'DEBUG'),
    },
    'loggers': {
        'django': {
            'handlers': ['console', 'file'],
            'level': os.getenv('DJANGO_LOG_LEVEL', 'DEBUG'),
            'propagate': False,
        },
        'django.utils.autoreload': {
            'handlers': ['console'],
            'level': 'WARNING',
            'propagate': False,
        },
    },
}
```