---
title: '[code-NodeJS] nodejs导出excel表数据'
date: 2020-01-08 18:16:38
tags:
    - NodeJS
    - TypeScript
categories:
    - [Code, NodeJS]
---

# 实现思路

- 配置基本配置
  - excel路径
  - 导出文件路径
  - 导出文件格式
  - 公式导出
- 读取excel表数据<!--more-->
  - 深层文件夹读取
- 处理excel表数据
  - 处理一张excel包含多张sheet
  - 定义导出数据格式
- 写入数据到文件
  - 导出普通字段
  - 导出公式ts文件



# 实现

## 项目初始化

- 安装node

- 安装npm包

  ```
  yarn：       [npm i yarn -g] 可以选择安装, 安装后可用"yarn add", 不安装用"npm i"
  typescript： [yarn add typescript --dev] 支持typescript
  xlsx：       [yarn add xlsx --dev] 读取excel表数据
  jsonfile：   [yarn add jsonfile --dev] 读取json数据
  ts-node：    [yarn add ts-node --dev] 代码提示
  ts-node-dev：[yarn add ts-node-dev --dev]
  nodemon：    [yarn add nodemon --dev] 监视启动目录中的文件，如果有文件更改，自动重启node应用
  codenotices：[yarn add @types/node @types/jsonfile @types/xlsx] 代码提示
  ```

- 初始化tsconfig

  ```
  项目根目录下执行: tsc -init
  ```

- 修改tsconfig配置(可参考官方文档https://www.tslang.cn/docs/handbook/compiler-options.html)

  ```
  "target": "es5", // 指定ECMAScript目标版本
  "module": "commonjs", // 指定生成哪个模块系统代码
  "sourceMap": true, // 生成相应的 .map文件
  "outDir": "./dist", // 重定向输出目录
  "rootDir": "./src", // 控制输出的目录结构
  "strict": true, // 启用所有严格类型检查选项
  "moduleResolution": "node", // 决定如何处理模块
  "esModuleInterop": true,    // 允许从没有设置默认导出的模块中默认导入
  "forceConsistentCasingInFileNames": true, 禁止对同一个文件的不一致的引用
  ```

  

- 设置脚本命令(执行：yarn | npm run 脚本命令)

  ```
  "scripts": {
      "start": "node dist/main.js", // 执行main.js
      "dev": "nodemon src/main.ts", // 监听并执行main.ts
      "build": "tsc -p ."           // 构建ts为js
  },
  ```

## 项目实现源码

https://github.com/guitarhgr/xlsx_2_json

src/types.ts：定义类型文件

src/main.ts：主程序文件



## 创建启动入口批处理程序

创建一个start.bat(右键创建一个文件将后缀名改为xxxx.bat)批处理程序：

```
@echo off
start cmd /k "yarn start"
```

这样就不用每次启动cmd输入启动脚本导出，每次就直接执行这个批处理程序start.bat.



## 用法

参考https://github.com/guitarhgr/xlsx_2_json/blob/master/README.md 