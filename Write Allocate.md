#Caches 

When a cache miss occurs - allocate a new cache line and write to it
As only part of the line is valid (part you wrote to), need a valid bit per word

Write Non-Allocate:
- Send data to lower memory level, and do NOT allocate a new cache line
