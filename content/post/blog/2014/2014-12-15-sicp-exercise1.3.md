---
layout : single
date: 2014-12-15
title : SICP 课后练习题1.3
math: true
categories : 
  - SICP
tags : 
  - lisp
  - programming
  - exercise
---

#### 练习1.3    请定义一个过程，它以三个数为参数，返回其中较大两个数之和。

```scheme
    (define (max-three-number a b c)
            (if (> a b)
            (if (> b c) (+ a b) (+ a c))
            (if (> a c) (+ b a) (+ b c))))
    
    (max-three-number 42 7 1)

    ;Value: 49
```    
  练习1.3，解决此练习中问题的方法比较多，本答案使用比较朴素的方法，先比较出最大的两个数字，然后将其相加，对于三个数字来说，先在前两个中选取一个大的，然后将其与后面两个中比较大的那一个相加。还有一种思路就是可以先定义出比较大小的方法，然后再调用之，或者先对数字按从小到大排序然后加最后两个，等等。
