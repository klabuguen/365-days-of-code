# Day 41: Swap Endian
#c-fundamentals 
## Write a Function that Swaps the Endianness.

```
unsigned int swapEndian(unsigned int val){
	val = ((val & 0xFFFF0000) >> 16) | ((val & 0x0000FFFF) << 16);
	return ((val & 0xFF00FF00) >> 8) | ((val & 0x00FF00FF) << 8);
}
```
