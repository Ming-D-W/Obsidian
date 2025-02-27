# day03 - Web APIs

> 学习目标：
>
> 学习事件流，事件委托，其他事件等知识
>
> 优化多个事件绑定和实现常见网页交互 

### 1. 事件流

#### 1.1 事件流和两个阶段说明

>目标：能够说出事件流经过的2个阶段

- 事件流指的是事件完整执行过程中的流动路径

  ![image-20220716162949039](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301030101490.png)

- 说明：假设页面里有个div，当触发事件时，会经历两个阶段，分别是捕获阶段、冒泡阶段
- 简单来说：捕获阶段是 从父到子  冒泡阶段是从子到父
- 实际工作都是使用事件冒泡为主

#### 1.2 事件捕获

>目标：简单了解事件捕获执行过程

- 事件捕获概念：从DOM的根元素开始去执行对应的事件 (从外到里)

- 事件捕获需要写对应代码才能看到效果

- 代码：

  ![image-20220716163212562](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301030101958.png)

- 说明：
  - addEventListener第三个参数传入 true 代表是捕获阶段触发（很少使用）
  - 若传入false代表冒泡阶段触发，默认就是false
  - 若是用  `元素.onclick`，则只有冒泡阶段，没有捕获

#### 1.3 事件冒泡

> 目标：能够说出事件冒泡的执行过程

- 事件冒泡概念: 当一个元素的事件被触发时，同样的事件将会在该元素的所有祖先元素中依次被触发。这一过程被称为事件冒泡
- 简单理解：当一个元素触发事件后，会依次向上调用所有父级元素的 同名事件
- 事件冒泡是默认存在的
- 事件监听`addEventListener`第三个参数是 false，或者默认都是冒泡

#### 1.4 阻止冒泡

> 目标：能够写出阻止冒泡的代码

- 问题：因为默认就有冒泡模式的存在，所以容易导致事件影响到父级元素
- 需求：若想把事件就限制在当前元素内，就需要阻止事件冒泡
- 前提：阻止事件冒泡需要拿到事件对象
- 语法：`事件对象.stopPropagation()`

#### 1.5 阻止默认行为

- 问题：有时我们需要阻止一些默认行为，比如说表单提交，a链接跳转

- 语法：`事件对象.preventDefault()`

  示例代码：

  ```javascript
  const form = document.querySelector('form')
  form.addEventListener('submit', function (e) {
      // 阻止默认行为  提交
      e.preventDefault()
  })
  
  const a = document.querySelector('a')
  a.addEventListener('click', function (e) {
      e.preventDefault()
  })
  ```

  

#### 1.6 解绑事件

- addEventListener方式监听的事件，解绑：removeEventListener(事件类型, 事件处理函数,  [获取捕获或者冒泡阶段])
- on事件方式，直接使用null覆盖偶就可以实现事件的解绑

​	示例：

```html
<button>点击</button>
<script>
    const btn = document.querySelector('button')
    function fn() {
        alert('点击了')
    }
    btn.addEventListener('click', fn)
    // 事件监听移除解绑
    btn.removeEventListener('click', fn)
    
    // btn.onclick = function () {
    //   alert('点击了')
    //   // on事件移除解绑
    //   btn.onclick = null
    // }
</script>
```

注意：<span style="color: red">匿名函数无法被解绑</span>

#### 1.7 鼠标经过事件的区别

鼠标经过事件：

- mouseover 和 mouseout 会有冒泡效果
- mouseenter  和 mouseleave   没有冒泡效果 (推荐)

#### 1.8 两种注册事件的区别

- 传统on注册
  - 同一个对象,后面注册的事件会覆盖前面注册(同一个事件)
  - 直接使用null覆盖偶就可以实现事件的解绑
- 事件监听注册
  - 语法: addEventListener(事件类型, 事件处理函数, 是否使用捕获)
  - 后面注册的事件不会覆盖前面注册的事件(同一个事件)
  - 可以通过第三个参数去确定是在冒泡或者捕获阶段执行
  - 必须使用removeEventListener(事件类型, 事件处理函数, 获取捕获或者冒泡阶段)
  - 匿名函数无法被解绑

### 2. 事件委托

> 目标：能够说出事件委托的好处

