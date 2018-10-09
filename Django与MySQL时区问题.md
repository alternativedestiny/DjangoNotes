# Django 与MySQL时区问题

## 前言

Django 使用MySQL数据库出现的时区问题

## 环境

- Windows 10
- pycharm 2017.3.3 professional edition
- python 3.6.4
- django 2.0.2

## 方法

1. 将Django 项目默认的UTC时区修改为本地时区

    打开Django 项目的settings.py文件，修改TIME_ZONE为
    ```python
    TIME_ZONE = 'Asia/Shanghai'
    ```

2. Django存取数据时的时区问题

    在数据库和Django都为本地时区时，通过Django写入数据库的数据，从数据库中看相差8个小时，显示出来也相差8个小时，这是因为Django 在写入数据库时将本地时区变成了UTC时区

    解决方法：将settings.py文件里的
    ```python
    USE_TZ = True
    ```
    改为
    ```python
    USE_TZ = False
    ```

## 备注

带图教程，[请点这里](https://blog.csdn.net/mildddd/article/details/79800860)