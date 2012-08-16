# Metaobject Protocol Based Language Design

- **What does a reflective implementation model provide?**

This implementation model provides the programmer with access to language implementation at a high level of abstraction, such that changes made to the language have a real impact on the outcome.

- **What is a _metaobject_?**

The basic elements of a programming language: classes, methods, generic functions, etc. These elements represent fragments of programs.

- **What is a protocol?**

A set of operations, or behaviors. A _metaobject protocol_, then, would be a series of operations or behaviors defined for metaobjects, that could be incrementally changed by a programmer to reap the benefits of a reflective implementation model.

- **What is meant by a region of languages?**

A single point in the region of languages would be a single implementation strategy; this single strategy does not represent all possible strategies. So, the region of languages is the set of all possible strategies. A goal for a languaged based on metaobject protocols would be to give the programmer the ability to select the specific point within this region, even on a per-feature basis. (The entire program need not even be tied to a specific point)
