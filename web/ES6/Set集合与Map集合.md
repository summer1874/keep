### new Set()
语法
> new Set([iterable]);

iterable

如果传递一个可迭代对象，它的所有元素将被添加到新的 Set中。如果不指定此参数或其值为null，则新的 Set为空。

返回值
一个新的Set对象

#### Set中的元素只会出现一次，即 Set 中的元素是唯一的。
```js
let mySet = new Set([1,2,3,1]);
console.log(mySet);
//Set(3) {1, 2, 3}
```
#### Set实例
##### `Set.prototype.size`
返回Set对象的值的个数。
```js
const mySet = new Set([1,2,3]);
console.log(mySet.size)//3
```
##### `Set.prototype.add(value)`
在Set对象尾部添加一个元素。返回该Set对象。
```js
const mySet = new Set([1,2,3]);
mySet.add(4);
console.log(mySet);//Set(4) {1, 2, 3, 4}
```
##### `Set.prototype.has(value)`
返回一个布尔值，表示该值在Set中存在与否。
```js
const mySet = new Set([1,2,3]);
console.log(mySet.has(1));//true
console.log(mySet.has(4));//false
```
##### `Set.prototype.delete(value)`
移除Set的中与这个值相等的元素,存在该元素返回`true`，否则返回`false`
```js
const mySet = new Set([1,2,3]);
mySet.delete(1);
console.log(mySet);//Set(2) {2, 3}
console.log(mySet.delete(1));//false
```
#####  `Set.prototype.clear()`
移除Set对象内的所有元素。
```js
const mySet = new Set([1,2,3]);
mySet.clear();
console.log(mySet);//Set(0) {}
```

##### `Set.prototype.entries()`
返回一个新的迭代器对象，该对象包含`Set`对象中的按插入顺序排列的所有元素的值的`[value, value]`数组。为了使这个方法和`Map`对象保持相似， 每个值的键和值相等。
```js
const mySet = new Set([1,2,3]);
const setIter = mySet.entries();

console.log(setIter.next().value); // [1, 1]
console.log(setIter.next().value); // [2, 2]
console.log(setIter.next().value); // [3, 3]
```
##### `Set.prototype.forEach(callbackFn[, thisArg])`
按照插入顺序，为`Set`对象中的每一个值调用一次`callBackFn`。如果提供了`thisArg`参数，回调中的`this`会是这个参数。
```js
var mySet = new Set(['one','tow','three']);

mySet.forEach((value1,value2,set) => { //箭头函数thisarg会被忽略
  console.log(value1,value2,set)
  //one one Set(3) {"one", "tow", "three"}
  //tow tow Set(3) {"one", "tow", "three"}
  //three three Set(3) {"one", "tow", "three"}

  //Set对象中没有索引值，前2个参数都是包含在Set中的元素的值
});
```
*`values(),keys()`*

#### 迭代Set
```js
const arr = ['clear','has','add','delete'];
const setIter = new Set(arr);

//for in迭代的是对象的key，而在Set中的元素没有key
for(let key in setIter){
  console.log(key)// //不存在
}

for(let key of setIter){
  console.log(key);
  //clear
  //has
  //add
  //delete
};

for(let key of setIter.keys()){//values()
  console.log(key);
  //clear
  //has
  //add
  //delete
}

for(let [key,value] of setIter.entries()){
  console.log(key,value);
  //clear clear
  //has has
  //add add
  //delete delete
}
```
#### new WeakSet();
>Set集合本身是强引用，只要new Set()实例化的引用存在，就不释放内存，这样一刀切肯定不好啊，比如你定义了一个DOM元素的Set集合，然后在某个js中引用了该实例，但是当页面关闭或者跳转时，你希望该引用应立即释放内存，Set不听话，那好，你还可以使用 Weak Set

**语法：**
>new WeakSet([iterable]);

##### 和Set的区别：

1.  WeakSet 对象中只能存放对象值, 不能存放原始值, 而 Set 对象都可以.

2.  WeakSet 对象中存储的对象值都是被弱引用的, 如果没有其他的变量或属性引用这个对象值, 则这个对象值会被当成垃圾回收掉. 正因为这样, WeakSet 对象是无法被枚举的, 没有办法拿到它包含的所有元素.

