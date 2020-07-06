# Pointers and dynamic memory

## Why is it necessary

In simple cases, the compiler can determine how much memory is required to run a program. But being limited to programs where the memory usage is known in advance would be pretty, well, limiting. For instance, when reading a file, there is no way to know if it will be 2KB or 2GB when compiling the program, so we need a way to indicate we need a given amount of memory to store the contents, and a way to indicate we are no longer using it so it can be reused, all of that _while the program is running_.

## Manual memory management vs. garbage collection

A lot of language deal with this runtime memory allocation and freeing by using a garbage collector. A garbage collector is basically some code that comes bundled with every program written in that language, keeps track of the memory the program is using and manages it automatically. This means it has to keep track of every memory allocation, what is using that memory, and pause every so often to free up memory that is no longer used by anything. As you might imagine, this can significantly slow down programs and is not always desirable.

On the other hand, manual memory management means the programmer has to manually do the job of the garbage collector. Allocating and freeing memory has to be done manually and correctly, and doing it improperly can lead to various issues, from hardly noticable to catastrophic (the best known example being memory leaks, which aren't that bad at all compared to other possible problems).

## C++ and RAII

Thankfully, most modern low level languages use the RAII pattern, or _Resource Acquisition Is Initialisation_, which was introduced by C++. The pattern is based around constructors and destructors. Instead of writing memory management code all the time, each type has a constructor and a destructor, which respectively take care of allocating and freeing the memory used by the type. The constructor is implicitely called when an instance of the type is created, and the destructor is implicitely called when an instance goes out of scope. All in all, RAII is an awesome pattern and this section will make heavy use of it.
