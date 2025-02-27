
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

