# AJAX实现网页动态数据显示

## 环境

- windows10
- pycharm2017.3.3 professional edition
- python3.6.4
- django2.0.2

## 方法

1. 创建后台读取数据函数，用于后台从数据库读取数据。在views.py文件内增加以下代码
    ```python
    from django.http import JsonResponse

    def data_fresh(request):
        context = {"data1": Test.objects.order_by("-time")[0].temp1,
                   "data2": Test.objects.order_by("-time")[0].temp2}
        return JsonResponse(context)
    ```
    data_fresh是函数名
    Test 是Django 项目下的模型
    ```order_by("-time")[0]``` 指按时间列倒序排列并取第一行数据
    temp1是第一行数据里的temp1数据
    如果没有数据库数据的话，直接写成固定的数据用来测试也是可以的

2. 加载函数，让HTML页面能够访问到函数。在urls.py添加一下代码
    ```python
    urlpatterns = [
        path('data_fresh/', views.data_fresh, name="data_fresh"),
    ]
    ```

3. 前端使用jQuery访问后台函数，要实现数据动态显示，还需要增加定时程序，在HTML页面插入以下代码
    ```html
    <script>
        $(document).ready(function(){
            function refresh(){
                $.getJSON("/data_fresh/", function (ret) {
                    $('#result').html(ret.data1);
                    $('#result2').html(ret.data2);
                })
            }
            setInterval(refresh, 3000);  // 每3s更新一次数据
        })
    </script>
    ```
    上面的程序将第1步里的temp1和temp2写入id 为result1和result2的标签里