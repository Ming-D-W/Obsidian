# 一、CSS三大特性

CSS 有三个非常重要的特性：`层叠性`、`继承性`、`优先级`。

## 1.1 层叠性（覆盖性）

给同一个选择器设置相同的样式，此时一个样式就会**覆盖**（层叠）另一个冲突的样式，**层叠性主要解决样式冲突的问题**。

层叠性原则：

- 样式冲突，遵循的原则是 `就近原则`，哪个样式距离结构近，就执行哪个样式
- 样式不冲突，不会层叠

注：就近的标准是：**后 > 前**

## 1.2继承性

现实中的继承：我们继承了父亲的姓。

CSS 中的继承：**子标签会继承父标签的某些样式**，如：文本颜色和字号，简单的理解就是：子承父业。

- 恰当地使用继承可以简化代码，降低 CSS 样式的复杂性
- 子元素可以继承父元素的样式（ `text-`、`font-`、`line-`、`color` ） 文本、字体、段落、颜色

**行高的继承**

```css
body {
    font: 12px/1.5 'Microsoft YaHei';
}
```

- 行高可以跟单位也可以不跟单位
- 如果子元素没有设置行高，则会继承父元素的行高为 1.5
- 此时子元素的行高是：**当前元素**的**文字大小** * 1.5
- body 行高 1.5 这样写法最大的优势就是**里面的子元素可以根据自己文字的大小自动调整行高**

**注意：**
01、超链接a元素不会继承父级盒子的color颜色，因为浏览器默认给a设置默认的颜色样式，我们需要单独设置a的color颜色；

![01](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210182335808.png)

02、标题标签h1,h2,h3,h5,h6不会直接继承父级盒子的文字大小font-size，因为他们本身自己有默认的文字大小并且是em相对单位，我们得到的结果是我们设置父级文字大小乘以这个倍数；所以我们需要单独设置；

![02](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210182335693.png)

## 1.3 优先级（权重）

- 选择器相同，则执行层叠性
- 选择器不同，则根据选择器权重执行

**选择器权重如下表所示：**

| 选择器               | 选择器权重 |
| -------------------- | ---------- |
| 继承 或  `*`         | `0,0,0,0`  |
| 元素选择器           | `0,0,0,1`  |
| 类选择器、伪类选择器 | `0,0,1,0`  |
| ID 选择器            | `0,1,0,0`  |
| 行内样式 style=""    | `1,0,0,0`  |
| !important 重要的    | `∞` 无穷大 |

**规则：**比较位级别，位级别相同时比较位大小。

**优先级注意问题：**

- 权重是由 4 组数字组成的，但是不会有进位！
- 可以理解为：`类选择器` 永远大于 `元素选择器`，`ID 选择器` 永远大于 `类选择器`，以此类推！
- 等级判断 `从左到右`，如果某一位数值相同，则判断下一位数值
- 可以简单的记忆：`通配符` 和 `继承` 权重为 0，`标签选择器` 为 1，`类`（`伪类`）选择器为 10，`ID` 选择器为 100，`行内样式表` 为 1000，`!important` 无穷大
- 继承的权重是 0，不管父元素权重多高，子元素得到的权重都是 0 ！
- `a` 链接浏览器默认指定了一个样式，所以它不参与继承，所以设置样式需要选中单独设置

```html
<head>

    <title>CSS三大特性之优先级——注意问题</title>
    <style>
        /* 父亲的权重是 100 */
        #father {
            color: red !important;
        }

        /* p 继承的权重为 0 */
        /* 所以以后我们看标签到底执行哪一个样式，就先看这个标签有没有直接被选出来
           如果直接被选择出来了，那么就与父亲无关了！*/
        p {
            color: pink;
        }
    </style>
</head>

<body>
    <!-- 继承的权重是 0，不管父元素权重多高，子元素得到的权重都是 0 -->
    <div id="father">
        <p>你还是很好看</p> <!-- pink -->
    </div>
    <!-- a 链接浏览器默认指定了一个样式，所以它不参与继承，所以给 a 改样式必须直接把 a 选出来 -->
    <a href="#">我是单独的样式</a>
</body>
```

**权重的叠加：**

如果是复合选择器，则会有权重叠加，需要计算权重。

