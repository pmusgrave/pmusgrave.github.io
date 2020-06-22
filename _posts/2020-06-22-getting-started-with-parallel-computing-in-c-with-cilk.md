---
layout: post
title:  "Getting Started with Parallel Computing in C with Cilk"
date:   2020-06-22 17:00:07 -0500
categories: blog
---
Cilk is a a small extension to the C language for parallel computing. In this tutorial, I'll be using the Tapir/LLVM compiler, which is built on top of clang-5.0. Cilk is much simpler to use than other concurrency platforms, such as Pthreads or TBB.

There are only three new keywords introduced by Cilk:
* `_Cilk_spawn` - allows a function call to be executed as a new thread
* `_Cilk_sync` - suspends a function's execution until all preceding threads have completed
* `_Cilk_for` - a for loop where each iteration can be executed as a new thread

#### Installation
The Cilk installation instructions are found [here](http://cilk.mit.edu/download/) and are straightforward. In my case, I prefer to keep the Tapir/LLVM version separate from normal clang executables, so I skip aliasing them to `clang` with the `update-alternatives` step and simply call the tapirclang binary manually as `clang-5.0`. This means `clang` is a vanilla clang-6.0 installation and `clang-5.0` is Tapir/LLVM.

#### A Parallel `Hello World`
```
#include <stdio.h>

int main(void) {
  _Cilk_for(int i = 0; i < 100; i++) {
    printf("hello, world %d\n", i);
  }

  return 0;
}
```
To compile, we just have to use the `-fcilkplus` compiler flag:
`$ clang-5.0 -fcilkplus main.c -o main`
`$ ./main`

The output is a list of numbers, some of which will be out of order depending on how the threads are scheduled during execution. Executing the program multiple times might result in a different order of numbers.

Cilk spawn and sync are used in a similar way. Simply add `_Cilk_spawn` before any function call and the runtime can schedule it as a new thread. Then add `_Cilk_sync` to halt execution.
```
...
x = _Cilk_spawn foo();
...
_Cilk_sync; // wait for thread to finish before using x
do_something(x);
```
