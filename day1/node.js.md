# 几个小命令

`ls`: 查看当前目录下有哪些文件（夹），可以加上`-a`参数显示所有文件（夹）

`ll`: 同`ls`, 只是显示方式不一样

`clear`: 清屏

`pwd`:  print work directory, 打印工作目录的路径

`cd 目录`: 进入某个目录, 如果不跟用户名，直接进行用户的根目录

`mkdir 目录名`：创建一个目录

`touch 文件名`：创建一个文件

`rm -rf 文件或者目录名`： 删除一个文件或者一个目录



`npm init`: 初始一个项目， 加`-y`参数可以不用提示直接创建`package.json`



在`package.json` 里可以添加任意的执行脚本。



如果node项目要监听代码的修改，可以使用 [nodemon](<https://www.npmjs.com/package/nodemon>)

```js
// http是node原生模块，不需要安装可以直接引入
const http = require('http')

// 使用http.createServer的方法创建一个server
const app = http.createServer((req, res) => {
  res.end('hello 1901!')
})
// 让server运行起来吧！！！
app.listen(3000, () => {
  console.log('server is running on http://localhost:3000')
})
```



一般在项目中，不会使用原生的方式来写应用。推荐有一些nodejs的框架

- express
- koa

# express

首先要安装`npm i express -S`

创建一个基本的express应用

```js
// 从express包里引入express方法, 这个不是原生的模块，所以需要先安装`npm i express -S`
const express = require('express')

// 创建一个express实例
const app = express()

// 定义一个路由，这个路由是通过get方法访问，当访问的时候，服务器发送一个响应给客户端
app.get('/', (req, res) => {
  res.send('hello express')
})

// 要让app运行起来，需要监听
app.listen(3000, () => {
  console.log('server is running on http://localhost:3000')
})
```

就可以通过`http://localhost:3000`访问，你将看到页面上有`hello express`