---
title: vue知识点汇总
date: 2019-05-24 22:30:25
tags: [vue]
categories: "vue"
---
#### 1、vue中key值的作用
> key 的特殊属性主要用在 Vue的虚拟DOM算法，在新旧nodes对比时辨识VNodes。如果不使用key，Vue会使用一种最大限度减少动态元素并且尽可能的尝试修复/再利用相同类型元素的算法。使用key，它会基于key的变化重新排列元素顺序，并且会移除key不存在的元素。  
> 有相同父元素的子元素必须有独特的key。重复的key会造成渲染错误。  
> 最常见的用例是结合 v-for:
```css
<ul>
  <li v-for="item in items" :key="item.id">...</li>
</ul>
```
> 它也可以用于强制替换元素/组件而不是重复使用它。当你遇到如下场景时它可能会很有用:  
> 完整地触发组件的生命周期钩子  
> 触发过渡
```css
<transition>
  <span :key="text">{{ text }}</span>
</transition>
```
> 当 text 发生改变时，<span> 会随时被更新，因此会触发过渡。

#### 2、vue中子组件调用父组件的方法
> 子组件调用父组件的方法可以使用this.$emit() 

#### 3、vue等单页面应用及其优缺点
> 优点  
1、具有桌面应用的即时性、网站的可移植性和可访问性  
2、用户体验好、快，内容的改变不需要重新加载整个页面  
3、基于上面一点，SPA相对对服务器压力小  
4、良好的前后端分离。SPA和RESTful架构一起使用，后端不再负责模板渲染、输出页面工作，web前端和各种移动终端地位对等，后端API通用化  
5、同一套后端程序代码，不用修改就可以用于Web界面、手机、平板等多种客户端  

> 缺点  
1、不利于SEO。（如果你看中SEO，那就不应该在页面上使用JavaScript，你应该使用网站而不是Web应用）  
2、初次加载耗时相对增多  
3、导航不可用，如果一定要导航需要自行实现前进、后退

#### 4、v-show和v-if指令的共同点和不同点?
* v-show指令是通过修改元素的displayCSS属性让其显示或者隐藏（不操作DOM元素）  
* v-if指令是直接销毁和重建DOM达到让元素显示和隐藏的效果（注意：v-if 可以实现组件的重新渲染）

#### 5、如何让CSS只在当前组件中起作用?
> 将当前组件的`<style>修改为<style scoped></style>`

#### 6、深度选择器/deep/(>>>)
> 以Element-ui为例。那就是在父组件写css时，样式选择器中加上 /deep/或者 >>> 这两个标记，即可渗透到子组件的样式中  
> 加上/deep/或者>>>后  
```css
.back_index /deep/.el-menu-item{
  color:#a7b1c2!important;
}

或者

.back_index >>> .el-menu-item{
  color:#a7b1c2!important;
}
```
> 子组件的样式就被父组件的样式给修改了

#### 7、<keep-alive></keep-alive>的作用是什么?
> `<keep-alive></keep-alive>` 包裹动态组件时，会缓存不活动的组件实例,主要用于保留组件状态或避免重新渲染。

#### 8、指令v-el和v-ref的作用是什么?
> v-el 为DOM元素注册一个索引，通过v-el我们可以获取到DOM对象  
```css
<span v-el:msg>hello</span>
```
> this.$els.msg  /hello

> v-ref 通过v-ref获取到整个组件（component）的对象。  
> 访问：this.$refs.v-ref后的值

