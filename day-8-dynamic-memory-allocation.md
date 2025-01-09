# Dynamic Memory Allocation
The two functions used to allocate memory are `malloc()` and `calloc` provided in the C  `stdlib` library.
## 1. The `malloc()` Function
`malloc()` is a function that allocates a **sequence of bytes** and returns the address of the first byte in the sequence. The function takes in a number of bytes as an argument, and allows the user to work with and modify data stored within an allocated sequence.

Note that `malloc()` returns a `void*` pointer, which means that for some compilers, the return value must be cast to a data type. For example -- in the code below, I cast the output of `malloc()` to an `int*` in order to specify the type of data that the pointer is pointing to.  However, most modern compilers may not need the cast to data type, and casting is simply good practice.

```
int *a, arraySize = 5;
a = (int*) malloc(sizeof(int)) * arraySize);
```

### Implement a Function that Creates and Returns a Dynamically Allocated Array

Keep in mind that this memory will exist until it is freed. This can become an issue that results in a memory leakage.
```
int *createArray(){
    int *myArray = (int*)malloc(SIZE * sizeof(int));
    if(myArray == NULL){
        printf("Memory could not be allocated. Exiting..");
        return 0;
    }
    printf("Enter element value: \n");
    for(int i = 0; i < SIZE; i++){
        printf("myArray[%d] = ", i);
        scanf("%d", &myArray[i]);
    }
    return myArray;
}
```

## 2. The `calloc()` function
`calloc()` is very similar to `malloc()` in that both functions can be used to 1) dynamically allocate memory and 2) return the address of the first byte in the allocated memory. A key difference is that `calloc()` sets all elements in the allocated memory to 0. Another difference is that `calloc()` expects to receive two arguments `size_t num`, *specifying the number of elements*, and `size_t size` *which specifies the size of each element*. 

```
    int *a, arraySize = 5;
    a = (int*)calloc(arraySize, sizeof(int));
```

## 3. The `free()` function
Anytime memory is dynamically allocated, it will remain in main memory until freed - the `free()` function may be used to release this dynamically allocated memory. To use the `free()` function, simply pass the address to the first element of the sequence that needs to be freed. For example, the memory allocated by `calloc()` in (2), can be freed by simply using the line of code below:

```
free(a);
```

#### **Common errors when using `free()`:**
- `free()` cannot be used to free portions of the dynamically allocated memory (e.g. `free(a+1)` would not work). The entire allocated sequence must be freed. 

```
int *a = (int*)malloc(sizeof(int)*5);
free(a+1); // This would not work
```

- `free()` cannot be used on a statically allocated array 
```
int *a;
free(a); // This is not valid
```

## 4. The Dangling Pointer
A dangling pointer can occur when a sequence of memory has been freed prior to use. One way to prevent this issue is by setting the pointer that was initially pointing to the first element of the sequence, to `NULL`.