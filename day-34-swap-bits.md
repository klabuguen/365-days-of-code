# Day 34: Swap Bits in a Given Number
#c-fundamentals #bit-manipulation
Given a number $x$ and two positions (from the right side) in the binary representation of $x$, write a function that swaps the bits at two given positions and returns the result.

```
unsigned int swapBits(unsigned int num, unsigned int p1, unsigned int p2){
	unsigned int bit1 = (num >> p1) & 1, bit2 = (num >> p2) & 1;
	if(bit1 == bit2) return num;
	num ^= (1U << p1);
	num ^= (1U << p2);
	return num;
}
```

**To Swap the Bits in a Given Number:**
1. Extract the bits at position 1 `p1` and position 2 `p2`
2. If the bits are equal, simply return num
3. Otherwise, XOR the bit at `p1` with 1 to flip the bit
4. XOR the bit at `p2` with 1 to flip the bit
5. Return the current value of num

See below for an example of how the function may be used:

```
int main(){
	unsigned int num, p1, p2;
	printf("Enter an unsigned integer: ");
	scanf("%d", &num);
	printf("Enter position 1: ");
	scanf("%d", &p1);
	printf("Enter position 2: ");
	scanf("%d", &p2);
	printf("The swapped value is: %d\n", swapBits(num, p1, p2));
	return 0;
}
```


**Results:**
- `42` in binary: `0b101010`
- Bit stored in `p1`: 0
- Bit store in `p2`: 1
- Result: `0b001011` or `11`

```
Enter an unsigned integer: 42
Enter position 1: 0
Enter position 2: 5
The swapped value is: 11
```