注意：再次强调！权重虽然会叠加，但一定不会进位！（1万个元素选择器也比不过一个类选择器）。

从左到右逐位比较，只有左一位同样大，才比较右边一位！

**例如：**

- `div ul li` ——> `0,0,0,3`
- `.nav ul li` ——> `0,0,1,2`
- `a:hover` ——> `0,0,1,1`
- `.nav a` ——> `0,0,1,1`

如果要对某一元素设置样式，那么就必须给它足够高的权重（注意：是给他，而不是他的父亲！）。

> 提高选择器权重的技巧之一：
>

```html
        /* ul li 权重 0,0,0,1 + 0,0,0,1 = 0,0,0,2 */
        ul li {
            color: green;
        }

        /* li 的权重是 0,0,0,1 */
        li {
            color: red;
        }

        /* .nav li 权重 0,0,1,0 + 0,0,0,1 = 0,0,1,1 */
        .nav li {
            color: pink;
        }
```

# 二、CSS盒子模型（重点）

页面布局要学习**三大核心**：**盒子模型**、**浮动**和**定位**。

学习好盒子模型能非常好的帮助我们布局页面。

## 2.1 看透网页布局的本质

网页布局过程：

- 先准备好相关的网页元素，网页元素基本都是盒子

- 利用 CSS 设置好盒子样式，然后摆放到相应位置

- 往盒子里面装内容

网页**布局的核心**本质： 就是**利用 CSS 摆盒子！**

## 2.2 盒子模型（Box Model）组成

所谓盒子模型：就是把 HTML 页面中的布局元素看作是一个矩形的盒子，也就是一个盛**装内容的容器**。
CSS 盒子模型本质上是一个盒子，封装周围的 HTML 元素，它包括：`边框`、`外边距`、`内边距`、和 `内容`。

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210182330795.png)

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210182330802.jpg)

## 2.3 边框（border）

`border` 可以设置元素的边框。

边框有三部分组成：`边框宽度（粗细）`、`边框样式`、`边框颜色`。

**语法：**

```css
border: border-width || border-style || border-color
```

| 属性           | 作用                      |
| -------------- | ------------------------- |
| `border-width` | 定义边框粗细，单位是 `px` |
| `border-style` | 边框的样式                |
| `border-color` | 边框颜色                  |


边框样式 border-style 可以设置如下值：

- `none`：没有边框，即忽略所有边框的宽度（默认值）
- `solid`：边框为单实线（最为常用的）
- `dashed`：边框为虚线
- `dotted`：边框为点线

**边框简写：**

```css
border: 1px solid red; 	/* 没有顺序 */
```

**边框四边写法：**

```css
    border-top: solid 2px red;
    border-bottom: solid 2px red;
    border-left: solid 2px red;
    border-right: solid 2px red;
```

##### 设置单独某个方向的某个属性

**语法：border-方位名词-属性：属性值；**

```css
    border-left-color: red;
    border-right-style: solid;
    border-top-width: 3px;
```

### 2.3.1 表格的细线边框（边框合并）

表格中两个单元格相邻的边框会重叠在一起，呈现出加粗的效果。

`border-collapse` 属性控制浏览器绘制表格边框的方式。

它控制相邻单元格的边框。

**语法：**

```css
border-collapse: collapse;
```

- `collapse` 单词是合并的意思
- `border-collapse: collapse;` 表示相邻边框合并在一起

```css
	table,
	td,
	th {
	    border: 1px solid black;
	    /* 合并相邻的边框 */
	    border-collapse: collapse;
	    font-size: 14px;
	    text-align: center;
	}
```

### 2.3.2 边框会影响盒子实际大小

边框会额外增加盒子的实际区域大小。因此我们有两种方案解决：

- 测量盒子大小的时候，不量边框
- 如果测量的时候包含了边框，则需要 width、height 减去边框宽度（注意减单边还是双边）

> 注意：盒子实际区域大小 = 内容区大小 + 内边距大小 + 边框大小 + 外边距大小

案例：

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>边框会影响盒子的实际大小</title>
    <style>
        /* 我们需要一个 200*200 的盒子, 但是这个盒子有 10 像素的红色边框 */
        div {
            width: 180px;
            height: 180px;
            background-color: pink;
            border: 10px solid black;
        }
    </style>
