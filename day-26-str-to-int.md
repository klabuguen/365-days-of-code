# Day 26: Convert a String to Integer

#c-fundamentals 

**Write a Function that Converts a String to an Integer**.
```
int myAtoi(const char *bufferIn){
	size_t i = 0;
	int isNegative = 0, num = 0; // 0 is false, 1 is true
	while(bufferIn[i] == ' '){
		i += 1;
	}
	if(bufferIn[i] == '-'){
		isNegative = 1;
		i += 1;
	} else if(bufferIn[i] == '+'){
		i += 1;
	}
	while((bufferIn[i] >= '0' && bufferIn[i] <= '9') && bufferIn[i] != '\0'){
		num = num * 10 + (bufferIn[i] - '0');
		i += 1;
	}
	return (isNegative == 1) ? num *= -1 : num;
}
```