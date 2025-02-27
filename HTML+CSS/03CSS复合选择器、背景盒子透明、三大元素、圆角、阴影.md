# 一、CSS的复合选择器

## 1.1 什么是复合选择器

在 CSS 中，可以根据选择器的类型把选择器分为：`基础选择器` 和 `复合选择器`，复合选择器是建立在基础选择器之上，对基础选择器进行**组合形成**的。

- 复合选择器可以更准确、更高效的选择目标元素（标签）
- 复合选择器是由两个或多个基础选择器，通过不同的方式组合而成的
- 常用的复合选择器包括：**后代选择器**、**子选择器**、**并集选择器**、**伪类选择器**等

## 1.2 后代选择器

`后代选择器` 又称为 `包含选择器`，可以选择父元素里面子元素。其写法就是把外层标签写在前面，内层标签写在后面，中间用空格分隔。当标签发生嵌套时，内层标签就成为外层标签的后代。

**语法：**

```css
元素1 元素2 { 样式声明 }
```

上述语法表示选择 元素 1 里面的**所有**元素 2 （后代元素）。 

**例如：**

```css
div p {
            color: red;
        }
```

- 元素1 和 元素2 中间用 **空格** 隔开
- 元素1 是父级，元素2 是子级，最终选择的是 元素2，即：元素1 是不会生效样式的
- 元素2 可以是儿子，也可以是孙子等，只要是 元素1 的后代即可
- 元素1 和 元素2 **可以是任意基础选择器**

## 1.3 子选择器

子元素选择器（子选择器）只能选择作为某元素的**最近一级子元素**，简单理解就是选亲儿子元素。

注意：是**最近一级而并非最近一个**！

**语法：**

```css
元素1>元素2 { 样式声明 }
```

上述语法表示选择元素1 里面的所有直接后代（子元素）元素2。

**例如：**

```css
div>p { 样式声明 } 	/* 选择 div 里面所有最近一级 p 标签元素 */
```

- 元素1 和 元素2 中间用 **大于号** 隔开

- 元素1 是父级，元素2 是子级，最终选择的是元素2，即元素1 是不会生效样式的

- 元素2 **必须是亲儿子，其孙子、重孙之类都不归他管**，你也可以叫：亲儿子选择器

## 1.4 交集选择器

  选中页面中 同时满足 多个选择器的标签，满足**即又的关系**，**主要是可以提高被选择元素的权重**；

  **基本语法**

   **选择器1选择器2 {  css样式 }**

  01、交集选择器可以更加精准的选择某一个元素，**相当于即又关系**，也就是两个需求都要满足（比如：我要找一个人，这个人是男生并且有个名字叫老王  ----  男生老王）；

  02、最常用的还是**标签选择器和类选择器的搭配使用**,选择器2也可以是id选择器；

  03、交集选择器两个选择器之间是绝对不能书写空格，有了空格就会变成后代选择器；

  ```html
      <style>
          div {
              width: 200px;
              height: 100px;
              background-color: aquamarine;
          }
  
          /*  选择器1选择器2 {  css样式 } */
          div.box {
              background-color: green;
          }
          /* 交集选择器的选择权重会大于直接类选择器 */
          .box {
              background-color: red;
          }
      </style>
      <div>1</div>
      <div class="box">2</div>
      <div>3</div>
  ```

  **注意：交集选择器后期经常用来提升元素的选择权重**，以下的代码会选择第二个样式；

  ```html
          .list .san {
              color: green;
          }
  
          .list li.san {
              color: gold;
          }
  ```

  

## 1.5 并集选择器

`并集选择器` 可以选择多组标签，同时为他们定义相同的样式，通常用于**集体声明**。
`并集选择器` 是各选择器通过**英文逗号** `,` 连接而成，任何形式的选择器都可以作为并集选择器的一部分。

**语法：**

```css
元素1, 元素2, 元素3 { 样式声明 }
```

```css
元素1,
元素2,
元素3 {
    样式声明
}
/* 推荐写法，编码风格 */
```

上述语法表示选择元素1、元素2 和 元素3。

**例如：**

```css
ul, div { 样式声明 }		 /* 选择 ul 和 div标签元素 */
```

- 元素1 和 元素2 中间用逗号隔开（最后一个不加逗号）
- 逗号可以理解为和的意思
- 并集选择器通常用于集体声明

