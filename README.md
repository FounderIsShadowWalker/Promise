# Promise
    Promise 是ES6的一个新的方法，做异步控制的。
## 异步控制的种类
   * Async
   * yield
   * waterfall(Node)
   * Promise

>引用 https://github.com/panyifei 的Promise。

### Promise的 API
 1.  then(success, reject)

`new Promise(function(resolve, reject){
 		setTimeout(resolve, 1000);
}).then(function(){}, function(){})`

***
#### 实现的思路
1. promise 首先起延时的作用，then方法相当于callback，同时要保证在同步的情况下一样可以先采集回调后在执行，我们需要在resolve方法里强制延时0秒,因为Promise方法首先是调用传进来的方法，同时注入resolve。
2. promise 的三个状态，pending, fulfiled, rejected, pending 表示目前还没有resolve，可以一直加then。fulfiled 表示已经被resolve了，加的方法无法加入回调队列了，只能立即执行了，rejected表示调用失败回调队列了。
3. resoleve 收入了一个promise，直接把没有执行完成的回调队列放在新的后面。
4. reject 同 resolve。
5. 关于失败回调队列，也就是reject方法，这个方法的实现仁者见仁了，有的直接throw Error 比如es6 就是这样。这里很欣赏作者的意图，把可以简单完成的事情弄的十分有趣。可以把 then 里的success 和 fail看做双车道，resolve 表示我是在 A 车道上, 一直成功 则一直在 A 车道上，一道reject了，执行 B 车道上的 fail，执行完，再返回 A 车道上。
6. 至于值的传递很好实现了，每次回调函数执行的结果，就是下一个回调函数执行的参数(记得写return 哦 @ ^ @!);

***
##### 我是爱读源码的顺顺
![Image](https://github.com/FounderIsShadowWalker/Promise/blob/master/founder.jpg)





