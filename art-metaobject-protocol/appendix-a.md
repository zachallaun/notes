#Appendix A: Intro to CLOS

## Classes and Instances

- **How do you define a simple class in CLOS?**

A class is defined with the `defclass` form, which accepts a class name, an inheritance list, and a let-like structure of slots and slot-defining attributes, such as `:initarg`, `:initform`, `:accessor`.

- **How do you instantiate an instance of a class?**

The `make-instance` form.

## Structure Inheritance

- **Does CLOS support multiple inheritance?**

Yes. One example is to use multiple inheritance to support "mixins", which capture useful pieces of behavior or structure. Using this model, a class has a primary superclass, and perhaps many mixins. This seems to reduce some of the complexity involved in supporting multiple inheritance. If superclasses are not independent, more complex rules for slot clashes must be used.

## Classes and Operations

- **What is a method and how is it used?**

A method is an operation individually implemented by a class, and it is invoked through a runtime dispatch that selects the appropriate implementation. In CLOS, this is _calling a generic function_, and is comparable to _sending a message_ in Smalltalk, for instance.

Methods will be invoked in terms of specificity; that is, if a method is defined on a super and subclass, the impl of the subclass will be used.

- **What is a generic, and how are they implemented?**

A generic specifies the _interface_ of a method. (This seems very similar to defprotocol in Clojure.) It is defined using `defgeneric`.

When a generic method is implemented, the arguments can have two forms: either a parameter name, or a pair consisting of a parameter name and the name of a class. For the implementation to be _applicable_, the object bound to the parameter name in the pair must be an instance of the class specified.

A generic method is implemented using the `defmethod` form.

## Multiple argument dispatch

- **How does CLOS support multi-methods?**

Many `defmethod`s can exist, and CLOS will dispatch based on the arguments, using what seems to be a simple form of type pattern-matching. (Dispatch based on the types of the arguments.)

## Structure Encapsulation

- **How can I access slots directly, avoiding `:accessor` fns?**

CLOS defines `slot-value`, which will accept an object and a slot-symbol. These are also settable. (You should just use accessors. They provide the intended access.)

## Methods in combination

- **Does CLOS abstract away necessary "setup" and "teardown" for specific methods?**

Yes, through the use of _before_ and _after_-methods: `(defmethod paint :before ((shape color-mixin)) ...)`

When a generic method is invoked, all applicable before methods will be called, then the primary method, then the after methods. This pattern is called the **standard method combination**.