</head>

<body>
    <div></div>
</body>

</html>
```

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210171330428.gif)

## 2.4 内边距（padding）

padding 属性用于设置**内边距**，即**边框与内容之间的距离**。

| 属性             | 作用     |
| ---------------- | -------- |
| `padding-left`   | 左内边距 |
| `padding-rigth`  | 右内边距 |
| `padding-top`    | 上内边距 |
| `padding-bottom` | 下内边距 |

padding 属性（简写属性）可以有一到四个值。

| 值的个数                       | 表达意思                                                     |
| ------------------------------ | ------------------------------------------------------------ |
| `padding: 5px;`                | 1 个值，代表上下左右都有 5 像素内边距                        |
| `padding: 5px 10px;`           | 2 个值，代表上下内边距是 5 像素，左右内边距是 10 像素        |
| `padding: 5px 10px 20px;`      | 3 个值，代码上内边距 5 像素，左右内边距 10 像素，下内边距 20 像素 |
| `padding: 5px 10px 20px 30px;` | 4 个值，上是 5 像素，右 10 像素，下 20 像素，左是 30 像素（顺时针） |

以上 4 种情况，我们实际开发都会遇到。

当我们给盒子指定 `padding` 值之后，发生了 2 件事情：

- 内容和边框有了距离，添加了内边距
- `padding` 影响了盒子实际区域大小

也就是说，如果盒子已经有了宽度和高度，此时再指定内边距，会撑大盒子区域！

解决方案：

- 如果保证盒子跟效果图大小保持一致，则让 width、height 减去多出来的内边距大小即可
- 如果盒子本身没有指定 width、height 属性，则此时 padding 不会撑开盒子区域大小



## 2.5 外边距（margin）

`margin` 属性用于设置**外边距**，即控制**盒子和盒子之间的距离**。

| 属性            | 作用     |
| --------------- | -------- |
| `margin-left`   | 左外边距 |
| `margin-right`  | 右外边距 |
| `margin-top`    | 上外边距 |
| `margin-bottom` | 下外边距 |

`margin` 简写方式代表的意义跟 `padding` 完全一致。

外边距典型应用：

外边距可以让**块级盒子水平居中**，但是必须满足两个条件：

- 盒子必须指定了宽度 `width`
- 盒子左右的外边距都设置为 `auto`

```css
.header { width: 960px; margin: 0 auto;}
```

常见的写法，以下三种都可以：

- `margin-left: auto; margin-right: auto;`
- `margin: auto;`
- `margin: 0 auto;`

注意：以上方法是让块级元素水平居中，行内元素或者行内块元素水平居中给其父元素添加 `text-align: center` 即可。

案例：

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>盒子模型之外边距margin</title>
    <style>
        div {
            width: 200px;
            height: 200px;
            background-color: pink;
        }

        /* 
        .one {
            margin-bottom: 20px;
        } 
        */

        .two {
            margin-top: 20px;
        }
    </style>
</head>

<body>
    <div class="one">1</div>
    <div class="two">2</div>
</body>

</html>
```

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210182330604.jpg)

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>块级盒子水平居中对齐</title>
    <style>
        .header {
            width: 900px;
            height: 200px;
            background-color: pink;
            /* 上下 100 左右 auto */
            margin: 100px auto;
        }
    </style>
</head>

<body>
    <div class="header"></div>
</body>

</html>
```

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210182330612.jpg)

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>行内元素、行内块元素水平居中对齐</title>
    <style>
        .header {
            width: 900px;
            height: 200px;
            background-color: pink;
            margin: 100px auto;
            /* 行内元素或者行内块元素水平居中给其父元素添加 text-align: center 即可 */
            text-align: center;
        }

        /* 这样是不起作用的 */
        /* 
        span {
            margin: 0 auto;
        } 
        */
    </style>
</head>

<body>
    <div class="header">
        <span>里面的文字</span>
    </div>
    <div class="header">
        <img src="../image/icon.png" alt="">
    </div>
</body>

</html>
```

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210182330638.jpg)

### 2.1 外边距合并

使用 `margin` 定义块元素的垂直外边距时，可能会出现外边距的合并。

