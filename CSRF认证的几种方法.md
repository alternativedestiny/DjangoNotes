# CSRF认证的几种方法

## 前言

在使用Django框架编写网页，使用AJAX技术进行前后端数据交互的时候会遇到csrf（Cross-site request forgery跨站请求伪造）问题，get请求不影响，post就需要csrf认证。

## 环境

- Django 2.0.6

## 方法

1. 在登陆表单中添加CSRF方法：

    ```html
    <form action="{% url 'login_check' %}" method="POST">
        {% csrf_token %}
        <label>
            <input type="text" name="username" placeholder="用户名">
        </label>
        <label>
            <input type="password" name="password" placeholder="密码">
        </label>
        <h4 style="color: white;">{{ message }}</h4><br>
        <input type="submit" value="登陆">
    </form>
    ```

2. 在HTML与JS分离的网页中的方法：

    ```html
    <script>
    // POST csrf_token
    $.ajaxSetup({
        data: {csrfmiddlewaretoken: '{{ csrf_token }}' }
    });
    </script>
    <script src="xxx.js"></script>
    ```

3. 在HTML与JS在同一文件中时可以使用2中的方法，但是当js中既有POST又有GET时，该方法会出现错误(当然全部使用POST也是可以的)。因此还有一种方法只对POST产生作用，不过这种方法对HTML与js分离的网页中无效：

    ```js
    $.post("/data_search/",{
            data1: a,
            data2: b,
            csrfmiddlewaretoken: '{{ csrf_token }}'  // csrf认证
        } , function () {
            // 要执行的函数
        }
    )
    ```