```html
<!doctype html>
<html lang="en">

<head>
    <title>复合选择器之并集选择器</title>
    <style>
        /* 要求1：请把熊大和熊二改为粉色 */
        /* div,
        p {
            color: pink;
        } */

        /* 要求2：请把熊大和熊二改为红色，还有小猪一家改为粉色 */
        div,
        p,
        .pig li {
            color: pink;
        }
        /* 语法规范：并集选择器通常竖着写 */
    </style>
</head>

<body>
    <div>熊大</div>
    <p>熊二</p>
    <span>光头强</span>
    <ul class="pig">
        <li>小猪佩奇</li>
        <li>猪爸爸</li>
        <li>猪妈妈</li>
    </ul>
</body>

</html>
```

## 1.6 伪类选择器

`伪类选择器` 用于**向某些选择器添加特殊的效果**，比如：给链接添加特殊效果（链接伪类），或选择第 n 个元素（结构伪类）。
`伪类选择器` 书写最大的特点是用**冒号** `:` 表示，比如：`:hover`、`:first-child`。 
因为伪类选择器很多，比如：`链接伪类`、`结构伪类` 等，所以这里先讲解常用的链接伪类选择器。

> 伪类的由来：因为在页面中并没有这个真实存在的类，所以称为 “伪类”。

### 1.6.1 常见伪类状态（了解）

选择器:link         鼠标未访问的链接（访问前）
选择器:visited    鼠标已访问的链接（访问后）
选择器:hover      鼠标移动到连接上（鼠标经过）
选择器:active      鼠标选定的链接（按下鼠标的时候）

**注意：**如果以上四个状态都要书写必须按照L~V~H~A的顺序来书写，否则就会失去效果；

```html
    <style>
        /* 鼠标访问前 */
        a:link {
            color: red;
        }

        /* 鼠标访问后 */
        a:visited {
            color: green;
        }

        /* 鼠标访问的时候 */
        a:hover {
            color: royalblue;
        }

        /* 鼠标按下的时候 */
        a:active {
            color: tomato;
        }
    </style>

    <a href="#"></a>
```

### 1.6.2 伪类选择器实际工作的用法（死了都要记）

实际开发中我们不会将伪类的四个状态都书写，我们只需要设置鼠标访问状态:hover即可；

01、统一设置一个超链接a的样式，表示我们四个状态的样式都一致；

02、然后通过样式覆盖的原理，设置鼠标访问:hover的样式即可；

```html
    <style>
        /*01、设置a的四个状态link、visited、hover、active的样式都一致 */
        .nav li a {
            font-style: 18px;
            color: #333;
        }

        /* 02、单独设置鼠标访问经过的样式覆盖前面的样式即可 */
        .nav li a:hover {
            color: red;
        }
    </style>
    <div class="nav">
        <ul>
            <li><a href="#">首页</a></li>
            <li><a href="#">产品分类</a></li>
            <li><a href="#">联系我们</a></li>
        </ul>
    </div>
```

### 1.6.3 focus伪类选择器

用于选取获表单元素的焦点，一般input表单或者文本域textarea才能获取该焦点；

```html
    <style>
        input:focus {
            background: springgreen;
        }

        textarea:focus {
            background-color: thistle;
        }
    </style>

    <input type="text">
    <textarea cols="30" rows="10"></textarea>
```

### 1.6.4 ::placeholder占位符的颜色修改（死了都要记）

我们只能用这样方法修改占位符的颜色，其他样是不能 在这里修改；

```css
        input::placeholder {
            color: red;
        }
```



## 1.7 复合选择器总结

| 选择器          | 作用                   | 特征             | 使用情况 | 隔开符号及用法                             |
| --------------- | ---------------------- | ---------------- | -------- | ------------------------------------------ |
| 后代选择器      | 用来选择后代元素       | 可以是子孙后代   | 较多     | 符号是空格 `.nav a`                        |
| 子代选择器      | 选择最近一级元素       | 只选亲儿子       | 较少     | 符号是大于 `.nav>p`                        |
| 并集选择器      | 选择某些相同样式的元素 | 可以用于集体声明 | 较多     | 符号是逗号 `.nav`, `.header`               |
| 链接伪类选择器  | 选择不同状态的链接     | 跟链接相关       | 较多     | 重点记住 `a{}` 和 `a:hover` 实际开发的写法 |
| `:focus` 选择器 | 选择获得光标的表单     | 跟表单相关       | 较少     | `input:focus` 记住这个写法                 |

强调：复合选择器的层级写得越细越好（可读性，可维护性，安全性），同时将复合选择器的层级写得越细，可以提前避免大部分的选择器优先级混乱！

