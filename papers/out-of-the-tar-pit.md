# Out of the Tar Pit
## Moseley & Marks, 2006

C. A. R. Hoare, in his 1980 Turing award speech:

> I conclude that there are two ways of constructing a software design: One way is to make it so simple that there are obviously no deficiencies and the other way is to make it so complicated that there are no obvious deficiencies. The first method is far more difficult.

- **What are some approaches to understanding software?**

_Testing_ espouses an outside-in approach, where components are examined as black boxes.

_Informal Reasoning_ examines the system from the inside, and is obviously the most common approach, as it is required in general development. For this reason, the authors assert that improvements on informal reasoning are paramount, as they lead to fewer errors being created, while improvements on testing can only lead to more errors being detected.

I'm not fully swayed by this line of reasoning, as test-first methodologies clearly have an impact on the number of errors being created. Their conclusion seems to be valuable, however:

> Given a start choice between investment in testing and investment in simplicity, the latter may often be the better choice because it will facilitate _all_ future attempts to understand the system...

- **How does state impact systems?**

The authors provide a wonderful example of state: Any person who has ever been told to "turn it off and on", "restart the program", or "reinstall" has been subject to the hazards of state.

Having mutable state in a system means that that system has a possibly-arbitrary number of states. This makes stateful programs very difficult to test, as a test of one state tells you nothing of how the system will perform while in another state.

State also makes comprehension and reasoning more difficult, as you have to keep many possible states in your head in order to make decisions. The authors point out that one extra _bit_ of state added to a program doubles the number of possible states.

Also painful is the fact that the very presence of state can contaminate otherwise "pure" procedures. Consider a pure function: even if the function's procedure itself does not enact side effects, what if the argument to the function was itself a piece of mutable state? In a concurrent system, where other (possible impure) procedures would have access to that piece of state, this could be disasterous! And an otherwise pure function must now consider state to ensure correctness.

- **How does control impact complexity?**

The sequencing of operations as a part of the language's semantics forces the programmer to concern herself with the _how_ of the system, as opposed to simply the _what_. Consider the example from the text:

```
a := b + 3
c := d + 2
e := f * 4
```

Clearly, none of these statements rely on a particular sequence of execution; they are independent. Because of this, compilers may "optimize" the execution by running them concurrently, for instance. The programmer, then, must duplicate the work of the compiler to understand the code. (This is trivial in this example, but in a larger system, it surely would not be.)

Control of concurrent programs introduces even more complexity, especially in the presence of mutable state; in this case, the authors would have us believe that we're surely fucked.

- **What are some other causes of complexity?**

There are many varied causes, and the authors contend that they boil down to the following:

1. Complexity breeds complexity. (Consider code duplication because the code being copied is too difficult to understand.)

2. Simplicity is hard.

3. Power corrupts. That is, dangerous language features (ex. manual memory management) will inevitably be used and abused.

- **What is meant by _intensional identity_?**

When an object is uniquely identifiable regardless of its attributes, it is said to have intensional identity. In contrast, _extensional identity_ would consider objects with the same attributes to be the same themselves.

- **How do object-oriented systems attempt to conquer complexity?**

OOP, generally speaking, wraps pieces of state in an object with attached methods. These methods are used to access and modify the internal state of the object, can can enforce constraints.

- **Where does OOP break down in this approach?**

Objects must rely on intensional identity; even if two objs start with the same attributes, their state might be modified, and as such they need to be distinguishable at all times. Code size suffers for this, as domain-specific equivalency must be supported by custom fns.

Further, even if objects enforce constraints on their own internal state, there is little good way to support mutual constrains across objects. (Two objects with internally "valid" states may still represent an "invalid" configuration for a program.)

Regarding control, while message-passing-based actor models can make concurrency simpler, most OOP systems rely on shared-state concurrency, which sucks, as we've already established.

- **How does logic programming mitigate the complexity arising from control?**

While Prolog tends to fall short of this goal (see: goal ordering, cuts), logic programming can offer more control flexibility in execution than other languages. The language Oz, for instance, allows programmers to (separately from the statement of their logic programmers) specify a control strategy to optimize the search for a solution.

Hypothetically, then, logic programming can let the programmer eschew control and implementation in favor of facts and relations. And if fine-grained control is needed, it can be had.

- **How are essential and accidental complexity different?**

Essential complexity represents the complexity inherent in the users' problem; that is, given an ideal world, it is the complexity that the programmer would still have to manage. Accidental complexity is everything else, such as those things that step from implementation or language choices.

It is accidental complexity that is brought around by issues of state and control.

- **What is the _synchrony hypothesis_?**

It is an assumption that finite and stateless computations take place in zero time, and as such it does not matter whether or not they happen in sequence or in parallel.

- **Why might accidental complexities be necessary?**

Performance and ease of expression.

- **What is meant by _separation_ as a means of limiting complexity?**

_Separation_ in this sense separates a system into three components of restricted power, possibly even using restricted languages or DSLs. (The idea here is that a restricted language is easier to comprehend.)

1. Essential state: May make no reference to the other two components. Thus, changes to essential state may require the other components to change themselves, but changes to the other components can never require changes in the essential state.

2. Essential logic: Given some essential state, this component says what must be true. It may not reference the accidental state in any way.

3. Accidental state and control: Changes to this component may never affect the others.
