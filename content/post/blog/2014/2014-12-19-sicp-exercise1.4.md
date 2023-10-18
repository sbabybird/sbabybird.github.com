---
layout : single
date: 2014-12-19
title : SICP 课后练习题1.4
math: true
categories : 
  - 编程语言
tags : 
  - lisp
  - SICP
---

#### 练习1.4    请仔细考察上面给出的允许运算符为复合表达式的组合式的求值模型，根据对这一模型的认识描述下面过程的行为。
```scheme
    (define (a-plus-abs-b a b)
            ((if (> b 0) + -) a b))
```            
  练习1.4，通过if判断，根据b的值决定对a b所使用的运算符是+还是-，如果b大于0，则组合式为(+ a b)，反之则为(- a b)，所以组合式结果永远返回a加上b的绝对值。
```scheme  
    (define (a-plus-abs-b a b)
      ((if (> b 0) + -) a b))
    ;Value: a-plus-abs-b

    (a-plus-abs-b 4 2)
    ;Value: 6

    (a-plus-abs-b 4 -2)
    ;Value: 6
```