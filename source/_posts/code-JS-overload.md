---
title: '[Code-JS] 函数重载'
date: 2019-12-16 10:49:48
tags:
    - JavaScript
categories:
    - [Code, JavaScript]
---

# 什么是函数的重载？

具有相同的名称，不同参数列表的函数
<!--more-->

# 重载函数的方法

## 实现方式

- 检查参数列表使用switch或者if-else来执行不同的行为，但这个方法，如果重载过多代码就会冗余笨拙(这里不做介绍)。

- 利用闭包和函数的length属性。

  ```
  闭包：MSDN的解释，函数与对其状态即词法环境（lexical environment）的引用共同构成闭包（closure）。也就是说，闭包可以让你从内部函数访问外部函数作用域。在JavaScript，函数在每次创建时生成闭包。
  函数的length属性：这个属性是函数声明时所需要传入的形参数量。而arguments.length是函数在调用时传入的参数数量。
  ```

## 利用闭包和函数length进行函数重载

### 方法实现

```typescript
/**
 * 添加重载函数：该方法每一层都会检查参数个数是否匹配。如果不匹配就继续检查上一层创建的函数
 * @param obj 绑定方法的对象
 * @param name 方法名
 * @param fn 方法
 */
const addOverloadFn = (obj: Object, name: string, fn: Function) => {
    // 保存一下之前的方法
    const oldFn = obj[name];

    // 创建一个新匿名函数作为新方法
    obj[name] = function () {
        // 判断该匿名函数的传入实际参数个数和声明的形参个数
        if (fn.length == arguments.length) {
            return fn.apply(this, arguments);
        }
        else if (typeof oldFn == 'function') {
            return oldFn.apply(this, arguments);
        }
    }
}
```

### 方法测试

```typescript
// 无参
addOverloadFn(gays, 'find', function () {
    return this.vals;
});

// 一个参数
addOverloadFn(gays, 'find', function (firstName: string) {
    const result = [];

    for (let i = 0; i < this.vals.length; i++) {
        if (this.vals[i].indexOf(firstName) == 0) {
            result.push(this.vals[i]);
        }
    }

    return result;
});

// 两个参数
addOverloadFn(gays, 'find', function (firstName: string, lastName: string) {
    const result = [];

    for (let i = 0; i < this.vals.length; i++) {
        if (this.vals[i] === `${firstName} ${lastName}`) {
            result.push(this.vals[i]);
        }
    }

    return result;
});

console.log(gays.find()); // ["Li Hua", "Han MeiMei", "Li Lei"]
console.log(gays.find('Li')); // ["Li Hua", "Li Lei"]
console.log(gays.find('Han')); // ["Han MeiMei"]
console.log(gays.find('Li', 'Hua')); // ["Li Hua"]
```



# 重载已有函数

# 提示

------

该文章是学习《JavaScript Ninja》的笔记，仅供自己学习使用，如有侵权请联系删除[1758575969@qq.com]。

------