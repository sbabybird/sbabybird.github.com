---
layout : single
date: 2014-12-15
title : SICP 课后练习题1.1
math: true
categories : 
  - 编程语言
tags : 
  - lisp
  - SICP
---

#### 练习1.1    下面是一系列表达式，对于每个表达式，解释器将输出什么结果？假定这一系列表达式是按照给出的顺序逐个求值的。
```scheme
10
;Value: 10

(+ 5 3 4)
;Value: 12

(- 9 1)
;Value: 8

(/ 6 2)
;Value: 3

(+ (* 2 4) (- 4 6))
;Value: 6

(define a 3)
;Value: a

(define b (+ a 1))
;Value: b

(+ a b (* a b))
;Value: 19

(= a b)
;Value: #f

(if (and (> b a) (< b (* a b)))
b
a)
;Value: 4

(cond ((= a 4) 6)
((= b 4) (+ 6 7 a))
(else 25))
;Value: 16

(+ 2 (if (> b a) b a))
;Value: 6

(* (cond ((> a b) a)
((< a b) b)
(else -1))
(+ a 1))
;Value: 16
```
练习1.1的内容比较简单，基本上直接就可以计算出表达式的值，所有表达式都可以在mit-scheme的交互解释器里进行验证。
