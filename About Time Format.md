# Time Format  

> [标准](https://www.w3.org/TR/NOTE-datetime)  
[ECMA-Date Time String Format](http://www.ecma-international.org/ecma-262/5.1/#sec-15.9.1.15)  
  
**UTC & GMT**  
UTC 是标准时间参照，而GMT（格林威治时间）、CST（北京时间）、PST（太平洋时间）等等是具体的时区。由于 UTC +0 的特殊性，所以有时也把 GMT 当成参照。  
如时区表[Time Zone Abbreviations – Worldwide List](https://www.timeanddate.com/time/zones/)  
![](/images/1526464175qy.png)  

**各种格式**  
1.new Date()  `Wed May 16 2018 17:55:25 GMT+0800 (CST)`

2.date.toGMTString()  `Wed, 16 May 2018 09:37:33 GMT`

3.date.toUTCString()  `Wed, 16 May 2018 09:37:33 GMT`  

4.date.toISOString()  `2018-05-16T09:37:33.341Z`  
> T	“T” appears literally in the string, to indicate the beginning of the time element.  
Z	is the time zone offset specified as “Z” (for UTC) or either “+” or “-” followed by a time expression HH:mm  

