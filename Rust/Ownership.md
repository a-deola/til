**_Ownership_** in the Rust is the set of rules  that guide how **_memory_** is managed in a program.

##### The Stack and  the Heap
The stack and heap are parts of memory available to a program at runtime, The stack stores values in a _**last in, first out**_ basis, adding data is called _**pushing onto the stack**_  and removing data is called _**popping off the stack**_ , all data stored on the stack must have a known, fixed size. Data with an unknown size at compile time or a size that might change must be stored on the heap instead.
   The heap is less organized, when data is stored on the heap the memory allocator finds an empty spot on the heap big enough and marks it as being in use then returns a pointer. This process is called _**allocation on the heap or allocating**_. The pointer can then be stored on the stack.
   
>[!note]
>allocating and accessing data on the heap is slower than pushing and popping off the stack cause the pointer is used

##### Ownership Rules
- Each value in Rust has an _owner_.
- There can only be one owner at a time.
- When the owner goes out of scope, the value will be dropped.
##### Variable Scope
A scope is the range within a program for which an item is valid 

##### References
References are a flexible means to refer to a value without taking ownership of it, they are written `&a` if  `a` has a type T then &a has type &T.
Using a reference on a value is called borrowing the value. 
There are two types of references:
- A _shared_ reference: The referent can be read but not mutated.
- A _mutable_ reference: The referent can be read and modified, there can't be other ref to a value with a mutable reference, following the **multiple reader or single writer principle**. Denoted by `&mut`

De referencing is done using the `*` operator