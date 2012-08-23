# Ch2: Expressions and their Notation

- **Explain `fghx` as a function application.**

`fghx` is equivalent to `((fg)h)x`: The function f accepts g, and returns a function that accepts h, and returns a function that accepts x. This is fundamentally different to `f(g(hx))`. _Currying is the standard._

## Exercises

1) Convert the following infix expression to both prefix and reverse Polish: `(b + sqrt(b * b - 4 * a * c)) / (2 * a)`

Prefix: `(/ (+ b sqrt(- (* b b) (* 4 a c))) (* 2 a))`
Reverse Polish: `(b (((b b *) (4 a c *) -) sqrt) +) (2 a *) /`

> Reverse Polish freaks me out. No clue if this is correct, really.

2) Fn of 3 arguments, a, b, and c, and returns a value equal to that of problem 1.

Rewrite rule: `f(a, b, c) = (b + sqrt(b * b - 4 * a * c)) / (2 * a)`
Lambda fn: `(lambda abc|(b + sqrt(b * b - 4 * a * c)) / (2 * a))`

Lambda reduction when arguments are 2, 6, and 8.

```
(lambda abc|(b + sqrt(b * b - 4 * a * c)) / (2 * a)) 2 6 8
(lambda bc|(b + sqrt(b * b - 4 * 2 * c)) / (2 * 2)) 6 8
(lambda c|(6 + sqrt(6 * 6 - 4 * 2 * c)) / (2 * 2)) 8
(6 + sqrt(6 * 6 - 4 * 2 * 8)) / (2 * 2)
```

3) Reduce the following:

- `[2/y]([3/x] (x + y))`

```
[2/y] (3 + y)
(3 + 2) => 5
```

- `[2/y,z/x] (x + y)`

```
(z + 2)
```

- `[2/y]([y/x] (x + y)`

```
[2/y] (y + y)
(2 + 2) => 4
```

- `[2/y,y/x] (x + y)`

My thought is that these reductions are supposed to occur simultaneously, which suggests that maybe this behavior is undefined? or would depend on implementation?

4) Describe using Baukus Naur Form a language of signed integers.

```
<digit> := 0|1|2|3|4|5|6|7|8|9
<integer> := {<digit>}+
<sign> := +|-
<signed-int> := {<sign>}<integer>
```

5) Write a set of BNF statements that accurately describes the syntax of BNF itself.

> TODO
