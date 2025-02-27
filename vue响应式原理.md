1. new Vue调用Vue构造函数，传入配置项{el: '#app', beforeCreate() {}, created() {}} 
2. Vue构造函数接收传入的配置项，调用`this._init(options)`方法 
3. `_init`方法是通过原型模式进行注入的【initMixin】 

```js
export function initMixin(Vue: typeof Component) {
  Vue.prototype._init = function (options?: Record<string, any>) {
    const vm = this
    // a uid
    vm._uid = uid++
    // expose real self
    initLifecycle(vm)
    initEvents(vm) // vue的原型方法执行挂载，比如$on/$emit/$off/$once
    initRender(vm) // 挂载编译模板的方法
    // 调用挂载前生命周期钩子函数
    callHook(vm, 'beforeCreate', undefined, false /* setContext */)
    // 解析inject数据，在data和props之前
    initInjections(vm) // resolve injections before data/props
    initState(vm) // 初始化data/methods/computed/props ...
    initProvide(vm) // 解析provide数据
    callHook(vm, 'created') // 调用创建后生命周期钩子
    // 如果el选项存在，开始直接调用mount编译模板
    if (vm.$options.el) {
      vm.$mount(vm.$options.el)
    }
  }
}
```

4. 提供一个initMixin方法，传入Vue构造函数 
5. initMixin方法内部会把_init挂载到Vue的原型上 
6. `_init`方法内部在执行数据挂载之前，先通过callHook函数调用beforeCreate函数 
7. 调用initData挂载数据 initState(vm) 
8. 内部会判断是否有data选项，如果有，通过initData执行数据的响应式处理 initData(vm) 
9. 处理data数据：判断data是不是一个函数，如果是函数,通过call方法让this指向vm之后再调用【使用的时候data函数内部的this指向的是vue实例】，如果不是一个函数，直接赋值 

10. 【数据的代理】遍历data数据： 【vm.msg => `vm._data.msg`】
	a.使用Object.defineProperty进行劫持

* 【获取属性】组件内部通过this.[data里面的键]获取值的时候，会返回vm上`_data`里面的数据
* 【设置属性】通过this.[date里面的键]设置值的时候，数据设置给数据，而不是直接添加到vm实例上

11. 调用observe(data)开始检测这个数据
	  a. 判断data是不是一个对象，如果不是对象，retrun
	  b. 判断data是否有__ob__这个属性【判断这个数据是否已经被响应式处理过，如果处理过了，return】
  
12. new Observer(data),开始执行真正的响应式操作
	  a. constructor会先给当前的数据打一个标记，__ob__,添加了这个属性的就不需要二次处理
	  b. 判断data是不是一个数组
		  ⅰ. 如果是数组data.__proto__ = arrayMethods【重写了数组7个方法】
		  ⅱ. 只有7个数组方法，调用的时候使用的是vue重写之后的，其他的数组方法依旧会找到原生数组

```js
let oldArrayMethods = Array.prototype; // 获取数组原型上的方法

// 创建一个全新的对象 可以找到数组原型上的方法，而且修改对象时不会影响原数组的原型方法
export let arrayMethods = Object.create(oldArrayMethods); // {}.__proto__

let methods = [ // 这七个方法都可以改变原数组
  'push',
  'pop',
  'shift',
  'unshift',
  'sort',
  'reverse',
  'splice'
]
```

