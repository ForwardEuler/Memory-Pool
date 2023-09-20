# Memory-Pool
A very simple implementation of memory pool; 
A simple memory pool implementation used for fast small objects allocation and deallocation. The pool expands automatically if pool is full.
This implementation is not thread safe, single memPool cannot be shared accross threads, speate memPools are needed for muti-threads. 
