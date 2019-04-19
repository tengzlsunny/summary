# 
Web标准的理解(结构：html, 表现：css，行为：js)
    易于维护：只需更改CSS文件，就可以改变整站的样式
    页面响应快：HTML文档体积变小，响应时间短
    可访问性：语义化的HTML（结构和表现相分离的HTML）编写的网页文件，更容易被屏幕阅读器识别
    设备兼容性：不同的样式表可以让网页在不同的设备上呈现不同的样式
    搜索引擎：语义化的HTML能更容易被搜索

> html
1. html新增属性
    > 语义化标签： footer, header , nav, aside , main , mark(高亮显示), progress(进度条), time, details ,wbr ， section
    > 新增input元素的种类: email　url number range tel search time color month week
    > 表单新特性: placeholder,required ,autofocus 
    > 新标签: audio video canvas
    > 全局属性: （data-type dataset.type） Hidden
2. 标签语义化的好处：
    *  HTML结构清晰
    *  代码可读性较好
    *  无障碍阅读
    *  搜索引擎可以根据标签的语言确定上下文和权重问题
    *  移动设备能够更完美的展现网页（对css支持较弱的设备）
    *  便于团队维护和开发

> css

     

1. 基本数据类型： **undefined、null、Number、String、Boolean**

2. 从输入URL到页面展示的详细过程： 
    1、输入网址
    2、DNS解析(域名解析 Domain Name System)：递归查询和迭代查询， 客户端先检查本地是否有对应的IP地址，若找到则返回响应的IP地址。若没找到则请求上级DNS服务器，直至找到或到根节点。
    3、建立tcp连接（目的是“为了防止已失效的连接请求报文段突然又传送到了服务端，因而产生错误”）
        三次握手：
        发送端先发送一个带有SYN（synchronize）标志的数据包给接收端
        传回一个带有SYN/ACK标志的数据包以示传达确认信息
        接收方收到后再发送一个带有ACK标志的数据包给接收端以示握手成功
        四次挥手：
        第一次挥手：Client发送一个FIN，用来关闭Client到Server的数据传送，Client进入FIN_WAIT_1状态。
        第二次挥手：Server收到FIN后，发送一个ACK给Client，确认序号为收到序号+1（与SYN相同，一个FIN占用一个序号），Server进入CLOSE_WAIT状态。
        第三次挥手：Server发送一个FIN，用来关闭Server到Client的数据传送，Server进入LAST_ACK状态。
        第四次挥手：Client收到FIN后，Client进入TIME_WAIT状态，接着发送一个ACK给Server，确认序号为收到序号+1，Server进入CLOSED状态，完成四次挥手。
    4、客户端发送HTPP请求
    5、服务器处理请求　
    6、服务器响应请求
    7、浏览器展示HTML
    8、浏览器发送请求获取其他在HTML中的资源。



4. 



   