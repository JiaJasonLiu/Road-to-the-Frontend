The expression $\mathbf{StateT[KeyT]}$ is what creates the mapping. 
- It's similar to property access at runtime (`state[key]`), but it performs the access **at the type level** during compilation. 
- It transforms the type of the key into the type of the corresponding value.