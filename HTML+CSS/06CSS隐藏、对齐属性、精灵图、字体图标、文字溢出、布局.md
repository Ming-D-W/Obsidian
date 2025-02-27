

## 三、css显示隐藏

### 占位隐藏（了解）

将盒子隐藏掉，然后盒子还是占有位置；

注意：很少使用，在清除浮动的时候会搭配使用；

```css
    /* 占位隐藏 */
    visibility: hidden;
    /* 占位显示 */
    visibility: visible;
```

### 不占位隐藏（死了都要记）

将盒子隐藏掉，然后盒子的位置同时被隐藏掉；

```css
    /* 不占位隐藏 */
    display: none;
    /* 显示隐藏的盒子 */
    display: block;
```

## 五、vertical-align属性（了解）

### 基本语法

**行内和行内块元素默认的对齐方式**是以**基线对齐**的，可能会导致元素和文字，元素和元素之间不能完全对齐；
通过给行内块元素或者行内元素vertical-align的不同取值设置对齐方式，该属性必须设置为当前的行内块元素或者行内元素：

```css
     /* bottom（底线对齐）  */
     vertical-align: bottom;
     /* top（顶线对齐）  */
     vertical-align: top;
     /* middle（中线对齐）  */
     vertical-align: middle;		
```

# 五、vertical-align 属性应用

CSS 的 vertical-align 属性使用场景：经常用于设置图片或者表单（行内块元素）与文字垂直对齐。

官方解释：用于设置一个元素的垂直对齐方式，但是它只针对于行内元素或者行内块元素有效。

语法：

```css
vertical-align: baseline | top | middle | bottom
```

| 值         | 描述                                   |
| ---------- | -------------------------------------- |
| `baseline` | 默认。元素放置在父元素的基线上         |
| `top`      | 把元素的顶端与行中最高元素的顶端对齐   |
| `middle`   | 把此元素放置在父元素的中部             |
| `bottom`   | 把元素的顶端与行中最低的元素的顶端对齐 |

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210212343296.png)

# 一、精灵图

## 1.1 为什么需要精灵图？

一个网页中往往会应用很多小的背景图像作为修饰，当网页中的图像过多时，服务器就会频繁地接收和发送
请求图片，造成服务器请求压力过大，这将大大降低页面的加载速度。

因此，为了有效地减少服务器接收和发送请求的次数，提高页面的加载速度，出现了 CSS 精灵技术（也称
CSS Sprites、CSS 雪碧）。

核心原理：将网页中的一些小背景图像整合到一张大图中 ，这样服务器只需要一次请求就可以了。

精灵技术目的：为了有效地减少服务器接收和发送请求的次数，提高页面的加载速度。

## 1.2 精灵图（sprites）的使用

使用精灵图核心：

1. 精灵技术主要针对于背景图片使用。就是把多个小背景图片整合到一张大图片中
2. 这个大图片也称为 sprites 精灵图 或者 雪碧图
3. 移动背景图片位置以控制显示区域， 此时可以使用 `background-position`
4. 移动的距离就是这个目标图片的 `x` 和 `y` 坐标。注意网页中的坐标有所不同
5. 因为一般情况下都是将精灵图往上往左移动，所以两个坐标数值基本是负值
6. 使用精灵图的时候需要精确测量，每个小背景图片的大小和位置

使用精灵图核心总结：

1. 精灵图主要针对于小的背景图片使用
2. 主要借助于背景位置来实现 `background-position`
3. 一般情况下精灵图都是负值（千万注意网页中的坐标： x轴右边走是正值，左边走是负值， y轴同理） 

【王者荣耀案例】

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210212344612.png)

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>精灵图使用</title>
    <style>
        .box1 {
            width: 60px;
            height: 60px;
            margin: 100px auto;
            background: url(images/sprites.png) no-repeat -182px 0;

        }

        .box2 {
            width: 27px;
            height: 25px;
            /* background-color: pink; */
            margin: 200px;
            background: url(images/sprites.png) no-repeat -155px -106px;

        }
    </style>
</head>

<body>
    <div class="box1"></div>
    <div class="box2"></div>
</body>

</html>
```

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210212344614.png)

## 1.3 案例：拼单词

<img src="https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210212344613.jpg" style="zoom:67%;" />

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>利用精灵图拼出自己名字</title>
    <style>
        span {
            display: inline-block;
            background: url(images/abcd.jpg) no-repeat;
        }

        .p {
            width: 100px;
            height: 112px;
            /* background-color: pink; */
            background-position: -493px -276px;
        }

        .i {
            width: 60px;
            height: 108px;
            /* background-color: pink; */
            background-position: -327px -142px;
        }

        .n {
            width: 115px;
            height: 112px;
            /* background-color: pink; */
            background-position: -255px -275px;
        }

        .k {
            width: 105px;
            height: 114px;
            /* background-color: pink; */
            background-position: -495px -142px;
        }
    </style>
</head>

<body>
    <span class="p">p</span>
    <span class="i">i</span>
    <span class="n">n</span>
    <span class="k">k</span>
</body>

</html>
```

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210212344614.png)

