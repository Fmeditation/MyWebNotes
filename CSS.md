CSS(Cascading  Style SheetS)

一、CSS标准规范

选择器+属性

1.基础选择器

1.1 标签选择器

1.2 类选择器

一个标签有多个类名，对应的css值有重复，听谁的？

1.3 id选择器  #   id唯一

1.4 通配符选择器 * { }

二、字体系列

```css
#serial {
    font-family: "Microsoft YaHei", arial;   //字体
    font-size: 20px;	//字号大小，标题大小比较特殊，需要单独指定大小
    font-weight: bold;	//字体粗细 通常用数字，无单位
    font-style: italic;		//字体样式 如：斜体
}

//复合属性写法，必须严格按照顺序 可以省略属性，但font-size 和 font-family是必须有的
#model {
    font:italic 700 16px 'Microsoft YaHei';
}
//order: font-style font-weight font-size font-family

font:12px/24px  	//表示字体大小和对应的行高，一种简写方式
font: 12px/1.5 		//字体大小12px，行高是字体大小的1.5倍，18px；
```

三、文本属性

```css
//文本外观
#serial {
    color:#FFFFFF;  	//十六机制、RGB、预定义颜色值(名字)
    text-align:right;	//水平位置 left、right、center 本质是盒子内的对齐
    text-decoration:line-through;	// none、underline、line-through、overline
    text-indent:10px;	//缩进 文本首行  也可以用em，一个em是当前一个文字的大小  2em
    line-height：10px；	//行间距、行高 行间距=上间距+文本高度+下间距
    
    text-shadow:10px 10px 5px red;
    //文字陰影，慘開盒子陰影，但只有4個參數，h-shadow v-shadow blur colir
}
```

四、CSS引入方式

内部样式表 ：	html文档中的<style></style>标签内；

行内样式表：在目标标签内<p style=" "></p> ；

 外部样式表：在css文件中写，并在<link href=" path" rel="stylesheet"></link>中引入

五、Emmet语法

| 输入              | 生成内容          |
| ----------------- | ----------------- |
| 标签名+tab        | 快速生成标签      |
| 标签名*3+tab      | 快速生成3个标签   |
| 父标签>子标签+tab | 快速生成父子标签  |
| 标签1+标签2+tab   | 快速生成兄弟标签  |
| .标签+tab         | 快速生成标签+类名 |
| #标签+tab         | 快速生成标签+id   |
| 标签+{}           | 快速生成标签+内容 |
| CSS 样式          |                   |

六、复合选择器

6.1 后代选择器

<ol>
    <li>ol-child1</li>
    <li>ol-child2</li>
    <li>ol-child3</li>
</ol>
<ul>
    <li>ul-child1</li>
    <li>ul-child2</li>
    <li>ul-child3</li>
</ul>
<style>
    ol li {
        color:red;
    }
</style>

上述例子用后代选择器 ol  li  来改变目标标签的颜色，可以复合，eg：.nav  a

6.2 子选择器 

    <ol class="nav">
        <li>child1</li>
        <li>
            <a href="#">link this</a>
        </li>
	</ol>
<style>
    .nav > li {
        color:red;
    } 
</style>

上述例子用子选择器 ol > li  来改变目标标签的颜色，特性：只覆盖到第一层

6.3 并集选择器

    <ol class="slide">
        <li>child a</li>
        <li>
            <ul clsaa="item">
                <li>subitem1</li>
                <li>subitem2</li>
            </ul>
            <a  class="linker" href="#">link this</a>
        </li>
	</ol>
<style>
    .slide ,
    .linker
    {
        color:green;
    } 
</style>

，用于选取多个标签

6.4 伪类选择器 

<div>
      <a href="link a">link a</a>
      <a href="link b">link b</a>
</div>
    <style>
      a:hover {
        color: green;
      }
    </style>

:hover	  :visited	 :link 	:active

七、显示模式

html元素分为块元素和行内元素

**行内元素**：h系列、p、ol、div等，具有以下特点：