##### 使用：
```js
//[clear,has,delete,add]
let set = new WeakSet();
const class_1 = {}, class_2 = {};
set.add(class_1);
set.add(class_2);
console.log(set) // WeakSet {Object {}, Object {}}
console.log(set.has(class_1)) // true
console.log(set.has(class_2)) // true
set.add('string');//抛出错误 TypeError: Invalid value used in weak set
```

#### new Map();
##### 键的相等
基于 `"SameValueZero"` 算法：`NaN` 是与 `NaN` 相同的(虽然 `NaN !== NaN`)。

##### 相对于Object，Map的优点
- 一个对象通常都有自己的原型,所以一个对象总有一个"prototype"键。不过，从 ES5 开始可以使用 map = Object.create(null)来创建一个没有原型的对象。
- 一个对象的键只能是字符串或者 Symbols，但一个 Map 的键可以是任意值。
- 你可以通过size属性很容易地得到一个Map的键值对个数，而对象的键值对个数只能手动确认。

##### 方法
*相对与`new Set()`,Map多了`set(),get()`方法*


`Map.set()`
设置Map对象中键的值。返回该Map对象。
```js
const map = new Map();
map.set(NaN,'NaN--键相等');
console.log(map);
```
`Map.get()`
返回键对应的值，如果不存在，则返回undefined。
```js
const element = document.querySelectorAll('#el');
const map = new Map();
map.set(element,'div');
map.get(element);
```
`Map.[clear(),delete(),has()]`



#### 实例
```js
//使用映射对象
const keyObj = {};
const keyFun = function () {};
const keystr = 'string';

let map = new Map();
map.set(keyObj,'object');
map.set(keyFun,'function');
map.set(keystr,'a string');

map.get(keyObj);//object
map.get({});//undefined
//keyObj !== {}

map.get(keyFun);//function () {}
map.get(function () {});//undefined
//keyFun !=== function () {}

map.get(keystr);//string
map.get('string');//a string
//keystr === a string

map.has('string')//true
map.delete(keyObj);//true  Map(2) {ƒ => "function", "string" => "a string"}
map.clear();//Map(0) {}

//forEach 迭代
const map = new Map();
map.set('one',1);
map.set('tow',2)
map.forEach((val,key)=>{
  console.log(key,val);
  //one 1
  //tow 2
});

//for...of
const objToStrMap = obj =>{//对象转Map
  let strMap = new Map();
  for (let k of Object.keys(obj)){
    strMap.set(k, obj[k]);
  }
  return strMap;
}
const map = objToStrMap({
  obj:{},
  fun:function(){},
  str:'string',
  num:1,
});


for(let key of map.keys()){
  console.log(key);
}
for(let val of map.values()){
  console.log(val);
}
for(let [key,val] of map.entries()){
  console.log(key,val)
}
```

#### new weakMap()
和Set要解决的问题一样，希望不再引用Map的时候自动触发垃圾回收机制。那么，你就需要Weak Map。(WeakMap 的 key 只能是 Object 类型。 原始数据类型 是不能作为 key 的)
- DOM 节点作为键名
- 部署私有属性。
```js
let map = new WeakMap();
const key = document.querySelector('.header');
map.set(key, 'element');

map.get(key) // "element"
```

### 转换
#### Map 转为数组
```js
const myMap = new Map()
  .set(true, 7)
  .set({foo: 3}, ['abc']);
  [...myMap]//使用扩展运算符（...）
```
#### 数组 转为 Map
```js
new Map([
  [true, 7],
  [{foo: 3}, ['abc']]
])
```
#### Map 转为对象
```js
function strMapToObj(strMap) {
  let obj = Object.create(null);//创建一个没有原型的对象
  for (let [k,v] of strMap) {
    obj[k] = v;
  }
  return obj;
}
```

#### 对象转为 Map
```js
function objToStrMap(obj) {
  let strMap = new Map();
  for (let k of Object.keys(obj)) {
    strMap.set(k, obj[k]);
  }
  return strMap;
}
```
[更多详情请查阅](http://es6.ruanyifeng.com/#docs/set-map#Set);