【PS 切片工具的使用】

<img src="https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210212344633.png" style="zoom: 50%;" />

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210212344634.png)

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210212344153.png)

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210212344192.png)

# 二、字体图标

## 2.1 字体图标的产生

字体图标使用场景：主要用于显示网页中通用、常用的一些小图标。

精灵图是有诸多优点的，但是缺点很明显。

1. 图片文件还是比较大的
2. 图片本身放大和缩小会失真
3. 一旦图片制作完毕想要更换非常复杂

此时，有一种技术的出现很好的解决了以上问题，就是字体图标 iconfont。

字体图标可以为前端工程师提供一种方便高效的图标使用方式，展示的是图标，但本质却属于字体。

## 2.2 字体图标的优点

- 轻量级：一个图标字体要比一系列的图像要小。一旦字体加载了，图标就会马上渲染出来，减少了服务器请求
- 灵活性：本质其实是文字，可以很随意的改变颜色、产生阴影、透明效果、旋转等
- 兼容性：几乎支持所有的浏览器，请放心使用

注意： 字体图标不能替代精灵技术，只是对工作中图标部分技术的提升和优化。

总结：

1. 如果遇到一些结构和样式比较简单的小图标，就用字体图标
2. 如果遇到一些结构和样式复杂一点的小图片，就用精灵图

字体图标是一些网页常见的小图标，我们直接网上下载即可。 因此使用可以分为：

1. 字体图标的下载
2. 字体图标的引入（引入到我们 html 页面中）
3. 字体图标的追加（在原有的基础上添加新的小图标）

## 2.3 字体图标的下载

推荐下载网站：

