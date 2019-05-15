---
title: 小程序和vue有哪些不同？
date: 2019-05-15 15:07:08
tags: [Vue]
categories: "Vue"
---
#### 1.生命周期
##### 小程序  
> onLoad：页面加载  
> > 一个页面只会调用一次，可以在 onLoad 中获取打开当前页面所调用的 query 参数。  

> onShow：页面显示  
> > 每次打开页面都会调用一次

> onReady：页面初次渲染完成  
> > 一个页面只会调用一次，代表页面已经准备妥当，可以和视图层进行交互。对界面的设置如 wx.setNavigationBarTitle请在 onReady之后设置。详见生命周期。  
```js
wx.setNavigationBarTitle({

title:this.data.titleName

});
```

> onHide：页面隐藏
> > 当 navigateTo或底部tab切换时调用。

> onUnload：页面卸载  
> > 当 redirectTo或 navigateBack的时候调用。

##### Vue.js
> 创建前/后：(这两个生命周期里获取不到dom元素)
> > 在beforeCreated阶段，vue实例的挂载元素$el和数据对象data都为undefined，还未初始化。在created阶段，vue实例的数据对象data有了，$el还没有。

> 载入前/后：（mounted生命周期里可以获取到dom元素）
> > 在beforeMount阶段，vue实例的$el和data都初始化了，但还是挂载之前为虚拟的dom节点，data.message还未替换。在mounted阶段，vue实例挂载完成，data.message成功渲染。

> 更新前/后：  
> > 当data变化时，会触发beforeUpdate和updated方法。

> 销毁前/后：
> > 在执行destroy方法后，对data的改变不会再触发周期函数，说明此时vue实例已经解除了事件监听以及和dom的绑定，但是dom结构依然存在

#### 2、数据双向绑定
##### 1、设置值
> 在vue中，只需要再表单元素上加上 v-model,然后再绑定 data中对应的一个值，当表单元素内容发生变化时， data中对应的值也会相应改变，这是vue非常nice的一点。
```js
<div id="app">
 <input v-model="reason" placeholder="填写理由" class='reason'/>
</div>
 
new Vue({
 el: '#app',
 data: {
    reason:''
 }
})
```

> 然而在小程序中，却没有这个功能。

> 当表单内容发生变化时，会触发表单元素上绑定的方法，然后在该方法中，通过 this.setData({key:value})来将表单上的值赋值给 data中的对应值。  
> > 下面是代码
```JS
<input bindinput="bindReason" placeholder="填写理由" class='reason' value='{{reason}}' name="reason" />
 
Page({
    data:{
        reason:''
    },
    bindReason(e) {
        this.setData({
        reason: e.detail.value
        })
    }
})

```
##### 2、取值
> vue中，通过 this.reason取值。

> 小程序中，通过 this.data.reason取值。 

