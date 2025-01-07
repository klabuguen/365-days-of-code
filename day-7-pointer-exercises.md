#c-fundamentals 
# Pointer Exercises
Intro here
## 1. Generic Swap Function
- Uses void* as arguments
- How do we know to dereference the tmp value to?
- Uses memcpy to copy memory from `a` to `tmpMemory`
- Uses memcpy to copy memory from `b` to `a`
- Uses memcpy to copy memory from `tmpMemory` to `b`
- Free `tmpMemory` at the end
- **How to solve this without memcpy?**