- 如果同时给多个元素注册事件，我们怎么做的？

  - for循环注册事件

  - ```javascript
    const lis = document.querySelectorAll('ul li')
    for (let i = 0; i < lis.length; i++) {
        lis[i].addEventListener('click', function() {
            console.log('我被点击了')
        })
    }
    ```

- 有没有一种技巧 注册一次事件就能完成以上效果呢？

#### 2.1 事件委托的原理及好处

事件委托是利用事件流的特征解决一些开发需求的知识技巧

- 优点：减少注册次数，提高了程序性能
- 原理：事件委托其实是利用事件冒泡的特点
  - 给父元素注册事件，当我们触发子元素的时候，会冒泡到父元素身上，从而触发父元素的事件
- 实现：事件对象.target. tagName 可以获得真正触发事件的元素

示例：

```javascript
ul.addEventListener('click', function (e) {
    if (e.target.tagName === 'LI') {
        e.target.style.color = 'red'
    }
})
```

总结：

- 事件委托的好处是什么？
- 事件委托是委托给了谁？父元素还是子元素？
- 如何找到真正触发的元素？
  - 事件对象.target.tagName

#### 2.2 案例 tab栏切换改造

需求：优化程序，将tab切换案例改为**事件委托**写法

分析：

- 给a的父级 注册点击事件，采取事件委托方式
- 如果点击的是a , 则进行排他思想，删除添加类
- 注意判断的方式 利用 e.target.tagName 
- 因为没有索引号了，所以这里我们可以自定义属性，给5个链接添加序号
- 下面大盒子获取索引号的方式  e.target.dataset.id 号， 然后进行排他思想

### 3. 其它事件

#### 3.1 页面加载事件

##### 3.1.1 页面加载时间 `load`

- 加载外部资源（如图片、外联CSS和JavaScript等）加载完毕时触发的事件

- 为什么要学？

  - 有些时候需要等页面资源全部处理完了做一些事情
  - 老代码喜欢把 script 写在 head 中，这时候直接找 dom 元素找不到

- 事件名：load

- 监听页面所有资源加载完毕：

  - 给 window 添加 load 事件

  - ```javascript
    window.addEventListener('load', function () {
    	// 执行的操作
    })
    ```

- 注意：不光可以监听整个页面资源加载完毕，也可以针对某个资源绑定load事件

##### 3.1.1 页面加载事件 `DOMContentLoaded`

- DOM完全加载和解析完成之后，DOMContentLoaded 事件被触发，而无需等待样式表、图像等完全加载

- 事件名：DOMContentLoaded

- 监听页面DOM加载完毕：

  - 给 document 添加 DOMContentLoaded 事件

  - ```javascript
    document.addEventListener('DOMContentLoaded', function () {
    	// 执行的操作
    })
    ```

总结：

- 页面加载事件有哪两个？如何添加？
  - load 事件： 监听整个页面资源给 window 加
  - DOMContentLoaded
    - 给 document 加
    - 无需等待样式表、图像等完全加载

#### 3.2 页面滚动事件

- 滚动条在滚动的时候持续触发的事件

- 为什么要学？

  - 很多网页需要检测用户把页面滚动到某个区域后做一些处理， 比如固定导航栏，比如返回顶部

- 事件名：scroll

- 监听整个页面滚动：

  - ```javascript
    window.addEventListener('scroll', function () {
        // 执行的操作
    })
    ```

  - 给 window 或 document 添加 scroll 事件

- 监听某个元素的内部滚动直接给某个元素加即可

#### 3.3 页面滚动事件-获取位置

- scrollLeft和scrollTop （属性）
  - 获取被卷去的大小
  - 获取元素内容往左、往上滚出去看不到的距离
  - 这两个值是可读写的
- 尽量在scroll事件里面获取被卷去的距离

![image-20220716172945394](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301030101844.png)

```javascript
window.addEventListener('scroll', function () {
    // 必须写到里面
    const n = document.documentElement.scrollTop
    // 得到是什么数据   数字型 不带单位
    // console.log(n)
})
```

- 开发中，我们经常检测页面滚动的距离，比如页面滚动100像素，就可以显示一个元素，或者固定一个元素
- document.documentElement   HTML 文档返回对象为HTML元素

总结：

- 被卷去的头部或者左侧用那个属性？是否可以读取和修改？
- 检测页面滚动的头部距离（被卷去的头部）用那个属性？

#### 3.4 案例 小兔鲜页面大于300就显示电梯导航