#### 3.组件通信
##### 1、子组件的使用
> 在vue中，需要：
> > 1、编写子组件  
> > 2、在需要使用的父组件中通过 import引入  
> > 3、在 vue的 components中注册  
> > 4、在模板中使用
```js
//子组件 bar.vue
<template>
    <div class="search-box">
    <div @click="say" :title="title" class="icon-dismiss"></div>
    </div>
</template>
<script>
    export default{
        props:{
            title:{
            type:String,
            default:''
            }
        }
    },
    methods:{
        say(){
            console.log('明天不上班');
            this.$emit('helloWorld')
        }
    }
    </script>
    
// 父组件 foo.vue
<template>
    <div class="container">
        <bar :title="title" @helloWorld="helloWorld"></bar>
    </div>
</template>
 
<script>
import Bar from './bar.vue'
export default{
data:{
    title:"我是标题"
},
methods:{
    helloWorld(){
        console.log('我接收到子组件传递的事件了')
    }
},
components:{
    Bar
}
</script>
```
> 子组件和父组件通信可以通过 this.$emit将方法和数据传递给父组件。
##### 小程序中
> 1、编写子组件  
> 2、在子组件的 json文件中，将该文件声明为组件
```js
{
    "component": true
}
```
> 3、在需要引入的父组件的 json文件中，在 usingComponents填写引入组件的组件名以及路径
```js
"usingComponents": {
    "tab-bar": "../../components/tabBar/tabBar"
 }
```
> 4、在父组件中，直接引入即可
```js
<tab-bar currentpage="index"></tab-bar>
```
> 完整代码如下
```js
// 子组件
<!--components/tabBar/tabBar.wxml-->
<view class='tabbar-wrapper'>
    <view class='left-bar {{currentpage==="index"?"active":""}}' bindtap='jumpToIndex'>
        <text class='iconfont icon-shouye'></text>
        <view>首页</view>
    </view>
    <view class='right-bar {{currentpage==="setting"?"active":""}}' bindtap='jumpToSetting'>
        <text class='iconfont icon-shezhi'></text>
        <view>设置</view>
    </view>
</view>
```
#### 4、父子组件通信
> 在vue中  
> 父组件向子组件传递数据，只需要在子组件通过 v-bind传入一个值，在子组件中，通过 props接收，即可完成数据的传递，示例：
```js
// 父组件 foo.vue
<template>
    <div class="container">
    <bar :title="title"></bar>
    </div>
</template>
<script>
import Bar from './bar.vue'
export default{
data:{
    title:"我是标题"
},
components:{
    Bar
}
</script>
 
// 子组件bar.vue
<template>
    <div class="search-box">
        <div :title="title" ></div>
    </div>
</template>
<script>
export default{
props:{
    title:{
        type:String,
            default:''
        }
    }
}
</script>
```
##### 小程序中
> 父组件向子组件通信和vue类似，但是小程序没有通过 v-bind，而是直接将值赋值给一个变量，如下：
```js
<tab-bar currentpage="index"></tab-bar>
```
> 此处， “index”就是要向子组件传递的值,在子组件 properties中，接收传递的值。
```js

properties: {
    // 弹窗标题
    currentpage: {   // 属性名
        type: String,  // 类型（必填），目前接受的类型包括：String, Number, Boolean, Object, Array, null（表示任意类型）
        value: 'index'  // 属性初始值（可选），如果未指定则会根据类型选择一个
    }
}
```
> 子组件向父组件通信和 vue也很类似，代码如下：
```js
//子组件中
methods: {
    // 传递给父组件
    cancelBut: function (e) {
        var that = this;
        var myEventDetail = { pickerShow: false, type: 'cancel' } // detail对象，提供给事件监听函数
        this.triggerEvent('myevent', myEventDetail) //myevent自定义名称事件，父组件中使用
    },
}
 
//父组件中
<bar bind:myevent="toggleToast"></bar>
 
// 获取子组件信息
toggleToast(e){
    console.log(e.detail)
}
```
> 如果父组件想要调用子组件的方法  
> vue会给子组件添加一个 ref属性，通过 this.$refs.ref的值便可以获取到该子组件，然后便可以调用子组件中的任意方法，例如：
```js
//子组件
<bar ref="bar"></bar>
 
//父组件
this.$refs.bar.子组件的方法
```
> 小程序是给子组件添加 id或者 class，然后通过 this.selectComponent找到子组件，然后再调用子组件的方法,示例：
```js
//子组件
<bar id="bar"></bar>
 
// 父组件
this.selectComponent('#bar').子组件的方法
```
#### 5、条件渲染
> vue:使用v-if指令，v-else表示v-if的else块，v-else-if表示v-if 的“else-if 块”
```html
<div v-if="type === 'A'">
    A
</div>
<div v-else-if="type === 'B'">
    B
</div>
<div v-else-if="type === 'C'">
    C
</div>
<div v-else>
    Not A/B/C
</div>
```
> 微信小程序：使用wx:if,wx:else表示wx:if的else块，wx:elif表示wx:if的"else-if"块
```html
<view wx:if="{{length > 5}}"> 1 </view>
<view wx:elif="{{length > 2}}"> 2 </view>
<view wx:else> 3 </view>
```
#### 6、显示隐藏元素
> VUE
```js
v-show="..."
```
> 微信小程序：
```js
hidden="{{...}}"
```
#### 7、绑定class
##### Vue
> 全用v-bind，或者简写为:bind,和本有的class分开写
```html
<div class="test" v-bind:class="{ active: isActive }"></div>
```
##### 小程序
```html
<view class="test {{isActive ? 'active':'' }}"></view>
```
#### 8、事件处理
##### Vue
> 使用v-on:event绑定事件，或者使用@event绑定事件(v-on可以简写为@)
```html
<button v-on:click="counter += 1">
    Add 1
</button>
<button v-on:click.stop="counter+=1">
    Add1
</button>  //阻止事件冒泡
```
##### 微信小程序
> 全用bindtap(bind+event)，或者catchtap(catch+event)绑定事件
```html
<button bindtap="clickMe">
    点击我
</button>
<button catchtap="clickMe">
    点击我
</button>  //阻止事件冒泡
```
#### 9、绑定事件传参
##### Vue
> vue绑定事件的函数传参数时，可以把参数写在函数后面的括号里
```html
<div @click="changeTab(1)">哈哈</div>
```
##### 微信小程序
> 微信小程序的事件我试过只能传函数名，至于函数值，可以绑定到元素中，在函数中获取
```html
<view data-tab="1" catchtap="changeTab">哈哈</view>
```
```js
changeTab(e){
   var _tab = e.currentTarget.dataset.tab;  
}
```
##### 暂时总结这么多
![这是一张图片](https://github.com/GitHubwyq/photos/blob/master/imgs/1540356271655.jpg?raw=true)



