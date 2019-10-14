# Django urls 路由与app子路由

## 前言

在网页本身较少的情况下Django 项目可以只使用单个app 和项目自带的urls文件进行路由，但是在网页较为复杂或项目内有多个app的情况下就不太合适了，这时就需要在app中单独设置路由

## 环境

- windows10
- pycharm2017.3.3 professional edition
- python3.6.4
- django2.0.2

## 方法

为方便表达，统一将项目同名文件下的urls.py文件称为主路由，项目app 内的urls.py 称为子路由

1. 项目内单个app路由配置（主路由）方法。
    使用创建项目时的路由文件，即项目同名文件下的urls.py文件

    ```python
    from django.contrib import admin
    from django.urls import path
    from . import views

    urlpatterns = [
        path('admin/', admin.site.urls),  # Django后台管理页面
        path('xxx1/', views.xxx1, name="xxx2"),
        path('xxx2/', views.xxx1, name="xxx2"),
    ]
    ```

    这样就形成的项目内的路由文件，其中“from . import views”是从项目的所有文件中寻找views文件并导入，在项目只有一个app 的情况下自然是导入该app 的views.py文件

2. 多app 情况下urls分离。
    其实即便不分离，使用1中的方法也是可以的，但是当网页不断丰富，app不断增加的情况下，就会对后面的维护工作造成诸多不便
    首先，在app 目录下创建子路由urls.py 文件（同名不要紧），并将原先主路由内该app下的网页迁移过来

    ```python
    from django.urls import path
    from app1 import views

    urlpatterns = [
        path('xxx1/', views.xxx1, name="xxx2"),
        path('xxx2/', views.xxx1, name="xxx2"),
    ]
    ```

    原主路由文件变成

    ```python
    from django.contrib import admin
    from django.urls import path, include

    urlpatterns = [
        path('admin/', admin.site.urls),
        path('', include('app1.urls')),
    ]
    ```

    不要忘了引入include，这样就能成功分离路由文件，而网页的访问地址不会改变