# 二、CSS 的背景（background）

通过 CSS 背景属性，可以给页面元素添加背景样式。
背景属性可以设置 `背景颜色`、`背景图片`、`背景平铺`、`背景图片位置`、`背景图像固定` 等。

## 3.1 背景颜色(bgc) *background-color*

`background-color` 属性定义了元素的背景颜色。

```css
background-color: 颜色值;
```

一般情况下元素背景颜色默认值是 `transparent`（透明），我们也可以手动指定背景颜色为透明色。

```css
background-color: transparent;
```

目前 CSS 还支持丰富的渐变色，但是某些浏览器不支持，这里了解即可，具体内容请查阅资料。

```html
    <title>渐变</title>
    <style>
        #grad1 {
            height: 200px;
            /* 浏览器不支持时显示 */
            background-color: red;
            /* 线性渐变 - 从上到下（默认情况下）*/
            background-image: linear-gradient(#e66465, #9198e5);
        }
    </style>
</head>

<body>
    <h3>线性渐变 - 从上到下</h3>
    <p>从顶部开始的线性渐变。起点是红色，慢慢过渡到蓝色：</p>

    <div id="grad1"></div>

    <p><strong>注意：</strong> Internet Explorer 9 及之前的版本不支持渐变。</p>
</body>

```

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210162054006.jpg)

## 3.2 背景图片(bgi)  *background-image*

`background-image` 属性描述了元素的背景图像，实际开发常用于 **logo** 或者一些**装饰性的小图片**或者是**超大的背景图片**, 优点是非常便于控制位置（精灵图也是一种运用场景）。

```css
background-image : none | url(url)
```

| 参数值 | 作用                           |
| ------ | ------------------------------ |
| `none` | 无背景图（默认的）             |
| `url`  | 使用绝对或相对地址指定背景图像 |

注意：背景图片后面的地址，千万不要忘记加 URL， 同时里面的路径不要加引号。

```css
background-color: pink;
background-image: url(../images/logo.png);
/* 1、背景图片不平铺 */
/* background-repeat: no-repeat; */
/* 2、默认情况下，背景图片是平铺的 */
/* background-repeat: repeat; */ /* 页面元素既可以添加背景颜色也可以添加背景图片，只不过背景图片区域会覆盖背景颜色 */
```

## 3.3 背景平铺(bgr) *background-repeat*

如果需要在 HTML 页面上对背景图像进行平铺，可以使用 `background-repeat` 属性。

```css
background-repeat: repeat | no-repeat | repeat-x | repeat-y
```

| 参数值      | 作用                                 |
| ----------- | ------------------------------------ |
| `repeat`    | 背景图像在纵向和横向上平铺（默认的） |
| `no-repeat` | 背景图像不平铺                       |
| `repeat-x`  | 背景图像在横向上平铺                 |
| `repeat-y`  | 背景图像在纵向上平铺                 |

## 3.4 背景图片位置(bgp) *background-position*

利用 `background-position` 属性可以改变图片在背景中的位置。

```css
background-position: x y;
```

参数代表的意思是：x 坐标 和 y 坐标，可以使用 `方位名词` 或者 `精确单位`。

| 参数值     | 说明                                              |
| ---------- | ------------------------------------------------- |
| `length`   | 百分数 \| 由浮点数字和单位标识符组成的长度值      |
| `position` | top \| center \| bottom \| left \| rigth 方位名词 |

- 参数是方位名词
  - 如果指定的两个值都是方位名词，则两个值前后顺序无关，比如 left top 和 top left 效果一致
  - 如果只指定了一个方位名词，另一个值省略，则**第二个值默认居中对齐**


- 参数是精确单位
  - 如果参数值是精确坐标，那么第一个肯定是 x 坐标，第二个一定是 y 坐标
  - 如果只指定一个数值，那该数值一定是 x 坐标，**另一个默认垂直居中**
- 参数是百分比
  - 取值为百分计算的值是按照父级盒子宽高计算的
  - 如果取值为一个值，那么这个值是表示左右的水平位置，垂直方向的位置默认居中显示；


```css
background-position: 50% 50%;
```


- 参数是混合单位
  - 如果指定的两个值是精确单位和方位名词混合使用，则第一个值是 x 坐标，第二个值是 y 坐标

## 3.5 背景图像固定(bga)*background-attachment*

`background-attachment` 属性设置背景图像是否固定或者随着页面的其余部分滚动。

`background-attachment` 后期可以制作 `视差滚动` 的效果。

