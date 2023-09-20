# Memory-Pool
A very simple implementation of memory pool; 
A simple memory pool implementation used for fast small objects allocation and deallocation. The pool expands automatically if pool is full.
This implementation is not thread safe, single memPool cannot be shared accross threads, speate memPools are needed for muti-threads. 

## Example Usage
```cpp
#include "mem_pool.h"

struct A {
    int a, b;
    A(int a, int b): a(a), b(b) {}
};

int main()
{
    //create pool with block size 3*sizeof(A)
    memPool pool(3*sizeof(A));
    //fast allocate memory on pool
    A* a1 = (A*)pool.memloc(sizeof(A));
    A* a2 = (A*)pool.memloc(sizeof(A));
    A* a3 = (A*)pool.memloc(sizeof(A));
    //auto expand after pool is full
    A* a4 = (A*)pool.memloc(sizeof(A));
    //free all memory allocated on pool
    pool.memfree();
    return 0;
}

```
