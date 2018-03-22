## 初识Vue.js

### Vue是什么
- 小巧 17k
- 渐进式
- 高级功能
    - 解耦视图与数据
    - 可复用的组件
    - 前端路由
    - 状态管理
    - 虚拟DOM(virtual DOM)
#### MVVM模型
![1515941474515.jpg](http://upload-images.jianshu.io/upload_images/5600906-f85ee6c66cc43b0e.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
#### Vue.js 有什么不同
jquery

**频繁操作DOM，后期维护繁琐,困难。**
```js
if(showBtn){
    var btn = $('<button>click</btton>');
    btn.on('click',function(){
        console.log('Clicked!');
    });
    $('#app').append(btn);
}
```
vue

>vue通过mvvm的模式拆分为视图与数据两部分，并将其分离。因此着关心数据即可，dom的问题vue会自动帮你搞定
```html
<body>
    <div id="app">
        <button v-if="showBtn" v-on:click="handleClick">
        Click
        </button>
    </div>
</body>
<script>
    new Vue({
        el:'#app',
        data:{
            showBut:true
        },
        methods:{
            handleClick:funtion(){
                console.log('Clicked!');
            }
        }
    })
</script>
```
*上述代码不需要理解，这里只是快速展示*

### 如何使用vue.js

#### 传统前端开发模式
`jQuery + RequierJS(SeaJS) + artTemplate(doT) + Gulp(Grunt)`


- 优点：简单，高效，实用。
- 缺陷：难以应付复杂的也业务场景（spa-单页面富应用），组件解耦，开发效率低，维护成本高。
#### Vue.js开发模式
。。。

开发几个简单的页面可以直接通过`script`加载`CND`文件.
```html
<script src="https://cdn.bootcss.com/vue/2.5.13/vue.common.js"></script>
```