```css
background-attachment : scroll | fixed
```

| 参数     | 作用                                                       |
| -------- | ---------------------------------------------------------- |
| `scroll` | 背景图像是随对象内容滚动的（可见区域取决于背景图像的高度） |
| `fixed`  | 背景图像固定                                               |

## 3.6 背景复合写法

为了简化背景属性的代码，我们可以将这些属性合并简写在同一个属性 `background` 中，从而节约代码量。
当使用简写属性时，没有特定的书写顺序，一般习惯约定顺序为：
`background`: `背景颜色` `背景图片地址` `背景平铺` `背景图像滚动` `背景图片位置`

![08](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210162112536.png)

```css
background: magenta url(./img/icon.png) no-repeat 5px center;
```

这是实际开发中，我们更提倡的写法。

## 3.7背景尺寸设置（bgs）*background-size*

如果背景图片小于当前的盒子或者大于当前的盒子，设置背景图的尺寸大小；

- 取值为cover（常用）

背景图等比缩放，一直到铺满整个盒子

```css
background-size: cover;
```

**注意：**该属性取值如果**背景图和盒子比例不一致**。可能会导致背景图过大超出盒子显示不全，溢出隐藏；

- 取值为contain 

背景图等比缩放，直到背景图的宽或者高和盒子一致就停止缩放

```css
background-size: contain;
```

**注意：**该属性取值如果背景图和盒子比例不一致可能会导致背景图不会完全铺满盒子；

- 取值为实际像素大小（移动端小图标常用）

设置背景图大小固定，一般我们可以让宽设置固定的值，然后让高为auto自动计算

```css
background-size: 45px auto;
```

## 3.8 背景颜色透明rgba（死了都要会）

我们可以设置背景颜色的透明度从而实现透明效果；

**语法： rgba(red, green, blue, alpha)**

alpha取值为0-1之间，0表示完全透明，1表示不透明，之间的数字表示透明的程度

```css
background-color: rgba(0,0,0,.5);
```

**注意：**rgba只能设置背景颜色透明不会影响盒子里面的内容透明；

## 3.10 背景总结

| 属性                   | 作用           | 值                                               |
| ---------------------- | -------------- | ------------------------------------------------ |
| `backgroud-color`      | 背景颜色       | 预定义的颜色值 / 十六进制 / RGB代码              |
| `backgroud-image`      | 背景图片       | url（图片路径）                                  |
| `backgroud-repeat`     | 是否平铺       | repeat / no-repeat / repeat-x / repeat-y         |
| `backgroud-position`   | 背景位置       | length / position 分别是 x 和 y 坐标             |
| `backgroud-attachment` | 背景附着       | scroll（背景滚动）/ fixed（背景固定）            |
| `背景简写`             | 书写更简单     | 背景颜色 背景图片地址 背景平铺 背景滚动 背景位置 |
| `背景色半透明`         | 背景颜色半透明 | background: rgba(0, 0, 0, 0.3); 后面必须是4个值  |

# 三、盒子透明opacity

**语法： *opacity*: 透明值；**

opacity 设置盒子的透明，取值为0-1之间，0表示完全透明，1表示不透明，之间的小数表示透明的程度

```css
 opacity: .5;
```

**注意：**用opacity 设置透明，不仅让背景颜色透明，也会影响盒子里面的内容也跟着透明，所以我们不建议使用，后期在制作css3的动画时会用到；

# 四、CSS 的元素显示模式

## 2.1 什么是元素显示模式

**作用：**网页的标签非常多，在不同地方会用到不同类型的标签，了解他们的特点可以更好的布局我们的网页。

`元素显示模式` 就是元素（标签）以什么方式进行显示，比如 `<div>` 自己占一行，比如一行可以放多个 `<span>`。

HTML 元素一般分为 `块元素` 和 `行内元素` 两种类型。

## 2.2 块元素

常见的块元素有 `<h1> ~ <h6>`、`<p>`、`<div>`、`<ul>`、`<ol>`、`<li>`、`<dl>`、`<dt>`、`<dd>`、`<table>`、`<tr>`、`<form>` 等，其中  `<div>` 标签是最典型的块元素。

**块级元素的特点：**

- 比较霸道，自己独占一行
- 高度，宽度、外边距以及内边距都可以控制
- 宽度默认是容器（父级宽度）的 100%
- 是一个容器及盒子，里面可以放行内或者块级元素

**注意：**

