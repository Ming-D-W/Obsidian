# vue指令（下）

## v-for 

### 基本使用

 v-for 作用: 遍历对象和数组

1. 遍历数组 (常用)

```jsx
v-for="item in 数组名"  item每一项
v-for="(item, index) in 数组名"  item每一项 index下标

注意：item和index不是定死的，可以是任意的名字，但是需要注意 第一项是值  第二项是下标
```

2. 遍历对象 (一般不用)

```jsx
<!--
  v-for也可以遍历对象（不常用）
  v-for="(值, 键) in 对象"
-->
<ul>
  <li v-for="value in user" :key="value">{{value}}</li>
</ul>
<ul>
  <li v-for="(value, key) in user" :key="key">{{value}} ---{{key}}</li>
</ul>
```

3. 遍历数字

```jsx
<!-- 
  遍历数字
  语法： v-for="(item, index) in 数字"
  作用：遍历具体的次数 item从1开始  index下标从0开始的
-->
<ul>
  <li v-for="(item, index) in 10" :key="item">{{item}} ---{{index}}</li>
</ul>
```

### 虚拟DOM 和 diff算法

**vue就地复用策略：** Vue会尽可能的就地（同层级，同位置），对比虚拟dom，复用旧dom结构，进行差异化更新。
![image-20221212150653908](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301041613730.png)
**虚拟dom**: 本质就是一个个保存节点信息, 属性和内容的 描述真实dom的 JS 对象

**diff算法：**

- 策略1：

  先同层级根元素比较，如果根元素变化，那么不考虑复用，整个dom树删除重建

  先同层级根元素比较，如果根元素不变，对比出属性的变化更新，并考虑往下递归复用。

- 策略2：

  对比同级兄弟元素时，默认按照**下标**进行对比复用。

  对比同级兄弟元素时，如果指定了 key，就会 **按照相同 key 的元素** 来进行对比。

### v-for 的key的说明

1. 设置 和 不设置 key 有什么区别？

   - 不设置 key， 默认同级兄弟元素按照下标进行比较。
   - 设置了key，按照相同key的新旧元素比较。

2. key值要求是?

   - 字符串或者数值，唯一不重复
   - 有 id 用 id,  有唯一值用唯一值，实在都没有，才用索引

3. key的好处?

   key的作用：提高虚拟DOM的对比复用性能

以后：只要是写到列表渲染，都推荐加上 key 属性。且 key 推荐是设置成 id， 实在没有，就设置成 index



## 样式处理

###  v-bind 对于class的增强

v-bind 对于类名操作的增强, 注意点, :class 不会影响到原来的 class 属性

:class="对象/数组"

```jsx
<template>
  <div>
    <!-- 
      v-bind： 作用：设置动态属性
      v-bind针对 class和style 进行增强
      允许使用对象或者数组
        对象：如果键值对的值为true，那么就有这个，否则没有这个类
        数组：数组中所有的类都会添加到盒子上
    -->
    <!-- <div class="box" :class="isRed ? 'red': ''">123</div> -->
    <!-- <div class="box" :class="{red: isRed, pink: isPink}">123</div> -->
    <div class="box" :class="arr">123</div>
  </div>
</template>
```
![](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301041635000.png)
### v-bind对于style 的增强

```jsx
<template>
    <div>
        <div :style="[size, color]">洛杉矶人民广场</div>
        <div :style="size">洛杉矶人民广场</div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            size: {
                fontSize: '20px',
                fontWeight: 'bold'
            },
            color: {
                color: 'pink'
            }
        }
    }
}
```

# 计算属性

## 基本使用
![[iShot_2023-01-02_11.40.08.png]]

需求：翻转字符串案例

> 计算属性是一个属性，写法上是一个函数，这个函数的返回值就是计算属性最终的值。
> 计算属性，只要他依赖的值发生变化的时候，才会重新计算
> 计算属性不能被当作方法调用,当成属性来用

>总结一下computed和methods的区别？

>methods：只要当前組件的任何数据有更新，methods肯定要执行

>computed：就年当前组件的数据有更新，如果当前计算属性依赖的值没有更新，不会重新计算

>计算属性：可以缓存

>【计算一次之后，结果会缓存起来，下一次用到的时候，直接使用缓存的结果（而不是重新计算）！】

>什么时候会重新计算：【计算属性依赖的值发生变化的时候，会重新计算】

定义计算属性

```jsx
// 组件的数据： 需要计算的属性
computed: {
  reverseMsg () {
    return this.msg.split('').reverse().join('')
  }
}
```

使用计算属性

```jsx
<p>{{ reverseMsg }}</p>
```

## 计算属性的缓存的问题

计算属性： 缓存

计算属性只要计算了一次，就会把结果缓存起来，以后多次使用计算属性，直接使用缓存的结果，只会计算一次。

计算属性依赖的属性一旦发生了改变，计算属性会重新计算一次，并且缓存

```jsx
// 计算属性只要计算了一次，就会把结果缓存起来，以后多次使用计算属性，直接使用缓存的结果，只会计算一次。
// 计算属性依赖的属性一旦发生了改变，计算属性会重新计算一次，并且缓存
export default {
  data () {
    return {
      msg: 'hello'
    }
  },
  computed: {
    reverseMsg() {
      console.log('我执行了')
      return this.msg.split('').reverse().join('')
    }
  }
}
```

