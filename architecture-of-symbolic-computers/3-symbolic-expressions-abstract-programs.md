# Ch3: Symbolic Expressions and Abstract Programs

- **What are the three types of nodes that can comprise a symbolic expression?**

1. A _terminal node_ is a simple value that is itself not a tuple.

2. A _nonterminal node_ is itself a tuple and can contain an arbitrary number of both terminal and nonterminal children.

3. A _root node_ is a nonterminal node that has no parents.

- **History lesson: where did `car` and `cdr` come from?**

Early LISP was implemented on an IBM 7090, which had 36bit words with two halfs, the address and the data. Conveniently, each of these halves could hold a pointer, and could be accessed with the instructions "contents of the address register" and "contents of the data register", respectively. Thus, `car` and `cdr`.

- **What kind of activities might an _abstract function_ perform?**

1. An _abstract predicate_ might test whether a string of characters represents some construct in the abstract syntax. May be something like `is-a-operator(x)`.

2. An _abstract selector_ removes a construct from some surrounding constructs. Thus, `get-operator` might remove an <operator> from an expression of the form <expr><operator><expr>. The abstract selector may also transform the removed object into a more machine-readable form, as opposed to a simple character string.

3. An _abstract creator_ takes machine-readable arguments and converts them back into the human-readable string representation. So, `create-term(x,y)` may take two terms and combine them back into a single syntactically valid term.

## Exercises

_1) Find equivalent forms of the following s-exprs that minimize dots._

- `(((1.(2.(3.nil))).(1.(2.nil))).nil)`

```
(((1.(2.(3.nil))).(1.(2.nil))).nil)
 ((1 2 3)         (1 2))
```

- `((1.2).(2.3))`

None of these forms are "proper" lists; all the dots are necessary.

- `((1 2 (3.nil).(4 5 6)))`

```
((1 2 (3.nil).(4 5 6)))
((1 2 (3)    .(4 5 6)))
```

3) How many memory cells are needed for each of the following?

- `((1 2)(3 4)(5 6))`

```
( (1 2)  (3 4)  (5 6)      )
(   _      _      _     _  ) ;; 4 cells
    |      |      |     |
 (_ _ _)(_ _ _)(_ _ _) nil   ;; 10 cells
  | | |  | | |  | | |
  1 2 n  3 4 n  5 6 n        ;; 6 cells (nil is the same cell in memory)
                             ;; --------
                             ;; 20 cells
```