独占一行、宽高边距都可以控制、默认宽度是父容器的100%、内部可嵌套其他行内、块元素；

但p和h不能在放块元素；

**块元素**：a、span、strong、i、u等，具有以下特点：

一行可以显示多个、宽高设置是无效的、默认宽度是本身内容的宽度、行业元素内只能放文本或其他行内元素；

a里面不能在放a，但是a里面能放块级元素；

**行内块元素**：img、td、input 它们同时具有块元素和行内元素的特点：

可以显示在同一行，宽高就是自身内容宽高、但宽高边界都可以控制；

**元素显示的转换**：display: inline /block/ inline-block

```html
  <style>
    a {
      height: 30px;
      width: 300px;
      display: block;
    }
    .ts1 {
      background-color: green;
      width: 200px;
      height: 300px;
      display: inline;
    }
    .ts2 {
      background-color:blueviolet;
      width: 300px;
      height: 200px;
      display: inline;
    }
    span {
      width: 300px;
      height: 300px;
      display: inline-block;
    }
  </style>
  <body>
    <a href="#">click me </a>
    <div class="ts1">show mode </div>
    <div class="ts2">test</div>
    <span> 我是一个行内元素，我是span</span>
    <h4>我该在哪</h4>
  </body>
```

显示转换demo

```html
  <style>
    .slider {
      width: 220px;
      height: 350px;
      background-color: dimgrey;
    }
    a {
      display: block;
      width: 220px;
      height: 50px;
      text-indent: 30px;
      font-size: 20px;
      font-weight: 700;
      color:white;
      text-decoration: none;
      line-height: 50px;
    }
    a:hover {
      background-color: orange;
    }
  </style>
  <body>
    <div class="slider">
      <a href="#">选驾校</a>
      <a href="#">注册交管123</a>
      <a href="#">科目一学习</a>
      <a href="#">科目二学习</a>
      <a href="#">科目三学习</a
      ><a href="#">学习检测</a>
      <a href="#">交通警示视频</a>
    </div>
  </body>
```

八、背景

```css
background-color: 	transprent | color;
background-image:	none | url;	
background-repeat:	repeat-x | repeat-y | no-repeat | repeat;  //默认平铺
background-position:	left top  | 20px,50px  |  20px center
//方位词：两个参数时顺序不重要，也可以只写一个参数，另一个默认居中；
//精确位置：20px，50px； 第一个x，第二个y ； 
//也可以方位和位置混用
background-attachment:	scroll 、 fixed
//背景的复合写法 无顺序要求
background: black url() no-repeat fixed center 20px;
//补充：rgba()第四个参数可以设置透明度
```

九、CSS三大特性

9.1 层叠性

样式存在冲突，遵循就近原则（样式离结构近），书写顺序最后的那个，远的会被覆盖，冲突的具体样式才会覆盖，其他的不会；层叠性针对于相同权重的选择器

9.2 继承性

子标签会继承父标签的某些样式，如text、font等文字相关的会继承，其他的不会被继承，eg在body中设置全局字体 

9.3 优先级

选择器相同：则按照层叠性来；

选择器不同：则按照权重来；

| 选择器               | 权重       |
| -------------------- | ---------- |
| 继承或者 *           | 0，0，0，0 |
| 元素选择器           | 0，0，0，1 |
| 类选择器、伪类选择器 | 0，0，1，0 |
| ID选择器             | 0，1，0，0 |
| 行业样式 style=" "   | 1，0，0，0 |
| !important           | limit      |

注意继承的权重是0

```html
  <style>
    .slider {
      color: blueviolet;
    }
    a {
      color: burlywood;
    }
    .slider .item {
      color: red;
    }
    .slider li {
      color: cornflowerblue;
    }
    .item {
      color: cyan;
    }
  </style>
  <body>
    <div class="slider">
      <ul>
        <li class="item">thats spec test</li>
        <li>thats spec 1</li>
        <li>thats spec 2</li>
      </ul>
      <a href="#">选驾校</a>
    </div>
  </body>

//尽管类选择器的优先级大于标签选择器，但类选择器选择的是父元素，而继承的权重是0
```

