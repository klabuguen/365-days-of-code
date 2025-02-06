# Day 36: Review of the C Preprocessor
#c-fundamentals 
## Overview

The preprocessor is a program that is invoked by the compiler in order to process C source code prior to compilation. It performs simple text replacements and macro expansions for preprocessor commands known has directives. Preprocessor directives begin with the hash symbol (#). 

![[/images/preprocessor.png]]

An example of a common preprocessor directive is the #include command which is used to include header files. 

## Preprocessor Directives

| Directive | Description                                                                       |
| --------- | --------------------------------------------------------------------------------- |
| #define   | Substitutes a preprocessor macro, similar to declaring constants                  |
| #include  | Inserts a particular header from another file                                     |
| #undef    | Undefines a preprocessor macro, useful to effectively change a macro's definition |
| #ifdef    | Returns true if this macro is defined                                             |
| #ifndef   | Returns true if this macro is not defined                                         |
| #if       | Tests if a compile time condition is true                                         |
| #else     | The alternative to the previous #if                                               |
| #elif     | Abbreviation of #else and #if in one statement                                    |
| #endif    | Ends preprocessor conditional                                                     |
| #error    | Prints error message on stderr                                                    |
| #pragma   | Issues special commands to the compiler                                           |

## Predefined Macros

| Macro     | Description                                                      |
| --------- | ---------------------------------------------------------------- |
| \__DATE__ | The current date as a string literal in "MMM DD YYYY" format     |
| \__TIME__ | The current time as a string literal in "HH:MM:SS" format        |
| \__FILE__ | The current filename as a string literal                         |
| \__LINE__ | The current line number as an integer                            |
| \__STDC__ | The value is 1 when the compiler complies with the ANSI standard |


## Examples

#### 1. Simple Macros

```
#include <stdio.h>
#include <stdlib.h>

#define ARRAY_LEN 100

int main(){

	printf("\n=== Simple Macros ===\n\n");

	double array[ARRAY_LEN];
	printf("Array length: %d\n", ARRAY_LEN);

#undef ARRAY_LEN
#define ARRAY_LEN 999

	printf("New array length: %d\n", ARRAY_LEN);
	
	printf("Source file: \"%s\", %d\n", __FILE__, __LINE__);
	printf("Compilation time: %s\n", __TIME__);
	
	return EXIT_SUCCESS;
	
}
```

In the code above, I use the #define command to define a custom macro, `ARRAY_LEN` that is set equal to `100`. The `ARRAY_LEN` macro is then undefined and re-defined to a value of `999`. The program also prints the values of the predefined macros `__FILE__`, `__LINE__` and `__TIME__`. 

#### 2. Macros with Arguments

```
#include <stdio.h>
#include <stdlib.h>

#define ARRAY_LEN 100
#define CALC_ARRAY_LEN(x) (sizeof(x) / sizeof(x[0]))
#define MAX(a, b) (a > b ? a : b)

int main(){

	printf("\n=== Function Like Macros ===\n\n");

	double array[ARRAY_LEN];
	printf("Array length: %d\n", ARRAY_LEN);

	int array_len = CALC_ARRAY_LEN(array);
	printf("Calculated array length: %d\n", array_len);

	int a = -1, b = 5;
	printf("MAX(%d, %d) = %d\n", a, b, MAX(a, b));

	int b_before = b;
	printf("MAX(%d, %d): %d\n", a, b_before, MAX(a, b++));
	printf("b before increment: %d\n", b_before);
	printf("b after increment: %d\n", b);
		
	return EXIT_SUCCESS;
	
}
```

In this example, I define two function-like macros, `CALC_ARRAY_LEN(x)` and `MAX(a,b)`, capable of taking in arguments. 

- `CALC_ARRAY_LEN(x)` determines the length of any given array, `x`. 
- `MAX(a,b)` is used to compare and calculate the max value between two numbers `a` and `b`. 

Issues may arise in which a macro may perform in an unintentional way. For example, `MAX(a,b++)` expands to `a > b++ ? a : b++`. This leads to the value of `b` incrementing twice, though one would have expected it to increment only once. 


#### 3. Conditional Compilation

```
#include <stdio.h>
#include <stdlib.h>

#define LOG_INFO
// #define BUFFER_SIZE 1024

int main(){
	printf("\n=== Conditional Compilation ===\n\n");
	
#ifdef SOME_MACRO
	printf("SOME_MACRO exists\n);
#endif 

#ifdef LOG_INFO
	printf("This is an INFO LOG!");
#else
	printf("Do not LOG any info!");
#endif 

#if BUFFER_SIZE > 2048
	printf("The buffer is huge, do something!\n");
#else 
	printf("The buffer is ok\n");
#endif

	return EXIT_SUCCESS;

}
```

The conditional compilation directives are used to designate parts of the program that the compiler can ignore. For example, `SOME_MACRO` does not exist, which means `printf("SOME_MACRO exists\n")` will be ignored by the compiler. However, because `LOG_INFO` is defined, the compiler will compile `printf("This is an INFO LOG!")` and ignore `printf("Do not LOG any info!")`. 

Finally, the preprocessor directive `#if BUFFER_SIZE > 2048` tells the compiler to compile `printf("The buffer is huge, do something!\n")` only when `BUFFER_SIZE` is greater than `2048`.  

```
#if defined BUFFER_SIZE && BUFFER_SIZE > 2048
	printf("The buffer is huge, do something!\n");
#elif defined BUFFER_SIZE 
	printf("The buffer is ok\n");
#else 
	printf("You forgot to define BUFFER_SIZE!\n");
#endif
```

The code snippet above uses the preprocessor directives `#if` to first determine whether or not `BUFFER_SIZE` exists, *then* checks if `BUFFER_SIZE` is greater than 2048. Using `elif`, if `BUFFER_SIZE` exists but is less than or equal to 2048, then `printf("The buffer is ok\n")` will be compiled. Otherwise, if `BUFFER_SIZE` is not defined, the line `printf("You forgot to define BUFFER_SIZE!\n")` will be compiled. 