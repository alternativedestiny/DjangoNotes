# Django 创建HTML模板方法

## 前言

## 环境

- Windows 10
- pycharm 2017.3.3 professional edition
- python 3.6.4
- django 2.0.2

## 方法

1. 在template 目录下创建HTML文件，假设命名为base.html
2. 完善base.html文件，将网页的公共部分完善
3. 在网页有区别的地方用如下代码锁定，其中xxx 相当于这个锁定模块的id，当其他页面调用此模板时就是通过xxx来识别位置的
    ```html
    {% block xxx %}{% endblock %}
    ```

4. 其他文件使用模板方法
    ```html
    {% extends 'base.html' %}
    {% block xxx %}.....{% endblock %}
    ```
5. 其效果相当于用.....处的内容替换{% block xxx %}{% endblock %}部分

## 备注