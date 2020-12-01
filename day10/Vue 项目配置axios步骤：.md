Vue 项目配置axios步骤：

1. 安装axios：npm install axios

2. 在src目录下新建文件夹：可以是https / services / requests 做请求的目录

3. 在新建的文件夹下面新建文件 index.js

4. 所有的配置全部都配置到index.js里面来统一导出。

5. `import axios from 'axios'` 引入axios

6. 创建axios实例：`const ajax = axios.create()` 

7. 如果使用mock时，需要创建一个`baseURL`接口

   * 配置请求：

     ```js
     const ajax = axios.create({
         baseURL: "http://jsonplaceholder.typecode.com"
     })
     
     // 取todos
     export const getTodos = () => {
         return ajax.get('/todos')
     }
     
     // 取单个todo
     export const getTodoById = (id) => {
         return ajax.get('/todos/${id}')
     }
     ```

8. 在main.js里面引入requests的全部配置：import * as $http from './requests'

9. 挂载到Vue上：Vue.prototype.$http = $http  

10. 在App.vue文件里接受 

    ```js
    created () {this.$http.getTodo()
    	.then(resp => {
    
    	})
    }
    ```

    

```js
// 根据是否是开发环境来确定是使用哪一个接口地址，因为开发环境和上线的接口地址大部分都不一样
const isDev = process.env.NODE_ENV === 'development'
const ajax = axios.create({
    baseURL: isDev ? 'http://jsonplaceholder.typicode.com' : '真实的项目api地址'
})
```

注：根据是否是开发环境来确定使用哪一个接口地址，因为开发环境和上线的接口地址是不一样的。前面的地址是开发地址，后面的是上线地址。



**interceptors` 拦截器**

**拦截请求(用途)：**

```js
ajax.interceptors.request.use((config) => {
    // 第一个用途：用于显示全局的loading状态
    document.querySelector('.modal').style.display = 'block'
    // 第二个用途：在请求参数里加上全局的参数，比如：token, 这个token实际项目中会从本地存储里取
    config.headers.token = "dsafefasdcse"
    // 必须return config, 如果不return，请求不会执行
    return config
})
```

**拦截响应(用途)：**

```js
ajax.interceptors.response.use(resp => {
    // 第一个用途：隐藏全局的loading
    document.querySelector('.modal').style.display = "none"
    // 第二个用途： 全局处理错误
    if (resp.status === 200) {
        // 如果正确就返回出去数据即可
        return resp.data
    }
    // 在这里统一处理状态错误, 这种必须要后端配合，接口返回的格式必须是完全一致的
})
```



devServer：只有在开发模式下才有用，上线后就无效了。

