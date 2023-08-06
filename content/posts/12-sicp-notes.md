+++
title = "sicp notes"
author = ["hengist"]
date = 2023-08-06T00:00:00+08:00
lastmod = 2023-08-06T22:17:10+08:00
tags = ["scheme", "sicp"]
draft = false
+++

At first this book talk about elements of programming is interesting

-   primitive expressions
-   means of combination
-   means of abstraction

in this book we are gonna use scheme language, and i use chicken interpreter, just because i like it's interesting name.

```scheme
this language use prefix notation like this
(+ 1 2 3 4 5 6 7 8 9)
name something like value
(define size 2)
this associate the value 2 with the name size

define procedure
(define (suqare x) (* x x))
or
(define square (lambda (x) (* x x))
this is some kind of syntactic sugar, but the lambda type is more essential.

a good question asked at the end of first class, what's the difference between the following two expressions
(define a (* 5 5 ))
(define (b) (* 5 5))
 a  ==> 25
(a) ==> Error: call of non-procedure: 25
 b  ==> #<procedure (b)>
(b) ==> 25
```
