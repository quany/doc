### 防抖
在事件被触发n秒后，再去执行回调函数。如果n秒内该事件被重新触发，则重新计时，结果就是将频繁触发的事件合并为一次，且在最后执行；

``
function ajax(data) {
    console.log(new Date().toLocaleTimeString() + '-'+data);
}
``


## 