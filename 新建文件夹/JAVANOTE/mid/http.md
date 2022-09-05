# 爬虫、反爬虫

# http是互联网世界的基石

    只要你使用网络，世界的某一个角落一定有个地址和你进行双向的http响应

    发的是什么样子决定了你拿回来的是什么样子


# HTTP请求与响应

    第一个请求说明了http要请求哪个路径
    GET / HTTP/1.1
    用get这个方法请求根路径 使用http1.1协议 

    Host: google.com
    host网络上计算机的别称，访问网路上某一台计算机，主机名为google.com 发送到那？
    由DNS把它变成一个ip地址 才能访问它




    User-Agent ：Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36
    你发送出去的请求 字节流 是有人替你发出的（游览器）
    游览器有个很长的字符串，后端根据这个东西知道你的信息





    如你的代码部署在服务器上，能接受http请求能发出回应
    但有的是游览器发出的，有的是爬虫

        给它放回一个错误的状态码status

        放回的数据中投毒

    
    计算机网络上all东西都需要ip地址
    在本地改变一个运营指向的ip地址
    sudo vi /etc/hosts
    127.0.01    www.google.com


## HTTP方法

    HTTP请求的第一个单词指明当前请求的方法

        GET 要求去读一个东西，获取网页
            请求的数据都在 HTTP request header 

        POST 真正的数据在body里 
            前端使用post将数据（账号密码、文件）放在body里 
            登录接口用post发起


## HTTP status

    HTTP/1.1 200 OK
    响应的第一行
        2xx 成功
        3xx 重定向
        4xx 客服端错误
        5xx 服务器错误


# Header

    request header


        accpet

        cookie

        user-agent

        referer
            告訴後端 游覽器當前頁面是從哪跳出來的（防盜獵）

    
    response

        相應是根據請求來的  

        游览器和服务器通过header进行对话（accept —— content-type）

        游览器想要什么样的数据就放在accept里面，想接受什么样的数据

        content（由框架自动完成）
        content-type：image/jpeg（给游览器什么样的数据）
        服务器可以告诉游览器当前的字节流是什么数据，游览器根据不同做出不同的响应
        content-tpye：application/zip
        直接下载
        

# Body

    在HTTP协议的标准里
    除了规定的字符，其他字符都要被转义

    HTTP request body

        get没有body
        host有

        后端是没有办法区分两个一样的HTTP请求是谁发出来的

        表单

        k-v对

    游览器向服务器发送一个下载请求，服务器返回 200 OK ，content-tpye：zip .....
    游览器就知道后面的是要下载的内容

    HTTP response body

        conten-type决定body里的数据如何被解释

        JSON

        HTML/XML

        二进制（图片/下载文件）


# HTTP协议是无状态的

    用户名密码问题

    发送的每个请求都是独立的（每次发的是请求可能不是同一服务器）
    所以HTTP不保留任何状态，HTTP协议是无状态的

# cookie

    维持状态（用户名密码问题）
    
    第一次执行登录请求的时候
    服务器返回的header里放入了 set-cookie:xxxx(随机字符串);...

    一旦服务器给你发送set-cookie后 之后发送的请求（同域名）都会带上这段字符串（下单....）

    这个cookie可以全程的代表你，有这段字符串就代表是你

    cookie是跟着域名走的