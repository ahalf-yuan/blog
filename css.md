# css  

#### 移动端字体 
> [你该知道的字体 font-family](https://github.com/chokcoco/iCSS/issues/6)

##### 字体书写规则  
综上，我觉得字体 font-family 定义的原则大概遵循：

**1、兼顾中西**   
中文或者西文（英文）都要考虑到。

**2、西文在前，中文在后**
由于大部分中文字体也是  带有英文部分的，但是英文部分又不怎么好看，同理英文字体中大多不包含中文。

所以通常会先进行英文字体的声明，选择最优的英文字体，这样不会影响到中文字体的选择，中文字体声明则紧随其次。

**3、兼顾多操作系统**  
选择字体的时候要考虑多操作系统。例如 MAC OS 下的很多中文字体在 Windows 都没有预装，为了保证 MAC 用户的体验，在定义中文字体的时候，先定义 MAC 用户的中文字体，再定义 Windows 用户的中文字体；

**4、兼顾旧操作系统,以字体族系列 serif 和 sans-serif 结尾**  
当使用一些非常新的字体时，要考虑向下兼容，兼顾到一些极旧的操作系统，使用字体族系列 serif 和 sans-serif 结尾总归是不错的选择。 

##### 总结  
- 不同的手机系统都有自己默认的字体。  
- 如果没有特殊的要求，移动端无需定义字体，使用默认字体(淘宝和天猫首页没有定义字体)，如果需要定义可参照以上规则。  
- 英文字体和数字字体可使用 Helvetica ，三种系统都支持。  


美团首页：
"Helvetica Neue",Helvetica,Arial,sans-serif"  

##### @font-face  
> [css3 @font-face](https://www.w3cplus.com/content/css3-font-face)  

@font-face是CSS3中的一个模块，他主要是把自己定义的Web字体嵌入到你的网页中。  
- 首先去网站下载自己想要的字体,例如[Google Fonts](https://fonts.google.com/)或[DaFont](https://www.dafont.com/)  
- 获取@font-face所需的.eot,.woff,.ttf,.svg等字体格式,通过第三方工具或者软件来实现，例如 fontsquirrel。  
- 文件放入项目中，定义，使用  
```css
   @font-face {
      font-family: 'SingleMaltaRegular';
      src: url('../fonts/singlemalta-webfont.eot');
      src: url('../fonts/singlemalta-webfont.eot?#iefix') format('embedded-opentype'),url('../fonts/singlemalta-webfont.woff') format('woff'),
	   url('../fonts/singlemalta-webfont.ttf') format('truetype'),
	   url('../fonts/singlemalta-webfont.svg#SingleMaltaRegular') format('svg');
      font-weight: normal;
      font-style: normal;
   }
   
   h2.singleMalta {
     font-family: 'SingleMaltaRegular'
   }
```  
#### 层叠顺序（stacking level）与堆栈上下文（stacking context）知多少？  
> [谈谈一些有趣的 CSS 话题](https://github.com/chokcoco/iCSS) 第3条  
[MDN](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Understanding_z_index/The_stacking_context)  
[W3C奇技淫巧之堆叠上下文](http://www.html-js.com/article/2523)

堆叠上下文  
#### filter  
> [你所不知道的 CSS 滤镜技巧与细节](https://www.cnblogs.com/coco1s/p/7519460.html)  

####  

## 常用实现  
> [谈谈一些有趣的 CSS 话题](https://github.com/chokcoco/iCSS)  

#### 文本单行省略与多行省略  
```css
/*
 * 单行
 * 需要 width
 */
overflow: hidden;
text-overflow:ellipsis;
white-space: nowrap; /*连续的空白符会被合并。文本内的换行无效*/
------------------

/* 多行 */
overflow: hidden;
text-overflow: ellipsis;
display: -webkit-box;
-webkit-box-orient: vertical;
-webkit-line-clamp: N; /* 控制显示的行数 */
line-height: X;        /* 对不支持浏览器的 */
max-height: X*N;       /* 对不支持浏览器的弥补 */
```  

