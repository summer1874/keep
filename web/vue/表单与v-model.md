## 表单与v-model
### 基本用法
`v-model`用于在表单类元素上的双向绑定数据。*例如在输入框上使用时，输出的内容会实时的映映射到绑定数据上。*
```html
<input type="text" v-model="message" placeholder="输入...">
<p>{{message}}</p>
<script>
...
data:{
    message:'',
}
...
<script>
```
>使用`v-model`后，表单控件显示值只依赖所绑定的数据，不在关系初始化的value值，即`value="..."`和`<textarea>...</textare>`时不会生效的。

>使用中文输入法时`v-model`在没有定词选择之前，时不会触发更新的。有这个需求可以是用`@input`来替代`v-model`。
```html
<textarea @input="handleInput"></textarea>
<p>{{message}}</p>

<script>
methoes:{
    handleInput:{
        this.massage = e.target.value;
    }
}
<script>
```
**单选按钮**

- 单选按钮单独使用时，直接使用`v-bind`来绑定一个布尔值即可，`v-model`也可。

- 组合使用实现互斥选择效果，就需要`v-model`配合`value`来使用。

```html
<!-- 单独使用 -->
<input type="radio" :checked="picked" ></input>

<!-- 组合使用实现互斥选择效果 -->
<input type="radio" v-model="pickeds" value="html"></input>
<input type="radio" v-model="pickeds" value="css"></input>
<input type="radio" v-model="pickeds" value="js"></input>

<script>
...
data: {
    pickeds:'js',
    picked:true,
},
...
</script>
```
*数据中的`pickeds`的值与`value`值一致时，就会选中该项。选择其他时,`data`里的`pickeds`也会动态改变。*

**复选框**
- 单独使用时用直接用`v-model`绑定一个布尔值。
- 组合使用绑定到一个数组类型的数据，这一过程也是双向的，在勾选时`value`会自动`push`到这个数组，反之亦然。

```html
<!-- 单独使用 -->
<input type="checkbox" v-model="picked" ></input>

<!-- 组合使用实现多选效果 -->
<input type="checkbox" v-model="pickeds" value="html"></input>
<input type="checkbox" v-model="pickeds" value="css"></input>
<input type="checkbox" v-model="pickeds" value="js"></input>

<script>
...
data: {
    pickeds:['js'],
    picked:true,
},
...
</script>
```
**选择列表**
- `<option>`是备选项，如果含有`value`，`v-model`会优先匹配`value`的值；如果没有,就会直接匹配`<option>`的`text`。

- `<selected>`添加`multipe`可以实现多选，此时的`v-model`绑定的是一个数组，与复选框方法类似(会自动生成数组)。

- 实际业务`<option>`一般通过`v-for`动态输出,`value`,`text`通过`v-bind`动态输出。
```html
<select v-model="selected" multiple>
    <option value="js">js</option>
    <option>html</option>
    <option value="css">css</option>
</select>

<script>
...
 data: {
    selected: ['html'],
},
...
</script>
```
*`<select>`在不同的浏览器显示有差异，且不美观，建议用组件代替。*

### 绑定值
`v-model`和`v-bind`在实际业务中的应用。
-   单选按钮

    ```html
    <input type="radio" :v-model="picked" :value="value"></input>

    <script>
    //选中时，app.picked === app.value,值都是1;
    ...
    data: {
        value:1,
        picked:true,
    },
    ...
    </script>
    ```

-   复选按钮
    ```html

    <input type="checkbox" v-model="taggle" :true-value="value1" :false-value="value2"></input>
   

    <script>
    //勾选时,app.taggle === app.value1;未勾选时,app.taggle === app.value2;
    ...
    data: {
        taggle:false,
        value1:1,
        value2:2,
    },
    ...
    </script>
    ```
- 选择列表
    ```html
    <select v-model="selected">
        <option :value="{number:123}">123</option>
    </select>

    <script>
    //当选中时，app.selected时一个Object,所以app.selected.number === 123;
    ...
    data: {
        selected: '',
    },
    ...
    </script>
    ```
### 修饰符
-   .lazy
    -   失焦或回车时更新。`v-model.lazy=""`

-   .number
    -   将输入转换为`Number`类型(在你输入数字的时触发。先输入数字后，再输入string格式不会再更新到数据)。`v-model.Number=""`
-   .trim
    - 自动过滤首尾空格。`v-model.trim=""`

**`vue2.0x`后,`v-model`可以用于自定义组件。满足定制化需求**