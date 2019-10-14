# Django用户验证方法

## 前言

这部分主要是需要保证网站的一些敏感页面不被普通游客访问到，需要一整套用户系统

## 环境

- windows10
- pycharm2017.3.3 professional edition
- python3.6.4
- django2.0.2

## 方法

1. 创建登陆页面，与普通HTML页面创建方法相同，比如下面这个最基本的登陆页面

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>登陆</title>
    </head>
    <body>
        <form action="{% url 'login_check' %}" method="POST">
            {% csrf_token %}
            <label>
                <input type="text" name="username">
            </label>
            <label>
                <input type="password" name="password">
            </label>
            <input type="submit" value="登陆">
        </form>
        <p>{{ message }}</p>
    </body>
    </html>
    ```

    login_check和{% csrf_token %}这两部分后面会介绍

2. 写登录页函数，以便于在其他页面使用跳转到登录页。在views.py文件下增加

    ```python
    def login(request):
        return render(request, "login.html", {"message": "请输入用户名和密码！"})
    ```

    别忘了添加到urls.py文件

    ```python
    path('login/', views.login, name="login"),
    ```

    跳转方法

    ```html
    <a href="{% url 'login' %}"></a>
    ```

3. 以上部分和创建一个普通页面的方法基本相同，接下来重头戏开始：用户登陆与验证。在views.py文件内创建登陆验证函数。若账号密码通过，则登陆并返回；否则留在登录页并显示 "登录名或密码错误！"字样

    ```python
    from django.contrib import auth
    from django.shortcuts import render, redirect

    def login_check(request):
        username = request.POST.get("username", "")
        password = request.POST.get("password", "")
        user = auth.authenticate(request, username=username, password=password)
        if user is not None:
            auth.login(request, user)
            return redirect("/dashboard/")
        else:
            return render(request, "login.html", {"message": "登录名或密码错误！"})
    ```

    同样不要忘记将函数写入urls.py文件

    ```python
    path('login_check', views.login_check, name="login_check"),
    ```

4. 未登录用户强制跳转，防止未登录用户看到数据，在需要设置访问限制的网页加入以下函数，比如table，判断用户登陆状况，若用户已登录，则允许跳转到table页面，否则强制跳转到登录页面

    ```python
    def table(request):
        # 判断登录情况，未登录强制跳转
        if request.user.is_authenticated:
            return render(request, "table.html")
        else:
            return render(request, "login.html", {"message": "请输入用户名和密码！"})
    ```

## 备注

- CSRF（Cross-site request forgery）跨站请求伪造。Django 为了防止CSRF 攻击有一些保护措施，因此我们在使用POST 时会出现django csrf token missing or incorrect的错误，因此需要在POST表单中加入 {% csrf_token %}，原理部分此时先不做深究，因为我也没有研究这方面
- 关于render的一些问题，因为render 本身自带一个request 参数，这个参数其实包含有很多信息，其中就有用户信息，因此在使用render时，即便我们没有向网页传递任何参数，网页依然可以访问到用户信息，比如使用{{user}}就可以显示用户名，这就是request起到的作用