注意：**内边距没有合并一说！浮动的盒子不会发生外边距合并！**

主要有两种情况:

- **相邻块元素垂直外边距的合并**
- **嵌套块元素垂直外边距的塌陷**

#### 2.1.1 相邻块元素垂直外边距的合并

当上下相邻的两个块元素（兄弟关系）相遇时，如果上面的元素有下外边距 `margin-bottom`，下面的元素有上外边距 `margin-top` ，则他们之间的垂直间距不是 `margin-bottom` 与 `margin-top` 之和。而是取两个值中的**较大者**，这种现象被称为相邻块元素垂直外边距的合并（准确的描述应该是：**大的外边距覆盖小的**）。

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210182330847.jpg)

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210182330923.jpg)

**解决方案：**

尽量只给一个盒子添加 `margin` 值。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>相邻块元素垂直外边距的合并</title>
    <style>
        .one {
            width: 200px;
            height: 200px;
            background-color: hotpink;
            margin-bottom: 100px;
        }

        .two {
            width: 200px;
            height: 200px;
            background-color: skyblue;
            margin-top: 100px;
        }
    </style>
</head>

<body>
    <div class="one">one</div>
    <div class="two">two</div>
</body>

</html>
```

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210182330937.gif)

#### 2.1.2 嵌套块元素垂直外边距的塌陷

对于两个嵌套关系（父子关系）的块元素，当子元素有上外边距，此时父元素会塌陷较大的外边距值（**外边距效果显示在父元素之上**）。

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210182330134.png)

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210182330139.jpg)

**解决方案：**

- 可以为父元素定义上边框（比如：可以给一个透明 transparent 边框）
- 可以为父元素定义上内边距
- 可以为父元素添加 `overflow: hidden`

还有其他方法，比如浮动、固定，绝对定位的盒子不会有塌陷问题，后面咱们再总结。

案例：

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>外边距合并-嵌套块级元素垂直外边距塌陷</title>
    <style>
        .father {
            width: 400px;
            height: 400px;
            background-color: black;
            margin-top: 50px;
        }

        .son {
            width: 200px;
            height: 200px;
            background-color: pink;
            margin-top: 100px;
        }
    </style>
</head>

<body>
    <div class="father">
        <div class="son"></div>
    </div>
</body>

</html>
```

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210182330140.gif)

---

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>外边距合并-嵌套块级元素垂直外边距塌陷</title>
    <style>
        .father {
            width: 400px;
            height: 400px;
            background-color: black;
            margin-top: 50px;
            /* border: 1px solid transparent; */
            overflow: hidden;
        }

        .son {
            width: 200px;
            height: 200px;
            background-color: pink;
            margin-top: 100px;
        }
    </style>
</head>

<body>
    <div class="father">
        <div class="son"></div>
    </div>
</body>

