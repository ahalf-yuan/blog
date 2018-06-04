# css - 布局

### Flex 布局 
> https://juejin.im/post/599970f4518825243a78b9d5   

1. display 属性设置为 flex 就可以   

2. 设为 Flex 布局以后，子元素的 float、clear 和 vertical-align 属性将失效

3. 在 flex 中，最核心的概念就是**容器和轴**，所有的属性都是围绕容器和轴设置的.**容器分为父容器和子容器。轴分为主轴和交叉轴（主轴默认为水平方向，方向向右，交叉轴为主轴顺时针旋转 90°）**。   

4. 父容器上有六个属性  
```css
flex-direction：主轴的方向。  
flex-wrap：超出父容器子容器的排列样式。  
flex-flow：flex-direction 属性和 flex-wrap 属性的简写形式。  
justify-content：子容器在主轴的排列方向。  
align-items：子容器在交叉轴的排列方向。  
align-content：多根轴线的对齐方式。
````   
- flex-direction 属性  
flex-direction 属性决定主轴的方向（主轴的方向不一定是水平的，这个属性就是设置主轴的方向，主轴默认是水平方向，从左至右，如果主轴方向设置完毕，那么交叉轴就不需要设置，交叉轴永远是主轴顺时针旋转 90°）  

- flex-wrap 属性  
 flex-wrap 属性决定子容器如果在一条轴线排不下时，如何换行。  
 flex-wrap: nowrap;          // 默认，不换行  
 flex-wrap: wrap;            // 换行，第一行在上方。  
 flex-wrap: wrap-reverse     // 换行，第一行在下方。
 
- justify-content 属性  
justify-content 属性定义了子容器在主轴上的对齐方式。  
justify-content: flex-start;      // 默认，左对齐  
justify-content: flex-end;        // 右对齐  
justify-content: center;          // 居中  
justify-content: space-between;   // 两端对齐，项目之间的间隔都相等。  
justify-content: space-around;    // 每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。  

- align-items 属性  
align-items属性定义子容器在交叉轴上如何对齐。具体的对齐方式与交叉轴的方向有关，下面假设交叉轴从上到下。  
```css
.ele{
    align-items: flex-start;    // 交叉轴的起点对齐。
    align-items: flex-end;      // 交叉轴的终点对齐。
    align-items: center;        // 交叉轴的中点对齐。
    align-items: baseline;      // 项目的第一行文字的基线对齐。
    align-items: stretch;       // 默认，如果项目未设置高度或设为auto，将占满整个容器的高度。
}
```

align-content 属性  
align-content 属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。  
```css
.ele{
    align-content: flex-start;   // 与交叉轴的起点对齐
    align-content; flex-end;     // 与交叉轴的终点对齐。
    align-content: center;       // 与交叉轴的中点对齐。
    align-content: space-between;// 与交叉轴两端对齐，轴线之间的间隔平均分布。
    align-content: space-around; // 每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
    align-content: stretch;     // 默认 轴线占满整个交叉轴。
}
```

5.子容器属性  
子容器也有 6 个属性：  
```css
order：子容器的排列顺序  
flex-grow：子容器剩余空间的拉伸比例  
flex-shrink：子容器超出空间的压缩比例  
flex-basis：子容器在不伸缩情况下的原始尺寸  
flex：子元素的 flex 属性是 flex-grow,flex-shrink 和  flex-basis 的简写  
align-self  
```

order 属性  
order 属性定义项目的排列顺序。数值越小，排列越靠前，默认为 0。   

flex-grow 属性   
flex-grow 属性定义子容器的伸缩比例。按照该比例给子容器分配空间。
```
.ele{
    flex-grow: <number>; /* default 0 */
}
```

flex-shrink 属性  
flex-shrink 属性定义了子容器弹性收缩的比例。如图，超出的部分按 1:2 的比例从给子容器中减去。此属性要生效，父容器的 flex-wrap 属性要设置为 nowrap
```
.ele{
    flex-shrink: <number>; /* default 0 */
}
```

flex-basis 属性   
flex-basis 属性定义了子容器在不伸缩情况下的原始尺寸，主轴为横向时代表宽度，主轴为纵向时代表高度。
```
.ele{
    flex-basis: <length> | auto; /* default auto */
}
```

flex 属性  
子元素的 flex 属性是 flex-grow,flex-shrink 和  flex-basis 的简写，默认值为 0 1 auto。后两个属性可选。  
该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。

align-self 属性  
子容器的 align-self 属性允许单个项目有与其他项目不一样的对齐方式，可覆盖父容器 align-items 属性。默认值为 auto，表示继承父元素的 align-items属性，如果没有父元素，则等同于 stretch。
```
.ele{
    align-self: auto;             // 继承父元素的 align-items 属性
    align-self: flex-start;       // 交叉轴的起点对齐。
    align-self: flex-end;         // 交叉轴的终点对齐。
    align-self: center;           // 交叉轴的中点对齐。
    align-self: baseline;         // 项目的第一行文字的基线对齐。
    align-self: stretch;          // 默认，如果项目未设置高度或设为auto，将占满整个容器的高度。
}
```

### grid 网格布局  

### 水平垂直居中  
- 行内水平、垂直居中  display: inline-block;或inline
text-align:center   
line-height 和 height 设置为相同
- 固定宽度居中
margin： 0 auto
- 水平垂直  
固定宽度或者固定高度的情况个人认为设置水平垂直居最简单，可以直接使用绝对定位。使用绝对定位就是子元素相对于父元素的位置，所以将父元素设置 position:reletive 对应的子元素要设置 position:absolute，然后使用 top:50%;left:50%，将子元素的左上角和父元素的中点对齐，之后再设置偏移 margin-top: 1/2 子元素高度;margin-left: 1/2 子元素宽度;。这种方式也很好理解。  
上面的绝对定位方法只要将 margin 改为 transform 就可以实现宽度和高度未知的居中（兼容性啊兄弟们！(ಥ_ಥ)）transformX:50%;transformY:50%；
```css
.inner{
  width: 100px;
  height: 50px;
  position: absolute;
  top: 50%;
  left: 50%;
  margin-top: -25px;
  margin-left: -50px;
  background: #fff;
  text-align: center;
}

.inner{
  width: 100px;
  height: 50px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: #fff;
  text-align: center;
}

```
### 三列布局  
- float + BFC 
```css  
.wrapper{
    overflow: hidden;  //清除浮动
}
.middle{
    width: 100%;
    float: left;
}
.middle .main{
    margin: 0 220px;
    background: red;
}
.left{
    width: 200px;
    height: 300px;
    float: left;
    background: green;
    margin-left: -100%;
}
.right{
    width: 200px;
    height: 300px;
    float: left;
    background: yellow;
    margin-left: -200px;
}
``` 
- flex 
```css
.wrapper{
    display: flex;
}
.left{
    width: 200px;
    height: 300px;
    background: green;
}
.middle{
    width: 100%;
    background: red;
    marign: 0 20px;
}
.right{
    width: 200px;
    height: 3000px;
    background: yellow;
}
```