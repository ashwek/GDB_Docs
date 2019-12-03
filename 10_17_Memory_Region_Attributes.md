# 10.17 Memory Region Attributes

----

Memory region attributes allow you to describe special handling required by regions of your target’s memory. GDB uses attributes to determine whether to allow certain types of memory accesses; whether to use specific width accesses; and whether to cache target memory. By default the description of memory regions is fetched from the target, but the user can override the fetched regions.

Defined memory regions can be individually enabled and disabled. When a memory region is disabled, GDB uses the default attributes when accessing memory in that region. Similarly, if no memory regions have been defined, GDB uses the default attributes when accessing all memory.

When a memory region is defined, it is given a number to identify it; to enable, disable, or remove a memory region, you specify that number.

```
mem lower upper attributes…
```
Define a memory region bounded by lower and upper with attributes _attributes_, and add it to the list of regions monitored by GDB. Note that upper == 0 is a special case: it is treated as the target’s maximum memory address. (0xffff on 16 bit targets, 0xffffffff on 32 bit targets, etc.)

```
mem auto
```
Discard any user changes to the memory regions and use target-supplied regions, if available, or no regions if the target does not support.

```
delete mem nums…
```
Remove memory regions _nums_ from the list of regions monitored by GDB.

```
disable mem nums…
```
Disable monitoring of memory regions _nums_. A disabled memory region is not forgotten. It may be enabled again later.

```
enable mem nums…
```
Enable monitoring of memory regions _nums_.

```
info mem
```
Print a table of all defined memory regions, with the following columns for each region:
 - **Memory Region Number** : Enabled or Disabled. Enabled memory regions are marked with ‘y’. Disabled memory regions are marked with ‘n’.
 - **Lo Address** : The address defining the inclusive lower bound of the memory region.
 - **Hi Address** : The address defining the exclusive upper bound of the memory region.
 - **Attributes** : The list of attributes set for this memory region.


The access mode attributes set whether GDB may make read or write accesses to a memory region. While these attributes prevent GDB from performing invalid memory accesses, they do nothing to prevent the target system, I/O DMA, etc. from accessing memory.
 - **ro** : Memory is read only.
 - **wo** : Memory is write only.
 - **rw** : Memory is read/write. This is the default.


The access size attribute tells GDB to use specific sized accesses in the memory region. Often memory mapped device registers require specific sized accesses. If no access size attribute is specified, GDB may use accesses of any size.
 - **8** : Use 8 bit memory accesses.
 - **16** : Use 16 bit memory accesses.
 - **32** : Use 32 bit memory accesses.
 - **64** : Use 64 bit memory accesses.

The data cache attributes set whether GDB will cache target memory. While this generally improves performance by reducing debug protocol overhead, it can lead to incorrect results because GDB does not know about volatile variables or memory mapped device registers.
 - **cache** : Enable GDB to cache target memory.
 - **nocache** : Disable GDB from caching target memory. This is the default.
