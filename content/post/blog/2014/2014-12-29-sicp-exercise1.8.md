---
layout : single
date: 2014-12-29
title : SICP 课后练习题1.8
categories : 
  - 编程语言
tags : 
  - lisp
  - SICP
math: true
---

#### 练习 1.8 求立方根的牛顿法基于如下事实，如果y是x的立方根的一个近似值，那么下式将给出一个更好的近似值：

$$ \frac{x/y^2+2y}{3} $$

请利用这一公式实现一个类似平方根过程的求立方根的过程。

解答：基本思路与求解平方根的实现是一致的，区别再有得到更好值`improve`的过程有变化，只需根据公式描述进行实现即可

```scheme
    (define (improve guess x)
        (/
         (+ (/ x (* guess guess)) (* guess 2))
         3))
         
    (define (good-enough? guess next)
                  (< (/ (abs (- guess next))
                        guess)
                     0.001)))
                     
    (define (abs x)
        (if (< x 0) (- x) x))
    
    (define (cbrt-iter guess x)
       (if (good-enough? guess (improve guess x))
                (improve guess x)
                (cbrt-iter (improve guess x) x)))

    (define (cbrt x)
        (cbrt-iter 1.0 x))
```
