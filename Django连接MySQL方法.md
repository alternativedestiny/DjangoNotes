# Django连接MySQL方法

## 参考资料

- http://blog.csdn.net/Sunshine_ZCC/article/details/73918408
- http://www.runoob.com/django/django-tutorial.html
- https://www.cnblogs.com/yuyang26/p/7411269.html

## 环境

- windows10
- pycharm2017.3.3 professional edition(必须专业版)
- python3.6.4
- django2.0.2

## 配置方法

默认已安装好Python MySQL Django

1. 安装mysqlclient
    ```cmd
    pip install mysqlclient
    ```
2. 连接数据库设置 settting.py文件
    ```python
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.mysql',
            'NAME': 'data1',  # 数据库名称
            'HOST':'',  # 主机地址
            'PORT':'3306',  # 端口号
            'USER':'xxxx',  # 用户名
            'PASSWORD':'xxxxxx',  # 密码
        }
    }
    ```
3. 创建模型 models.py文件
    ```python
    from django.db import models
    # Create your models here.
    class Test(models.Model):
        name = models.CharField(max_length=20)
    ```

4. 注册模型 admin.py文件
    ```python
    from django.contrib import admin
    from TestModel.models import Test
    # Register your models here.
    admin.site.register(Test)
    ```

5. 创建表结构，在项目文件夹目录的命令行运行
    ```python
    python manage.py makemigrations  # 让 Django 知道我们在我们的模型有一些变更
    python manage.py migrate   # 创建表结构
    ```
6. 创建超级用户，在项目文件夹目录的命令行运行
    ```cmd
    python manage.py createsuperuser
    ```