# Data Structures
Ideas about types of data structures


## Introduction

Data structures are a fundamental aspect to computer programming. They are as important as code. In fact the data structure chosen informs what the code must do, not the other way around.

In this regard data structures are fundamental to any kind of pragmatic program.

Pure functions are also fundermental. For example f(x), where f(x) = x * x. Realistically a pure function when implemented on a real machine will be interacting with memory such as a stack, and a stack is itself a data structure, so sometimes the data structures are there, but hidden.

Some modern techniques also try to defer the choice of data structure to as late as possible. Consider the use of C++ container types being used in conjunction with the auto keyword. This can allow swapping out the container type rather easily allowing a change in data structure with minimal disruption to the consuming code. This is certainly a good idea in many situations. However there are plenty of things to be mindful of so I do not think this is a complete divorce of code from data structures. It reinforces the idea that choosing the right data structure is important, so much so that in case you get it wrong you will want to be able to change it easily.


## Some basic data structures

Let's look at some fundamental data structures:

  - An array
  - A linked list *(A singly linked list)*
  - A doubly linked list
  - A binary tree
  - A tree *(A M-ary tree)*
  - A dictionary *(A hash table)*

Some have alternative or more specific names, but these are some of the most common data structures that are very widely used. It is assumed that the reader is already familiar with these data structures and the relative pros and cons to them.


## Traversal

The data structures need to be used by code to access them and update them. This is how the pros and cons of data structures are measured.

Traversal of a data structure is one of the more fundametal operations that can be performed. Some data structures offer different traversals. Lets look quickly at each.

An array can be traversed from start to end or end to start by incrementing or decrementing an index in to the array. Very straight forward.

A singly linked list can only be traversed from start to end using the chain of `next` pointers.

A doubly linked list can be traversed in either direction as there are two sets of pointers. As an aside, an xor linked-list can achieve this with one set of pointers.

A binary tree has three types of traversal. An in-order traversal, a pre-order traversal and a post-order traversal.

Test if github supports plantuml:

```plantuml
A
B
C
A -> B
B -> C
```


```plantuml
@startuml
A
B
C
A -> B
B -> C
@enduml
```

@startuml
A
B
C
A -> B
B -> C
@enduml


