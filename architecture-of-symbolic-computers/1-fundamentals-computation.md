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