- 块元素里面可以嵌套任何元素，但是段落标签p里面不能嵌套div标签，因为浏览器解析的时候会将p      嵌套div解析成两个p标签，一个div标签显示；

## 2.3 行内元素

常见的行内元素有 `<a>`、`<span>`、`<em>`、`<strong>` 等，其中 `<span>` 标签是最典型的行内元素，有的地方也将行内元素称为内联元素。

**行内元素的特点：**

- 相邻行内元素在一行上，一行可以显示多个

- 高、宽直接设置是无效的

- 默认的宽是由内容多少撑开的

- 设置内外边距上下不生效，左右生效

- 行内元素中只能嵌套文本图片或者其他行内元素，但是**超链接a里面可以嵌套块级元素**

**注意：**

- 链接里面不能再放链接
- 特殊情况链接 `<a>` 里面可以放块级元素，但是给 `<a>` 转换一下块级模式最安全

## 2.4 行内块元素

在行内元素中有几个特殊的标签：`<img>`、`<input>`、`<th>`、`<td>`、`button`，它们同时具有 `块元素` 和 `行内元素` 的特点，有些资料称它们为 `行内块元素`。

**行内块元素的特点：**

- 和相邻行内元素（行内块）在一行上，但是他们之间会有空白缝隙。一行可以显示多个（行内元素特点）
- 默认宽度就是它本身内容的宽度（行内元素特点）
- 高度，行高、外边距以及内边距都可以控制（块级元素特点）

## 2.5 元素显示模式总结

| 元素模式   | 元素排列               | 设置样式                 | 默认宽度         | 包含                   |
| ---------- | ---------------------- | ------------------------ | ---------------- | ---------------------- |
| 块级元素   | 一行只能放一个块级元素 | 可以设置宽度和高度       | 容器的 100%      | 容量级可以包含任何标签 |
| 行内元素   | 一行可以放多个行内元素 | 不可以直接设置宽度和高度 | 它本身内容的宽度 | 容纳文本或其他行内元素 |
| 行内块元素 | 一行放多个行内块元素   | 可以设置宽度和高度       | 它本身内容的宽度 |                        |

学习元素显示模式的主要目的是分清它们各自的特点，当我们网页布局的时候，在合适的地方用合适的标签元素。

## 2.6 元素显示模式转换display（死了都要记）

实际开发中各个元素的显示模式是可以通过display设置不同的属性值实现的；

- **将元素转化为块元素（重点）   display:block;**
- **将元素转化为行内元素      display:inline;**   
- **将元素转化为行内块元素     display:inline-block;**

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>元素显示模式之显示模式的转换</title>
    <style>
        a {
            width: 150px;
            height: 50px;
            background-color: orange;
            /* 把行内元素 a 转换为 块级元素 */
            display: block;
        }

        div {
            width: 300px;
            height: 100px;
            background-color: black;
            color: white;
            /* 把 div 块级元素转化为行内元素 */
            display: inline;
        }

        span {
            width: 300px;
            height: 30px;
            background-color: skyblue;
            /* 行内元素转化为行内块元素 */
            display: inline-block;
        }
    </style>
</head>

<body>
    <a href="#">我是行内元素</a>
    <a href="#">我是行内元素</a>
    <div>我是块级元素</div>
    <div>我是块级元素</div>
    <span>行内元素转化为行内块元素</span>
    <span>行内元素转化为行内块元素</span>
</body>

</html>
```

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210162055936.jpg)

# 五、css3常用新属性（死了都要会）

## 5.1 圆角*border-radius*

CSS 3 新增了圆角边框样式。

border-radius 属性用于设置元素的外边框圆角。

border-radius 顾名思义：边框半径。

（椭）圆与边框的交集形成圆角效果。

```html
        div {
            width: 300px;
            height: 150px;
            background-color: pink;
            border-radius: 24px;
        }
```

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210162220391.jpg)
- 圆角矩形

*border-radius*取值为一个实际像素

```css
        .box {
            width: 300px;
            height: 100px;
            background-color: #f00;
            border-radius: 15px;
        }
```

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210162228283.png)

- 圆形

矩形必须是正方形，设置border-radius取值大于等于高度一半或者直接设置50%

```css
        .box {
            width: 100px;
            height: 100px;
            background-color: #f00;
            /* border-radius: 50px; */
            border-radius: 50%;
        }
```

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210162228292.png)

- 胶囊形状

矩形必须是长方形，设置border-radius取值大于等于高度一半；

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210162228294.png)

```css
        .box {
            width: 300px;
            height: 50px;
            background-color: #f00;
            border-radius: 25px;
        }
