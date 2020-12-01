**ref**：在Vue里使用`ref`获取焦点或组件或DOM

```html
<tag ref="a"></tag>
```

使用this.$refs.a就可以获取焦点

**slot**：Vue插槽

**component**：`is`动态组件

**is**：动态组件语义化标签；Vue里面的表格`table`下面的`tbody`里面不能嵌套其它的组件

**key**：是Vue本身的，通过`key`去找组件，所以动态绑定`key`的时候并不会被渲染。

#### Vue动画

Vue提供了`transition`的封装组件

[animate](https://daneden.github.io/animate.css/) 动画

**transition**：负责给他的子元素添加和移除class

**transition-group**：多个元素动画

生命周期：

* 创建阶段
  * beforeCreate
    * 这个什么都没有`undefined`
  * create
    * 没有this.$el
    * 也没有真实的DOM
    * 但是已经有数据，那么就可以在这里更改数据了。如果数据是同步修改，就是带入到下一个生命周期。但是异步修改，当数据修改完之后就会进入更新阶段。在这里做ajax请求时比较推荐的方法。

* 挂载阶段
  * beforeMount
    * 这里已经能看到this.$el，当时还没有进行真实的模板数据替换，看到的还是插值表达式
  * mounted

* 更新阶段
  * beforeUpdate
  * updated

* 销毁阶段
  * beforeDestroy
  * destroyed

**Vue：$nextTick**

```js
方法一：
//在这里的dom是没有应用更新数据的dom
this.$nextTick(() => {
    //在这里的dom是应用更新数据的dom
    this.initSwiper()
})
方法二：
this.$nextTick()
    .then(() => {
    	this.initSwiper()
	})
```

##### 虚拟DOM

**DOM树**

diff算法

#### Vue CLI

Vue.js开发的标准工具

PWA：渐进式网页应用

scoped：只在当前生效







