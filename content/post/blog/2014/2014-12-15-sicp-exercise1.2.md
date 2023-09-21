---
layout : single
date: 2014-12-15
title : SICP 课后练习题1.2
math: true
categories : 
  - SICP
tags : 
  - lisp
  - programming
  - exercise
---

#### 练习1.2    请将下面表达式变换为前缀形式：


$$ \frac{5+4+\Bigl(2-\Bigl(3-\left(6+\frac{4}{5}\right)\Bigr)\Bigr)}{3\left(6-2\right)\left(2-7\right)} $$
```scheme
(/ (+ 5
4
(- 2
(- 3
(+ 6 (/ 4 5)))))
(* 3
(- 6 2)
(- 2 7)
))

;Value: -37/150
```
练习1.2，直接将数学表达式转换为前序表达式即可，在写的时候可以遵循一下排版规则，即同一个运算符的表达式垂直对齐。
