---
layout : single
date: 2014-12-23
title : SICP 课后练习题1.6
math: true
categories : 
  - SICP
tags : 
  - lisp
  - programming
  - exercise
---

采用牛顿法求平方根的过程如下。开始时，我们有了被开方数的值（现在需要做的就是算出它的平方根）和一个猜测值。如果猜测值已经足够好了，有关工作也就完成了。如若不然，那么就需要改进猜测值（求出猜测值与被开方数除以猜测值的平均值），并重复这个计算过程。具体编写代码如下（在MIT scheme解释器中）。

定义`sqrt-iter`过程，与上述描述完全对应。
```scheme
    1 ]=> (define (sqrt-iter guess x)
        (if (good-enough? guess x)
            guess
            (sqrt-iter (improve guess x)
                       x)))
                       
    ;Value: sqrt-iter
```    
定义改进猜测值的过程`improve`，返回猜测值与被开方数除以猜测值的平均值。
```scheme
    1 ]=> (define (improve guess x)
            (average guess (/ x guess)))

    ;Value: improve
```    
定义求平均数的过程`average`。
```scheme
    1 ]=> (define (average x y)
            (/ (+ x y) 2))

    ;Value: average
```
定义判断猜测值是否足够好的过程`good-enough?`。
```scheme
    1 ]=> (define (good-enough? guess x)
        (< (abs (- (square guess) x)) 0.001))

    ;Value: good-enough?
```    
定义求绝对值和平方的过程
```scheme
    1 ]=> (define (abs x)
            (if (< x 0) (- x) x))

    ;Value: abs

    1 ]=> (define (square x) (* x x))

    ;Value: square
```
定义最上层的过程，用于启动整个工作（使用`1`这个数字作为任何数的初始猜测值）。
```scheme
    1 ]=> (define (sqrt x)
            (sqrt-iter 1.0 x))

    ;Value: sqrt
```
执行`sqrt`过程，并以`9`为参数，求得平方根为`3`
```scheme
    1 ]=> (sqrt 9)

    ;Value: 3.00009155413138
```

#### 练习1.6    Alyssa P.Hacker看不出来为什么需要将if提供为一种特殊形式，她问：“为什么我不能直接通过`cond`将它定义为一个常规过程呢？”Alyssa的朋友Eva Lu Ator断言确实可以这样做，并定义了`if`的一个新版本：
```scheme
    1 ]=> (define (new-if predicate then-clause else-clause)
        (cond (predicate then-clause)
              (else else-clause)))

    ;Value: new-if
```
Eva给Alyssa演示她的程序：
```scheme   
    (new-if (= 2 3) 0 5)
    5
    
    (new-if (= 1 1) 0 5)
    0
```    
她很高兴地用自己的`new-if`重写了求平方根的程序：
```scheme
    1 ]=> (define (sqrt-iter guess x)
        (new-if (good-enough? guess x)
                guess
                (sqrt-iter (improve guess x)
                           x)))

    ;Value: sqrt-iter
```    
当Alyssa试着用这个过程去计算平方根时会发生什么事情呢？请给出解释。

解答：

这个练习引入了一个新的思考，刚开始时，我以为是牵涉到了过程的局部参数概念，因为在新编写的`new-if`过程中，看似可以完成条件判断并返回正确的值，但是在本例中使用却存在问题，即在递归调用`sqrt-iter`时，传给该过程的`guess`和`x`为`new-if`的局部参数，被返回给了`new-if`这个过程，不会向上返回到上一层`sqrt-iter`里，这样就导致了改进的猜测值永远不会被使用，使得这个计算过程永远不会结束（除非第一个猜测值恰好合适），从而导致递归调用的陷入无限循环。我在`MIT-scheme`解释器里的执行结果是，解释器自动退出并提示我递归调用深度超出最大值。

上述看起来是合理的，但是后来我考虑了其他情况，及本书在前面章节里提到了if`(if <predicate> <consequent> <alternative>)`语句是条件表达式的受限形式，在执行时，先判断`predicate`是否为真，然后根据结果只执行其后`consequent/alternative`中的一个。如果使用本例新定义的`new-if`则作为普通过程执行，传入的参数会因为解释器使用应用序求值的原因，两个表达式都会被立即求值，反应到本例中就是`guess`和`(sqrt-iter (improve guess x) x)`都会被立即求值，后面的那句是属于递归调用，这样也会导致改进的猜测值永远不会被使用，陷入无限层的递归调用中。
```scheme    
    1 ]=> (sqrt 9)

    ;Aborting!: maximum recursion depth exceeded
```
思考：

最初的时候，我的针对此题的思考方式是变量的作用域问题（可能lisp不会有此问题），后来发现，也许不是这样，而是由于对传入参数立即求值导致的，后续的网上搜索结果也显示出大家的答案都倾向于后者。