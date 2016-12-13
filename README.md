
# ah
基于weex搭建的跨平台小应用


### 初次尝试

weex最佳实践已总结入下文：

* weex-实战：https://github.com/ihuixu/ihuixu.github.io/blob/master/_posts/2016-12-11-weex-%E5%AE%9E%E6%88%98.markdown

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
  eventname : function(){
  
  }
}
```


* weex：created方法内添加

```javascript
this.$on('eventname',function(e){
```

