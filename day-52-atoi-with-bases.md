# Day 52: Implement atoi() with Bases

Similar to [[day-26-str-to-int]] but supporting Base 2 and Base 16.

```
int32_t myAtoiBase(const char *str, int base) {
	if (base != 2 && base != 10 && base != 16) {
		return 0; // Invalid base
	}
	
	int32_t result = 0;
	bool isNegative = false;
	int i = 0;
	
	// Handle negative sign for base 10
	if (str[i] == '-') {
		isNegative = true;
		i++;
	}
	
	// Iterate over each character
	while (str[i] != '\0') {
	
		char c = str[i];
		int digit;
		
		if (c >= '0' && c <= '9') {
			digit = c - '0';
		} else if (c >= 'A' && c <= 'F' && base == 16) {
			digit = c - 'A' + 10;
		} else if (c >= 'a' && c <= 'f' && base == 16) {
			digit = c - 'a' + 10;
		} else {
			i++; // Invalid character, skip ahead
		}
		
		// Ensure digit is within valid range for the base
		// If it is not, then skip to the next iteration
		if (digit >= base) {
			continue; // invalid digit for base, skip ahead
		}
		
		result = result * base + digit;
		i++;	
	}
	return isNegative ? -result : result;
}
```