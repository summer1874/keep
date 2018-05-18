## v-bind及class与style绑定
v-bind指令用来绑定class和style的多种方法。
### 了解v-bind指令
```html
<img :src="imgUrl">

<script>
    ...
    data:{
        imgUrl:'portrait.jpg'
    }
    ...
</script>
```
`imgUrl`会动态渲染到`img src` 中。当数据变化时，`src`就会重新绘制。
### 绑定class的几种方式
#### 对象语法
```html
<div class="top-bar" :class="{'active':isActive,'error':isError}"></div>
<!--渲染结果-->
<div class="top-bar active"></div>


<script>
    ...
    data:{
        isActive:true,
        isError:false,
    }
    ...
</script>
```
- **根据依赖的数据来判断是否在`<div>`中加入class。**
- **`:class`是可以与普通class共存，`activ eerror`,会根据依赖的数据是否添加到class。**

```html
<div :class="classses"></div>
<!--渲染结果-->
<div class="active">

<script>
    computed:{
        classes:function(){
            return {
                active: this.isActive && ! this.error,
                'text-fail':this.error && this.error.type == 'fail'
            }
        }
    }
</script>
```
当表达式过长或逻辑复杂时，可以使用计算属性`(computed)`来进行逻辑处理。一般用于条件多余两个时。

#### 数组语法
用于绑定多个class,给`:class`绑定一个数组，应用一个`class`列表。
```html
<!--基本使用-->
<div :class="[activeCls,errorCls]"></div>

<!--使用三运表达式-->
<div :class="[isActive? activeCls :'',errorCls ]"></div>

<!--数组语法中使用对象语法-->
<div :class="[{'active':isActive},errorCls]"></div>

<!--逻辑复杂时，可使用 data，computed ,methods这三种方法-->
<div :class="classes"></div>

<!--渲染后
<div class="active error"></div>
<div class="active error"></div>
<div class="active error"></div>
<div class="top-bar top-bar-large"></div>
-->
<script>
    ...
    data:{
        activeCls:'active',
        errorCls:'error',
        isActive:true,
        size:'large',
        disabled:false,
    },
    computed:{
        classes:function(){
            return [
                'top-bar',
                {
                    ['top-bar-' + this.size]:this.size !== '',
                    ['btn-disabled']:this.disabled
                }//ES6扩展对象的功能性-属性名可计算
            ]
        }
    }
    ...
</script>
```
#### 在组件上使用
### 绑定内联样式
```html
<!--基本用法-->
<div :style="{'color':color,'fontSize':font-size+'px'}">

<!--为了方便阅读和维护一般使用 data ,computed这两种方法-->
<div :style="styeles">

<script>
    data:{
        styles:{
            color:'red'，
            fontSize:14 + 'px'
        }
    }
</script>
```