- icomoon 字库 [https://icomoon.io/](https://icomoon.io/)

IcoMoon 成立于 2011 年，推出了第一个自定义图标字体生成器，它允许用户选择所需要的图标，使它们成一字型。该字库内容种类繁多，非常全面，唯一的遗憾是国外服务器，打开网速较慢。

- 阿里 iconfont 字库 [https://www.iconfont.cn/](https://www.iconfont.cn/)

这个是阿里妈妈 M2UX 的一个 iconfont 字体图标字库，包含了淘宝图标库和阿里妈妈图标库。可以使用 AI 制作图标上传生成。 重点是，免费！

> 以下内容以 icomoon 字库 为例。

## 2.4 字体图标的引入

下载完毕之后，注意原先的文件不要删，后面会用！

1. **把下载包里面的 fonts 文件夹放入页面根目录下**

不同浏览器所支持的字体格式是不一样的，字体图标之所以兼容，就是因为包含了主流浏览器支持的字体文件。

- TureType (.ttf) 格式 .ttf 字体是 Windows 和 Mac 的最常见的字体，支持这种字体的浏览器有 IE9+、Firefox3.5+、Chrome4+、Safari3+、Opera10+、iOS Mobile、Safari4.2+；
- Web Open Font Format (.woff) 格式 woff 字体，支持这种字体的浏览器有 IE9+、Firefox3.5+、Chrome6+、Safari3.6+、Opera11.1+；
- Embedded Open Type (.eot) 格式 .eot 字体是 IE 专用字体，支持这种字体的浏览器有 IE4+；
- SVG (.svg) 格式 .svg 字体是基于 SVG 字体渲染的一种格式，支持这种字体的浏览器有 Chrome4+、Safari3.1+、Opera10.0+、iOS Mobile Safari3.2+；

2. **在 CSS 样式中全局声明字体：简单理解把这些字体文件通过 css 引入到我们页面中**

一定注意字体文件路径的问题。

```css
@font-face {
	font-family: 'icomoon';
	src: url('fonts/icomoon.eot?7kkyc2');
	src: url('fonts/icomoon.eot?7kkyc2#iefix') format('embedded-opentype'),
	url('fonts/icomoon.ttf?7kkyc2') format('truetype'),
	url('fonts/icomoon.woff?7kkyc2') format('woff'),
	url('fonts/icomoon.svg?7kkyc2#icomoon') format('svg');
	font-weight: normal;
	font-style: normal;
}
```

3. **html 标签内添加小图标**

复制小图标对应的字符（一个小方框）到 html 中，一般建议放在 `<span></span>` 标签里。 

4. **给标签定义字体**

```css
span {
	font-family: "icomoon";
}
```

注意：务必保证这个字体和上面 @font-face 里面的字体保持一致（默认为：icomoon）。

## 2.5 字体图标的追加

如果工作中，原来的字体图标不够用了，我们便需要添加新的字体图标到原来的字体文件中。

选择 Import Icons 按钮，把原压缩包里面的 selection.json 重新上传，然后选中自己想要新的图标，从新下载压缩包，并替换原来的文件即可。

## 2.6 字体图标加载的原理

服务器只需接受一次浏览器请求便可以将 fonts 文件一次性返回，如此而来网页中所有用到 fonts 字体图标的部分便一次性加载好了，大大减轻了服务器压力。

```html
<!doctype html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>字体图标的使用</title>
  <style>
    /* 字体声明 */
    @font-face {
    	font-family: 'icomoon';
      	src: url('fonts/icomoon.eot?p4ssmb');
      	src: url('fonts/icomoon.eot?p4ssmb#iefix') format('embedded-opentype'),
        url('fonts/icomoon.ttf?p4ssmb') format('truetype'),
        url('fonts/icomoon.woff?p4ssmb') format('woff'),
        url('fonts/icomoon.svg?p4ssmb#icomoon') format('svg');
      	font-weight: normal;
      	font-style: normal;
      	font-display: block;
    }

    span {
      font-family: 'icomoon';
      font-size: 100px;
      color: salmon;
    }
  </style>
</head>

<body>
  <span></span>
  <span></span>
</body>

</html>
```

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210212344315.png)

# 六、溢出的文字省略号显示

## 6.1 单行文本溢出省略号显示

三个必要条件：

```css
/* 1. 先强制一行内显示文本 */ 
white-space: nowrap; 	/*（ 默认 normal 自动换行）*/ 
/* 2. 超出的部分隐藏 */ 
overflow: hidden; 
/* 3. 文字用省略号替代超出的部分 */ 
text-overflow: ellipsis;
```

案例：

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>单行文本溢出显示省略号</title>
    <style>
        div {
            width: 150px;
            height: 80px;
            background-color: pink;
            margin: 100px auto;
            /* 这个单词的意思是如果文字显示不开自动换行 */
            /* white-space: normal; */
            /* 1.这个单词的意思是如果文字显示不开也必须强制一行内显示 */
            white-space: nowrap;
            /* 2.溢出的部分隐藏起来 */
            overflow: hidden;
            /* 3.文字溢出的时候用省略号来显示 */
            text-overflow: ellipsis;
        }
    </style>
</head>

<body>
    <div>
        啥也不说，此处省略一万字
    </div>
</body>

</html>
```

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210212345292.png)

## 6.2 多行文本溢出省略号显示

多行文本溢出显示省略号，有较大兼容性问题， 适合于 webkit 浏览器或移动端（移动端大部分是 webkit 内核）。

```css
overflow: hidden;
text-overflow: ellipsis;
/* 弹性伸缩盒子模型显示 */
display: -webkit-box;
/* 限制在一个块元素显示的文本的行数 */
-webkit-line-clamp: 2;
/* 设置或检索伸缩盒对象的子元素的排列方式 */
-webkit-box-orient: vertical;
```

更推荐让后台人员来做这个效果，因为后台人员可以设置显示多少个字，操作更简单。

案例：

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>单行文本溢出显示省略号</title>
    <style>
        div {
            width: 150px;
            height: 65px;
            background-color: pink;
            margin: 100px auto;
            overflow: hidden;
            text-overflow: ellipsis;
            /* 弹性伸缩盒子模型显示 */
            display: -webkit-box;
            /* 限制在一个块元素显示的文本的行数 */
            -webkit-line-clamp: 3;
            /* 设置或检索伸缩盒对象的子元素的排列方式 */
            -webkit-box-orient: vertical;
        }
    </style>
</head>

<body>
    <div>
        啥也不说，此处省略一万字,啥也不说，此处省略一万字此处省略一万字
    </div>
</body>

</html>
```

Chrome 浏览器效果：

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210212345299.png)

## 一、定位布局position

### 概念作用

定位布局可以让盒子自由的在某个盒子内移动位置或者固定屏幕中某个位置，并且可以压住其他盒子；

一个完美的定位是由定位模式和边偏移量同时完成的：**定位 = 定位模式 + 边偏移（方位名词更改）**

### 边偏移量

指的就是top、bottom、left、right属性，left和right值控制左右位置偏移，top和bottom只控制上下偏移；

### 定位模式分类

#### 静态定位：position:static; （了解）

