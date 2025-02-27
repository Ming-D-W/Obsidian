# day01 - Web APIs

> 学习目标：
>
> 可以对元素属性进行操作
>
> 可以对元素内容进行设置
>
> 可以对元素样式进行设置

### 1. 变量声明

#### 1.1 var、 let 和 const

变量声明有三个，我们应该用哪个呢？

- 首先 var 先排除，老派写法，问题很多，可以淘汰掉。
- let  or  const ？
- 建议：<span style="color: red">const优先</span>，尽量使用const，原因是：
  - const 语义化更好
  - 很多变量我们声明的时候就知道他不会被更改了，那为什么不用 const呢？
  - 实际开发中也是，比如react框架，基本const
- 如果你还在纠结，那么我建议：
  - 有了变量先给const，如果发现它后面是要被修改的，再改为let

练习：

请问以下的 可不可以把let 改为 const？

```javascript
// 测试1
document.write('我叫' + '刘德华')
let uname = '刘德华'
let song = '忘情水'
document.write(uname + song)

// 测试2
let num1 = +prompt('请输入第一个数值：')
let num2 = +prompt('请输入第二个数值：')
alert(`两者相加的结果是：${num1 + num2}`)

```

请问以下的 可不可以把let 改为 const？

```javascript
// 测试1
let num = 1
num = num + 1
console.log(num)  // 结果是2

// 测试2
for (let i = 0; i < nums.length; i++) {
    document.write(nums[i])
}
```

请问以下的 可不可以把let 改为 const？

```javascript
// 测试1
let arr = ['red', 'green']
arr.push('pink')
console.log(arr)  // ['red', 'green', 'pink']

// 测试2
let person = {
    uname: 'pink老师',
    age: 18,
    gender: '女'
}
person.address = '黑马'
console.log(person)
```

注意：

- const  声明的值不能更改，而且const声明变量的时候需要里面进行初始化
- 但是对于引用数据类型，const声明的变量，里面存的不是 值，不是值，不是值，是 地址。

测试

```javascript
// 可以改为 const 吗
let person = {
    uname: 'shadow',
    age: 17,
    gender: '女'
}
person.gender = '男'
console.log(person.gender)  // 男
console.log(person)

// 下面写法可以吗？
const names = []
names = [1, 2, 3]

const obj = {}
obj = {
    uname: 'shadow'
}
```

总结：

1. 以后声明变量我们优先使用哪个？
2. 为什么const声明的对象可以修改里面的属性值？
3. 什么时候使用let声明变量？

### 2. Web API 基本认知

#### 2.1 作用和分类

- 作用: 就是使用 JS 去操作 html 和浏览器
- 分类：DOM (文档对象模型)、BOM（浏览器对象模型）
- ![image-20220716125239880](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301030104062.png)

#### 2.2 什么是DOM

- DOM（Document Object Model——文档对象模型）是用来呈现以及与任意 HTML 或 XML文档交互的API
- 简单理解：DOM是一个对象，用来操作网页的。
  - 例如：改变网页内容、样式等。

#### 2.3 总结：

- Web API阶段我们学习哪两部分？
- DOM是什么？有什么作用？

#### 2.4 DOM树

- 将 HTML 文档以树状结构直观的表现出来，我们称之为文档树或 DOM 树
- 作用：文档树直观的体现了标签与标签之间的关系

![image-20220716125929571](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301030104811.png)



![image-20220716125954370](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301030104613.png)



节点是文档树的组成部分，**每一个节点都是一个 DOM 对象**，主要分为元素节点、属性节点、文本节点等。

1. 【元素节点】其实就是 HTML 标签，如上图中 `head`、`div`、`body` 等都属于元素节点。
2. 【属性节点】是指 HTML 标签中的属性，如上图中 `a` 标签的 `href` 属性、`div` 标签的 `class` 属性。
3. 【文本节点】是指 HTML 标签的文字内容，如 `title` 标签中的文字。



#### 2.5 DOM对象

- DOM对象：浏览器根据html标签生成的 JS对象
  - 所有的标签属性都可以在这个对象上面找到
  - 修改这个对象的属性会自动映射到标签身上
- DOM的核心思想
  - 把网页内容当做对象来处理
- document 对象
  - 是 DOM 里提供的一个对象
  - 网页所有内容都在document里面

#### 2.6 总结

- DOM 树是什么？
- DOM对象怎么创建的？
- document 是什么？

### 3. 获取DOM对象

- 根据CSS选择器来获取DOM元素  (重点)

- 其他获取DOM元素方法（了解）

  思考：我们想要操作某个标签首先做什么？

#### 3.1 根据CSS选择器来获取DOM元素  (重点)

##### 3.1.1 选择匹配的第一个元素

```javascript
// 语法
document.querySelector('css选择器')

// 参数 包含一个或多个有效的CSS选择器 字符串

// 返回值  匹配的第一个元素,如果没有匹配到，则返回null

// 示例
document.querySelector('#box div')
```

##### 3.1.2 选择匹配的多个元素

