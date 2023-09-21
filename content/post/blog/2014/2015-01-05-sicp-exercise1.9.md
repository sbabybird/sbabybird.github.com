---
layout : single
date: 2015-01-05
title : SICP 课后练习题1.9
math: true
categories : 
  - SICP
tags : 
  - lisp
  - programming
  - exercise
---

#### 练习 1.9  下面两个过程各定义了一种加起两个正整数的方法，他们都基于过程inc(它将参数增加1)和dec(它将参数减少1) 。请用代换模型展示这两个过程在求值`(add 4 5)`时所产生的计算过程。这些计算过程是递归的或者迭代的吗？


```scheme
    (define (add a b)
      (if (= a 0)
          b
          (inc (add (dec a) b))))
          
    (define (add a b)
      (if (= a 0)
          b
          (add (dec a) (inc b))))
          
```

解答：根据代换模型分别展开如下
   
```scheme
    (add 4 5)
    (inc (add 3 5))
    (inc (inc (add 2 5)))
    (inc (inc (inc (add 1 5))))
    (inc (inc (inc (inc (add 0 5)))))
    (inc (inc (inc (inc 5))))
    (inc (inc (inc 6)))
    (inc (inc 7))
    (inc 8)
    (9)
    
    (add 4 5)
    (add 3 6)
    (add 2 7)
    (add 1 8)
    (add 0 9)
    (9)
```
根据展开可以看出，第一个计算过程是递归的，因为明显有一个逐步扩展然后又收缩的递归计算链条。第二个计算过程是迭代的，没有扩展、收缩的过程，而是使用a和b存储了常量。
