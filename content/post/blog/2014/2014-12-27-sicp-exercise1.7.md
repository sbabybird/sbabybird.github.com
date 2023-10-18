---
layout : single
date: 2014-12-27
title : SICP 课后练习题1.7
math: true
categories : 
  - 编程语言
tags : 
  - lisp
  - SICP
---

#### 练习 1.7 对于确定很小的数的平方根而言，在计算平方根中使用的检测good-enough?是很不好的。还有，在现实的计算机里，算术运算总是以一定的有限精度进行的。这也会使我们的检测不适合非常大的数的计算。请解释上述论断，用例子说明对很小和很大的数，这种检测都可能失败。实现good-enough?的另一种策略是监视猜测值在从一次迭代到下一次的变化情况，当改变值相对于猜测值的比率很小时就结束。请设计一个采用这种终止测试方式的平方根过程。对于很大和很小的数，这一方式都能工作吗？

解答：good-enough?当前采用的判断方式是，对比猜测值的平方结果与X的值之间的差距，当差距小于某个阙值时（比如0.001），就停止计算。当X很小或很大时，这种检测就会失败，比如，假设我们的阙值设置为0.001，那么当X本身小于这个阙值时，就会检测失败，得出错误结果，当X很大时，也会由于精度不足而一直达不到最佳猜测值，导致死循环。

因此，要解决这一问题，可以按照题目中给出的思路对good-enough?过程进行修改，不再判断猜测值平方与X的差距，而是判断两次猜测值之间的比率。

```scheme
    1 ]=> (define (good-enough? guess next)
                  (< (/ (abs (- guess next)) 
                        guess) 
                     0.001)))
                     
    ;Value: good-enough?
                  
    1 ]=> (define (sqrt-iter guess x)
        (if (good-enough? guess (improve guess x))
                (improve guess x)
                (sqrt-iter (improve guess x) x)))

    ;Value: sqrt-iter

    1 ]=> (sqrt 0.00000000001)

    ;Value: 3.1622776601874535e-6

    1 ]=> (sqrt 100000000000000000000000000000000000000000000)

    ;Value: 1.0000000000001497e22
```
    
在新的`good-enough?`中，传入的是两次猜测值，所以还要修改`sqrt-iter`过程，在调用时计算两次猜测值。
