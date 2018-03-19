# Chrome - Timing Panel  
 
- 背景简介：  
 实现类似搜索框只能提示的功能，当用户输入内容发生变化，动态请求提示内容  
 
- 问题：  
 提示内容非常慢  

故，看了下chrome时间面板，下图所示，可以看出：  
(1) chrome浏览器`同一域名`的并发数是六个，后面的会进行阻塞  
(2) 阻塞时间就是Queueing + Stalled 的时间   
(3) Waiting时间长说明：服务器端查询时间较长...  
(4) Content Download 所用时间较短，说明：服务返回结果到客户端用时较少  

> `Waiting (TTFB)`  
等待初始响应所用的时间，也称为至第一字节的时间。 此时间将捕捉到服务器往返的延迟时间，以及等待服务器传送响应所用的时间。  
 `Content Download / Downloading `   
接收响应数据所用的时间。

 ![](/images/1521464958sz.png)  
 ![](/images/1521464995zh.png)  
 