9.4 权重的叠加

复合选择器会有权重叠加的问题，代码中的ul可以证实（0，0，0，2） 

十、盒子模型

10.1 border 

```css
border-width:	1px;
border-style:	dashed;
border-color:	red;
border:1px solid red ;
border-bottom:	1px solid red;

border-radius:10px;  //圆角边框 CSS3，单位也可以是百分数，50%  宽度的一半，可以跟2.3.4个值分别代表lt、rt、rb、lb，
//或者分开写：border-top-left:
//对于table来说，相邻的td的两个边框叠在一块，视觉看起来会变粗，这时可用：
border-collapse: collapse;
//border会影响视觉上盒子的大小，eg：
.item {
    width:200px;
    height:200px;
    border:1opx;
}
//视觉上这个盒子的宽高都为220px
```

10.2 padding

```css
padding:	10px;   //上下左右
padding:	5px 10px ;  //上下5，左右10
padding:	5px 10px 20px;	//上5 左右 10 下20
padding:	5px 10px 15px 20px  //上右下左

//同border一样，padding也会影响盒子的大小，eg：本来200宽高的盒子，加了10的padding，变成220
//如果盒子本身没有指定宽高，则padding不会影响其盒子大小
```

10.3 margin

```css
//marign的写法、参数个数与padding一致
//外边距可以让盒子水平居中，但必须满足两个条件：
1.盒子必须指定宽度；
2.盒子左右外边距设置为auto；
margin:0 auto;

以上是对于块级元素，对于没有宽高的行内元素或者行内块元素来说，可以设置其父元素text-align:center;
```

10.4 盒子阴影

| 属性     | 描述                             |
| -------- | -------------------------------- |
| h-shadow | 水平阴影位置，允许为负，required |
| v-shadow | 垂直阴影位置，允许为负，required |
| blur     | 模糊距离                         |
| spread   | 阴影尺寸                         |
| color    | 阴影颜色                         |
| insert   | 外部阴影改为内部阴影             |

```html
  <style>
    h3 {
      background-color: blueviolet;
      height: 200px;
      padding: 10px;
      border-radius: 20px;

      box-shadow: 10px 20px 10px 20px royalblue inset;
      /* 影子不占据空间，不会占用（挤）其他元素 */
    }
  </style>
  <body>
    <h3>thats a text</h3>
  </body>
```

十一、浮动

11.1 浮动

传统网页布局的三种方式：普通流（标准流）、浮动、定位

| 布局方式 | 描述                                 |
| -------- | ------------------------------------ |
| 标准流   | 按照默认方式排列，div、行内、块 etc. |
| 浮动     | 改变元素默认的排列方式               |
| 定位     |                                      |

float 属性用于创建浮动框，将其移动到一边，直到左右（右）边缘触及或包含块或另一个浮动的边缘

**浮动特性**：

1.浮动特性会脱离标砖流；脱标以后不再保留原先的位置；

2.浮动的元素会一行内显示且元素顶部对齐；父元素如果装不下一行的所有元素，会另起一行；

3.浮动的元素具有行内块元素的特性；（行内元素有了宽高、块内元素可以在一行（不单独占一行了，如果没设置宽高，则根据内容来适配））

浮动经常搭配标准流的父元素来使用

```html
  <style>
    * {
      margin: 0;
      padding: 0;
    }
    ul {
      width:930px;
      height: 350px;
      background-color: burlywood;
      margin: 0 auto;
    }
    li {
      width:290px;
      height: 300px;
      float: left;
      list-style: none;
      background-color: cyan;
      margin-top: 25px;
      margin-left: 10px;
      margin-right: 10px;
    }
  </style>
  <body>
    <span>他说这世界不该是我们的</span>
    <ul>
      <li>骑行装备</li>
      <li>跑步装备</li>
      <li>游泳装备</li>
    </ul>
  </body>
```

