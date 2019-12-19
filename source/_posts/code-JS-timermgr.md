---
title: '[Code-JS] 定时器管理器'
date: 2019-12-19 16:15:02
tags:
    - JavaScript
categories:
    - [Code, JavaScript]
---

# 为什么需要一个定时器管理器？

保留大量定时器的引用，会干扰浏览器的运行。增加浏览器的垃圾回收任务发生的可能性(垃圾回收就是浏览器遍历其分配过的内存，并试图删除没有任何应用的未使用对象的过程)。有些浏览器页面上的动画可能出现卡顿。
<!--more-->

# 使用定时器管理器的好处

- 每个页面(整个项目)在同一时间只需要运行一个定时器
- 可以根据需要暂停/恢复定时器

# 实现

把要执行所有的方法都添加到一个列表里面，由一个定时器去驱动。

```typescript
/*
 * @classdesc 定时器管理器
 */
class TimerMgr {
    /**
     * 时间间隔(毫秒)
     */
    private _timeStep: number = 0;

    /**
     * 是否运行
     */
    private _isRunning: boolean = false;

    /**
     * 是否暂停
     */
    private _isPaused: boolean = false;

    /**
     * 定时器id
     */
    private _timer: number = null;

    /**
     * 执行方法列表
     */
    private _funcList: Function[] = [];

    /**
     * 
     * @param timeStep 时间间隔(默认为0)
     */
    constructor (timeStep: number = 0) {
        this._timeStep = timeStep;
    }

    /**
     * 添加
     * @param 执行方法
     */
    add = (func: Function) => {
        this._funcList.push(func);

        if (this._isRunning || this._isPaused) return;

        this.run();
    }

    /**
     * 开始
     */
    start = () => {
        this._isPaused = false;
    }

    /**
     * 运行
     */
    run = () => {
        this._timer && clearTimeout(this._timer);
        this._timer = null;

        if (this._isPaused) return;

        // 判断是否存在执行的方法列表
        if (!this._funcList.length) {
            this._isRunning = false;
            return;
        }

        this._isRunning = true;

        // 遍历方法列表执行添加的方法
        for (let i = 0; i < this._funcList.length; i++) {
            let func:Function = this._funcList[i];

            // 如果有返回值为false则删除
            if (func() === false) {
                this._funcList.splice(i, 1);
                i--;
            }

            func = null;
        }

        this._timer = setTimeout(this.run, this._timeStep);
    }

    /**
     * 暂停
     */
    stop = () => {
        this._isPaused = true;
    }

    /**
     * 清除
     */
    clear = () => {
        this._timer && clearTimeout(this._timer);

        this._timer = null;
        this._funcList = [];
    }
}

// 测试
export const timerMgr = new TimerMgr();

let count = 1;
// console.log() 1-10
timerMgr.add(() => {
    if (count > 10) {
        return false;
    }

    console.log(`count:: ${count}`);
    count++
});

// 一直执行
timerMgr.add(() => {
    console.log('loop');
});
```

