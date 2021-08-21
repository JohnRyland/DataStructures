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

### Array

An array can be traversed from start to end or end to start by incrementing or decrementing an index in to the array. Very straight forward.

### Linked lists

A singly linked list can only be traversed from start to end using the chain of `next` pointers.

A doubly linked list can be traversed in either direction as there are two sets of pointers. As an aside, an xor linked-list can achieve this with one set of pointers.

### Trees

A binary tree has three types of traversal. An in-order traversal, a pre-order traversal and a post-order traversal.

Consider the binary tree shown in figure 1.

![Binary-Tree](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/JohnRyland/DataStructures/main/images/binary-tree.pu)<br>
#### Figure 1. A binary tree
-----

Depending on the traversal order used we will visit the nodes in the alphabetical order depicted, from A, B, C, D to E as shown in the below diagrams. In all cases we are still dereferencing the same chain of links in the same way, but the difference between them is where the current node is visited, whether it is visited before descending the left side of the node (pre-order), between descending the left and right side (in-order), or after descending both the left and right sides (post-order).

![Binary-Tree In-Order Tarversal](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/JohnRyland/DataStructures/main/images/binary-tree-in-order-traversal.pu)<br>
#### Figure 2. In-order traversal of a binary tree
-----

![Binary-Tree Pre-Order Traversal](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/JohnRyland/DataStructures/main/images/binary-tree-pre-order-traversal.pu)<br>
#### Figure 3. Pre-order traversal of a binary tree
-----

![Binary-Tree Post-Order Traversal](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/JohnRyland/DataStructures/main/images/binary-tree-post-order-traversal.pu)<br>
#### Figure 4. Post-order traversal of a binary tree
-----

For non-binary trees where each node can have an arbitary number of children, the above pre-order and post-order traversal orders still make sense and are possible however the in-order traversal is less easy to define or useful for these trees.

### Hash tables

Typical hash table implementations consist of a set of buckets with each bucket containing a singly linked list of nodes. A full traversal by iterating each bucket (in forward or backward order) and then for each bucket iterating the linked list of nodes is possible. If full reverse order was required, conceivably the hash table's buckets could contain doubly linked lists or xor linked lists.


## Searching

Another very important use for a data structure is searching for data within it. Without sorting, any data structure can trivially be searched if it supports traversal. We already saw how traversal can be supported by all the data structures mentioned so far.

Most of the data structures can be sorted to rearrange the items in to some kind of canonical order to help them be searched more quickly. For example an array can be sorted using the C standard library function `qsort` to achieve this which then makes it possible to search efficiently using the `bsearch` library function which does so using a binary search strategy. 

Sometimes just plain traversal on modern machines can be as efficient on small sets of data as more elaberate algorithms. This is due to a number of reasons. Firstly memory and it's caches are optimized for sequential usage patterns. When you access a single byte of memory, a full cache line of 64 bytes are fetched in the process. If you access only 1 byte in every 64 bytes scattered through the address space, you will only achieve 1/64th the potential of the memory's bandwidth. If you access all 64 bytes of the cache line before moving on to the next cache line you will be unlocking the full potential of that bandwidth. You might manually or the compiler or CPU might even be able to preload the next cache line in advance for you so that you don't even need to wait for memory to load in to the cache lines. This is part of the power of sequential access. Another aspect is the predictability of the code's branching. A sequential iteration through an array is a simple loop that the CPU's branch predictors have an easy time with.

However when the data gets really big then definately smarter algorithms win out. Unfortunately there is no easy rule as to what that size actually is and you might not control what size your input data is. If you know what your data will be, the best strategy is to profile. If you don't know but performance isn't going to matter when the data is small, use the smarter algorithm, otherwise perhaps do both and based on the size of the input switch implementations. There is no easy answer as to when to use which particular data structure and algorithm.


## Insertions and deletions

The next aspect of various data structures is how well they support adding and removing new data. Sometimes this is required and sometimes not. The simplest data structure to support insertions and deletions is the linked list. I think this is still practically the first thing computer science students learn so I don't think I need to explain this. Arrays can be grown by reallocation which has it's own problems because you can't have pointers in to items in the array. A static array would be one where insertions and deletions aren't supported.

Trees and hash tables are almost as easy as lists for supporting insertions and deletions.


## Actual implementation details

So far this discussion of data structures has been mostly theoretical. But what about some actual implementation detail considerations.

The first I want to talk about is intrusive vs non-intrusive implementations.

![Intrusive List](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/JohnRyland/DataStructures/main/images/intrusive-list.pu)<br>
#### Figure 5. Intrusive List
-----

An intrusive list is one where the items contained in the list themselves have the next pointers as shown in figure 5 where the `value` member and `next` member are both in the nodes.

