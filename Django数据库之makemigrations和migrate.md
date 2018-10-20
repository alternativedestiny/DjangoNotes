# Django数据库之makemigrations和migrate

## 环境

- windows10
- pycharm2017.3.3 professional edition
- python3.6.4
- django2.0.2

## 方法

1. makemigrations会在当前目录下生成一个migrations文件夹，该文件夹的内容就是数据库要执行的内容
    ```cmd
    python manage.py makemigrations
    ```
2. migrate就是执行之前生成的migrations文件，这一步才是操作数据库的一步
    ```cmd
    python manage.py migrate
    ```

## 备注

Django每次更新模型都需要执行以上两步，需要注意的是Django模型增加内容需要设定变量的初始值，否则会在第一步出现问题