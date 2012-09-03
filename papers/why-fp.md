# Why Functional Programming Matters
## John Hughes, 1990

> It is a logical impossibility to make a language more powerful by omitting features, no matter how bad they may be.

- **What characterizes functional programming?**

The fundamental unit of computation is the function, which is applies to arguments. The entire program can generally be seen as a function applied to its input, and returning its output. Functions are defined in terms of other functions, down and down until you reach language primitives.

There are generally no side-effects. That is, a function does nothing more than return the value of its application. Given the same input repeatedly, the function always returns the same result.

Because of this, the application of a function can be seen as a simple value; in fact, a function call could be replaced in-line with the body of the function being called. This is called referential transparency. It then follows that a program doesn't need to be executed in any particular order.

> This is the key to functional programming's power -- it allows improved modularization.

- **Write a recursive sum, and an abstracted sum using a fold.**

```
sum Nil        = 0
sum (Cons n l) = n + sum l

foldr f x Nil        = x
fildr f x (Cons a l) = f a (foldr f x l)

sum = foldr (+) 0
product = foldr (*) 1
anytrue = foldr (or) False
alltrue = foldr (and) True
```

`fold f a` replaces all Conses with f and all Nils with a. For instance:

```
foldr (+) 0 [1, 2, 3]
foldr (+) 0 (Cons 1 (Cons 2 (Cons 3 Nil)))
(+) 1 ((+) 2 ((+) 3 0))
```

- **Can can map be defined in terms of a fold?**

```
map f = foldr (Cons . f) Nil

map (+1) [1, 2, 3]
foldr (Cons . (+1)) Nil (Cons 1 (Cons 2 (Cons 3 Nil)))
((Cons . (+1)) 1 ((Cons . (+1)) 2 ((Cons . (+1)) 3 Nil)))
(Cons 2 (Cons 3 (Cons 4 Nil)))
[2, 3, 4]
```

- **Why is lazy evaluation impractical in imperative languages?**

Programming with lazy evaluation in a language with side-effects would be rather difficult, as it would be difficult to determine exactly _when_ a side-effect would take place. Doing so would require the programmer to know a huge amount about the context in which the side-effects were defined. This is basically the opposite of modularity.
