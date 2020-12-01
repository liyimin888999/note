# EJS（模板渲染引擎）

## 入门

安装ejs

```js
npm install ejs
```

express设置渲染引擎为ejs

```js
app.set('view engine','ejs')
```

将模板字符串和一些数据作为参数传递给EJS，Duang，HTML出来了。

```js
var ejs = require('ejs'),
    people = ['geddy','neil','alex'],
    html = ejs.render('<%= people.join(","); %>',{
        people:people
    });
```

## 文档

实例

```html
<% if(user) { %>
   <h2><%= user.name %></h2>
<% } %>
```

用法

```js
var template = ejs.compile(str, options);
template(data);
// => 输出绘制后的 HTML 字符串
esj.render(str,data,options);
// => 输出绘制后的 HTML 字符串
ejs.renderFile(filename,data,options,function(err,str){
    // str => 输出绘制后的 HTML 字符串
})；
```

参数

* `cache`缓存编译后的函数，需要提供`filename`
* `filename`被`cache`参数用做键值，同时也用于`include`语句
* `context`函数执行时的上下文环境
* `compileDebug`当为`false`时不编译调试语句
* `client`返回独立的编译后的函数
* `delimiter`放在角括号中的字符，用于标记标签的开与闭
* `debug`将生成的函数体输出
* `_with`是否使用`with() {}`结构。如果为`false`,所有局部数据将储存在`locals`对象上。
* `localsName`如果不使用`with`，`localsName`将作为储存局部变量的对象的名称。默认名称是`locals`
* `rmWhitespace`删除所有可安全删除的空白字符，包括开始与结尾处的空格。对于所有标签来说，它提供了一个更安全版本的`-%>`（在一行的中间并不会剔除标签后面的换行符）。
* `escape`为`<%=`结构设置对应的转义（escape）函数。它被用于输出结果以及在生成的客户端函数中通过`toString()`输出。（默认转义XML)。

标签含义

* `<%`'脚本'标签，用于流程控制，无输出。
* `<%_`删除其前面的空格符
* `<%=`输出数据到模板（输出是转义HTML标签）
* `<%-`输出非转义的数据到模板
* `<%#`注释标签，不执行，不输出内容
* `<%%`输出字符串‘<%’
* `%>`一般结束标签
* `-%>`删除紧跟其后的换行符
* `_%>`将结束标签后面的空格符删除

包含（include）

通过`include`指令将相对于模板路径中的模板片段包含进来。（需要提供‘filename’参数。）例如，如果存在“./views/users.ejs”和“./views/user/show.ejs”两个模板文件，你可通过`<%- include('user/show'); %>`代码包含后者。

你可能需要能够输出原始内容的标签（`<%-`）用于include指令，避免对输出的HTML代码做转义处理。

```html
<ul>
    <% users.forEach(function(user){ %>
        <%- include('user/show',{user: user}); %>
    <% }); %>
       })
</ul>
```

自定义分隔符

可针对单个模板或全局使用自定义分隔符：

```js
var ejs = require('ejs'),
    users = ['geddy','neil','alex'];

//单个模板文件
ejs.render('<?= users.join(" | "); ?>',{
    users:users
},{
    delimiter:'?'
});
// => 'geddy | neil | alex'

//全局
ejs.delimiter = '$';
ejs.render('<$= users.join(" | "); $>',{
    users:users
});
// => 'geddy | neil | alex'
```

