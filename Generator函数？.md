# 什么是Generator函数？

### 1.   Generator是为了解决什么问题？

Q：Generator函数是ES6提供的一种异步变成解决方案，解决了以往的回调套回调的噩梦，包括promise也一样。

```javascript
function* generatorTexr() {
    const result = yield ajax('locahost:8000/test')
    const res = JSON.pase(result).value
    console.log(res)
}
function ajax(url) {
    asyncAjax(url, (res) => {
        f.next(res)
    })
}
const f = generatorText();
f.next()
```

### 2. Generator函数概念

通常在函数后面加一个'*', 返回结果是一个指针对象，具有next方法，用来遍历对象。

#### 2.1. async/await本质是什么？

本质是内置了执行器的Generator函数。

#### 2.2. 如何通过Generator函数实现async函数

对比：Generator函数与async函数

```javascript
let g = function* (){
    let ret = yield asyncSum(1, 2) // 1阶段
    return ret
}

let g = async function() {
    let ret = await asyncSum(1, 2) // 1阶段
    return ret
}
```

两者都是在1阶段的时候暂停执行等待ret结果出来后再继续执行。

不同点在于yield函数之后后半部分之后，需要再次调用next(),并将值作为参数传进next,

async函数其实就是内置了一个执行器的Generator函数，执行器就是用来自动执行Generator函数。