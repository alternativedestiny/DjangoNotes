# Django项目创建流程

## 前言

## 环境

- Windows 10
- pycharm2017.3.3 professional edition(必须专业版)
- python3.6.4
- django2.0.2

## 方法

1. 打开Pycharm专业版，创建Django项目
2. 创建APP，
    在控制台下面输入

    ```cmd
    python manage.py startapp xxx
    ```

    创建名为xxx 的app，注意路径，最好在Pycharm下方的控制台里面输入命令
3. 设置
    在settings.py 文件内的INSTALLED_APPS 中添加创建的app名称，将LANGUAGE_CODE 中的内容改为zh-hans，即设置中文。
4. 创建模型及数据库
    使用MySQL数据库的可以参考，[Django 连接MySQL方法](http://blog.csdn.net/mildddd/article/details/79557844)
    1. 在app 目录下models.py文件内创建项目模型，[字段类型参考文档](https://www.cnblogs.com/lhj588/archive/2012/05/24/2516040.html)
    2. 在app 目录下views文件内创建函数，并根据需求创建HTML文件
    3. 完善urls.py文件的内容
    4. 创建数据库，在控制台执行以下两条命令

        ```cmd
        python manage.py makemigrations
        python manage.py migrate
        ```

    5. 创建数据库超级用户，在控制台执行以下命令

        ```cmd
        python manage.py createsuperuser
        ```

    6. 注册数据库里的表格，在app 目录下的admin.py文件里注册

        ```python
        from .models import xxx
        admin.site.register(xxx)
        ```

        Django 自带sqllite3数据库，需要更换数据库请参考[Django 连接MySQL方法](http://blog.csdn.net/mildddd/article/details/79557844)

5. 启动服务

    ```cmd
    python manage.py runserver
    ```

## 备注

带图教程，[请点这里](https://blog.csdn.net/mildddd/article/details/79557937)
