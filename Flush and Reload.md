#Sidechannels 

Inverse of [[Prime and Probe]]

Relies on shared virtual memory and ability to flush by virtual address

Attacker flushes a shared line of interest through:
- Dedicated instructions
- Eviction through contention

Once victim has executed, the attacker reloads the evicted line by touching it - measuring the time taken.

- Fast reload - victim touched this line, cache tag was used by the victim
- Slow reload - cache tag was not used by victim tag

Works when two programs use a shared library - like Linux's mmap, takes advantage of copy on write (pre copy).

