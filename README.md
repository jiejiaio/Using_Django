manage.py

```python
def main(commands=None, *ids):
    os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'ReasonableProductivityAPI.settings')
    try:
        from django.core.management import execute_from_command_line
    except ImportError as exc:
        raise ImportError(
            "Couldn't import Django. Are you sure it's installed and "
            "available on your PYTHONPATH environment variable? Did you "
            "forget to activate a virtual environment?"
        ) from exc
    print(sys.argv)
    # python manage.py -> sys.argv = ['...manage.py'] 
    # python manage.py migrate -> sys.argv = ['...manage.py', 'migrate']
    if commands is None or len(sys.argv) > 1:
        execute_from_command_line(sys.argv)
    else:
        for _id in ids:
            execute_from_command_line(f'manage.py {commands[_id]}'.split())


for key, value in {
    'username': 'jiejia',
    'password': 'qweasd',
    'email': 'jiejia@example.com'
}.items():
    # os.environ.setdefault: 如果环境变量不存在, 会使用默认值; 如果存在, 使用已存在的值
    os.environ.setdefault(f'DJANGO_SUPERUSER_{key.upper()}', value)

COMMANDS = {
    1: 'runserver 8000',
    2: 'startapp users',
    3: 'makemigrations',
    4: 'migrate',
    5: 'createsuperuser --no-input --skip-check',
    # 需要 django.contrib.staticfiles 这个app;
    # 如果使用了whitenoise, 并想对static文件进行版本控制, 先注释掉(settings.py) STATICFILES_STORAGE = 'whitenoise.storage.CompressedManifestStaticFilesStorage'
    # 再运行 collectstatic, 生产环境中取消注释, 启动前 先运行 collectstatic
    6: 'collectstatic --no-input', 
    7: 'test',
    8: 'inspectdb XT_用户清单',
    9: 'help',
}

if __name__ == '__main__':
    # main()
    main(COMMANDS, 1)
```