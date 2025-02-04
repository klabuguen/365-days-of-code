# Day 35: Rotate the Bits of a Number
#c-fundamentals #bit-manipulation 
Bit rotation is similar to a shift except that the bits shifted off from one end are shifted on to the other end. In a left rotation, the bits that are shifted off from the left end are shifted back on to the right end. In a right rotation, the bits that are shifted off at right end are shifted back on to left end.

Write a function that rotates the bits of a number, supporting both a left rotation and right rotation:

```
int rotate(int num, unsigned int bits, char direction){
	if(direction == 'l'){
		return rotateLeft(num, bits);
	}
	else if(direction == 'r'){
		return rotateRight(num, bits);
	}
	else{
		printf("Invalid character Enter either 'l' or 'r'.");
	}
	return -1;
}
```

- I create the function `rotate` above which will rotate an integer `num` by a specified number of bits `unsigned int bits` in the direction specified by the user. 

```
int rotateLeft(int num, unsigned int bits){
	return num << bits | num >> (INT32_BITS - bits);
}
```

- The helper functions `rotateLeft` and `rotateRight` are used to  return the new integers, shifted by the specified bits and direction.
- To rotate to the left: 
	1. Shift `num` to the left by the specified number of bits.
	2. In order to shift the shifted off bits back on to the right end, shift `num` to the right by *32 bits subtracted by the specified number of shifted bits*.
	3. Finally, OR the results of both and return the value.

```
int rotateRight(int num, unsigned int bits){
	return num >> bits | num << (INT32_BITS - bits);
}
```

- To rotate to the right:
	1. Shift `num` to the right by the specified number of bits.
	2. In order to shift the shifted off bits back on to the left end, shift `num` to the left by *32 bits subtracted by the specified number of shifted bits*.
	3. Finally, OR the results of both and return the value.

Below is an example of how the function may be used:
```
int main(){
	int num;
	unsigned int bits;
	char direction;
	
	printf("Please enter a number: ");
	scanf("%d", &num);
	printf("Please enter how the number of bits you would like to shift by: ");
	scanf("%d", &bits);
	printf("Please enter the direction: ");
	scanf(" %c", &direction);
	
	printf("The new number is: %d\n", rotate(num, bits, direction));
	
	return 0;
}
```

- I allow the user to specify `num`, `bits`, and `direction` then print the results of the rotation.

**Results:**
```
Please enter a number: 16
Please enter how many bits you would like to shift by: 4
Please enter the direction: r  
The new number is: 1
```

```
Please enter a number: 1 
Please enter how many bits you would like to shift by: 2
Please enter the direction: r
The new number is: 1073741824
```

```
Please enter a number: 1 
Please enter how many bits you would like to shift by: 4
Please enter the direction: l
The new number is: 16
```

```
Please enter a number: 1073741824
Please enter how many bits you would like to shift by: 2
Please enter the direction: l
The new number is: 1
```