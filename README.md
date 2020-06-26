Pycharm方式
![New Project...](01.png)
---
命令行方式
```shell script
mkdir myproject
cd myproject
# 创建虚拟环境
python -m venv venv
# 激活虚拟环境
./venv/Scripts/activate.bat
# 安装依赖
pip install django mysqlclient djangorestframework
# 导出依赖至requirements.txt
pip freeze > requirements.txt
# 创建Django项目
django-admin startproject myproject .
# 创建Django app
django-admin startapp myapp
```
