# Preface

> This book aims to demonstrate the merits of, and describe implementations for, two non-von Neumann computer architectures: Functional and Logic. Totally badass.

- **What is meant by a computer architect, and computer architecture?**

The author intends _architecture_ to be defined in a broad sense as "the art or science of building." In this case, computer systems are the structures, and a computer architect must consider both hardware and software. This is important, as a clever and efficient hardware implementation is wasted if the software abstractions built on it are too cumbersome to be useful.

- **What is an _abstract machine_?**

A computer architecture that isn't actually implemented on hardware, but that could be a target for interpreters or compilers. This is a convenient middle ground.

- **What is meant when a language is said to be _function-based_?**

A function-based language is based on a system of applying or mapping a certain set of symbols to a set of values, as in function application in mathematics. In this paradigm, one declares a symbol to "be" the same thing as some objet or expression, and builds new things on top of this. Things like reassignment, side effects, program counters, et al. are simply unnecessary.

This also means that functions can be "first-class citizens", and that they can be passed as arguments to other functions, yielded from the invocation of functions, examined by functions, etc.

- **How does _logic-based_ programming differ?**

A logic-based system derives a set of substitutions such that an expression has a certain property. It is the responsibility of the implementation to come up with reasonable and efficient substitutions, and the responsibility of the programmer to fully declare the parameters that "bind" an expression.