![Non-Intrusive List](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/JohnRyland/DataStructures/main/images/non-intrusive-list.pu)<br>
#### Figure 6. Non-Intrusive List
-----

The non-intrusive list has the advantage that the item doesn't need to know it belongs to a list so can be used on arbitary data, however the downside is that additional small allocations will be needed for the nodes and additional pointer dereferences to access the data. Depending how the nodes and items are allocated, this may cause access patterns that are not well tuned with the way computers cache memory.


## Intrusive hash tables, binary trees

Once the concept of intrusive lists is understood, it is not a big jump to realize that this can be easily be applied to binary trees and hash tables. Given that a hash table is buckets of linked lists, changing those lists to intrusive lists is almost a no-op of mental activity. As well it should be fairly obvious how to make binary tree nodes be intrusive also.


## Implementation details of m-ary trees

A binary tree is a fairly easy concept to understand once linked lists are understood. Instead of a next pointer in each node, the node contains a left pointer and right pointer. The more general case is a m-ary tree which has instead of just 2 children, has m children. Each node might consist of a parent pointer and an array of children pointers such as in figure 7.

![Tree Node](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/JohnRyland/DataStructures/main/images/tree-node.pu)<br>
#### Figure 7. Tree node
-----

This example is intrusive similar to previous examples, however contained in each node is another data structure, the list of children. This is unfortunate. The list is a list of pointers, so in effect it is a non-intrusive list.

But we can do better. It might not be immediately obvious but we can represent the same information in another way. Instead of thinking about each element as having a parent and multiple children, another way of framing this is that each element has a parent, an eldest child and a next youngest sibling. This suprisingly is the same amount of pointers a binary tree contains if including parent pointers (optional in both cases depending on your requirements). You can iterate all children by jumping to the eldest child, then from that element iterating the next youngest siblings across.

![Intrusive Tree Node](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/JohnRyland/DataStructures/main/images/intrusive-tree-node.pu)<br>
#### Figure 7. A better intrusive tree node
-----

If we recall our earlier tree example in figure 1, when rearranged in this way it would appear as below in figure 8 using this alternative representation.

![Intrusive Tree](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/JohnRyland/DataStructures/main/images/intrusive-tree.pu)<br>
#### Figure 8. Intrusive tree
-----

Space wise this is no different than a binary tree when used as a binary tree, but can be used to have nodes with arbitary numbers of children.


## Cache friendly structures

As already mentioned, memory access patterns are important. Accessing memory by blocks at a time or sequentially is better than accessing small amounts of it randomly. Also if our data structures are smaller we can make better use of the available memory bandwidth.

As machines have moved from 32-bits to 64-bits, the corresponding size of a pointer has doubled from 4 bytes to 8 bytes. This makes using pointers more expensive. From this point of view one of the best data structures is the humble array and using indexes in to the array instead of pointers. Arrays are cache friendly and provided the array will not have more than 4 billion items, can be cheaper to reference items of the array using indexes.

With all of the data structures looked at so far, there is no reason that the items of these could not be allocated out of a pool instead. The concept is simple. A memory pool is simply a large pre-allocated chunk of memory. Then fixed size items can be allocated out of this pool. For example if we have a linked list, each list item could be allocated from a memory pool associated with this linked list. When it is time to delete the entire list, a single deallocation of the chunk of memory the pool pre-allocated can be made, effectively deleting all the items.

Now all the items of the list are in memory with addresses that are close together. Practically the list is almost an array. This isn't a great example as most of the time you would be better off just using an array and avoiding the complexities of needing a memory pool.

The way malloc is frequently implemented is first by pre-allocating a chunk of memory from the heap. Then a number of pools are created for different sized allocations. Then when a request for a certain sized piece of memory is made it will check the appropriate pool and walk what is called the free list to find an available piece of memory to return. Malloc also needs to be thread-safe so there will often be a mutex that needs to be locked. The free list is often just a linked list inside each of the pools linking together the free sections of memory using that free memory itself as the nodes. When an allocation is made, it adjusts the free list to jump past that allocated piece of memory. And when memory is freed it does the reverse, adding the freed memory back in to the free list.

With a memory pool impementation, it too could implement such a concept as a free list. Because typically memory pools are for fixed sized allocations, the free list only needs to take the first item it finds, it doesn't need to search for a better fitting free chunk of memory. This is wonderful as allocations can be done in constant time if the pool can be guarenteed to be created large enough for the peak number of items it ever needs to allocate. Deallocations can also be in constant time as it simply adds the item back in to the free list.

We combine this together with our better intrusive tree node, and we have a table of these nodes which represent a m-ary tree but are stored as an array. We should then replace using pointers with indexes for the space saving. So we end up with something like figure 9.

![Pool Tree Node](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/JohnRyland/DataStructures/main/images/pool-tree-node.pu)<br>
#### Figure 9. Pool tree node
-----



