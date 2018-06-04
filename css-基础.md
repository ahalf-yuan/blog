# css-基础  

#### 移动端字体 
> [你该知道的字体 font-family](https://github.com/chokcoco/iCSS/issues/6)

**字体书写规则**  
	综上，我觉得字体 font-family 定义的原则大概遵循
- **1、兼顾中西**   
	中文或者西文（英文）都要考虑到。
- **2、西文在前，中文在后**  
	由于大部分中文字体也是  带有英文部分的，但是英文部分又不怎么好看，同理英文字体中大多不包含中文。
	所以通常会先进行英文字体的声明，选择最优的英文字体，这样不会影响到中文字体的选择，中文字体声明则紧随其次。
- **3、兼顾多操作系统**  
	选择字体的时候要考虑多操作系统。例如 MAC OS 下的很多中文字体在 Windows 都没有预装，为了保证 MAC 用户的体验，在定义中文字体的时候，先定义 MAC 用户的中文字体，再定义 Windows 用户的中文字体；
- **4、兼顾旧操作系统,以字体族系列 serif 和 sans-serif 结尾**  
	当使用一些非常新的字体时，要考虑向下兼容，兼顾到一些极旧的操作系统，使用字体族系列 serif 和 sans-serif 结尾总归是不错的选择.

**总结**  
- 不同的手机系统都有自己默认的字体。 
- 如果没有特殊的要求，移动端无需定义字体，使用默认字体(淘宝和天猫首页没有定义字体)，如果需要定义可参照以上规则。  
- 英文字体和数字字体可使用 Helvetica ，三种系统都支持。  


美团首页：
"Helvetica Neue",Helvetica,Arial,sans-serif"  

#### @font-face  
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

#### css可以和不可以(默认)继承的属性  
> [谈谈 CSS 关键字 initial、inherit 和 unset](https://github.com/chokcoco/iCSS/issues/13) 
[Which CSS properties are inherited?
Ask](https://stackoverflow.com/questions/5612302/which-css-properties-are-inherited)  
[css可以和不可以继承的属性](https://www.cnblogs.com/thislbq/p/5882105.html)  
不存在不能继承的属性。CSS 的每个属性都有一个「是否继承（inherited）」的特性（严格来说是「是否默认继承」）  
说到底，CSS 属性的取值就是由默认值（initial），继承（inherit）与加权系统构成的（其实还有 unset(未设置)、revert(还原)），厘清它们的关系及使用方法对熟练使用 CSS 大有裨益。

* 字体系列属性
font：组合字体  
font-family：规定元素的字体系列  
font-weight：设置字体的粗细  
font-size：设置字体的尺寸  
font-style：定义字体的风格  
font-variant：设置小型大写字母的字体显示文本，这意味着所有的小写字母均会被转换为大写，但是所有使用小型大写字体的字母与其余文本相比，其字体尺寸更小。  
font-stretch：对当前的 font-family 进行伸缩变形。所有主流浏览器都不支持。  
font-size-adjust：为某个元素规定一个 aspect 值，这样就可以保持首选字体的 x-height。  
* 文本系列属性  
text-indent：文本缩进  
text-align：文本水平对齐  
line-height：行高  
word-spacing：增加或减少单词间的空白（即字间隔）  
letter-spacing：增加或减少字符间的空白（字符间距）  
text-transform：控制文本大小写  
direction：规定文本的书写方向  
color：文本颜色  
* 元素可见性：visibility  
* 表格布局属性：caption-side、border-collapse、border-spacing、empty-cells、table-layout  
* 列表布局属性：list-style-type、list-style-image、list-style-position、list-style  
* 生成内容属性：quotes  
* 光标属性：cursor  
* 页面样式属性：page、page-break-inside、windows、orphans  
* 声音样式属性：speak、speak-punctuation、speak-numeral、speak-header、speech-rate、volume、voice-family、pitch、pitch-range、stress、richness、、azimuth、elevation  

#### 权重  

#### block，inline和inline-block概念和区别  
> [block，inline和inline-block概念和区别](https://www.cnblogs.com/caiquan/p/5931613.html)  

- display:block  
block元素会独占一行，多个block元素会各自新起一行。默认情况下，block元素宽度自动填满其父元素宽度。
block元素**可以设置width,height属性。块级元素即使设置了宽度,仍然是独占一行。
block元素可以设置margin和padding属性。**
- display:inline  
inline元素不会独占一行，多个相邻的行内元素会排列在同一行里，直到一行排列不下，才会新换一行，其宽度随元素的内容而变化。
inline元素**设置width,height属性无效。
inline元素的margin和padding属性，水平方向的padding-left, padding-right, margin-left, margin-right都产生边距效果；但竖直方向的padding-top, padding-bottom, margin-top, margin-bottom不会产生边距效果。**
- display:inline-block  
简单来说就是将对象呈现为inline对象，但是对象的内容作为block对象呈现。之后的内联对象会被排列在同一行内。比如我们可以给一个link（a元素）inline-block属性值，使其**既具有block的宽度高度特性又具有inline的同行特性。**  

#### 盒子模型

#### BFC


#### inline-block布局问题  
- **基线对齐**  
> [css 使用display：inline-block的问题求解？](https://www.zhihu.com/question/28057944) 

inline-block 元素的基线是这个元素下正常文档流中最后一个 line box 的基线，除非这个元素中没有正常流的 line box 或者本身的 overflow 属性值不是默认的 visible ，这个时候 inline-block 元素的基线位置是margin的底边缘。
（对于一个 inline-block 元素，如果它内部没有内联元素，或者它的overflow属性不是visible，那么默认vertical-align: baseline。否则，就是它内部最后一个元素的基线。如下图。） 

![](/images/1525516507ik.png)  
解决： inline-block 设置 vertical-align: top; 或者触发BFC。
- **元素间隙**  
原因：如果HTML源代码中元素之间有空格，那么列与列之间会产生空隙  
> [去除inline-block元素间间距的N种方法](http://www.zhangxinxu.com/wordpress/2012/04/inline-block-space-remove-%E5%8E%BB%E9%99%A4%E9%97%B4%E8%B7%9D/)  

#### 浏览器如何渲染文本  
> [浏览器如何渲染文本](http://blog.jjgod.org/2011/04/09/how-do-browsers-render-text/)

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

