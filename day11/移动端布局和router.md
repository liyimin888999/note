## 百分比布局

1. 宽度百分比是基于宽度的，高度百分比是基于父级容器高度的，margin和padding的百分比是基于父级容器宽度的
2. 绝对定位元素的基准点是包含元素的padding的
3. 绝对定位元素直接设置四周为零，即可让它宽度和高度均为100%
4. css也可以进行计算，并且单位还可以不同  calc。



### 移动端布局：百分比

布局单位：em / rem / vw

`em`：相对于父级；

```html
<span style="font-size: 20px;">
    字体大小<!--20px-->
    <span style="font-size: 20px;">
    	字体大小<!--40px-->
    </span>
</span>
```

`rem`：相对于根元素。

`@media`：媒体查询的断点 

`vw`：就是把屏幕平分成一百份，1vw就是屏幕的1%



**1px边框**：`box-shadow:0 0 0 .5 #f00;` 



### 移动端事件

`click事件`：有300毫秒的延迟。

`ontouchstart事件`：

**Zepto.js**   **touch.js**   **hammer.js** 



#### SPA单页Web应用

#### router动态组件

`route`：是当前页面的路由信息

Vue-router

1. 需要单独安装，不是集成到Vue里的。

2. 正常的情况下，需要一个routes的配置文件，并且把这个配置文件做为routes参数传入到VueRouter实例化的参数里。 VueRouter的实例又将做为参数传递到最外层的Vue实例的router参数。

   ```js
   // 路由的配置文件
   export default [{
     path: '',
     name: '',
     compoents: {
       default: 组件
       anotherView: 组件
     }
   }]
   ```

   ```js
   …………
   export default new VueRouter({
     ……
     routes: 就是上面的路由配置文件
   })
   ```

   ```
   new Vue({
     ……
     router: 就是上面的VueRouter实例
   })
   ```

   

3. 有一个组件叫`router-view`, 这个组件用于帮路由配置中的组件占位。可以有一个名字，那就对应路由组件里的components, 没有名字的，就对应default **这是最容易忽视的地方**

4. 还有一个组件叫router-link，用于跳转，跳转的方式有：

   

5. 只要使用了router, 每个组件上就有一个 `$route` 和`$router` ， 第一个表示当前路由所对应的所有路由信息。第二个是路由的方法

6. 传递参数的时候要注意，有显式传参和隐式传参

   * 显示传参：query传参，配置动态路由的key
   * 隐式传参：在params里传参，必须是某一个事件驱动来传参。



