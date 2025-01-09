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
int *a, arraySize = 5;
a = (int*)malloc(arraySize * sizeof(int));
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
A dangling pointer can occur when a sequence of memory has been freed prior to use. This means that the data it references will not longer be valid, leading to unpredictable behavior once that memory is accessed. One way to prevent this issue is by setting the pointer that was freed and pointing to the first element of the sequence, to `NULL`.

```
    int *a, arraySize = 5;
    a = (int*)malloc(arraySize * sizeof(int));
    free(a);
    a = NULL;
```

## 5. The `realloc()` function
The `realloc()` function may be used to reallocate dynamic memory. The memory must have previously been allocated using `malloc()`, `calloc()`, or `realloc()`, and must not yet be freed. `realloc()` requires two arguments 1) `void * ptr` a pointer to the memory area to be reallocated and 2) `size_t new_size` the new size of the array in bytes. 

In the example code below, `realloc()` is used to dynamically allocate memory to `int *tmp` with `newSize = size + 2` using the contents provided in `int *a`. The function `realloc()`  dynamically allocates memory of size `newSize * sizeof(int)` for `*tmp`, copies the contents from `*a` to `*tmp`, and frees the memory allocated to `*a`. I then initialize `tmp[newSize - 2]` and `tmp[newSize - 1]`. I also attempt to print the values of `*a`, which should have been freed at this point. Notice that the previous array values are random values -- this is because `*a` was not set to `NULL`. 

```
    int *a, size = 5;
    a = (int*)calloc(size, sizeof(int));
    printf("Initializing array: ");
    for(int i = 0; i < size; i++){
        a[i] = i + 1;
        printf("%d ", a[i]);
    }
    
    printf("\nReallocate array: ");
    int *tmp, newSize = size + 2;
    tmp = (int*)realloc(a, newSize * sizeof(int));
    tmp[newSize - 2] = 6;
    tmp[newSize - 1] = 7;
    for(int i = 0; i < newSize; i++){
        printf("%d ", tmp[i]);
    }
    
    printf("\nPrevious array: ");
    for(int i = 0; i < newSize; i++){
        printf("%d ", a[i]);
    }
```

```
Initializing array: 1 2 3 4 5 
Reallocate array: 1 2 3 4 5 6 7 
Previous array: 59597 0 -633097145 -1562072072 5 0 1041 
```