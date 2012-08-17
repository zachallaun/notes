# Ch2: Introspection and Analysis

- **Exercise 2.2**

A _diamond_ occurs when a class inherits from some other class along two different paths. Consider:

```cl
(defclass position ()
  (x y))
(defclass cad-element (position ...) ...)
(defclass display-element (position ...) ...)

(defclass displayable-cad-element (display-element cad-element) ())
```

In this example, one would expect the `displayable-cad-element` to retain two sets of `(x y)` pairs, but it would not. This is called a _diamond_, with `position` at the _apex_.

Write a function `(has-diamond-p <class>)` that determines whether there are any diamonds with `<class>` at the apex.

```cl
(defun has-diamond-p (class)
  (let ((subclasses (class-direct-subclasses class)))
    (some (lambda (subclass)
            (> 1 (remove-if-not (lambda (superclass)
                                  (member superclass subclasses))
                                (class-direct-superclasses subclass))))
          subclasses)))
```
