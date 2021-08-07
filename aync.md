# 异步函数规范

# 错误返回方式

js 不能像某些语言一样返回多个函数，但是可以返回数组
借助于对象析构，完成函数多个数据返回功能

```javascript
import { readfileAsync } from "fs";
function loadconfig() {
    try {
        let config = readfileAsync("./config");
        return [config, null];
    } catch (err) {
        return [null, err];
    }
}

let [data, err] = loadconfig();

// 如果错误不重要可以丢弃
let [data] = loadconfig();

// Promise 一样可以用类似方法
let [data, err] = await loadconfig();
```

# 同步函数转异步函数

部分包库会默认采用 await，但是这类库兼容性相对差些
借助 webpack 可以完全兼容 ES5

如果函数是同步函数，尽量用 promise 处理保证成 异步函数（Promise 函数）

```javascript
// 以sleep函数为参考
function sleep(time) {
    return new Promise((reslove) => {
        setTimeout(reslove, time);
    });
}

async dosomthing(){
    await dosth1()
    // 程序等待3秒后执行下一步
    await sleep(3000)
    await dosth2()
}


```
