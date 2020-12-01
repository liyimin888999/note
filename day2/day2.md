# Day2

`npm list -g --depth=0` 查看全局安装

`npx`临时使用包

` npx express-generator backend`   临时安装express-generator 包到backend文件夹中

app.js

```js
//创建HTTP状态错误信息
var createError = require('http-errors');
//express
var express = require('express');
//原生模块path
var path = require('path');
//express的cookie处理中间件（middleware）
var cookieParser = require('cookie-parser');
//日志中间件
var logger = require('morgan');
//引入首页的路由
var indexRouter = require('./routes/index');
//引入users的路由
var usersRouter = require('./routes/users');
//引入asce的路由
var asceRouter = require('./routes/asce');

//创建express的实例
var app = express();

// view engine setup 设置view渲染引擎为ejs
app.set('views', path.join(__dirname, 'views'));
app.set('view engine', 'ejs');

//app.use是实例上的方法，表示应用中间件
app.use(logger('dev'));
app.use(express.json());
app.use(express.urlencoded({ extended: false }));
app.use(cookieParser());
app.use(express.static(path.join(__dirname, 'public')));
// 把路由也当成中间件来挂载
app.use('/', indexRouter);
app.use('/users', usersRouter);
app.use('/', asceRouter);

// catch 404 and forward to error handler
app.use(function(req, res, next) {
  next(createError(404));
});

// error handler
app.use(function(err, req, res, next) {
  // set locals, only providing error in development
  res.locals.message = err.message;
  res.locals.error = req.app.get('env') === 'development' ? err : {};

  // render the error page
  res.status(err.status || 500);
  res.render('error');
});
//相当于返回
module.exports = app;

```

**安装MongoDB**

**新建文件夹**

`c:\data\db` 

**命令行下运行MongoDB服务器**

​	必须从MongoDB目录中的bin目录执行mongod.exe

​	`c:\mongodb\bin\mongod --dbpath c:\data\db`

**连接MongoDB**

​	`c:\mongodb\bin\mongo`

**查看数据库**

​	`show dbs`

###### 创建数据库

​	use （库名）

###### 向数据库插入数据

​	db.html5(库名).insert({name: 'wang'})

`npm i mongoose`安装mongoose包  app连接mongodb

------

**Mongoose API**

###### 连接数据库

```js
const mongoose = require('mongoose');
mongoose.connect('mongodb://localhost:27017/html5',{useNewUrlParser: true});
```



Mongoose()

* mongoose 模块的exports对象是此类的实例。大多数应用只会使用这一个实例

Schema()

* 参数

  + [definition] <<Object | Schema | Array>> 可以是一下之一：描述模式路径的对象，或要复制的模式，或者对象和模式的数组
  + [options] <<Object>> 

* 例

  ```js
  var child = new Schema({ name: String });
  var schema = new Schema({ name: String, age: Number, children: [child] });
  var Tree = mongoose.model('Tree', schema);
  
  // setting schema options
  new Schema({ name: String }, { _id: false, autoIndex: false })
  ```

Connection()

* 参数

  + base <<Mongoose>> 一个mongoose的实例

  连接构造函数

  出于实际原因，Connection等于Db 

Document()

Model()

* 参数
  + doc  <<Object>>初始值的值 
  + optional  <<[fields]>>对象，包含在返回此文档的查询中选择的字段。你**不是**需要设置此参数，以确保Mongoose处理您的查询projetion。 

Model是一个与MongoDB交互的主要工具。Model的一个实例称为Document。 

在Mongoose中，术语"Model"指的是类的子`mongoose.Model`类。你不应该`mongoose.Model`直接使用这个类。的`mongoose.model()`和`connection.model()`功能创建的子类`mongoose.Model`，如下所示。 

* 例

```js
// `UserModel` is a "Model", a subclass of `mongoose.Model`.
const UserModel = mongoose.model('User', new Schema({ name: String }));

// You can use a Model to create new documents using `new`:
const userDoc = new UserModel({ name: 'Foo' });
await userDoc.save();

// You also use a model to create queries:
const userFromDb = await UserModel.findOne({ name: 'Foo' });
```

