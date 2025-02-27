- 在 `<body>` 中的 `<script>` 标签中书写 JS 代码
- 将 JS 代码单独保存为 `.js` 文件，然后在 HTML 文件中使用 `<script src=""></script>` 引入

> JavaScript 不能脱离 HTML 网页运行！
>
> （当然，今后学习 Node.js 后，JavaScript 可以独立成为一个运行平台）

## 在 \<body> 中书写 JS 代码

在 `<body>` 中的 `<script>` 标签中书写 JS 代码

- index.html

```html
<body>
    <!-- 在 HTML5 之前，必须要加上 type 属性，并且里面的内容一定要正确！-->
    <!-- 
    <script type="text/javascript">
    </script> 
    -->

    <!-- 目前都是使用 HTML5，所以不用写 type 属性，默认就是 JS -->
    <!-- 推荐把 script 文件写到 body 的末尾 -->
    <script>
        // 弹窗输出一句话
        // 每一句 JS 代码以分号结尾！
        alert("你好，JavaScript！");
    </script>
</body>
```


## 将 JS 代码单独保存为 \.js 文件

将 JS 代码单独保存为 \.js 文件，然后在 HTML 文件中使用 `<script src=""></script>` 引入

- 文件结构

![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202211041857874.png)

- index.html

```html

<body>
    <!--
    也可以放在 body 末尾（推荐）
    <script src="./js/index.js"></script>
	-->
</body>

```

- index.js

```javascript
alert("你好，JavaScript！");
```


> 以上两种 JS 的书写方法，强烈推荐第二种！

## 内联 JavaScript(行内)

代码写在标签内部

示例代码：

```html
<body>
    <button onclick="alert('逗你玩那~~')">点击我月入过万</button>
</body>
```

 **注意：** 此处作为了解即可，但是后面vue框架会用这种模式
