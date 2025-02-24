# Day 25: Convert a Float to a String
#c-fundamentals 

**Write a Function that Converts a Float to a String**. The following signature is provided:

```
int myFtoa(char *bufferOut, float value, size_t size, int precision);
```

- `char *bufferOut`: character array used to store the resulting string
- `float value`: variable that stores the float that must be converted to a string
- `size_t size`: size of `bufferOut`
- `int precision`: number of decimal places include in `bufferOut`
## Steps:
1. Check for invalid parameters (`bufferOut == null`, `size ==0,` or `precision < 0`) then `return -1` if they are present
2. Handle negative numbers (keep track with `bool isNegative`)
3. Convert the integer part directly
4. Determine the fractional part with the following formula:  $fractPart = value - intPart$
5. Count the digits in the integer part
6. Determine required buffer space, if allocated size is too small then `return -1` (can use formula:  $minBufferSpace = isNegative + numIntDigits + decimalPoint + precision + 1$, where added 1 is for null terminator
7. Add negative sign if necessary
8. Convert integer part manually
9. If no precision, place `\0` in buffer and return number of characters written
10. To process precision, add the decimal point
11. Convert the fractional part
12. Null terminate the string
13. Return the number of characters written


```
int myFtoa(char *bufferOut, float value, size_t size, int precision){
    if(bufferOut == NULL || size == 0 || precision < 0){
        return -1; // Invalid parameters
    }

    bool isNegative;
    size_t i = 0;

    // Handle negative float
    if(value < 0) {
        isNegative = true;
        bufferOut[i] = '-';
        value *= -1;
    }

    // Extract integer and fractional parts
    int intPart = (int) value;
    float fracPart = value - intPart;

    // Convert integer part to string
    int tmpInt = intPart, intLength = 0;
  
    // Manually determine integer length
    while(tmpInt != 0){
        tmpInt /= 10;
        intLength++;
    }
  
    // Check for buffer overflow
    if(i + intLength >= size) return -1;

    // Write each integer digit to buffer
    for(size_t j = intLength - 1; j >= 0; j--){
        bufferOut[i + j] = (intPart % 10) + '0';
        intPart /= 10;
    }

    i += intLength;

    // Handle decimal point
    if(precision > 0){
        bufferOut[i] = '.';
        i++;
    }

    // Convert fractional part
    int digit = 0;

    for(size_t j = 0; j < precision; j++){
        fracPart *= 10;
        digit = (int)fracPart;
        fracPart -= digit;
        bufferOut[i] = digit + '0';
        i++;
    }

    bufferOut[i] = '\0';
    return i;
}
```