浮动盒子只会影响后面的标准流（盖住），不会影响前面的标准流

**清除浮动**：现实场景中子盒子的数量是可变的，不能写死父盒子的高度，策略是不设置父盒子的高度，但这样又会导致父盒子高度为0，通过清除浮动来避免浮动带来的影响。

1.额外标签法-隔墙法

在子元素的最后添加一个块元素，清除该盒子的浮动，不常用，如下：

```html
  <style>
    * {
      margin: 0;
      padding: 0;
    }
    ul {
      background-color: burlywood;
      margin: 0 auto;
      border:  1 solid brown;
    }
    li {
      width:290px;
      height: 300px;
      float: left;
      list-style: none;
      background-color: cyan;
      margin-top: 25px;
      margin-left: 10px;
      margin-right: 10px;
    }
    .foot {
      width: 200px;
      height: 200px;
      background-color:brown ;
    }
    .sep {
      clear: both;
    }
  </style>
  <body>
    <span>他说这世界不该是我们的</span>
    <ul>
      <li>骑行装备</li>
      <li>跑步装备</li>
      <li>游泳装备</li>
      <div class="sep"></div>
    </ul>
    <div class="foot">
    </div>
  </body>
```

2.父元素添加overflow

设置父元素的overfow属性为hidden、auto、scroll

```html
  <style>
    * {
      margin: 0;
      padding: 0;
    }
    ul {
      overflow: hidden;
      background-color: burlywood;
      margin: 0 auto;
      border:  1 solid brown;
    }
    li {
      width:290px;
      height: 300px;
      float: left;
      list-style: none;
      background-color: cyan;
      margin-top: 25px;
      margin-left: 10px;
      margin-right: 10px;
    }
    .foot {
      width: 200px;
      height: 200px;
      background-color:brown ;
    }
  </style>
  <body>
    <span>他说这世界不该是我们的</span>
    <ul>
      <li>骑行装备</li>
      <li>跑步装备</li>
      <li>游泳装备</li>
    </ul>
    <div class="foot">
    </div>
  </body>
```

3.:after 伪元素

```html
 <style>
    .clearfix:after {
      content: "";
      display: block;
      height: 0;
      clear: both;
      visibility: hidden;
    }
    .clearfix {
      *zoom:1;
    }
    * {
      margin: 0;
      padding: 0;
    }
    ul {
      background-color: burlywood;
      margin: 0 auto;
      border:  1 solid brown;
    }
    li {
      width:290px;
      height: 300px;
      float: left;
      list-style: none;
      background-color: cyan;
      margin-top: 25px;
      margin-left: 10px;
      margin-right: 10px;
    }
    .foot {
      width: 200px;
      height: 200px;
      background-color:brown ;
    }
  </style>
  <body>
    <span>他说这世界不该是我们的</span>
    <ul class="clearfix">
      <li>骑行装备</li>
      <li>跑步装备</li>
      <li>游泳装备</li>
    </ul>
    <div class="foot">
    </div>
  </body>
```

4.双伪元素清除

```html
 <style>
    .clearfix:before, .clearfix:after {
      content: "";
      display: table;
    }
    .clearfix::after {
      clear: both;
    }
    .clearfix {
      *zoom:1;
    }
    * {
      margin: 0;
      padding: 0;
    }
    ul {
      background-color: burlywood;
      margin: 0 auto;
      border:  1 solid brown;
    }
    li {
      width:290px;
      height: 300px;
      float: left;
      list-style: none;
      background-color: cyan;
      margin-top: 25px;
      margin-left: 10px;
      margin-right: 10px;
    }
    .foot {
      width: 200px;
      height: 200px;
      background-color:brown ;
    }
  </style>
  <body>
    <span>他说这世界不该是我们的</span>
    <ul class="clearfix">
      <li>骑行装备</li>
      <li>跑步装备</li>
      <li>游泳装备</li>
    </ul>
    <div class="foot">
    </div>
  </body>
```

