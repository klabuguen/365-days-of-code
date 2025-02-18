# Day 49: Count Leading Zero Algorithm
#c-fundamentals #bit-manipulation 

```
#define INT32_SIZE 32

int countLeadingZero(int num){
	if(num == 0) return INT32_SIZE;
	int count = 0;
	while((num & (1 << 31)) == 0){
		count++;
		num <<= 1;
	}
	return count;
}
```