#### 9、Vuex的原理和使用方法
<div style='display:flex;justify-content: flex-start'>
    ![这是一张图片](https://github.com/GitHubwyq/photos/blob/master/imgs/20190524212213.png?raw=true)
</div>  

##### 数据单向流动
> 一个应用可以看作是由上面三部分组成: View, Actions,State,数据的流动也是从View => Actions => State =>View 以此达到数据的单向流动。  
> 但是项目较大的, 组件嵌套过多的时候, 多组件共享同一个State会在数据传递时出现很多问题.Vuex就是为了解决这些问题而产生的。    
> Vuex可以被看作项目中所有组件的数据中心,我们将所有组件中共享的State抽离出来,任何组件都可以访问和操作我们的数据中心。  

> Vuex的组成：一个实例化的Vuex.Store由state, mutations（更改信息是同步更改）和actions（更改信息是异步更改）三个属性组成:  
> > 1、state中保存着共有数据  
> > 2、改变state中的数据有且只有通过mutations中的方法,且mutations中的方法必须是同步的  
> > 3、如果要写异步的方法,需要些在actions中, 并通过commit到mutations中进行state中数据的更改.

#### 10、vue中Computed 和 Watch的使用和区别
> computed: 可以关联多个实时计算的对象，当这些对象中的其中一个改变时都会出发这个属性。具有缓存能力，所以只有当数据再次改变时才会重新渲染，否则就会直接拿取缓存中的数据。（有缓存）

> Watch：当你需要在数据变化响应时，执行异步操作，或高性能消耗的操作，自定义 watcher 的方式就会很有帮助

> vue官网的例子:如下
```html
<div id="myDiv">
    <input type="text" v-model="firstName">
    <input type="text" v-model="lastName">
    <input type="text" v-model="fullName">
</div>
```
> computed方式
```js
new Vue({
  el:"#myDiv",
    data:{
      firstName:"Den",
      lastName:"wang",

  },
  computed:{
    fullName:function(){
        return  this.firstName  + " " +this.lastName;
    }
  }
})
```
> watch方式
```js
new Vue({
  el: '#myDiv',
  data: {
    firstName: 'Foo',
    lastName: 'Bar',
    fullName: 'Foo Bar'
  },
  watch: {
    firstName: function (val) {
      this.fullName = val + ' ' + this.lastName
    },
    lastName: function (val) {
      this.fullName = this.firstName + ' ' + val
    }
  }
})
```
#### 11、active-class是哪个组件的属性？
> active-class是vue-router模块的router-link组件中的属性，用来做选中样式的切换

> 使用方法  
> 1、直接在路由js文件中配置linkActiveClass
```js
export default new Router({
  linkActiveClass: 'active',
})
```
> 2、在router-link中写入active-class
```js
router-link to="/home" class="menu-home" active-class="active">首页</router-link>
```

#### 12、怎么定义vue-router的动态路由？怎么获取传过来的动态参数？
> 在router目录下的index.js文件中，对path属性加上/:id。  使用router对象的params.id 例如 :  this.$route.params.id

#### 13、vue-router有哪几种导航钩子？
#### 1.全局钩子  
> 主要包括beforeEach和aftrEach,

##### beforeEach函数有三个参数：
> 1、to: router即将进入的路由对象  
> 2、from: router当前导航即将离开的路由  
> 3、next: Function继续执行函数  
> > * next()：继续执行
> > * next(false)：中断当前的导航。
> > * next(‘/‘) 或 next({ path: ‘/‘ })：跳转新页面，常用于登陆失效跳转登陆
##### afterEach函数不用传next()函数
> 这类钩子主要作用于全局,一般用来判断权限,以及以及页面丢失时候需要执行的操作,例如:
```js
//使用钩子函数对路由进行权限跳转
router.beforeEach((to, from, next) => {
  const role = localStorage.getItem('ms_username');
  if(!role && to.path !== '/login'){
      next('/login');
  }else if(to.meta.permission){
      // 如果是管理员权限则可进入，这里只是简单的模拟管理员权限而已
      role === 'admin' ? next() : next('/403');
  }else{
      // 简单的判断IE10及以下不进入富文本编辑器，该组件不兼容
      if(navigator.userAgent.indexOf('MSIE') > -1 && to.path === '/editor'){
          Vue.prototype.$alert('vue-quill-editor组件不兼容IE10及以下浏览器，请使用更高版本的浏
            览器查看', '浏览器不兼容通知', {
              confirmButtonText: '确定'
          });
      }else{
          next();
      }
  }
})
```
#### 2、路由独享的守卫
> 你可以在路由配置上直接定义 beforeEnter 守卫：
```js
const router = new VueRouter({
  routes: [
    {
      path: '/foo',
      component: Foo,
      beforeEnter: (to, from, next) => {
        // ...
      }
    }
  ]
})
```

#### 3、组件内的守卫
> 最后，你可以在路由组件内直接定义以下*路由导航守卫：
> > * beforeRouteEnter  
> > * beforeRouteUpdate (2.2 新增)  
> > * beforeRouteLeave
```js
const Foo = {
  template: `...`,
  beforeRouteEnter (to, from, next) {
    // 在渲染该组件的对应路由被 confirm 前调用
    // 不！能！获取组件实例 `this`
    // 因为当守卫执行前，组件实例还没被创建
  },
  beforeRouteUpdate (to, from, next) {
    // 在当前路由改变，但是该组件被复用时调用
    // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
    // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
    // 可以访问组件实例 `this`
  },
  beforeRouteLeave (to, from, next) {
    // 导航离开该组件的对应路由时调用
    // 可以访问组件实例 `this`
  }
}
```
> beforeRouteEnter 守卫 不能 访问 this，因为守卫在导航确认前被调用,因此即将登场的新组件还没被创建。  
> 不过，你可以通过传一个回调给 next来访问组件实例。在导航被确认的时候执行回调，并且把组件实例作为回调方法的参数
```js
beforeRouteEnter (to, from, next) {
  next(vm => {
    // 通过 `vm` 访问组件实例
  })
}
```
> 注意 beforeRouteEnter 是支持给 next 传递回调的唯一守卫。对于 beforeRouteUpdate 和 beforeRouteLeave 来说，this 已经可用了，所以不支持传递回调，因为没有必要了。
```js
beforeRouteUpdate (to, from, next) {
  // just use `this`
  this.name = to.params.name
  next()
}
```
> 这个离开守卫通常用来禁止用户在还未保存修改前突然离开。该导航可以通过 next(false) 来取消
```js
beforeRouteLeave (to, from , next) {
  const answer = window.confirm('Do you really want to leave? you have unsaved changes!')
  if (answer) {
    next()
  } else {
    next(false)
  }
}
```

#### 14、router路由跳转时，传参方式params query区别
> 1、传参可以使用params和query两种方式  
> 2、使用params传参只能用name来引入路由，即push里面只能是name:’xxxx’,不能是path:’/xxx’,因为params只能用name来引入路由，如果这里写成了path，接收参数页面会是undefined  
> 3、使用query传参使用path来引入路由  
> 4、params是路由的一部分,必须要在路由后面添加参数名。query是拼接在url后面的参数，没有也没关系  
> 5、二者还有点区别，直白的来说query相当于get请求，页面跳转的时候，可以在地址栏看到请求参数，而params相当于post请求，参数不会再地址栏中显示

#### 15、Vue的双向数据绑定原理是什么？
> vue.js 是采用数据劫持结合发布者-订阅者模式的方式，通过Object.defineProperty()来劫持各个属性的setter，getter，在数据变动时发布消息给订阅者，触发相应的监听回调

#### 16、如何封装 vue 组件
> 首先，组件可以提升整个项目的开发效率。能够把页面抽象成多个相对独立的模块，解决了我们传统项目开发：效率低、难维护、复用性等问题。然后，使用Vue.extend方法创建一个组件，然后使用Vue.component方法注册组件。子组件需要数据，可以在props中接受定义。而子组件修改好数据后，想把数据传递给父组件。可以采用emit方法。



