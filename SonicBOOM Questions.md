Hi, 

I have been reading up on SonicBOOM and some of the details outlined in the paper - https://carrv.github.io/2020/papers/CARRV2020_paper_15_Zhao.pdf - and I had a few questions surrounding the design choices made when implementing BOOMv3.

1. (Section 3.1) Why is an additional pipeline stage needed after the frontend decoders? I see that the decoders always need 4 instructions per packet, and anywhere between 4-8 instructions can be fetched in a given cycle (with the C-extension), but don't quite understand why there is an additional pipeline stage needed **after** the decoding. What do the 4 fetch blocks in Figure 2 actually represent?

2. (Section 3.2) How was the branch predictor tightly coupled with the fetch unit in BOOMv2, and why is this fixed by TAGE? Is it because TAGE makes use of pipelining and gshare doesn't?

3. (Section 3.2) How does the snapshotting repair mechanism work? Surely this is quite expensive. For the RAS, maybe using a shift register to observe how many times we push to the stack while in a "predicted" state, and pop that number on a mispredict might be cheaper? Do the L0 and L1 BTBs also use snapshotting?

4. (Section 4.2) How are short-forwards actually detected? As this seems quite time critical, how does it do it so quickly?

5. (Section 5.1) Why is the load store unit able to issue two loads, but only one store per cycle? 

6. (Section 5.1) Why are the load-address and store-address CAMs duplicated?

7. How would SonicBOOM look in a multicore environment? Does it have the necessary architecture in place to solve problems like cache-coherency?


These questions are bunched together, so I apologise for posting them at once and appreciate any responses!

Best regards,

Rushil