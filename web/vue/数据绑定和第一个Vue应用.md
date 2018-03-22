## 数据绑定第一个Vue应用
用最简单的html代码感受vue.js的核心功能
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>第一个vue应用</title>
</head>
<body>
    <div id="app">
        <input type="text" v-model="name" placeholder="你的名字">
        <i>晚安,{{ name }}</i>
    </div>
    <script src="https://cdn.bootcss.com/vue/2.5.13/vue.js"></script>
    <script>
       var app =  new Vue({
            el:'#app',
            data:{
                name: ''
            }
        })
    </script>
</body>
</html>

```
### Vue实例与数据绑定
#### 实例与数据
通过构造函数Vue就可以创建一个Vue的根实例，并启动Vue应用
```js
//变量app就代表了这个Vue实例。事实上几乎所有代码都是一个对象，写入Vue实例的选项内的。
var app = new Vue({
    //选项
    el:document.getElementById('app'), //或者是'#app'
    //必不可少的一个选项，用于指定一个页面中已经存在的DOM元素来挂载Vue实例。它可以是HTMLElement，也可以是CSS选择器。挂载成功后，可以通过app.$el来访问该元素。
    data:{
        name:'vue.js'
    }
    //可以说明应用内需要双向绑定的数据。建议将所有会用到的数据都预先在data内声明，这要不至于将数据散落在业务逻辑中，难以维护。
    //VUE实例也代理了data对象的所有属性。所以可以通过app.name来访问data里的数据。
})
```
#### 生命周期
常用生命周期钩子
- **crated** 实例创建完成后调用，此阶段完成了数据的观测等，但尚未挂载，$el还不可用。需要初始化处理一些数据是会比较有用。
- **mounted** el挂载在实例上后调用。一般我的的第一个业务逻辑会在这里开始。
- **beforeDestroy** 实例销毁之前调用。主要解绑一些使用addEventListentr监听的事件等。

这些钩子与el和data类似，也是可以作为选项写入Vue实例内，并且钩子的this指向的是调用它的Vue的实例。
```js
var app = new Vue({
    el:'app',
    data:{
        a:1
    },
    crated:funtion(){
        console.log(this.a);//1
    },
    mounted:funtion(){
        console.log(this.$el);//<div id="app"></div>
    }
})
```
#### 插值与表达式
- 使用(Mustache语法)`{{}}`是基本的文本插值方法，它会自动将双向绑定的数据实时显示出来。

- 如果想输出html，使用`v-html`。但使用`v-html`有可能导致xss攻击，所以要在服务端对用户提交的信息进行处理，一般可将`<>`进行转义。

- 如果想显示`{{}}`标签，而不进行替换，使用`v-pre`即可跳过这个元素和它的子元素的变异过程。`<span v-pre>{{这里的内容是不会被编译的}}</pre>`

- `{{}}`内除了简单的绑定属性值外，还可以用JavaScript表达式进行简单的运算，三元运算符等
    ```html
    <div id="app">
        {{number / 10}}
        {{isOk:'确定'?'取消'}}
        {{text.split(',').reverse().join(',')}}
    </div>
    <script>
    var app =  new Vue({
            el:document.getElementById('app'),
            data:{
                number:1,
                isOk:true,
                text:'123,456'
            }
            
        })
    </script>
    ```
- Vue.js只支持单个表达式，不支持语句与控制流。另外在表达式中，不能使用用户自定义的全局变量，只能使用vue白名单内的全局变量。
    ```html
    <!--这是语句，不是表达式-->
    {{var book = "vue"}}
    <!--不能使用流控制，要使用三元运算-->
    {{if(ok) return msg}}
    ```

#### 过滤器
Vue.js 支持在`{{}}`插值的尾部和`v-bind` 表达式 (*后者从 2.1.0+ 开始支持*)添加管道`|`对数据进行过滤。过滤的规则是自定义的，通过vue实例添加`filters`选项来进行设置。
```html
<!-- 在双花括号中 -->
{{ message | capitalize }}

<!--过滤器函数总接收表达式的值 (之前的操作链的结果) 作为第一个参数。 b 接受 a ,c 接收 b-->
{{a | b | c}}

<!-- 在 `v-bind` 中 -->
<div v-bind:id="rawId | formatId"></div>
```

```js
filters: {
  capitalize: function (value) {
    if (!value) return ''
    value = value.toString()
    return value.charAt(0).toUpperCase() + value.slice(1)
  }
}

//全局定义过滤器
Vue.filter('capitalize', function (value) {
  if (!value) return ''
  value = value.toString()
  return value.charAt(0).toUpperCase() + value.slice(1)
})
```


### 指令与事件
最常用的一项功能，以`v-`为前缀。指令的主要职责是当其表达式的值发生改变时，相应的将某种行为应用到DOM上。

**基础用法**
- v-if
  ```html
  <p v-if="show">根据show的属性值来判断是否显示这段文本</p>
  ```
- v-bind
  ```html
  <a v-bind:src="href">动态更新HTML元素上的属性，如id，class，src等</a> 
  ```
- v-on
  ```html
     <div id="app">
        <p v-if="show">show and hide</p>
        <button v-on:click="toggle">点击显示或隐藏</div>
    </div>
    <script>
        var app = new Vue({
            el:'#app',
            data:{
                show:true
            },
            methods:{
                toggle:function(){
                    if(this.show){
                        this.show = false;
                    }else{
                        this.show = true;
                    }
                }
            }
        })
    </script>

    <!--内联语句-->
     <button v-on:click="show = fasle">点击隐藏</div>
    <!--业务中常用-->
    <script>
     methods:{
        toggle:function(){
            this.ifShow();
        },
        ifShow:function(){
            if(this.show){
                this.show = false;
            }else{
                this.show = true;
            }
        }
    }
    </script>        
  ```

### 语法糖
语法糖是指不影响功能的情况下，添加某种方法实现同样的效果，从而方便程序开发。

Vue.js的`v-bind`和`v-on`都提供了语法糖。也可说是**缩写**。

```html
<!-- v-bind 缩写 :-->
<a :src="href"></a>

<!-- v-on 缩写 @ -->
<button @click="close"><button>
```
---
