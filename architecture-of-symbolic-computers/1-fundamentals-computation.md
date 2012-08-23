# Ch1: Fundamentals of Computation

- **How are _problems_ and _instances_ related?**

Problems are usually generic, such that one or more parameters describe values that are not present in the problem statement. When the parameters are assigned values, an _instance_ of the problem is created; different value assignments would lead to a different instance.

A _deterministic_ problem has exactly one solution for a particular instance or class of instances, while a _nondeterministic_ problem may have more than one solution.

- **How does the use of the term _variable_ differ from other uses?**

The term variable seems to indicate that its value might actually _vary_, but this is not what is meant here. In the context of a problem, a parameter may be called a _free variable_, which is to say it has not been bound to any variable. (This is in contrast to a _bound variable_, of course.)

Once a variable has been bound, though, it can never vary, and can never be rebound, at least during that computation. The variable, then, is synonymous with the value bound to it.

The parameter may still be called a variable because it can take on different values for different instances of a problem.

- **How does a problem statement relate to the method of solving it?**

It doesn't. The statement of the problem refers to the input parameters and the desired solution, but it doesn't specify the manner in which the problem should be solved. That process could be called an _algorithm_.

> The author should check out Coq re: validity.

- **How are procedural and declarative languages different?**

A procedural language emphasizes the description of the steps of algorithms, while declarative languages emphasize problem descriptions and the desired outcome.

- **What are the three methods of describing programming language semantics?**

- Interpretative semantics

Interpretative semantics describes the translation of the pieces of a programming languages syntax into code that for some abstract machine.

- Axiomatic semantics

Axiomatic semantics describe a change in "state" given the execution of some feature of the language. In particular, an axiom would describe the "before" and the "after", but would not describe the process or algorithm.

These kinds of semantics can be helpful in describing instructions to abstract machines; you know what will happen given an instruction, but it isn't your responsibility to know about the actual implementation of that particular instruction.

- Denotational semantics

Denotational semantics describe the mapping of language notation onto abstract, human-understandable values. (For instance, perhaps the binary 00000011 to the number 3.)

- **What are the key characteristics of the von Neumann model?**

This model contains a memory unit, to which access is granted by a CPU. A program lives in memory and contains an ordered sequence of instructions, which specify some activity of the CPU to modify the contents in memory. A program counter is used by the CPU to select instructions from memory, and a programming language specifies how instructions can be contained in memory.

- **What is the _von Neumann bottleneck_?**

All memory must be accessed sequentially by the CPU; the speed of the program, then, is limited by the "speed" and "width" of the path between the CPU and the memory.

- **What is one way in which the bottleneck can be overcome?**

For many programs, _assignment_ is of key importance. That is, you attach a name to some register in memory. Then, the program sequences access and modification of those memory registers; each access and modification is subject to the von Neumann bottleneck.

If, however, variables did not vary, and "assignment" became attaching a value to a symbol that would not change during execution, there would be more opportunities to break the bottleneck.

- **How can an object be characterized?**

An object is a thing that can be described and differentiated from other objects. Associated with an object is a value that could be compared with the values of other objects. Thus, "2" is the same as the Roman numeral "II", but different from "3" and "III".

- **What is the difference between a subset and a _proper_ subset?**

That B is a subset of A means that all elements of B are members of the set A. For B to be a proper subset of A, there must also be some element of A that is not a member of B. (Note, that if B is a subset of A, and A a subset of B, then the sets are equal.)

- **How does one describe _relations_ mathematially?**

Relations are described as a set of tuples where each tuple satisfies some property. Relations may be even more specifically described as having a certain arity.

If a relation has an arity of 1, it is a one-place relation, and the set of objects satisfying the relation are called properties.

If the arity is 2, it's called a binary relation. This kind of relation can conveniently model type.

> The author then goes on to describe a bit of set theory. Future me, if you ever become confused about _reflexive_, _symmetric_, _antisymmetric_, or _transitive_ relations, or equivalence relations or classes, or transitive closures... see p18-19.

- **How can functions be seen as relations?**

A function is a binary relation over some sets AxB, where each element in A appears in exactly one tuple, and maps to some element of B.

In this way, _function evaluation_ or _application_ can be seen as simply "looking up" the element in A, and returning the corresponding element from B. If the function relation's tuples does not contain every element of A, it is said to be _partial_.

Generally, the notation is `f:A->B`, where A is the domain, and B is the range. For a function where the range may be a set of functions, the notation may look something like `f:Z->(Z->Z)`.

> Haskell!

> Recall injective/one-to-one, surjective/onto, and bijective fns

- **What makes a function composable with another function?**

A function g is composable with a function f if g's range is a subset of f's domain. Also important is that g and f could be composed into a "single" function, called a _composition_ function, with the notation `(f.g)`, such that `f(g(a)) == (f.g)(a)`.

## Exercises

1. Sum and product of the k-th through k+m-th largest numbers of a set.

**Parameters**:
```
set S, number A, number B, such that:
  A > 0
  B > A
  B < (number of elements in S)
```
Sort the elements of `S`, extract the A through B elements of the sorted collection, and find the sum and product of those elements.