## 成绩案例-计算属性处理总分 和 平均分

+ 在computed中提供计算属性

```jsx
computed: {
  sumScore () {
    return this.list.reduce((sum, item)=> sum + item.score, 0)
  },
  avgScore () {
    return this.list.length ? (this.sumScore / this.list.length).toFixed(2) : 0
  }
},
```

+ 在模板中直接渲染计算属性

```jsx
<tfoot>
  <tr>
    <td colspan="5">
      <span>总分：{{sumScore}}</span>
      <span style="margin-left:50px">平均分：{{avgScore}}</span>
    </td>
  </tr>
</tfoot>
```

## 计算属性的完整写法

```js
// 1. 计算属性默认情况下只能获取，不能修改。
// 2. 计算属性的完整写法
<template>
  <div>
    <input type="text" v-model.number="num">
    <input type="text" v-model="newNum">
  </div>
</template>

<script>
export default {
  computed: {
    newNum: {
      get() {
        // 使用newNum的值触发get方法
        return this.num + 1
      },
      set(kk) {
        // 给newNum赋值触发set方法
        return this.num = kk - 1
      }
    }
  },
  data() {
    return {
      num: 18
    }
  },
}
</script>
```

# 属性监听

## 基本使用

当需要监听某个数据是否发生改变，就要用到watch

```jsx
/* 
  watch: {
    // 只要属性发生了改变，这个函数就会执行
    属性: function () {

    }
  }
*/
watch: {
  // 参数1： value    变化后的值
  // 参数2： oldValue 变化前的值
  msg (value, oldValue) {
    console.log('你变了', value, oldValue)
  }
}
```

## 复杂类型的监听-监听的完整写法

> 如果监听的是复杂数据类型，需要深度监听，需要指定deep为true,需要用到监听的完整的写法

```jsx
// 1. 默认情况下，watch只能监听到简单类型的数据变化,如果监听的是复杂类型，只会监听地址是否发生改变，不会监听对象内部属性的变化。
// 2. 需要使用监听的完整写法 是一个对象
watch: {
  // friend (value) {
  //   console.log('你变了', value)
  // }
  friend: {
    // handler 数据发生变化，需要执行的处理程序
    // deep: true  如果true,代表深度监听，不仅会监听地址的变化，还会监听对象内部属性的变化
    // immediate: 立即 立刻  是否立即监听 默认是false  如果是true,代表页面一加载，会先执行一次处理程序
    handler (value) {
      console.log('你变了', value)
    },
    deep: true,
    immediate: true
  }
},
```

## 成绩案例-监听数据进行缓存

+ 监听list的变化

```jsx
watch: {
  list: {
    deep: true,
    handler() {
      localStorage.setItem('score-case', JSON.stringify(this.list))
    }
  }
},
```

+ 获取list数据的时候不能写死，从localStorage中获取

```jsx
data() {
  return {
    list: JSON.parse(localStorage.getItem('score-case')) || [],
    subject: '',
    score: '',
  }
},
```





# vscode断点调试

前言：作为前端开发，我们经常会遇到代码错误，需要进行调试

常见的调试方案：

- 不调试，直接看代码找问题
- console.log 打印日志
- **用 VSCode 的 debugger 来调试** （**断点调试**）

前两种，适合找一些简易的错误，如果短时间错误没有排查出来，建议使用 **vscode断点调试**。

![image-20220603234332440](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301040210090.png)





## 配置步骤 （两步）

1. 新建 `.vscode` 目录,  `launch.json` 文件， 填入配置内容

   注意：`端口号` 需要和 启动服务器 `端口号` 统一

```jsx
{
  "configurations": [
    {
      "name": "Launch Chrome",
      "request": "launch",
      "type": "pwa-chrome",
      "url": "http://localhost:8080",
      "sourceMapPathOverrides": {
        "webpack://src/*": "${workspaceFolder}/src/*"
      }
    }
  ]
}
```

效果如下图：

![image-20220603233902480](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301040210646.png)



2. `vue.config.js` 填入配置内容

```jsx
const { defineConfig } = require('@vue/cli-service')
module.exports = defineConfig({
  transpileDependencies: true,
  // -----------------------------------------------------------
  configureWebpack: config => {
    // 配置断点调试，实际上线时，可删除
    config.output.devtoolModuleFilenameTemplate = info => {
      const resPath = info.resourcePath
      return `webpack://${resPath}`
    }
  }
  // -----------------------------------------------------------
})
```

效果如下：

![image-20220603234122367](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301040210670.png)



两个配置加完，重新启动服务器，就可以在vscode源代码中进行断点调试啦！



## 使用演示

1. 代码行号前面，点击打上断点

![image-20220603234435355](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301040210930.png)

2. 启动服务器

![image-20220603234739226](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301040210491.png)

3. 开始调试

![image-20220603234836207](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301040210955.png)

4. 效果预览

![image-20220603235019255](https://photo-album-1314189846.cos.ap-shanghai.myqcloud.com/202301040210276.png)



5. 左侧还有变量，监视，调用堆栈等，可以自行参考使用 （可选）

