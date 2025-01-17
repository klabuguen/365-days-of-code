# Day 10: 2D Dynamic Memory Exercises
#c-fundamentals 
## 1. Create a Function that Creates a Dynamically Allocated 2D Matrix
*Implement a function that creates a dynamically allocated 2D matrix.*

There are multiple ways of implementing a function that creates a dynamically allocated 2D matrix. I give two examples: one that **returns** the 2D matrix and another that takes in a triple pointer as an argument then allocates memory for the 2D matrix to it.
#### **Return the 2D Array:**
In the function below, I return the dynamically allocated 2D array. 
```
int **allocate2DMatrix(int rowSize, int colSize){
    int **a = (int**)calloc(rowSize, sizeof(int*));
    for(int i = 0; i < rowSize; i++){
        a[i] = (int*)calloc(colSize, sizeof(int));
    }
    return a;
}
```

#### **Pass the 2D Array by Reference:**
```
void allocate2DMatrixRef(int ***a, int rowSize, int colSize){
    *a = (int**)calloc(rowSize, sizeof(int*));
    for(int i = 0; i < rowSize; i++){
        (*a)[i] = (int*)calloc(colSize, sizeof(int));
    }
}
```

 #### **VERY IMPORTANT: Common Error:**
 - `(*a)[0]` vs `*a[0]`: When I originally wrote this code, I was running into a `Segmentation Fault`. I found that the error was due to accessing `*a[i]` -- which dereferences the value stored in `a[i]` -- rather than dereferencing the pointer `***a` then accessing the element at `i`. 
## 2. Create a Function that Initializes a 2D Matrix
*Implement a function that initializes a dynamically allocated 2D matrix.*

I wrote a simple function that initializes a 2D matrix by adding the current value of `i` to the current value `j`. The function `init2DMatrix()` takes a triple pointer, or reference to 2D matrix, as well as the row and column size.  It then iterates through each (row, col) pair in the 2D matrix to initialize the values. 

```
void init2DMatrix(int ***a, int rowSize, int colSize){
    for(int i = 0; i < rowSize; i++){
        for(int j = 0; j < colSize; j++){
            (*a)[i][j] = i + j;
        }
    }
}
```

## 3. Create a Function that Prints a 2D Matrix
*Implement a function that prints the values in a dynamically allocated 2D matrix.*

The `print2DMatrix()` function takes the double pointer `int **a`, as well as row and column sizes. It then iterates through each (row, col) pair in the 2D matrix and prints the value.

Keep in mind that `int **a` is a sufficient argument *(instead of `int ***a`)* to the function because the 2D matrix is not modified by the function -- I simply access the elements in the matrix and print them. 

```
void print2DMatrix(int **a, int rowSize, int colSize){
    printf("Printing matrix:\n");
    for(int i = 0; i < rowSize; i++){
        printf("[ ");
        for(int j = 0; j < colSize; j++){
            printf("%d ", j);
        }
        printf("]\n");
    }
}
```

## 4. Create a Function that Frees the Dynamically Allocated 2D Matrix
*Implement a function that frees the memory of a dynamically allocated 2D matrix.*

One may think that freeing the dynamically allocated 2D matrix is as simple as calling the `free()` function. This is untrue, however, because calling `free()` on the 2D matrix will only free the array of pointers, but will not free the memory allocated for each column in the matrix. 

**This is incorrect:**
```
int **a = (int**)calloc(rowSize, sizeof(int*));
for(int i = 0; i < rowSize; i++){
	// Allocate memory for each column
	a[i] = (int*)malloc(colSize, sizeof(int));
}

// Attempt to free memory
free(a); // This is incorrect
```

#### The proper way to free memory allocated to the 2D matrix:
In the implementation below, the function `free2DMatrix()` requires 2 arguments: *1) a triple pointer to the 2D matrix and 2) the rowSize*. I iterate through each row, free the memory allocated in each `free((*a)[i])`, then free the memory allocated for the array of pointers `free(*a)`. 

