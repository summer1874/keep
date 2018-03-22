
### ES6引入的一种新的原始数据类型（`Symbol`）。前六种 `undefined`，`null`，`Number`，`String`，`Boolean`，`Object`

### 主要作为属性名
- 唯一性
```js
//防止key值冲突覆盖
const name = Symbol.for('name')
let obj = {
  name: 'map',
  [name]: 'set',
};
```
#### 语法
>Symbol([description])

**`description`** *可选*

可选的，字符串。`symbol`的`description`可以用于调试，但无法访问到`symbol`本身。

#### 声明
```js
const s = Symbol();
const s1 = Symbol('name');
//name只作为描述。
typeof s
//Symbol
```
#### Symbol不能使用new来实例化，它不是一个完整的构造函数。
```js
const s = new Symbol();
//Symbol is not a constructor

```
#### 唯一性
```js
const s1 = Symbol();
const s2 = Symbol();
s1 === s2;//false

//当作为函数调用时会返回一个symbol值,symbol值是独一无二的。
```
#### Symbol与类型强制转换
Symbol不支持类型转换
```js
//Number转换成字符串
let num = 1;
console.log(typeof num)//number
console.log(num + 'string');//'1string'
//Symbol转换成字符串
let sb = Symbol();
console.log(typeof sb);//
console.log(sb + 'string');//Cannot convert a Symbol value to a string
```
#### 全局共享的 Symbol
>上面使用`Symbol()` 函数的语法，不会在你的整个代码库中创建一个可用的全局symbol类型。 要创建跨文件可用的symbol，甚至跨域（每个都有它自己的全局作用域） , 使用 `Symbol.for()` 方法和  `Symbol.keyFor()` 方法从全局的symbol注册表设置和取得symbol。

#### Symbol.for(key)
##### 语法
>Symbol.for(key)

**参数**

**`key`**

一个字符串，作为 `symbol` 注册表中与某 `symbol` 关联的键（同时也会作为该 `symbol` 的描述）。

**`返回值`**

返回由给定的 `key` 找到的 `symbol`，否则就是返回新创建的 `symbol`。

##### 示例
```js
Symbol.for("foo"); // 创建一个 symbol 并放入 symbol 注册表中，键为 "foo"
Symbol.for("foo"); // 从 symbol 注册表中读取键为"foo"的 symbol

Symbol.for("bar") === Symbol.for("bar"); // true，证明了上面说的
Symbol("bar") === Symbol("bar"); // false，Symbol() 函数每次都会返回新的一个 symbol


var sym = Symbol.for("mario");
sym.toString();
// "Symbol(mario)"，mario 既是该 symbol 在 symbol 注册表中的键名，又是该 symbol 自身的描述字符串
```
为了防止冲突，最好给你要放入 symbol 注册表中的 symbol 带上键前缀。
```js
Symbol.for("mdn.foo");
Symbol.for("mdn.bar");
```
#### Symbol.keyFor(sym)

##### 概述
Symbol.keyFor(sym) 方法用来获取 symbol 注册表中与某个 symbol 关联的键。

##### 语法
>Symbol.keyFor(sym);
**参数**

**`sym`**

存储在 symbol 注册表中的某个 symbol
##### 示例
```js
// 创建一个 symbol 并放入 Symbol 注册表，key 为 "foo"
var globalSym = Symbol.for("foo");
Symbol.keyFor(globalSym); // "foo"

// 创建一个 symbol，但不放入 symbol 注册表中
var localSym = Symbol();
Symbol.keyFor(localSym); // undefined，所以是找不到 key 的

//symbol 并不在 symbol 注册表中
Symbol.keyFor(Symbol.iterator) // undefined
```

#### 实例
```js
let name = Symbol.for('name');
let obj = {
  [name]: 'hero',
  sex: 'man',
  age: 28,
};

//Symbols 在 for...of,for...in迭代中 不可枚举
for(let [key,value] of Object.entries(obj)){
  console.log(key,value);

}
for(let key in obj){
  console.log(key,obj[key]);
}
//sex man
//age 28

//返回在给定对象自身上找到的所有 Symbol 属性的数组。
Object.getOwnPropertySymbols(obj).forEach(function(item){
  console.log(obj[item]);//hero
})
//返回由目标对象的自身属性键组成的Array。
Reflect.ownKeys(obj).forEach(function(item){
  console.log('ownkeys',item,obj[item]);
  //ownkeys sex man
  //ownkeys age 28
  //ownkeys Symbol(name) hero
})
```