需求：当页面滚动大于300像素的距离时候，就显示侧边栏，否则隐藏侧边栏

- 需要用到页面滚动事件
- 检测页面被卷去的头部，如果大于300，就让侧边栏显示
- 显示和隐藏配合css过渡，利用opacity加渐变效果

#### 3.5 页面滚动事件-滚动到指定的坐标

- scrollTo() 方法可把内容滚动到指定的坐标
- 语法：`元素.scrollTo(x, y)`
- 例如：`window.scrollTo(0, 1000)`

#### 3.6 案例 返回顶部

需求：点击返回按钮，页面会返回顶部

分析：

- 绑定点击事件
- 利用scrollTop 让页面返回顶部

#### 3.7 页面尺寸事件

- 会在窗口尺寸改变的时候触发事件：resize

  - ```javascript
    window.addEventListener('resize', function () {
        console.log(1)
    })
    ```

- 检测屏幕宽度：

  - ```javascript
    window.addEventListener('resize', function () {
        console.log(document.documentElement.clientWidth)
    })
    ```

#### 3.8 页面尺寸事件-获取元素宽高

- 获取宽高
  - 获取元素的可见部分宽高（不包含边框，margin，滚动条等）
  - clientWidth和clientHeight

#### 3.9 案例 Rem 基准值

需求：分析 flexible.js 源码

![image-20220716174828665](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301030101263.png)

### 4. 元素尺寸与位置

- 使用场景：

  - 前面案例滚动多少距离，都是我们自己算的，最好是页面滚动到某个元素，就可以做某些事
  - 简单说，就是通过js的方式，得到元素在页面中的位置
  - 这样我们可以做，页面滚动到这个位置，就可以做某些操作，省去计算了

  ![image-20220716175105498](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301030101846.png)

#### 4.1 元素尺寸与位置-尺寸

- 获取宽高：

  - 获取元素的自身宽高、包含元素自身设置的宽高、padding、border
  - offsetWidth和offsetHeight  
  - 获取出来的是数值,方便计算
  - 注意: 获取的是可视宽高, 如果盒子是隐藏的,获取的结果是0

- 获取位置：

  - 获取元素距离自己定位父级元素的左、上距离
  - offsetLeft和offsetTop  注意是只读属性

  ![image-20220716175319154](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301030102022.png)

总结：

- offsetWidth和offsetHeight是得到元素什么的宽高？
  - 内容 + padding +  border
- offsetTop和offsetLeft 得到位置以谁为准？
  - 带有定位的父级
  - 如果都没有则以 文档左上角 为准

#### 4.2 案例 仿京东固定导航栏案例

需求：当页面滚动到秒杀模块，导航栏自动滑入，否则滑出

分析：

- 用到页面滚动事件
- 检测页面滚动大于等于 秒杀模块的位置 则滑入，否则滑出
- 主要移动的是秒杀模块的顶部位置

#### 4.3 案例 实现bilibili 点击小滑块移动效果

需求：当点击链接，下面红色滑块跟着移动

分析：

- 用到事件委托
- 点击链接得到当前元素的 offsetLeft值
- 修改line 颜色块的 left 值  =  点击链接的offsetLeft
- 添加过渡效果 

#### 4.4 getBoundingClientRect

- `element.getBoundingClientRect()`方法返回元素的大小及其相对于视口的位置

![image-20220716193501337](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301030102560.png)

总结：

| 属性                        | 作用                                     | 说明                                              |
| --------------------------- | ---------------------------------------- | ------------------------------------------------- |
| scrollLeft和scrollTop       | 被卷去的头部和左侧                       | 配合页面滚动来用，可读写                          |
| clientWidth 和 clientHeight | 获得元素宽度和高度                       | 不包含border,margin,滚动条 用于获取元素大小，只读 |
| offsetWidth和offsetHeight   | 获得元素宽度和高度                       | 包含border、padding，滚动条等，只读               |
| offsetLeft和offsetTop       | 获取元素距离自己定位父级元素的左、上距离 | 获取元素位置的时候使用，只读属性                  |

### 5. 案例 电梯导航

需求：点击不同的模块，页面可以自动跳转不同的位置

分析：

- 页面滚动到对应位置，导航显示，否则隐藏模块
- 点击导航对应小模块，页面 会跳到对应大模块位置
- 页面滚动到对应位置，电梯导航对应模块自动发生变化