# day05 - Web APIs

> 学习目标：
>
> 利用 BOM 对象实现对历史、地址、浏览器信息的操作或获取
>
> 利用本地存储实现学生信息表案例

### 1. Window对象

#### 1.1 BOM(浏览器对象模型)

- BOM(Browser Object Model ) 是浏览器对象模型

  ![image-20220717101306377](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301030103542.png)

- window对象是一个全局对象，也可以说是JavaScript中的顶级对象

- 像document、alert()、console.log()这些都是window的属性，基本BOM的属性和方法都是window的。

- 所有通过var定义在全局作用域中的变量、函数都会变成window对象的属性和方法

- window对象下的属性和方法调用的时候可以省略window

#### 1.2 延时定时器

##### 1.2.1 基本使用

- JavaScript 内置用来让代码延迟执行的函数，叫 setTimeout
- 语法：![image-20220717101617668](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301030103957.png)
- setTimeout 仅仅只执行一次，所以可以理解为就是把一段代码延迟执行, 平时省略window
- 清除延时函数：![image-20220717101601146](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301030103745.png)
- 注意点
  - 延时器需要等待,所以后面的代码先执行
  - 每一次调用延时器都会产生一个新的延时器

##### 1.2.2 两种定时器对比

- 延时函数: 执行一次
- 间歇函数:每隔一段时间就执行一次,除非手动清除

##### 1.2.3 案例 5秒钟之后消失的广告

需求：5秒钟之后，广告自动消失

分析：

​	①：设置延时函数

​	②：隐藏元素

#### 1.3 JS 执行机制

##### 1.3.1 思考

```javascript
console.log(111)
setTimeout(function() {
    console.log(222)
}, 1000)
console.log(333)
// 问：输出的结果是什么？

console.log(111)
setTimeout(function() {
    console.log(222)
}, 0)
console.log(333)
// 问：输出的结果是什么？
```

##### 1.3.2 JS执行机制概述

JavaScript 语言的一大特点就是<span style="color: red">单线程</span>，也就是说，<span style="color: red">同一个时间只能做一件事</span>。

这是因为 Javascript 这门脚本语言诞生的使命所致——JavaScript 是为处理页面中用户的交互，以及操作 DOM 而诞生的。比如我们对某个 DOM 元素进行添加和删除操作，不能同时进行。 应该先进行添加，之后再删除。

单线程就意味着，所有任务需要排队，前一个任务结束，才会执行后一个任务。这样所导致的问题是： 如果 JS 执行的时间过长，这样就会造成页面的渲染不连贯，导致页面渲染加载阻塞的感觉。

##### 1.3.3 同步和异步的概念

为了解决这个问题，利用多核 CPU 的计算能力，HTML5 提出 Web Worker 标准，允许 JavaScript 脚本创建多个线程。于是，JS 中出现了同步和异步。

- 同步

  前一个任务结束后再执行后一个任务，程序的执行顺序与任务的排列顺序是一致的、同步的。比如做饭的同步做法：我们要烧水煮饭，等水开了（10分钟之后），再去切菜，炒菜。

- 异步

  你在做一件事情时，因为这件事情会花费很长时间，在做这件事的同时，你还可以去处理其他事情。比如做饭的异步做法，我们在烧水的同时，利用这10分钟，去切菜，炒菜。

<span style="color: red">他们的本质区别： 这条流水线上各个流程的执行顺序不同。</span>

##### 1.3.4 同步任务和异步任务

- 同步任务

  同步任务都在主线程上执行，形成一个执行栈。

- 异步任务

  JS 的异步是通过回调函数实现的。

  一般而言，异步任务有以下三种类型:

  1、普通事件，如 click、resize 等

  2、资源加载，如 load、error 等

  3、定时器，包括 setInterval、setTimeout 等

  异步任务相关添加到<span style="color: red">任务队列</span>中（任务队列也称为消息队列）。

##### 1.3.5 执行顺序

1. 先执行<span style="color: red">执行栈中的同步任务</span>。
2. 异步任务放入任务队列中。
3. 一旦执行栈中的所有同步任务执行完毕，系统就会按次序读取<span style="color: red">任务队列</span>中的异步任务，于是被读取的异步任务结束等待状态，进入执行栈，开始执行。

![image-20220717104959682](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301030103149.png)

思考：

```javascript
console.log(1)

document.addEventListener('click', function () {
    console.log(4)
})

console.log(2)

setTimeout(function () {
    console.log(3)
}, 3000)
```



#### 1.4 location对象

##### 1.4.1 基本概念

- location 的数据类型是对象，它拆分并保存了 URL 地址的各个组成部分
- 常用属性和方法：
  - href 属性获取完整的 URL 地址，对其赋值时用于地址的跳转
  - search 属性获取地址中携带的参数，符号 ？后面部分
  - hash 属性获取地址中的哈希值，符号 # 后面部分
  - reload 方法用来刷新当前页面，传入参数 true 时表示强制刷新

##### 1.4.2 基本使用

- href 属性获取完整的 URL 地址，对其赋值时用于地址的跳转![image-20220717105434757](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301030103604.png)

案例 5秒钟之后跳转的页面

需求：用户点击可以跳转，如果不点击，则5秒之后自动跳转，要求里面有秒数倒计时

