### 为什么要去使用Promise

​    **1.指定回调函数的方式更加灵活**

​        **\* 旧的：必须在启动异步任务前指定**

​        **\* Promise：启动异步任务=>返回Promise对象=>给Promise对象绑定回调函数(甚至可以在异步任务结束后指定) **



​    **2.支持链式调用，可以解决回调地狱问题**

​        **回调地狱：回调函数嵌套调用，外部回调函数异步执行的结果是嵌套的回调函数执行的条件**

​        **回调地狱的缺点：不便于阅读，不便于异常处理**

​        **解决方案：Promise的链式调用**

​        **终级解决方案：async/await**



### vue中的v-show和v-if是做什么用的，两者区别是什么  ###

**v-if 是“真正的”条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地销毁和重建**

**v-if也是惰性的：如果在初始渲染条件为假，则什么也不做一直到条件第一次变为真，才会开始渲染条件块**

**相比之下，v-show就简单得多 不管初始条件是什么，元素总是会被渲染，并且简单地基于CSS进行切换**

**一般来说，v-if 有更高的切换开销，而v-show有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用v-show较好；如果运行时条件不太可能改变，则使用v-if较好**

### scss和stylus中如果style上使用scoped属性，如何做到对组件css样式的改变

**scss:**

**1. 下载scss npm install sass-loader node-sass --save**

2.

```vue
<style lang='scss' scoped>
```

**3.scss样式穿透： 父元素   / deep/   子元素**



**stylus:**

**1. 下载scss npm install stylus stylus-loader --save**

2.

```vue
<style lang='stylus' scoped>
```

**3.scss样式穿透： 父元素  >>>  子元素**



### v-model的使用

**可以实现双向绑定，在input或者select或者文本域配合value使用**



### vue中标签如何绑定事件

**v-on:click 简写 @click**

**绑定事件：<input @click="function" />**

**在移动端click有300ms延迟的问题，解决这个问题可以引入fastclick**

**下载 npm install fastclick**

**引入** 

```vue
import FastClick from 'fastclick'

FastClick.attach(document.body)
```



### 项目打包loader

**loader：加载器**

**用途：es6=>es5, scss,stylus=>css,然后打包成js文件**



### $nextTick的作用

**说明：$nextTick 是在下次DOM更新循环结束之后执行延迟回调，在修改数据之后使用$nextTick，则可以在回调中获取更新后的DOM**

**场景使用：需要在视图更新之后，基于新的视图进行操作**



### 脚手架 组件 data为什么必须是函数？

**因为js本身的特性带来的，如果data是一个对象，那么由于对象本身属于引用类型，当我们修改其中的一个属性时，会影响到所有vue实例的数据。如果将data作为一个函数返回一个对象，那么每一个实例的data属性都是独立的，不会相互影响了。**



### 对keep-alive的了解

**1.keep-alive是什么**

​		**内置组件，能在组件切换过程中将状态保留在内存中，防止重新渲染DOM**

**2.说明**

​		**keep-alive 它不会在DOM树中渲染**

**3.使用场景，几乎和渲染有关系**

**4.多2个生命周期**

​		**activated**

​		**deactivated**



### vue中 key的作用

**总结：**

​		**key的作用主要是为了高效的更新虚拟DOM**

**diff算法的问题**

**1.如果节点类型不同，直接干掉前面所有的节点，再创建并插入新的节点，不会再比较这个节点以后的子节点**

**2.如果节点类型相同，则会重新设置节点的属性，从而实现节点的更新**

**要使用key来给每一个节点做一个唯一表示，diff算法可以正确的识别此节点，找到正确的位置插入新的节点**



### watch和compute差异

**watch是进行数据监听，然后进行相应的操作，执行方法等。computed和methods的合体使用，比较耗性能，与vue性能优化相背而驰，尽量减少使用！**

**computed是数据改变进行相应的数据变化，由老数据变化新数据（return返回），会利用缓存机制对数据进行缓存，只有当依赖数据变化的时候才会进行相应的变化。**





### vue组件传值

#### 1.父传子

**父组件:**

```vue
<Header :msg='msg'></Header>
```

**子组件:**

```vue
	props: ['msg']
或
	props: {
		msg: 数据类型
	}
```

#### 2.子传父

子组件：

```vue
this.$emit('自定义事件名称'，要传的数据)
```

父组件：

```vue
<Header @childInput='getMsg'></Header>
methods: {
	getMsg(msg){
		....
	}
}
```

#### 3.兄弟组件之间传值

通过一个中转bus

A兄弟传值：

```vue
import bus from '@/common/bus'
bus.$emit("toB", this.msg)
```

B兄弟传值：

```vue
import bus from '@/common/bus'
bus.$on('toB', (data) => {
	....
})
```



### vue-cli项目中src目录每个文件夹和文件的用法

**src** 

​	**assets                                静态资源 （图片、js、css）**

​	**components					非路由组件**

​	**views								 路由组件**

​	**routers							 路由配置**

​	**store								 vuex(仓库)**

​	**App.vue						   挂载的第一个组件**

​	**main.js							 全局的文件**





