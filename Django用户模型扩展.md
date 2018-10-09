# Django用户模型扩展

## 前言

Django 模型本身自带User模型，可以完成基本的用户功能，不过由于其自带属性较少（用户名，密码，姓，名，邮箱，权限），有时难以满足使用，因此需要涉及用户模型扩展。
本方法思路是创建一个普通模型，使其与Django自带用户模型形成一一对应关系

- 优点是创建使用比较简单，并对原先模型影响较小；
- 缺点是与用户模型联系不够紧密，无论是模型还是数据库，两部分内容都是分离的，仅仅是有对应关系。

所以需要根据具体情况斟酌使用。

## 环境

- windows10
- pycharm2017.3.3 professional edition
- python3.6.4
- django2.0.2

## 方法

使用Profile扩展，默认已使用Django自带用户模型

1. 创建用户模型扩展模型，在views.py文件内

    ```python
    from django.contrib.auth.models import User

    # 用户模型扩展
    class Profile(models.Model):
        user = models.OneToOneField(User)  # 与Django自带用户模型建立对应关系
        company = models.CharField(max_length=40, default="")  # 公司
        location = models.CharField(max_length=80, default="")  # 地址
    ```

2. 在admin.py文件内注册模型

    ```python
    from .models import *  # 从models.py引入所有模型

    class ProfileAdmin(admin.ModelAdmin):
    list_display = ("user", "company", "location")

    admin.site.register(Profile, ProfileAdmin)
    ```

3. 模型的使用，在网页内
    - Django自带模型
    ```html
    <p>{{ user.email }}</p>
    ```
    - 扩展模型
    ```html
    <p>{{ user.profile.company }}</p>
    ```

## 参考文档

- [django用户认证系统——拓展 User 模型2](https://www.cnblogs.com/AmilyWilly/p/8469851.html)
- [如何扩展Django用户模块](http://python.jobbole.com/86806/)
- [Django-Model操作数据库(增删改查、连表结构）](https://www.cnblogs.com/yangmv/p/5327477.html)