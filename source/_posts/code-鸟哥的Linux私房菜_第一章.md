---
title: '[Code-鸟哥的Linux私房菜] 第一章-Linux是什么与如何学习'
date: 2021-02-20 20:31
tags:
    - 鸟哥的Linux私房菜
categories:
    - [Code, Linux, 鸟哥的Linux私房菜]
---

## 芝士就是力量
<!--more-->
```
1. 操作系统(Operation System)主要在管理与驱动硬件，因此必须要能够管理内存、管理装置、负责行程管理以及系统呼叫等等。因此，只要能够让硬件准备妥当的情况，就是一个简单的操作系统了。

2. Unix的前身是有贝儿实验室(Bell lab)的Ken Thompson利用汇编语言写成的，后来在1971-1973年间由Dennis Ritchie以C程序语言进行改写，才称为Unix。

3. 1977年由Bill Joy释出BSD(Berkeley Software Distribution), 这些称为Unix-like的操作系统。

4. 1984年由Andrew Tanenbaum开始制作Minix操作系统，该系统可以提供原始码以及软件。

5. 1984年由Richard Stallman提倡GNU计划，倡导自由软件(Free software)，强调其软件可以「自由的取得、复制、修改与再发行」，并规范出GPL授权模式，任何GPL(General Public License)软件均不可单纯仅贩卖其软件，也不可修改软件授权。

6. 1991年由芬兰人Linus Torvalds开发出Linux操作系统。简而言之，Linux成功的地方主要在于：Minix(Unix)，GNU, Internet, POSIX及虚拟团队的产生。

7. 复合Open source理念的授权相当多，比较知名的如：Apache/BSD/GPL/MIT等。

8. Linux本身就是个最简单的操作系统，其开发网站建立在http://www.kernel.org，我们亦称Linux操作系统最底层的数据为「核心(Kernel)」。

9. 从Linux kernel 3.0开始，已经舍弃奇数、偶数的核心版本规划，新的规划使用主线版本(MainLine)为依据，并提供长期支持版本(longterm)来加强某些功能的持续维护。

10. Linux distributions的组成含有：「Linux Kernel + Free Software + Documentations(Tools) + 可完全安装的程序」所制成的一套完整的系统。

11. 常见的Linux distributions分类有「商业、社群」分类法，或「RPM、DPKG」分类法.

12. 学习Linux最好从头由基础开始学习，找到一本适合自己的书籍，加强实做才能学会。
```



## Linx的应用

#### 企业环境

```
1. 网络服务器
2. 关键任务的应用(金融数据库、大型企业网络环境)
3. 学术机构的高效能运算任务
```

#### 个人环境

```
1. 桌面计算机
2. 手持系统(PDA、手机等)
3. 嵌入式系统
```

#### 云端应用

```
1. 云程序
2. 端设备
```



## Linux学习路线

```
1. 计算机概论与硬件相关知识
2. Linux的安装与指令
3. Linux操作系统的基础技能
4. vi文本编辑器
5. Shell与Shell Script的学习
6. 会软件管理员
7. 计算机网络基础
```



## 简答

1. 你在你的主机上面安装了一张网络卡，但是开机之后，系统却无法使用，你确定网络卡是好的，那么可能的问题出在哪里？该如何解决？

   ```
   因为所有的硬件都没有问题，所以问题可能出在系统的核心(kernel)不支持这张网络卡。
   解决的方法：
   	(1) 到网络卡的开发商网站；
   	(2) 下载支持你主机操作系统的驱动程序;
   	(3) 安装网卡驱动程序后，就可以使用了。
   ```



2. 一个操作系统至少要能够完整的控制整个硬件，请问，操作系统应该要控制硬件的那些单元？

   ```
   根据硬件的运作，以及数据在主机上面的运算情况与写入/读取情况，我们知道至少要能够控制：
   	(1) input/output control;
   	(2) device control;
   	(3) process management;
   	(4) file management等等！
   ```