```javascript
// 语法
document.querySelectorAll('css选择器')

// 参数 包含一个或多个有效的CSS选择器 字符串

// 返回值 元素对象集合

// 示例
document.querySelectorAll('ul li')
```

##### 3.1.3 总结

- 获取一个DOM元素我们使用谁？
- 获取多个DOM元素我们使用谁？能直接修改吗？ 如果不能可以怎么做到修改?

##### 3.1.5 注意

- `document.querySelectorAll('css选择器')` 得到的是一个伪数组
  - 有长度有索引号
  - 但是没有数组的方法，如push()，pop()
  - 想要得到里面的每一个元素对象，**需要遍历**。

#### 3.2 总结

- 获取页面中的标签我们最终常用那两种方式？
- 他们两者的区别是什么？
- 他们两者小括号里面的参数有神马注意事项？
  - 里面写的是css选择器
  - 必须是字符串

#### 3.3 其它获取DOM元素的方法（了解）

```javascript
// 根据id获取一个元素对象
document.getElementById('id')

// 根据 标签名 获取多个元素对象
document.getElementsByTagName('tagName')

// 根据 类名 获取多个元素对象
document.getElementsByClassName('className')
```

### 4. 操作元素内容

- 元素对象.innerText 属性
- 元素对象.innerHTML 属性

#### 4.1 元素.innerText 属性

获取或设置标签内容

示例：

```javascript
const box = document.querySelector('.box')
console.log(box.innerText)  // 获取文字内容
box.innerText = '我是一个盒子' // 修改文字内容
```

注意：<span style="color: red">不识别 html 标签</span>

#### 4.2 元素.innerHTML 属性

获取或设置标签内容

示例：

```javascript
const box = document.querySelector('.box')
console.log(box.innerHTML) // 获取标签内容
box.innerHTML = '<strong>我要更换</strong>' // 设置标签内容
```

注意：<span style="color: red">识别 html 标签 </span>

#### 4.3 总结

- 设置/修改DOM元素内容有哪2种方式？
- 二者的区别是什么？

#### 4.4 年会抽奖案例

- 需求：从数组随机抽取一等奖、二等奖和三等奖，显示到对应的标签里面。
- 分析
  - 声明数组: const personArr = ['周杰伦', '刘德华', '周星驰', 'Pink老师', '张学友']
  - 一等奖:随机生成一个数字（0~数组长度），找到对应数组的名字
  - 通过innerText 或者 innerHTML 将名字写入span元素内部
  - 二等奖依次类推

### 5. 操作元素属性

#### 5.1  操作元素常用属性

- 通过 JS 设置/修改标签元素属性，比如通过 src更换 图片

- 常见的属性比如： href、title、src 等
- 语法：`元素对象.属性 = 值`

示例：

```javascript
// 1. 获取图片元素
const img = document.querySelector('img')
// 2. 修改图片对象的属性   对象.属性 = 值
img.src = './images/2.webp'
```

##### 5.1.2 练习 页面刷新，图片随机更换

- 需求：当我们刷新页面，页面中的图片随机显示不同的图片
- 分析：
  - 随机显示，则需要用到随机函数
  - 更换图片需要用到图片的 src 属性，进行修改
  - 核心思路：
    - 获取图片元素
    - 随机得到图片序号
    - 图片.src = 图片随机路径

#### 5.2 操作元素样式属性

- 可以通过 JS 设置/修改标签元素的样式属性
- 比如通过 轮播图小圆点自动更换颜色样式等

##### 5.2.1 通过 style 属性操作CSS

- 语法：`对象.style.样式属性 = 值`

示例：

```javascript
// 1. 获取元素
const box = document.querySelector('.box')
//2. 修改样式属性 对象.style.样式属性 = '值'  别忘了跟单位
box.style.width = '300px'
// 多组单词的采取 小驼峰命名法
box.style.backgroundColor = 'hotpink'
box.style.border = '2px solid blue'
box.style.borderTop = '2px solid red'
```

注意：

- 修改样式通过style属性引出
- 如果属性有-连接符，需要转换为小驼峰命名法
- 赋值的时候，需要的时候不要忘记加css单位
- <span style="color: red">修改的是行内样式</span>

案例：  页面刷新，页面随机更换背景图片

- 需求 当我们刷新页面，页面中的背景图片随机显示不同的图片
- 分析：
  - 随机函数
  - css页面背景图片  background-image
  - 标签选择body， 因为body是唯一的标签，可以直接写 document.body.style 

```javascript
// console.log(document.body)
// 取到 N ~ M 的随机整数
function getRandom(N, M) {
    return Math.floor(Math.random() * (M - N + 1)) + N
}
// 随机数
const random = getRandom(1, 10)
document.body.style.backgroundImage = `url(./images/desktop_${random}.jpg)`
```

##### 5.2.2 操作类名(className) 操作CSS

- 如果修改的样式比较多，直接通过style属性修改比较繁琐，我们可以通过借助于css类名的形式。
- 语法：`元素对象.className = 'active'`

示例：

