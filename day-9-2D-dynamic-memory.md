# Day 9: 2D Dynamic Memory
#c-fundamentals 
## 1. Creating An Array of Pointers
To create a static array of pointers, I declare an array `int *a[SIZE]`, where the number of elements is defined as `#define SIZE 4`. I dynamically allocate memory using the `calloc()` function, and assign the starting address to each pointer in `*a`. Keep in mind that `sizeof(int*)`, or the size of a pointer, depends on the machine architecture. On the machine I run and compile this code on, `sizeof(int*)` is 8 bytes or 64 bits. 

```
int *a[SIZE];
for(int i = 0; i < SIZE; i++){
    a[i] = (int*) calloc(i+1, sizeof(int*));
}
```

This creates a 2D array with the following structure:

```
Stack:
+-----------+        +-------------------+
| a[0]      | -----> | 0                 |
+-----------+        +-------------------+
| a[1]      | -----> | 0 | 0             |
+-----------+        +-------------------+
| a[2]      | -----> | 0 | 0 | 0         |
+-----------+        +-------------------+
| a[3]      | -----> | 0 | 0 | 0 | 0     |
+-----------+        +-------------------+

Heap (dynamically allocated memory):
- heap[0] contains 1 integer initialized to 0 (size = `i + 1 = 1`).
- heap[1] contains 2 integers initialized to 0 (size = `i + 1 = 2`).
- heap[2] contains 3 integers initialized to 0 (size = `i + 1 = 3`).
- heap[3] contains 4 integers initialized to 0 (size = `i + 1 = 4`).
```

- Row 0 contains 1 column, accessed using `a[0][0]`
- Row 1 contains 2 columns, accessed using `a[1][0]` and `a[1][1]`
- Row 2 contains 3 columns, accessed using `a[2][0]`, `a[2][1]`, and `a[2][2]`
- Row 3 contains 4 columns, accessed using `a[3][0]`, `a[3][1]`, `a[3][2]`, and `a[3][3]`


## 2. Creating a (Completely) Dynamically Allocated 2D Array
Creating a dynamically allocated 2D array is similar to (1), except that `a` is now declared as a double pointer. Say that I define two constants using `#define ROW_SIZE 5` and `#define COL_SIZE 5`. I dynamically allocate memory of size `ROW_SIZE * sizeof(int*)` using the `calloc()` function. I then iterate through each row in `**a` and dynamically allocate memory of size `COL_SIZE * sizeof(int)`. 

```
int **a = (int**)calloc(ROW_SIZE, sizeof(int*));
for(int i = 0; i < ROW_SIZE; i++){
	a[i] = (int*)calloc(COL_SIZE, sizeof(int));
}
```

This creates a dynamically allocated 5x5 array of integers:

```
Level 1: Array of Pointers (ROW_SIZE = 5)
a --> +-------+       +-------+              
       | a[0]  | ---> | Row 0 |         
       +-------+       +-------+    
       | a[1]  | ---> | Row 1 | 
       +-------+       +-------+   
       | a[2]  | ---> | Row 2 |
       +-------+       +-------+      
       | a[3]  | ---> | Row 3 |       
       +-------+       +-------+    
       | a[4]  | ---> | Row 4 |
       +-------+       +-------+
       
Level 2: Matrix Data (COL_SIZE = 5, all values initialized to 0)
Row 0 --> +---+---+---+---+---+
          | 0 | 0 | 0 | 0 | 0 |
          +---+---+---+---+---+
Row 1 --> +---+---+---+---+---+
          | 0 | 0 | 0 | 0 | 0 |
          +---+---+---+---+---+
Row 2 --> +---+---+---+---+---+
          | 0 | 0 | 0 | 0 | 0 |
          +---+---+---+---+---+
Row 3 --> +---+---+---+---+---+
          | 0 | 0 | 0 | 0 | 0 |
          +---+---+---+---+---+
Row 4 --> +---+---+---+---+---+
          | 0 | 0 | 0 | 0 | 0 |
          +---+---+---+---+---+
```