```

* 椭圆

如果设置border-radius取值为50%，会绘制椭圆

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210162228296.png)

```
        .box {
            width: 300px;
            height: 50px;
            background-color: #f00;
            border-radius: 50%;
        }
```

- 半圆

设置border-radius取值个数为4个值：分别是：**左上角  右上角  右下角 左下角**

语法：**border-radius：左上角  右上角  右下角 左下角；**

```
        .box {
            width: 100px;
            height: 100px;
            background-color: #f00;
            border-radius: 0 50px 50px 0;
        }

        .box1 {
            width: 100px;
            height: 100px;
            background-color: #f00;
            border-radius: 50px 0 0 50px;
        }
```

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210162228285.png)

注意：

- 参数值可以为数值或百分比的形式
- 如果是正方形，想要设置为圆形，那么只需要把数值修改为高度或者宽度的一半即可，或者直接写为 50%
- 如果是个矩形，设置为高度的一半就可以做 “胶囊” 效果了



## 5.2 盒子阴影

CSS 3 新增了盒子阴影。

box-shadow 属性用于为盒子添加阴影。

语法：

```css
box-shadow: h-shadow v-shadow blur spread color inset;
box-shadow:水平阴影   垂直阴影   模糊距离   阴影大小   阴影颜色  内/外阴影；
```

| 值         | 描述                                                         |
| ---------- | ------------------------------------------------------------ |
| `h-shadow` | 必须。水平阴影的位置，允许负值。                             |
| `v-shadow` | 必须。垂直阴影的位置，允许负值。                             |
| `blur`     | 可选。模糊距离（虚实程度）。                                 |
| `spread`   | 可选。阴影的尺寸（大小）。                                   |
| `color`    | 可选。阴影的颜色，请参阅 CSS 颜色值（阴影多为半透明颜色）。  |
| `inset`    | 可选。将外部阴影（outset）改为内部阴影（outset 不能指定，默认为空即可）。 |

```html
        div {
            width: 200px;
            height: 200px;
            background-color: salmon;
            margin: 100px auto;
            /* box-shadow: 10px 10px; */
        }

        /* 伪类不仅仅可以用于 a 链接，还能用于其他标签 */
        /* 原先盒子没有影子,当我们鼠标经过盒子就添加阴影效果 */
        div:hover {
            box-shadow: 10px 10px 10px -4px rgba(0, 0, 0, .3);
        }
```

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210162220395.gif)

**三边阴影、双边阴影、单边阴影的设置方法：**

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>盒子阴影 三边阴影、双边阴影、单边阴影</title>
    <style>
        div {
            width: 100px;
            height: 100px;
            background-color: #000;
            margin: 25px auto;
            color: white;
        }

        .a {
            box-shadow: 0 0 25px 5px red;
        }

        /* 三边阴影就是直接把整个阴影部分往下边移 */
        .b {
            box-shadow: 0 6px 10px 0 red;
        }

        /* 两边阴影要用盒子嵌套来解决 */
        .c1 {
            box-shadow: 0 10px 10px -5px red;
        }

        .c2 {
            width: 100%;
            box-shadow: 0 -10px 10px -5px red;
        }

        /* 单边阴影就是直接把整个阴影部分往下边移，并且减小阴影大小 */
        .d {
            box-shadow: 0 10px 10px -5px red;
        }
    </style>
</head>

<body>
    <div class="a">四边阴影</div>
    <div class="b">三边阴影</div>
    <div class="c1">
        <div class="c2">两边阴影</div>
    </div>
    <div class="d">一边阴影</div>
</body>

</html>
```

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210162220384.jpg)

## 5.3 文字阴影

CSS 3 新增了文字阴影。

text-shadow 属性用于为文本添加阴影。

语法：

```css
text-shadow: h-shadow v-shadow blur color;
text-shadow:水平阴影   垂直阴影   模糊距离   阴影颜色 ；
```

| 值         | 描述                                |
| ---------- | ----------------------------------- |
| `h-shadow` | 必须。水平阴影的位置。允许负值。    |
| `v-shadow` | 必须。垂直阴影的位置。允许负值。    |
| `blur`     | 可选。模糊的距离（虚实程度）。      |
| `color`    | 可选。阴影的颜色。参阅 CSS 颜色值。 |

```html
div {
            font-size: 50px;
            color: salmon;
            font-weight: 700;
            text-shadow: 5px 5px 6px rgba(0, 0, 0, .3);
        }
```

