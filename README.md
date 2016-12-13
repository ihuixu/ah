
# ah
基于weex搭建的跨平台小应用

### 快速开始

#### 最佳实践

1.安装weex-toolkit

```javascript
npm install  -g  weex-toolkit
```

2.安装 weexpack

```javascript
npm install -g weexpack
```


3.新建项目

```javascript
weexpack init [name]
cd [name]
npm install
```

#### 如何开发模式

1.package.json中的三种命令

```javascript
"scripts": {
    "build": "webpack",
    "dev": "webpack --watch",
    "serve": "serve -p 8080"
  }
```

2.开发模式

```javascript
npm run dev
```

3.在设备上访问

```javascript
weex src/app.we --qr
```

--qr 展示二维码，可使用weexplayground进行扫码访问

4.浏览器上访问

```javascript
npm run serve
```



#### 如何debug

1.浏览器：使用chrome development tools

2.客户端：

```javascript
weex debug
```



### 踩坑点

#### 1.常用的涉及到发http请求的第三方库都不能用

尝试引入leancloud进行数据操作，浏览器端正常，客户端失败

* 原因：浏览器和客户端的发送请求方法不一致，必须使用weex的stream进行操作，才能在客户端内正常，参考：http://alibaba.github.io/weex/doc/modules/stream.html
* 解决：未知，暂时带有发请求的第三方库用不了


#### 2.布局并不是浏览器看起来正常了，客户端就能正常

元素absolute的时候，浏览器上不写全top left等值也能正常显示，而客户端在不写全的时候会出现布局错误

* 原因：浏览器和客户端对布局的解释不一样
* 解决：尽量把布局写齐写全写死，显示效果不完全依赖浏览器解析

### 使用上与Vue不同的点

#### 1.repeat vs for

* list:[{id:1},{id:2}]


```javascript
<div repeat={{list}}>{{id}}</div>
```

vs

```javascript
<div v-for="item in list">{{item.id}}</div>
```

#### 2.if vs v-if

#### 3.Vue.component({}) vs [name].we

* weex 以文件路径定义组件

#### 4.使用weex-components

#### 5.weex特征

* 总结在：https://github.com/alibaba/weex/blob/ec10e8d3e9946c88f11aa9237a0879d3c8d5aae3/doc/references/cheatsheet.md

#### 6.onappear 和 ondisappear

weex的组件通用事件

#### 7.事件

```javascript
vm.$dispatch('eventname', params);
```

* vue：event下面添加方法

```javascript
event:{
  eventname : function(data){
    
  }
}
```


* weex：created方法内添加

```javascript
this.$on('eventname',function(e){
  var detail = e.detail
})
```