```javascript
// 1. 获取元素
const div = document.querySelector('div')
// 2.添加类名  class 是个关键字 我们用 className
div.className = 'nav box'
```

注意：

- 由于class是关键字, 所以使用className去代替
- className是使用新值换旧值, 如果需要添加一个类,需要保留之前的类名

##### 5.2.3 总结

- 使用 className 有什么好处？
- 使用 className 有什么注意事项？

##### 5.2.4 通过 classList 操作类控制CSS

- 为了解决className 容易覆盖以前的类名，我们可以通过classList方式追加和删除类名

- 语法：

  ```javascript
  // 追加一个类
  元素.classList.add('类名')
  // 删除一个类
  元素.classList.remove('类名')
  // 切换一个类
  元素.classList.toggle('类名')
  ```

##### 5.2.5 总结 

使用 `className` 和`classList`的区别？

- `className`修改大量类名的时候更方便
- `classList`修改不多类名的时候更方便
- `classList` 是追加和删除不影响以前类名

##### 5.2.6 轮播图随机版

需求：当我们刷新页面，页面中的轮播图会显示不同图片以及样式

- 图片会随机变换
- 底部盒子背景颜色和文字内容会变换
- 小圆点随机一个高亮显示

分析：

- 准备一个数组对象，里面包含详细信息
- 随机选择一个数字，选出数组对应的对象，更换图片，底部盒子背景颜色，以及文字内容
- 利用这个随机数字，让小圆点添加高亮的类（addClass）  利用css 结构伪类选择器

#### 5.3 操作表单元素 属性

- 表单很多情况，也需要修改属性，比如点击眼睛，可以看到密码，本质是把表单类型转换为文本框
- 正常的有属性有取值的 跟其他的标签属性没有任何区别
- 语法
  - 获取： 元素对象.属性名
  - 设置： DOM对象.属性名 = 新值

示例：

```javascript
// 1 获取元素
// const uname = document.querySelector('input')
// 2. 获取值  获取表单里面的值 用的  表单.value
// console.log(uname.value) // 电脑
// console.log(uname.innerHTML)  innertHTML 得不到表单的内容
// 3. 设置表单的值
// uname.value = '我要买电脑'
// console.log(uname.type)
// uname.type = 'password'
```

- 表单属性中添加就有效果,移除就没有效果,一律使用布尔值表示 如果为true 代表添加了该属性 如果是false 代表移除了该属性
- 比如： disabled、checked、selected

示例：

```javascript
// 1. 获取
const ipt = document.querySelector('input')
// console.log(ipt.checked)  // false   只接受布尔值
ipt.checked = true
// ipt.checked = 'true'  // 会选中，不提倡  有隐式转换

// 1.获取
const button = document.querySelector('button')
// console.log(button.disabled)  // 默认false 不禁用
button.disabled = true   // 禁用按钮
```

#### 5.4 自定义属性

- 内置属性: 标签天生自带的属性 比如class id title等, 可以直接使用点语法操作比如： disabled、checked、selected
- 自定义属性：
  - 在html5中推出来了专门的data-自定义属性	
  - 在标签上一律以data-开头
  - 在DOM对象上一律以dataset对象方式获取
  - ![image-20220716142852846](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301030104379.png)

### 6. 定时器-间歇函数

- 网页中经常会需要一种功能：每隔一段时间需要自动执行一段代码，不需要我们手动去触发
- 例如：网页中的倒计时
- 要实现这种需求，需要定时器函数
- 定时器函数有两种，今天我先讲间歇函数

#### 6.1 定时器函数基本使用

##### 6.1.1 开启定时器

- setInterval(函数名, 间隔时间)  函数名不要加小括号

示例：

```javascript
setInterval(function () {
    console.log('一秒执行一次')
}, 1000)
```

注意：

- 函数名字不需要加括号
- 定时器返回的是一个数字，作为定时器的 ID

##### 6.1.2 关闭定时器

- clearInterval(定时器ID)

示例：

```javascript
let m = setInterval(function () {
    console.log(11)
}, 2000)
console.log(m)
```

##### 6.1.3 总结

- 定时器函数有什么作用？
- 定时器函数如何开启？
- 定时器函数如何关闭？

#### 6.2 案例 阅读注册协议

需求：按钮60秒之后才可以使用

分析：

- 开始先把按钮禁用（disabled 属性）
- 一定要获取元素
- 函数内处理逻辑
  - 秒数开始减减
  - 按钮里面的文字跟着一起变化
  - 如果秒数等于0 停止定时器 里面文字变为 同意  最后 按钮可以点击

### 7. 综合案例 轮播图定时器版

需求：每隔一秒钟切换一个图片

分析：

- 准备一个数组对象，里面包含详细信息
- 获取元素
- 设置定时器函数
  - 设置一个变量++
  - 找到变量对应的对象
  - 更改图片、文字信息
  - 激活小圆点：移除上一个高亮的类名，当前变量对应的小圆点添加类
- 处理图片自动复原从头播放（放到变量++后面，紧挨）
  - 如果图片播放到最后一张， 就是大于等于数组的长度，则把变量重置为0