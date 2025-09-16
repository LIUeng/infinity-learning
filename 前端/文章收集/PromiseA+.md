# 注意

你不知道的 Promise 有多少

## 状态机

- pending 等待
- fulfilled 完成
- rejected 失败

## 参数

> 接受一个函数

- 执行多次 resolve 函数，只会接收第一个 resolve 执行之后的状态
- 同时执行 resolve 和 reject，按照顺序接收状态（resolve 先执行，就不接收 reject 执行的状态）
- reject 或者抛出异常不会阻断状态（原型）链函数的执行

```javascript
// 1
new Promise((resolve, reject) => {
  resolve(1); // 有效
  resolve(2); // 无效
  resolve(3); // 无效
  // ...
});

// 2
new Promise((resolve, reject) => {
  reject('error'); // 有效
  resolve(1) // 无效
});

// 3
new Promise((resolve, reject) => {
  reject('error');
})
  .then(() => { /* 不执行 */ }, () => { /* 执行 */ })
  .then(() => { /* 继续执行 */ });
```

## 实例方法

- 未被 resolve 或者 reject 的状态不会被实例方法接收，且不会执行

```javascript
// 1
new Promise((resolve, reject) => {
  // do nothing
})
  .then(() => { /* 不执行 */ })
  .catch(() => { /* 不执行 */ })
  .finally(() => { /* 不执行 */ });
```

### then

> 接收两个参数 Null | Function，返回 Promise 实例对象

```javascript
Promise.prototype.then = function(onFulfilled, onRejected) {
  // 代码实现...
  return new Promise(() => {});
}
```

- 下一个 then 的状态取决于上一个 resolve 或者 return 返回的状态
- reject 或者抛出异常的状态会被下一个 then 的第二个函数参数接收
- then 函数中抛出的异常同样会被 catch 或者下一个 then 函数的第二个参数接收

```javascript
// 1
new Promise((resolve, reject) => {
  resolve(1);
}).then(v => {
  // 1
  return v;
}).then(v => {
  // v = 1
  console.log('v =', v);
});

// 2
new Promise((resolve, reject) => {
  // 1
  reject('error');
  // 2
  throw new Error('error');
}).then(function onFulfilled(res) { /* 不执行 */ }, function onRejected(err) {
  // err = error
  console.log('err =', err);
});

// 3
new Promise((resolve, reject) => {
  resolve(1);
}).then(() => {
  throw new Error('error');
}).then(() => {}, () => {
  // 接收抛出的异常状态
});
```

### catch

> 接受一个函数参数

```javascript
Promise.prototype.catch = function(onRejected) {
  return this.then(null, onRejected);
}
```

- 接收被 reject 之后或者抛出异常的状态
- 如果错误状态被下一个 then 的第二个函数参数接收，则 catch 不会重复执行

```javascript
// 1
new Promise((resolve, reject) => {
  // 1
  reject('error');
  // 2
  throw new Error('error');
}).catch(err => {
  // err = error
  console.log('err =', err);
});

// 2
new Promise((resolve, reject) => {
  reject('error');
}).then(() => {}, err => {
  // err = error
  console.log('err =', err);
}).catch(() => { /* 不执行 */ });
```


### finally

> 接受一个函数参数

```javascript
Promise.prototype.finally = function(fn) {
  return this.then(v => {
    return Promise.resolve(fn()).then(() => {
	  return v;
    });
  }, err => {
    return Promise.resolve(fn()).then(() => {
      throw err;
    });
  });
}
```

- finally 函数不会隔断状态（原型）链的执行

```javascript
new Promise((resolve, reject) => {
  resolve(1);
}).finally(() => {
  console.log('finally');
}).then(v => {
  // 输出 v = 1
  console.log('v =', v);
});
```

## 静态方法

### resolve

- 传什么参数就返回什么参数
- 传入的参数是函数以及对象例外，如果存在 then 属性且是函数，会被作为 Promise 的函数参数

```javascript
// 简单实现
Promise.resolve = function(value) {
  return new Promise(resolve => {
    resolve(value);
  });
}

// 特殊情况 参数为一个对象或者函数 object | function
let fn = () => {};
fn.then = () => {};
Promise.resolve(fn)
Promise.resolve({ then: fn });
```

### reject

```javascript
Promise.reject = function(err) {
  return new Promise((resolve, reject) => {
    reject(err);
  })
}
```

### all

- 返回所有的 resolve 状态
- 遇到  reject 状态停止执行

```typescript
type AllTypes = Array<null|undefined|Promise|numbers|string|object>
```

### race

- 返回第一个完成的 resolve/reject 状态

### allSettled

- 所有 resolve/reject 状态被返回

```json
[
  { status: 'fulfilled', value: '' },
  { status: 'rejected', reason: '' }
]
```

### any

- 任何一个 resolve 的状态返回
- 存在全部 reject 的状态则提示所有状态被 rejected（AggregateError）