# Ch4: The Lambda Calculus

- **Show some ways in which lambda expressions can be simplified.**

```
(lambda x|(lambda y|(lambda z|M)))
(lambda x|lambda y|lambda z|M)
(lambda xyz|M)
```

This also implies that all lambda expressions are curried "implicitly"; that is, the expression `(lambda xy|xy)` is actually equal to the expression `(lambda x|(lambda y|(xy)))`.

- **Explicitly describe, in English, the meaning of the statement `(lambda xy|y(yx))`.**

```
(lambda ;; A lambda expression
xy      ;; with two binding variables (or identifiers)
|       ;; that will be substituted into the expression that comprises
y       ;; the application of the value of y onto the value
(yx))   ;; resulting from the application of the value of y onto the value of x
```

- **What is the difference between a free and a bound instance?**

A bound instance is an identifier which can be found as a binding variable in some containing lambda expression, while a free instance cannot. In the expression `(lambda x|x)y`, `x` is a bound variable, while `y` is free.

- **What are the legal lambda reductions?**

1. _Alpha reduction_, or renaming. (This can be necessary if a free variable occuring in an argument would be "accidentally" bound once substituted. For instance: `(lambda xy|yx)(y + 1)`)

2. _Beta reduction_, or application.

3. _Eta reduction_, which is a type of "optimization" in which redundant arguments are eliminated. For instance:

```
(lambda x|(lambda x|yx)x)5
;; is equal to
(lambda x|yx)5
```

(Note that the result is the same as application.)

Two lambda expressions are considered equal if one expression can yield the other through any series of these reductions. The "simplest" form of a lambda expression is the form that can no longer be reduced through Beta or Eta converstions, and this is called reducing the expression to _normal order_.

- **What is the practical significance of the Church-Rosser Theorem?**

The Church-Rosser Theorem (CRT) comes in two parts.

CRT I states that if an expression A can be reduced into two expressions B and C, then there is also another expression D that could reduce into B and C.

CRT II states that if A reduces to B somehow, and B is normal-order, then we can reduce to B from A by doing the _leftmost_ reduction at each step. The leftmost reduction is found by looking at the expression from left to right, and at each lambda expression found, performing all Beta/Eta reductions possible.

This theorem basically gives us an algorithm for reducing an expression to normal order. It also guarantees that each expression has only one possible normal order form (if any).

> See p83 for a great example of the benefits/tradeoffs of normal and applicative-order reductions.

- **How can integers be represented using the lambda calculus?**

Integers can be defined recursively by defining what 0 looks like, as well as some successor function `s` that accepts an integer and returns the subsequent one.

Then:

```
(lambda sz|z) ;; 0

s(x) = (lambda xyz|y(xyz)) ;; successor function

0 = (lambda sz|z)        ;; 0 applications of s
1 = (lambda sz|sz)       ;; 1 application of s to 0
2 = (lambda sz|s(sz))    ;; 2 applications of s to 0
3 = (lambda sz|s(s(sz))) ;; 3 applications of s to 0
...
n = (lambda sz|s(s(...(sz)...))) ;; n applications of s to 0
```

- **How can addition and multiplication be defined?**

Addition:

```
(lambda wzyx|wy(zyx))

;; Consider: add 1 and 1
(lambda wzyx|wy(zyx))(lambda sz|sz)(lambda sz|sz)
(lambda wayx|wy(ayx))(lambda sz|sz)(lambda sz|sz) ;; Alpha
(lambda ayx|(lambda sz|sz)y(ayx))(lambda sz|sz)   ;; Beta
(lambda yx|(lambda sz|sz)y((lambda sz|sz)yx))     ;; Beta
(lambda yx|(lambda z|yz)((lambda sz|sz)yx))       ;; Beta
(lambda yx|y((lambda sz|sz)yx))                   ;; Beta
(lambda yx|y((lambda z|yz)x))                     ;; Beta
(lambda yx|y(y(x)))                               ;; Beta, == 2
```

Multiplication:

```
(lambda wzy|w(zy))

;; Consider: multiply 2 and 2
(lambda wzy|w(zy))(lambda sx|s(s(x)))(lambda sx|s(s(x)))
(lambda zy|(lambda sx|s(s(x)))(zy))(lambda sx|s(s(x)))   ;; Beta
(lambda y|(lambda sx|s(s(x)))((lambda sx|s(s(x)))y))     ;; Beta
(lambda y|(lambda sx|s(s(x)))(lambda x|y(y(x))))         ;; Beta
(lambda y|(lambda sa|s(s(a)))(lambda x|y(y(x))))         ;; Alpha
(lambda y|(lambda a|(lambda x|y(y(x)))((lambda x|y(y(x)))a))) ;; Beta
(lambda y|(lambda a|(lambda x|y(y(x)))(y(y(a)))))        ;; Beta
(lambda y|(lambda a|y(y(y(y(a))))))                      ;; Beta
(lambda sz|s(s(s(s(z)))))                                ;; Alpha, == 4
```

- **How can Boolean logic be represented in the lambda calculus?**

```
(lambda xy|x) ;; True
(lambda xy|y) ;; False

(lambda w|wFT)  ;; not
(lambda wz|wzF) ;; and
(lambda wz|wTz) ;; or

;; not T
(lambda w|wFT)(lambda xy|x)
(lambda xy|x)FT
(lambda xy|x)(lambda xy|y)(lambda xy|x)
(lambda xy|y)

;; and T T
(lambda wz|wzF)(lambda xy|x)(lambda xy|x)
(lambda z|(lambda xy|x)zF)(lambda xy|x)
(lambda xy|x)(lambda xy|x)F
(lambda xy|x)

;; or F F
(lambda wz|wTz)(lambda xy|y)(lambda xy|y)
(lambda z|(lambda xy|y)Tz)(lambda xy|y)
(lambda xy|y)T(lambda xy|y)
(lambda xy|y)
```