Note that it *is* possible to free the dynamically allocated memory by using a double pointer (e.g. `int **a)`, but this could result in a dangling pointer. Remember that it is a best practice to set the pointer to `NULL` as soon as it is freed, as demonstrated in the code below, setting `(*a) == NULL`.

```
void free2DMatrix(int ***a, int rowSize){
    for(int i = 0; i < rowSize; i++){
        free((*a)[i]);
    }
    free(*a);
    (*a) = NULL;
}
```

#### **Alternative method, using a double pointer:**
I included an alternative method below, using the double pointer `int **a` as an argument to `free2DMatrix()`. It's possible to free the memory allocated for the 2D array, but it is not possible to update the original starting address of the previously allocated memory to `NULL`.

```
 void free2DMatrix(int **a, int rowSize){
	 for(int i = 0; i < rowSize; i++){
		 free(a[i]);
	 }
	 free(a);
	 // However - unable to set a = NULL
}
```

## 5. `main()` Example Using Functions

```
int main() {
    int **a, **b, rowSize = 5, colSize = 5;
    
    // Allocate 2D Matrix using allocate2DMatrix()
    printf("Using allocate2DMatrix():\n");
    a = allocate2DMatrix(rowSize, colSize);
    init2DMatrix(&a, rowSize, colSize);
    print2DMatrix(a, rowSize, colSize);
    
    // Allocate 2D Matrix using allocate2DMatrixRef()
    printf("\nUsing allocate2DMatrixRef():\n");
    allocate2DMatrixRef(&b, rowSize, colSize);
    init2DMatrix(&b, rowSize, colSize);
    print2DMatrix(&b, rowSize, colSize);
    
    // Free the memory allocated for the 2D matrices
    free2DMatrix(&a, rowSize);
    free2DMatrix(&b, rowSize);
    
    return 0;
}
```

```
Using allocate2DMatrix():
Printing matrix:
[ 0 1 2 3 4 ]
[ 1 2 3 4 5 ]
[ 2 3 4 5 6 ]
[ 3 4 5 6 7 ]
[ 4 5 6 7 8 ]

Using allocate2DMatrixRef():
Printing matrix:
[ 0 1 2 3 4 ]
[ 1 2 3 4 5 ]
[ 2 3 4 5 6 ]
[ 3 4 5 6 7 ]
[ 4 5 6 7 8 ]


=== Code Execution Successful ===
```


# More 2D Dynamic Memory Practice:

## 1. Implement two functions that 1) Swap two rows and 2) Swap two columns. Both functions must receive a dynamic 2D array. 

**Swap Two Rows:**
```
void swap2DMatrixRows(void **a, int row1, int row2){
    void *tmp = a[row1];
    a[row1] = a[row2];
    a[row2] = tmp;
}
```

*Output*
```
Swapping Rows:
Printing matrix:
[ 3 4 5 6 7 ]
[ 1 2 3 4 5 ]
[ 2 3 4 5 6 ]
[ 0 1 2 3 4 ]
[ 4 5 6 7 8 ]
```

**Swap Two Columns:**
Unlike the solution above I implemented to swap two rows, there is no clever trick to swapping two columns. In the solution below, I swap two columns with one another by swapping the values in the two columns `a[i][col1]` and `a[i][col2]`. 

```
void swap2DMatrixCols(int **a, int rowSize, int col1, int col2){
    for(int i = 0; i < rowSize; i++){
        int tmp = a[i][col1];
        a[i][col1] = a[i][col2];
        a[i][col2] = tmp;
    }
}
```

*Output*
```
Swapping Columns:
Printing matrix:
[ 0 4 2 3 1 ]
[ 1 5 3 4 2 ]
[ 2 6 4 5 3 ]
[ 3 7 5 6 4 ]
[ 4 8 6 7 5 ]
```