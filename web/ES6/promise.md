### promise
解决异步回调地狱
a->b,事件触发，回调

es5
```js
let ajax = function(callback){
    console.log('进入')
    setTimeout(()=>{
        callback && callback()
    },1000)
}
ajax(()=>{
    console.log('回调成功！')
})
```
```js
function promise(a){
    return new Promise((resolve,reject)=>{
        if(a){
            resolve();
        }else{
            reject();
        }
    })
}
promise().then(()=>{console.log(1)})
```