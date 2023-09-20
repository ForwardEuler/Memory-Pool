# Memory-Pool
A very simple implementation of memory pool; 
A simple memory pool implementation used for fast small objects allocation and deallocation. The pool expands automatically if pool is full.
This implementation is not thread safe, single memPool cannot be shared accross threads, speate memPools are needed for muti-threads. 

## Example Usage
```cpp
#include "mem_pool.h"
#include <vector>
#include <cstdio>

struct A {
    int a, b;
    A(int a, int b): a(a), b(b) {}
};

int main()
{
    //create pool with block size 3*sizeof(A)
    memPool pool(3*sizeof(A));
    //fast allocate memory on pool
    void* ptr1 = pool.memloc(sizeof(A));
    A* a1 = new(ptr1) A(1, 2);
    void* ptr2 = pool.memloc(sizeof(A));
    A* a2 = new(ptr2) A(3, 4);
    void* ptr3 = pool.memloc(sizeof(A));
    A* a3 = new(ptr3) A(5, 6);
    //auto expand after pool is full
    void* ptr4 = pool.memloc(sizeof(A));
    A* a4 = new(ptr4) A(7, 8);

    std::vector<A*> v={a1, a2, a3, a4};
    for (auto& a: v)
    {
        printf("%d %d\n", a->a, a->b);
    }

    int* l = (int*)pool.memloc(15*sizeof(int));
    for (int i = 0; i < 15; i++)
    {
        l[i] = i;
        printf("%d ", l[i]);
    }

    //free all memory allocated on pool
    pool.memfree();
    return 0;
}

```
