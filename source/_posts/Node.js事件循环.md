---
title: Node.js事件循环
categories: Node.js
tags: Node.js
---

> <https://juejin.cn/post/6844903999506923528>

基于 libuv 实现

分为6个阶段

1. timers阶段
   这个阶段执行timer（setInterval、setTimeout）的回调函数
2. I/O callbacks（I/O事件回调阶段）
   执行延迟到下一个循环迭代的I/O回调，即上一轮循环中未被执行的一些I/O回调
3. idle，prepare（闲置阶段）
   仅node内部使用
4. poll
   获取新的I/O事件，例如操作读取文件等
5. check
   执行 setImmediate 的回调

   如果 setTimeout(callback, 0) 和 setImmediate(callback) 都在主模块中调用，执行顺序随机，取决于机器性能
   如果 都不在主模块中调用，则 setImmediate的回调 永远先执行
6. close callback
   比如 socket.on('close', callback) 的callback会在这个阶段执行
