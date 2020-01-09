---
title: '[Code-JS] 函数重载'
date: 2019-12-16 10:49:48
tags:
    - JavaScript
    - TypeScript
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

​	函数包装是一种封装函数逻辑的技巧，用于在单个步骤内重载创建新函数或继承函数。最有价值的场景是，在重载一些已经存在的函数时，同时保持原始函数在被包装后依然能够有效使用。

​	例如Prototype's的readAttribute()方法：

```typescript
/**
 * 包装函数
 * @param obj 包装对象
 * @param fnName 方法名
 * @param fn 方法
 */
const wrap = (obj: Object, fnName: string, fn: Function) => {
    const originFn: Function = obj[fnName];

    return obj[fnName] = function () {
        return fn.apply(
            this,
            [originFn.bind(this)].concat(
                Array.prototype.slice.call(arguments)
            )
        )
    }
};

const obj = {
    readAttribute: (a: number, b?: number) => {
        console.log(`${a}::${b}`);
    }
};

wrap(obj, 'readAttribute', (originFn: Function, a: number, b: number) => {
    !b ? console.log(`wrapped ${a}::${b} `) :
         originFn(a, b);
    
});

obj.readAttribute(1);
```

该函数实现了对一个已经存在函数的重写，取而代之的是一个新函数。但这个新函数仍然可以访问原有函数提供的方法。这意味着，一个函数可以很安全的被重载，并同时仍然保留原有的功能。



# 提示

------

该文章是学习《JavaScript Ninja》的笔记，仅供自己学习使用，如有侵权请联系删除[1758575969@qq.com]。

------