分析：

​	①：目标元素是链接

​	②：利用定时器设置数字倒计时

​	③：时间到了，自动跳转到新的页面



- search 属性获取地址中携带的参数，符号 ？后面部分

  ```javascript
  console.log(location.search)
  ```

  

- hash 属性获取地址中的哈希值，符号 # 后面部分

  ```javascript
  console.log(location.hash)
  ```



- reload 方法用来刷新当前页面，传入参数 true 时表示强制刷新![image-20220717110105172](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301030103941.png)

##### 1.4.3 总结

- <span style="color: red">location.href</span> 属性获取完整的 URL 地址，对其赋值时用于地址的跳转
- search 属性获取地址中携带的参数，符号 ？后面部分
- hash 属性获取地址中的啥希值，符号 # 后面部分
- reload 方法用来刷新当前页面，传入参数 true 时表示强制刷新

#### 1.5 navigator对象(了解)

- navigator的数据类型是对象，该对象下记录了浏览器自身的相关信息
- 常用属性和方法：通过 userAgent 检测浏览器的版本及平台

```javascript
// 检测 userAgent（浏览器信息）
!(function () {
    const userAgent = navigator.userAgent
    // 验证是否为Android或iPhone
    const android = userAgent.match(/(Android);?[\s\/]+([\d.]+)?/)
    const iphone = userAgent.match(/(iPhone\sOS)\s([\d_]+)/)
    // 如果是Android或iPhone，则跳转至移动站点
    if (android || iphone) {
        location.href = 'http://m.itcast.cn'
    }
})()

```



#### 1.6 history对象

- history 的数据类型是对象，主要管理历史记录， 该对象与浏览器地址栏的操作相对应，如前进、后退、历史记录等

- 常用属性和方法：

  | history对象方法 | 作用                                                      |
  | --------------- | --------------------------------------------------------- |
  | back()          | 可以后退功能                                              |
  | forward()       | 前进功能                                                  |
  | go(参数)        | 前进后退功能，如果是1，前进1个页面，如果是-1，后退1个页面 |

  history 对象一般在实际开发中比较少用，但是会在一些 OA 办公系统中见到。

### 2. 本地存储

#### 2.1 本地存储介绍

- 以前我们页面写的数据一刷新页面就没有了
- 为了在本地存储大量的数据，HTML5规范提出了相关解决方案。
  - 数据存储在用户浏览器中
  - 设置、读取方便、甚至页面刷新不丢失数据
  - 容量较大，sessionStorage和localStorage约 5M 左右

#### 2.2 本地存储分类 - localStorage

##### 2.2.1 基本使用

> 目标： 能够使用localStorage 把数据存储的浏览器中

- 作用: 可以将数据永久存储在本地(用户的电脑), 除非手动删除，否则关闭页面也会存在

- 特性：

  - 可以多窗口（页面）共享（同一浏览器可以共享）
  - 以键值对的形式存储使用

- 语法：

  - 存储数据

    ```javascript
    localStorage.setItem(key, value)
    ```

  - 获取数据

    ```javascript
    localStorage.getItem(key)
    ```

  - 删除数据

    ```javascript
    localStorage.removeItem(key)
    ```

##### 2.2.2 浏览器查看localStorage数据

![image-20220717111433293](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301030103794.png)

#### 2.3 本地存储分类 - sessionStorage

特性：

- 生命周期为关闭浏览器窗口
- 在同一个窗口(页面)下数据可以共享
- 以键值对的形式存储使用
- 用法跟localStorage 基本相同



#### 2.4 总结

- localStorage 作用是什么？  
- localStorage 存储，获取，删除的语法是什么？  



#### 2.5 储存复杂类型数据

##### 2.5.1 储存

> 目标： 能够存储复杂数据类型以及取出数据

- 本地只能存储字符串,无法存储复杂数据类型![image-20220717111838385](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301030103603.png)
- 解决：需要将复杂数据类型转换成JSON字符串,在存储到本地
- 语法：JSON.stringify(复杂数据类型)![image-20220717111925477](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301030103357.png)
  - 将复杂数据转换成JSON字符串    存储 本地存储中![image-20220717111955242](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301030103866.png)

##### 2.5.2 取出

问题：因为本地存储里面取出来的是字符串，不是对象，无法直接使用

![image-20220717112209939](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301030103567.png)

- 解决：把取出来的字符串转换为对象
- 语法：JSON.parse(JSON字符串)![image-20220717112301639](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301030103975.png)

### 3. 综合案例 学生就业信息表

需求： 录入学生信息，页面刷新数据不丢失

模块分析：

​	①：新增模块， 输入学生信息，数据会存储到本地存储中

​	②：渲染模块，数据会渲染到页面中

​	③：删除模块，点击删除按钮，会删除对应的数据

思路分析：

​	①：因为页面刷新不丢失数据，所以可能存在已有数据，所以第一步，我们先找本地存储里面查找是否有数据，如果有数据先进行渲染页面，如果没有数据，我们放一个空数组，用来存放数据

​	②：渲染模块，数据会渲染到页面中

​	③：新增模块， 输入学生信息，数据会存储到本地存储中，然后渲染页面

​	④：删除模块，点击删除按钮，会删除对应的数据，然后渲染页面