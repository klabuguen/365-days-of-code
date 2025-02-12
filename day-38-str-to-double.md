# Day 38: Convert a String to a Double
#c-fundamentals 
## Write a Function that Converts a String to a Double.

```
double myAtof(const char *buffer){
	double result = 0.0, fraction = 0.0, divisor = 10.0;
	int exponent = 0;
	bool isNegative = false, isExponentNegative = false, hasFraction = false;
	size_t i = 0;
	
	while(buffer[i] == ' '){
		i += 1;
	}
	
	if(buffer[i] == '-'){
		isNegative = true;
		i += 1;
	}else if(buffer[i] == '+'){
		i += 1;
	}
	
	while((buffer[i] >= '0' && buffer[i] <= '9') || buffer[i] == '.'){
	if(buffer[i] == '.'){
		hasFraction = true;
	} else{
		if(hasFraction){
			fraction += (buffer[i] - '0') / divisor;
			divisor *= 10.0;
		} else{
			result = result * 10.0 + (buffer[i] - '0');
			}
		}
		i += 1;
	}
	
	result += fraction;
	
	if(buffer[i] == 'e' || buffer[i] == 'E'){
		i += 1;
		if(buffer[i] == '-'){
			isExponentNegative = true;
			i += 1;
		} else if(buffer[i] == '+'){
			i += 1;
		}
		while(buffer[i] >= '0' && buffer[i] <= '9'){
			exponent = exponent * 10 + (buffer[i] - '0');
			i += 1;
	}
	
	double power = 1.0;
	
	for(size_t j = 0; j < exponent; j++){
		power *= 10.0;
	}
	
	if(isExponentNegative){
		result /= power;
	} else{
		result *= power;
		}
	}
	
	return isNegative ? -result : result;
}
```
