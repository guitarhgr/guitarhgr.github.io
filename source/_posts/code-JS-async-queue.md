---
title: '[Code-JS] 异步队列'
date: 2020-01-09 20:59:27
tags:
    - JavaScript
    - TypeScript
categories:
    - [Code, JavaScript]

---

# 应用场景

当需要将方法以异步的方式进行执行，但同时又需要保证执行的顺序。例如：

- 弹出一系列提示消息(自动控制)
- 多个弹窗，一个弹窗关闭后，再弹出下一个弹窗(手动控制)



# 思路

- 将需要执行的方法放在同一个队列当中
- 上一个方法执行时暂停队列
- 上一个方法执行完后，再自动/手动去调用下一个执行方法。



# 实现

```typescript
export class AsyncQueue {
    private _queue: Function = [];
}
```

