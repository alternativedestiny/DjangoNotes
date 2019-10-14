# Django表单提交GET&POST

## 前言

之前在编写用户登陆界面的时候使用到了有关AJAX和POST部分的内容，但是没有搞太清楚，这次在写下拉菜单选项的时候，正好一块写一下GET和POST

## 环境

- windows10
- pycharm2017.3.3 professional edition
- python3.6.4
- django2.0.2

## 方法

1. GET&POST都是AJAX函数的简写
   比如在jQuery使用POST时，POST函数语法如下

    ```js
    jQuery.post(url,data,success(data, textStatus, jqXHR),dataType)
    ```

    原AJAX函数如下

    ```js
    $.ajax({
      type: 'POST',
      url: url,
      data: data,
      success: success,
      dataType: dataType
    });
    ```

    同理，GET函数语法如下

    ```js
    $(selector).get(url,data,success(response,status,xhr),dataType)
    ```

    原AJAX函数如下

    ```js
    $.ajax({
      url: url,
      data: data,
      success: success,
      dataType: dataType
    });
    ```

    可以看到GET和POST函数差别其实不大，但是之前在用PHP的时候，GET是明文传递参数，在用户登陆的情况下传递用户名和密码显然是不太合适的，具体区别参考 [HTTP 方法：GET 对比 POST](http://www.runoob.com/tags/html-httpmethods.html)
2. Django表单提交的方法，views.py文件内

    ```python
    def xxx(request):
        if request.method == 'get':
            motor_name = request.GET.get("data1", "")
    ```

    通过上面的程序就可以读取到前端页面发送的名为data1变量内的值
    经过测试增加了

    ```python
    if request.method == 'get':
    ```

    这句后程序更加稳定。使用POST方法相同，只需把上面程序GET改成POST即可，但是需要注意csrf问题。
