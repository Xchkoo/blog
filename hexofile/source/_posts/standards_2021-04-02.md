---
title: '2021代码规范'
date: 2021-04-02 22:42:18
tags: ['coding','code standards']
categories: ['coding','code standards']
---
### 前言
为防止coding过程中码风的不断切换导致的可读性差，本人特意编写了一套主要继承于python、go语法和GNU\LINUX规范的代码规范。

<hr>

本人(Xchkoo)代码规范应遵循以下条例:

### 一、 $\color{darkviolet}{首项}$
1. 所有左大括号都不应换行并应在前加一个空格。

2. 所有逗号后都应该有一个空格。

3. 规定TAB键是4个空格，不应连续出现2个以上的空格。

4. 代码块后应空一行，文件结束处应换行（遵循python规范）。

5. 所有注释都应该是`/* ... */`，不能出现`//` 。

6. 在例如oi等算法题程序不能使用linker的项目中必须将cpp文件分为3个块(block)：全局变量声明块、函数与类块、main块。
应用`/* ... */`包括起来，使用类似jinja2的语法。但start和end要大写。
块与块之间要有两行空行。
例：
```
/* START global variate block */
    ....    
/* END global variate block */
```
块内可以有小块(part),小块之间用一行空行分隔。
例：
```
/* START tree part */
...
/* END */
```
tips:在jinja2中，end不需要但提倡写出block名。
### 二、 $\color{darkviolet}{变量}$
 1. 绝对不可出现毫无意义的缩写如next->nxt，但广为使用的number->num是合理的。

 2. 绝对不可用拼音命名变量（同理于函数和类）但是用日语罗马字应大加赞赏。

 3. 变量命名不提倡驼峰命名法，应使用蛇形命名法且只能使用_分割单词。（驼峰命名法应该在变量名过长有过多_时使用）注意！：-及——非法。

### 三、  $\color{darkviolet}{语句、函数和类}$
 1. 若语句为单行 应只在块和语句中加一个空格
 例：`if(...) continue;`
 2. 函数应同理于python，在开头使用注释编写帮助文档：
 ```
 /* 在此处写下帮助文档 */ 。
```
 3. 类中的变量和方法应该命名为`simplifiedClassName_name`。

 4. 类名应大写首字母。

 5. 不应使用《C++ primer》中不提倡的类用法。

 6. 应封装类中变量，提供接口。

 7. 类应尽量富鲁棒性。

### 四、 $\color{darkviolet}{命名空间}$
  在oi题中应遵循剃刀原则即使用```using namespace std```。
  在项目中应使用`std::`。

#### <div align="justify" style="color:red;">*** Xchkoo reserves all the right for the final explanation ***</div>

<hr>

![配图](/1.webp)