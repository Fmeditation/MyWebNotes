# HTML（Hyper Text  Markup  language)

## 一、常用浏览器及内核

IE(Trident)、FireFox(Gecko)、Google、Safari(Webkit)、Opera(Blink)

## 二、W3C 万维网联盟制定的标准（web标准）

结构、表现、行为

## 三、HTML

### 3.1 快捷键

|     快捷键      |       功能       |
| :-------------: | :--------------: |
| shift + alt + ↓ |    复制当前行    |
|     ctrl +d     | 选中所有相同单词 |
|                 |                  |
|                 |                  |
|                 |                  |
|                 |                  |
|                 |                  |
|                 |                  |
|                 |                  |

### 3.2 字符集

```html
<!DOCTYPE html>   //是一个html文档，文档类型声明标签
<html lang="en">   //中英文文档
<head>
      <meta charset="UTF-8">  //字符编码格式
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Document</title>
</head>
<body>
      
</body>
</html>
```

### 3.3 标签

#### 3.3.1 标题标签            

   <h1>-<h6>

#### 3.3.2 段落标签				

分段	<p>

#### 3.3.3 换行标签			

​	强制换行 	单标签	<br/>

#### 3.3.4 文本格式化标签			

| 标签                          | 说明     |
| ----------------------------- | -------- |
| <em></em> or <i></i>          | 倾斜     |
| <del></del> or <s></s>        | 删除线   |
| <ins></ins> or <u></u>        | 下滑线   |
| <strong></strong> or  <b></b> | 标签加粗 |

#### 3.3.5 <div>盒子标签<span> 

盒子标签，没有语义

#### 3.3.6 图像标签	

<img src=""  alt="这段文字代替图片" title="鼠标放在图片上显示文字" width="50" height="50" boeder="5"/>

#### 3.3.7 超链接标签 

​    <a  id="jumpto" href="http://www.baidu.com" target="_self">go to bilibili</a>

_self 和 _blank 之分    #代表空链接     

#### 3.3.8 锚点链接  

去往页面中不同的位置 <a href=" jumpto"></a>

#### 3.3.9 特殊字符显示

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <a href="#two">click here jump to author</a>
    <strong>加粗了吗</strong>
    <b>加粗了吗</b>
    <em>倾斜了吗</em>
    <i>倾斜了吗</i>
    <del>带删除线</del>
    <s>带删除线</s>
    <ins>下划线</ins>
    <u>下划线</u>
    <img src="" alt="这段文字代替图片"/ >
    <a href="www.baidu.com" target="_self">go to bilibili</a>
    <a href="www.baidu.com" target="_blank">go to bilibili</a>
    <h3>Pink Floyd</h3>
    <p>
      是一支来自英国的传奇摇滚乐队，成立于1965年。乐队在音乐史上具有极其重要的地位，他们的音乐风格融合了摇滚、前卫、迷幻和艺术元素，创造了独特而深远的音乐作品。
    </p>
    <p>
      乐队最初由 Syd Barrett、Roger Waters、Richard Wright 和 Nick Mason
      组成，后来 David Gilmour 加入取代了 Syd Barrett。Pink Floyd
      的音乐常常被认为是概念性和探索性的，他们以复杂的音乐结构、深刻的歌词和创新的声音效果而闻名。
      Pink Floyd 的专辑《The Dark Side of the Moon》、《Wish You Were
      Here》、《Animals》和《The Wall》等被认为是摇滚乐史上的经典之作。
    </p>
    <p>
      其中，《The Dark Side of the
      Moon》尤其被誉为史上最伟大的专辑之一，持续在各种排行榜上位列前茅。
      除了音乐上的创新和影响力，Pink
      Floyd的舞台表演也备受赞誉，他们创造了许多视觉和声音效果的壮举，给观众留下深刻的印象。
      尽管在音乐历史上他们的辉煌时期已过，但 Pink
      Floyd的音乐仍然影响着许多乐迷和音乐人，被广泛认为是摇滚乐的先驱和传奇之一。
    </p>
    <p id="two">
      author:chat-GPT <br />
      2024.03.07
    </p>
  </body>
</html>

```

#### 3.3.10 表格标签

<table border="10" align="center">
    <th>name</th>
    <th>gender</th>
	<th>age</th>
    <tr>
        <td>glimour</td>
        <td>male</td>
        <td>25</td>
    </tr>
    <tr>
        <td>luna</td>
        <td><a href="#">female</a></td>
        <td>28</td>
    </tr>

<th></th>代表表头单元格，而<thead></thead>和<tbody></tbody>代表表格结构

<table border="10" align="center">
    <thead>
       <tr>
    <th>name</th>
    <th colspan="2">gender</th>
        </tr>
    </thead>
    <tbody>
         <tr>
        <td>glimour</td>
        <td>male</td>
        <td>25</td>
    </tr>
    <tr>
        <td>luna</td>
        <td><a href="#">female</a></td>
        <td rowspan="2">28</td>
    </tr>
            <tr>
        <td>miniuniu</td>
        <td><a href="#">female</a></td>
   合并单元格：rowspan、colspan

#### 3.3.11 列表标签

1.有序列表

<ol>
    <li>听</li>
    <li>思考</li>
    <li>练习</li>
</ol>

2.无序列表

<ul>
    <li>结构</li>
    <li>表现</li>
    <li>行为</li>
</ul>

ul只能放li不能放其他标签，而li是一个容器标签，可以放其他标签

3.自定义列表

<dl>
    <dt>关于</dt>
    <dd>用户手册</dd>
    <dd>开源手册</dd>
    <dd>软件开源许可</dd>
</dl>

dl中只能包含dt和dd，dt和dd则无限制

#### 3.3.3.12 表单标签112123edqw

三大属性 action、name、methodwqeq21safa

<form>
 <label for="sub">user:</label><input type="text" value="floyd" id="sub"> <br>
 password:<input type="password" value="fagqwq214">  <br>
 gender: male<input type="radio" name="gender" checked=true>  female<input type="radio" name="gender"> <br>
 education: primary <input type="checkbox"> medium<input type="checkbox"> university<input type="checkbox" checked=true> <br>
    career:<select>
        <option>enginner</option>
        <option>saler</option>
        <option selected=true>teacher</option>
    </select>  <br>
<textarea rows="5" cols="15"></textarea> <br>
<input type="submit" value="submit">
<input type="reset" value="reset">
</form>






