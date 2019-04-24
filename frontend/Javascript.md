### 防抖
在事件被触发n秒后，再去执行回调函数。如果n秒内该事件被重新触发，则重新计时，结果就是将频繁触发的事件合并为一次，且在最后执行；

```js
function ajax(data) {
    console.log(new Date().toLocaleTimeString() + '-'+data);
}
```


### 发布订阅模式
```js
let Emitter = function () {
    this._listeners = {};
}
// 监听事件
Emitter.prototype.on = function (eventName, callback) {
    let listeners = this._listeners[eventName] || [];
    listeners.push(callback);
    this._listeners[eventName] = listeners;
}
// 触发事件
Emitter.prototype.emit = function (eventName) {
    let args = Array.prototype.slice.apply(arguments).slice(1);
    let listeners = this._listeners[eventName];
    if(!Array.isArray(listeners)) return;
    let self = this;
    listeners.forEach(function (cb) {
        try {
            cb.apply(self, args);
        } catch (e) {
            console.error(e);
        }
    })
}
// 移除监听事件
Emitter.prototype.removeListener = function (eventName) {
    delete this._listeners[eventName];
}
```