3. 我在Windows上面玩的游戏，可不可以拿到Linux上去玩？

   ```
   当然不行！因为游戏也是一个应用程序(application)，他必须要使用到核心所提供的工具来开发他的游戏，所以这个游戏是不可在不同的平台间运作的。除非这个游戏已经进行了移植。
   ```

   

4. Linux本身仅是一个核心与相关的核心工具而已，不过，他已经可以驱动所有的硬件，所以，可以算是一个很简单的操作系统了，经过其他应用程序的开发之后，被整合称为Linux distribitions。请问众多的distributions之间，有何异动？

   ```
   相同：
   	(1) 同样使用https://www.kernel.org所释出的核心；
   	(2) 支持同样的标准，如FHS，LSB等；
   	(3) 使用几乎相同的自由软件(例如GNU里面的gcc/glibc/apache/bind/sendmail...)；
   	(4) 几乎相同的操作接口(例如均使用bash/KDE/GNOME等等)；
   
   不同：
   	(1) 使用kernal与各软件的版本可能会不同；
   	(2) 各开发商加入的应用工具不同;
   	(3) 使用的套件管理模式不同(dpkg与RPM)
   ```



5. Unix是谁写出来的？GNU计划是谁发起的？

   ```
   Unix是Ken Thompson写的，1973年再由Dennis Ritchie以C语言改写成功。至于GNU与FSF则是Richard Stailman发起的。
   ```



6. GNU的全名为何？他主要由哪个基金会支持？

   ```
   GNU是GNU is Not Unix的简写，是个无穷循环！另外，这个计划是由自由软件基金会(Free Software Fundation, FSF)所支持的！两者都是由Stialman先生所发起的！
   ```



7. 何谓多人(Multi-user) 多任务(Multi-task)？

   ```
   Multi-user: 指的是Linux允许多人同时连上主机之外，每个用户皆有其个人的使用环境，并且可以同时使用系统的资源！
   Multi-task: 指的是多任务环境，在Linux系统下，CPU与其他例如网络资源可以同时进行多项任务，Linux最大的特色之一即在于其多任务时，资源分配较为平均！
   ```



8. 简单说明GNU General Public License(GPL)与Open Source的精神。

   ```
   (1) GPL的授权之软件，乃为自由软件(Free software)，任何人皆可拥有它；
   (2) 开发GPL的团体(或商业企业)可以经由该软件的服务来取得服务的费用；
   (3) 经过GPL授权的软件，其属于Open source的情况，所以应该公布其原始码；
   (4) 任何人皆可修改经由GPL授权过的软件，是符合自己的需求；
   (5) 经过修改后Open Source应该回馈给Linux社群。
   ```



9. 什么是POSIX？为何说Linux使用POSIX对于发展有很好的影响？

   ```
   POSIX是一种标准规范，主要针对在Unix操作系统上面跑的程序来进行规范。若你的操作系统符合POSIX，则符合POSIX的程序就可以在你的操作系统上面运行。Linux由于支持POSIX，因此很多Unix上的程序可以直接在Linux上运行，因此程序的移植相当简易！也让大家容易转换平台，提升Linux的使用率。
   ```



10. 简单说明Linux成功因素？

    ```
    (1) 借由Minix操作系统开发的Unix Like，没有版权的纠纷；
    (2) 借助于CNU计划所提供的各项工具软件，gcc/bash等；
    (3) 借由Internet广为流传；
    (4) 借由支持POSIX标准，让核心能够适合所有软件的开发；
    (5) Linus Torvalds强调务实，虚拟团队的自然形成！
    ```





# 提示 

------

该笔记是摘抄自《鸟哥的Linux私房菜》，仅供自己学习使用，如有侵权请联系删除[1758575969@qq.com]。原内容来自[鸟哥的Linux私房菜](http://linux.vbird.org/linux_basic/0105computers.php#chipset)

------

