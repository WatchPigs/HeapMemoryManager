## Heap Memory Manager
In main.cpp, there is a test for the feature of this heap memory manager.
This project implements my own "malloc()/free()" and "new/delete" on heap memory. It includes two kinds of memory allocators.

#### General memory allocator (to allocate custom sized memory for user)：
* Use Doubly linked list to manage allocated and unallocated memory blocks
* Suballocate from end of the heap memory.
* Subtract needed size (i_size) from end of heap memory to get enough memory for user.
* Round down to aligned address.
* aligned address ⇒ end of block = user memory.
* Create new MemoryBlock for user memory.
* Have a working block collection function that looks through the list of unallocated memory blocks, combining any that can be into a single larger unallocated block. 

#### Fixed size memory allocator (to allocate small fixed size memory for user)：
* Benefits:
	* Doesn’t require a fit search when making an allocation of that size.
	* No internal fragmentation.
	* Reduces per-alloc overhead.
	* In real game development, most memory allocations have small fixed size.
* Use BitArray (with bitwise operator) to manage allocated and unallocated memory blocks (one bit, 1 for in use, 0 for not).
* Use the compiler intrinsics _BitScanForward() and _BitScanForward64() to help find the first set bit or unset bit to locate the needed memory block.