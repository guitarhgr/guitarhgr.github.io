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

- 存粹的异步测试
- 弹出一系列提示消息(自动控制)
- 多个弹窗，一个弹窗关闭后，再弹出下一个弹窗(手动控制)<!--more-->



# 思路

- 将需要执行的方法放在同一个队列当中
- 上一个方法执行时暂停队列
- 上一个方法执行完后，再自动/手动去调用下一个执行方法。



# 实现

```typescript
/**
 * @classdesc 异步队列
 */
export class AsyncQueue {
    /**
     * @prop 方法队列
     */
    private _queue: Function[] = [];
    
    /**
     * @prop 是否暂停
     */
    private _isPaused: boolean = false;

    /**
     * @prop 间隔时间
     */
    private _intervalTime: number = 1;

    /**
     * 是否自动开始
     */
    private _isAutoStart: boolean = true;

    /**
     * 是否自动继续
     */
    private _isAutoResume: boolean = true;

    /**
     * 定时器id
     */
    private _timer: number = null;

    /**
     * 
     * @param intervalTime 间隔时间(默认为1)
     * @param isAutoResume 是否自动继续(默认为true)
     * @param isAutoStart  是否自动开始(默认为true)
     */
    constructor (intervalTime: number = 1, isAutoResume: boolean = true, isAutoStart: boolean = true) {
        this._intervalTime = intervalTime;
        this._isAutoResume = isAutoResume;
        this._isAutoStart = isAutoStart;
    }

    /**
     * 添加
     * @param fn 方法
     */
    add = (fn: Function) => {
        this._queue.push(fn);
        
        this._isAutoStart && this.run();
    }

    /**
     * 运行
     */
    run = () => {
        if (this._isPaused || !this._queue.length) return;

        // 暂停
        this.stop();

        // FIFO
        this._queue.shift()();

        if (!this._isAutoResume) return;

        // 继续
        this.resume();
    }

    /**
     * 继续
     */
    resume = () => {
        this._timer && clearTimeout(this._timer);

        this._timer = setTimeout(() => {
            this._isPaused = false;
            this.run();
        }, this._intervalTime);
    }

    /**
     * 暂停
     */
    stop = () => {
        this._isPaused = true;
    }
}
```



# 使用

简单的测试使用

```typescript
const asyncQueue = new asyncQueue(1000);

asyncQueue(() => {
	console.log('test1');
});

asyncQueue(() => {
	console.log('test2');
});

asyncQueue(() => {
	console.log('test3');
});
```

# 提示

------

该文章是学习《JavaScript Ninja》的笔记，仅供自己学习使用，如有侵权请联系删除[1758575969@qq.com]。

------