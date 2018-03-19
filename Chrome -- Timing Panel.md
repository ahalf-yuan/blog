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

>  `Stalled`  
浏览器得到要发出这个请求的指令，到请求可以发出的等待时间，一般是代理协商、以及等待可复用的TCP连接释放的时间，不包括DNS查询、建立TCP连接等时间等  
`Request sent`  
请求第一个字节发出前到最后一个字节发出后的时间，也就是上传时间  
`Waiting (TTFB)`  
等待初始响应所用的时间，也称为至第一字节的时间。 此时间将捕捉到服务器往返的延迟时间，以及等待服务器传送响应所用的时间。(请求发出后，到收到响应的第一个字节所花费的时间(Time To First Byte))  
 `Content Download / Downloading `   
 收到响应的第一个字节，到接受完最后一个字节的时间，就是下载时间   

 ![](/images/1521464958sz.png)  
 ![](/images/1521464995zh.png)  
 
- [了解 Resource Timing](https://developers.google.cn/web/tools/chrome-devtools/network-performance/understanding-resource-timing?hl=zh-cn)  
- [关于请求被挂起页面加载缓慢问题的追查](http://fex.baidu.com/blog/2015/01/chrome-stalled-problem-resolving-process/)  
- [chrome的timeline的问题？](https://segmentfault.com/q/1010000002399481)





