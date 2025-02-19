# Day 48: Display a Number in Binary
#c-fundamentals #bit-manipulation 

```
#define INT_SIZE 32

void displayBinary(int num){
	printf("%d in binary: 0b", num);
	for(size_t i = 0; i < INT_SIZE; i++){
		if(num & (1 << 31)) printf("1");
		else printf("0");
		num <<= 1;
	}
	printf("\n");
}
```
