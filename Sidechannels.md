#Sidechannels

Shared memory attacks:
- [[Prime and Probe]]
- [[Evict and Time]]
- [[Flush and Reload]]

Reading other process's memory:
- Old Linux optimisation mapped OS kernel into every process's virtual address space, and it was tagged as supervisor-mode access only
- On syscall, no need to flush, just flip supervisor bit

As a result, Spectre could look into the kernel virtual address space - as it usually includes all of physical memory

Validity of access to secret data is only detected at commit time - designers assumed that microarchitectural state is NOT observable

Partial mitigation:
- OS randomises virtual address mapping
- KPTI - reload TLB when in kernel mode, massive slowdown

[[SonicBOOM]]
To access data that's in a different address space, need to train the brain predictor:
- BTB poisoning for indirect jumps - TODO

Use 'retpolines' to partially mitigate RAS / BTB-based Spectre attacks
https://support.google.com/faqs/answer/7625886