</html>
```

<img src="https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210182330141.jpg" style="zoom:50%;" />

**注意：外边距的合并在利用盒子布局页面的时候是经常发生的！**

## 2.6 清除内外边距

网页元素很多都带有默认的内外边距，而且不同浏览器默认的也不一致。因此我们在布局前，首先要清除下网页元素的内外边距。

```css
* {
	padding:0; 	/* 清除内边距 */
	margin:0; 	/* 清除外边距 */
}
```

注意：行内元素为了照顾兼容性，尽量只设置左右内外边距，不要设置上下内外边距（某些时候，行内元素对上下内外边距不生效）。但是转换为块级和行内块元素就可以了。

# 三、盒子模型相关布局问题以及技巧（重点）

## 3.1 盒子的实际占位大小计算

盒子的实际占位大小指的就是我们设置好宽高的基础上累加padding和border的大小；

**盒子的实际宽度  = width + 左右的padding + 左右的border；**

**盒子的实际高度  = height+ 上下的padding + 上下的border；**

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210182357046.png)

## 3.2 padding和border撑大盒子问题

如果盒子宽高设置固定了，再去给盒子添加padding和border就会将盒子的大小撑大；

### **解决方案1：人为手动加多少减多少**：

加多少减多少，将我们自己设置的宽高减去对应的padding和border即可；

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210182357048.png)

### 解决方案2：开启css3的盒子内减模式

直接给盒子设置css3的内减模式 **box-sizing: border-box;**

浏览器在解析的时候就会自己算我们的尺寸，会将设置的padding和border全部减去然后重新计算盒子的大小；

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210182357047.png)

## 3.3 外边距塌陷问题（了解）

### 情况1：上下排列的盒子外边距合并

**上下排列的两个盒子，上面的盒子设置了marin-bottom,下面的盒子设置了margin-top，最终显示的样式两个值谁大就显示谁，小的值被大的值合并了；**

**解决方案**：单独设置给其中某一个盒子，不要两者都设置；

### 情况2：嵌套盒子外边塌陷（外边距穿透）

如果两个盒子有嵌套包含的父子级关系，如果给子级盒子设置了margin-top，效果显示父级盒子也会跟着掉下来；

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210182357047.jpg)

**解决方案1：**给父级盒子设置边框border，只能设置border-top，如果父盒子本身就有border就不会出现塌陷问题；

**解决方案2：**给父级盒子设置内边距padding，只能设置padding-top，如果父盒子本身就有padding就不会出现塌陷问题；

**解决方案3：**给父级盒子设置overflow:hidden；、display:flow-root；利用盒子的BFC模式；

**解决方案4：**如果父级盒子或者子级盒子有了浮动或者定位就不会出现塌陷；

## 3.4 外边距的经典应用：设置盒子水平居中

想要使用**margin:0 auto;**设置一个盒子居中必须满足两个条件：

> 01、盒子必须是块元素，独自占一行；
>
> 02、盒子必须要有固定的宽度；

**注意：实际开发中最常用就是设置版心盒子居中；**

**版心：**网页的主体内容显示的区域，一般是一个固定宽度的盒子，在浏览器的中心显示；版心的类名一般用w或者container表示；目前市场的版心一般都在1200左右（传智1200，京东1190、小米1226）；

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210182357053.png)

**实际的开发中版心是不需要固定的高度的，因为每一个模块的高度不一样；**

```css
        .w {
            width: 1200px;
            margin: 0 auto;
            background-color: red;
        }
```

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210182357048.png)

## 3.4.1 行内元素和行内块元素居中text-align：center；

将行内元素和行内块元素放在一个父级盒子中，设置父级盒子tac即text-align：center；就可以居中

## 3.5 清除内外边距

有些html标签浏览器在解析的时候有默认的内边距padding或者外边居marign，我们需要将默认的样式清除，再去设置自己的样式；

比如：body有8px的默认外边距，ul有默认的内边距等

我们只需在css的最前面将所有标签的margin和padding清0即可；

```css
    * {
        margin: 0;
        padding: 0;
    }
```

## 3.6 细线表格（边框合并）--- 死了都要记

实际工作我们经常使用表格展示数据，我们用css设置细线表格，我们只需要给table、th、td标签同时设置边框border，然后设置边框合并属性*border-collapse*: collapse;即可实现；

```css
        table,
        th,
        td {
            border: 1px solid #ccc;
            border-collapse: collapse;
        }
```

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210182357781.png)

## 3.7 border书写三角形效果（了解）

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210182357783.png)

盒子宽高必须都是0，然后设置盒子四条边都是透明，最后单独设置一个方向的边的颜色即可；

```css
    width: 0;
    height: 0;
    border: 20px solid transparent;
    border-top-color: red;
```

# 四、css3过渡动画（死了都要记） 

**语法：transition: 属性   时间  运动曲线 延时;**

> ```
> 属性：需要改变过渡的属性
> 时间：整个过度动画需要多长时间完成
> 运动曲线 ：动画运动形式默认取值为ease。匀速运动linear；
> 延时：鼠标移入需要等待一段时间再去加载过渡动画；
> ```

**实际开发中一般只会调用属性和时间**

```
transition: 属性   时间；
```

> **注意：**
> 01、同时修改多个属性，需要用英文逗号隔开
> 	transition: width 1s, background-color 1s, height 1s;
> 02，**用逗号隔开书写多个属性过渡太麻烦，我们只需要用一个all表示所有的属性即可**
> 	**transition: all 1s ；**
> 03、**过渡加在本身上，谁做动画给谁加；**