就是盒子默认的显示方式，相当于啥也没做
就算是给静态定位盒子设置了边偏移是无效的；

#### 相对定位：position:relative;

**参照对象（参照物）**：根据自己原来的位置进行定位；

**特点：**

> 01、相对定位的盒子**不会脱离标准流**，设置边偏移后盒子原来的位置还存在；
> 02、相对定位**不会改变盒子的默认显示模式**；
> 03、相对定位很少单独使用，后期经常**配合绝对定位完成子绝父相的效果**，做绝对定位盒子父亲；

#### 绝对定位：position:absolute;

**参照对象（参照物）**：

> 01、默认的参照对象是父级盒子，如果没有父级盒子就以浏览器为参照定位；
>
> 02、如果有父级盒子并且父级盒子有定位属性，就以父级盒子为参照定位；
>
> 03、如果有父级盒子但是父级盒子没有定位属性，就会一级一级的往上找祖先盒子，就近的祖先盒子有定位  	属性性就以当前的祖先盒子为参照，如果所有的祖先盒子都没有定位属性就以浏览器为参照；

**特点：**

> 01、绝对定位的盒子完全**脱离了文档流，不会占有原来的位置**，属于不占位的定位；
> 02、绝对定位会**改变盒子的显示模式为行内块的元素**的特点；
> 03、绝对定位一般会**配合相对定位实现子绝父相的定位效果**，很少自己单独使用；	

#### 固定定位：*position*: fixed; 

**参照对象（参照物）：**是浏览器的可视窗口为参照定位；

**特点：**

> 01、固定定位的盒子完全脱离文档流，属于不占位定位；
> 02、固定定位会将盒子的显示模式更改为行内块的特点；	

#### 粘性定位：position: sticky; 

**参照对象（参照物）：**
一开始条件没有满足的时候是相对定位，当条件满足以后马上更改为固定定位，所以可以理解为参照物没有满足条件的时候为自己本身，满足了条件后更改为浏览器的可视窗口；

**注意：**粘性定位的盒子必须满足设置边偏移的四个值分别是top,right,bottom,left中的一个，比如上下滚动设置top值；以下代码必须满足元素的top值为0的时候就会执行粘性定位样式；

```
    position: sticky;
    top: 0;
```

## 二、定位布局的一些技巧（死了都要记）

### 子绝父相

#### 原因

父级盒子是用来做布局占位用的，如果使用了绝对定位父级盒子就会完全脱离文档流，导致后面的盒子布局混乱；

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210230900882.png)

所以我们父级盒子有一般都用相对定位，这样父级盒子会占有原来的位置也不会改变盒子的显示模式，就不会影响后面盒子的布局了；

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210230900891.png)

#### 基本规则

> 01、子级绝对父级相对；
>
> 02、如果父级盒子有有对应的定位属性，也可以直接做父级定位子级，不一定是子绝父相；

### 固定定位的盒子跟随版心定位

如果想要固定定位的盒子跟随版心定位需要按照以下步骤设置：

> **01、首先盒子必须是固定定位*position*: fixed;，然后设置left取值为50%；**
>
> **02、然后设置盒子的margin-left取值为版心的一半加合适的距离；**

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210230900892.jpg)

以下代码是将版心设置为1200的标准设置的：

```css
        .sub-nav {
            position: fixed;
            top: 300px;
            left: 50%;
            margin-left: 620px;
            width: 60px;
            height: 300px;
            background-color: palegreen;
        }
```

### 定位的盒子如何实现水平和垂直居中显示

**情况1：**如果盒子是相对定位我们可以直接使用margin设置盒子居中显示；

**情况2：**如果盒子是绝对定位或者固定定位，因为盒子完全脱离了标准流margin居中就会失效，我们需要按照以下的方法实现盒子的水平和垂直居中；

> 01、设置定位盒子的left:50%;和top:50%;让盒子直接定位整个父级平分的右侧和下面；
>
> 02、设置margin-left：- 盒子宽度一半；和margin-top:-盒子高度一半；

```css
        .box {
            position: absolute;
            top: 300px;
            left: 50%;
            top: 50%;
            margin-left: -150px;
            margin-top: -150px;
            width: 300px;
            height: 300px;
            background-color: palegreen;
        }
```

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202210230900893.jpg)

### 定位盒子的层叠位置

定位的元素，写在后面的盒子会将前面的盒子压住，如果想要调整盒子的先后顺序，就需要用z-index来设置：

z-index的取值是任意的整数，可以是负数或者正数，默认的取值理解为0，值越大盒子越靠前；

**注意：z-index必须配合定位属性一起使用，取值不能带任何单位；**


