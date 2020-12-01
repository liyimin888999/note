## Hybrid app.  混合app

nNative app:  原生app

​	iOS:Objective C/Swift来开发

​	Android: java

​	缺点: 开发周期长，开发不灵活，需要维护多套代码

​	优点: 用户体验好，因为调用的是原生，更流畅

Web app: 网页

​	优点: 开发起来很快，足够灵活，只需要维护一套代码(html/css/javascript)

​	缺点: 早期没办法直接调用原生的接口，比如定位之类的，借助于H5的功能可以有部分原生的调用能力，很多api还得基于https

PWA: Progressive Web App , (渐进式增强WEB应用) 简称PWA



##### HYbrid: 网页和原生的接合

1. 原生主导

   原生开发为主，web为辅，想微信，JD

   原生为主，做主要的框架，其中的某些模块使用H5来编写，原生会提供一个类似于内置浏览器的东西来访问这个H5页面->webview

2. H5主导

   直接开发网页，原生提供JS接口，让网页去调用。完了之后，用原生的工具进行打包。

##### 混合开发的一些工具或者框架:

Phonegap

Cordova

React Native(不是真正的混合开发)

Dcloud H5+

electron: 桌面应用混合开发 electron(用网页的形式来写应用)

bootstrap: 引导程序