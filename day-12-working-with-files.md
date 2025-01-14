# Day 12: Review of Working with Files in C
#c-fundamentals 
## What is a File?
- A stream of bytes, generally stored in nonvolatile memory. 
- Types: Text files, binary files
- When a file is opened, a communication channel is created that allows the user to read and/or write to the file

## Example:

###  1. Create a pointer of a `FILE` type:
```
FILE *fp;
```

- *Note: `FILE` is a `struct` dedicated to working with files and defined in `<stdio.h>` as:* 
```
typdef struct _iobuf
{
	void* _Placeholder_;
} FILE;
```

### 2. Open/Access the File `fopen`, Defined in `<stdio.h>`:
- `<file_name>` is the path to the file.
- `<type_of_operation>` specifies whether to read, write, or append to the file. Other modes exist (where can this be found?).
	- `"w"`: Write to file. This operation will create a new file if the file does not exist, or will override a file if it already exists.
	- `"r"`: Read from file. If attempting to read from a file that does not exist, opening the file will fail. 
	- `"a"`: Append to file. 

```
// fp = fopen(<file_name>,<type_of_operation>);
fp = fopen("file.txt", "w");
```

### 3. Check if `fopen()` was Successful and Work with the File:
```
if(fp == NULL){
	printf("The file failed to open.");
}
else{
	printf("The file has been opened.");
	// Work with the file here.
}
```

### 4. Close the File:
This function will go inside the `else` statement in (3). 
```
fclose(fp);
```

## Common Functions when Working with Files: 
### 1. `int fgetc(FILE *stream)`
- Receives pointer to file as argument
- Abbreviation of file get character
- Gets a single character and can be used to assign a character to a variable
###### Example:
`file.txt`:
```
Hello World
```

```
    FILE *fp = fopen("file.txt", "r");
    char myChar;
    if(fp == NULL){
        printf("Failed to open file.\n");
    }
    else{
        printf("Succesfully opened file.\n");
        myChar = fgetc(fp);
        printf("myChar = %c\n", myChar);
        myChar = fgetc(fp);
        printf("myChar = %c\n", myChar);
        fclose(fp);
        printf("Succesfully closed file.\n");
    }
```

`Output`:
```
Succesfully opened file.
myChar = H
myChar = e
Succesfully closed file.
```

### 2. `int fputc(int char, FILE *stream)`
- Receives character literal and `FILE` pointer as arguments
- Abbreviation of *file put character*
- Writes character to file
###### Example:
```
    FILE *fp = fopen("file.txt", "w");
    char myChar;
    if(fp == NULL){
        printf("Failed to open file.\n");
    }
    else{
        printf("Succesfully opened file.\n");
        fputc('H', fp);
        fputc('i', fp);
        fputc('!', fp);
        fclose(fp);
        printf("Succesfully closed file.\n");
    }
```

`file.txt`
```
Hi!
```

`Output:`
```
Succesfully opened file.
Succesfully closed file.
```

### 3. `int fprintf(FILE *stream, const char *format,  ... )`
- Receives `FILE` pointer, format specifier(s), and *additional argument(s)* corresponding to format specifier(s) as arguments
- Writes formatted data to a specified stream, determined by the `FILE` pointer

###### Format Specifiers, `%specifier`:
| specifier | Output                                                                                                                                                              | Example      |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ |
| d _or_ i  | Signed decimal integer                                                                                                                                              | 392          |
| u         | Unsigned decimal integer                                                                                                                                            | 7235         |
| o         | Unsigned octal                                                                                                                                                      | 610          |
| x         | Unsigned hexadecimal integer                                                                                                                                        | 7fa          |
| X         | Unsigned hexadecimal integer (uppercase)                                                                                                                            | 7FA          |
| f         | Decimal floating point, lowercase                                                                                                                                   | 392.65       |
| F         | Decimal floating point, uppercase                                                                                                                                   | 392.65       |
| e         | Scientific notation (mantissa/exponent), lowercase                                                                                                                  | 3.9265e+2    |
| E         | Scientific notation (mantissa/exponent), uppercase                                                                                                                  | 3.9265E+2    |
| g         | Use the shortest representation: %e or %f                                                                                                                           | 392.65       |
| G         | Use the shortest representation: %E or %F                                                                                                                           | 392.65       |
| a         | Hexadecimal floating point, lowercase                                                                                                                               | -0xc.90fep-2 |
| A         | Hexadecimal floating point, uppercase                                                                                                                               | -0XC.90FEP-2 |
| c         | Character                                                                                                                                                           | a            |
| s         | String of characters                                                                                                                                                | sample       |
| p         | Pointer address                                                                                                                                                     | b8000000     |
| n         | Nothing printed.  <br>The corresponding argument must be a pointer to a signed int.  <br>The number of characters written so far is stored in the pointed location. |              |
| %         | A % followed by another % character will write a single % to the stream.                                                                                            | %            |

###### Example:
```
    FILE *fp = fopen("file.txt", "w");
    const char name[3] = "Kat";
    int day = 12, daysInYear = 365;
    
    if(fp == NULL){
        printf("Failed to open file.\n");
    }
    else{
        printf("Succesfully opened file.\n");
        fprintf(fp, "Hello world! My name is %s.\n", name);
        fprintf(fp, "Today is day %d of my %d days of code challenge.\n", day, daysInYear);
        fprintf(fp, "The date is %s.\n", __DATE__);
        fclose(fp);
        printf("Succesfully closed file.\n");
    }

```

`file.txt`
```
Hello world! My name is Kat.
Today is day 12 of my 365 days of code challenge.
The date is Jan 12 2025.
```

`Output`:
```
Succesfully opened file.
Succesfully closed file.
```

### 4.`int fscanf(FILE *stream, const char *format, ...)`
- Receives `FILE` pointer, string consisting of format specifiers, and *additional argument(s)* corresponding to format specifier(s) as arguments
- Reads formatted input data from a specified stream, determined by the `FILE` pointer
- Allows extraction and parsing of data from a file

###### Example:
`file.txt`:
```
5
```

```
    FILE *fp = fopen("file.txt", "r");
    int num;
    if(fp == NULL){
        printf("Failed to open file.\n");
    }
    else{
        printf("Succesfully opened file.\n");
        fscanf(fp, "%d", &num);
        printf("num from `file.txt` = %d\n", num);
        fclose(fp);
        printf("Succesfully closed file.\n");
    }
```

`Output`:
```
Succesfully opened file.
num from `file.txt` = 5
Succesfully closed file.
```

### 5. `int fputs(const char *str, FILE *stream, )
- Receives string or array of `char` and `FILE` pointer as arguments
- Writes the C string pointed by `str` to  `stream`.
- Does ***not*** add a `"\n"` automatically at the end of the string

###### Example:
`file.txt`
```
HelloWorld!!!
```

```
    FILE *fp = fopen("file.txt", "w");
    if(fp == NULL){
        printf("Failed to open file.\n");
    }
    else{
        printf("Succesfully opened file.\n");
        fputs("HelloWorld!!!", fp);
        fclose(fp);
        printf("Succesfully closed file.\n");
    }
```

`Output`:
```
Succesfully opened file.
Succesfully closed file.
```

### 6. `char fgets(char *str, int num, FILE *stream)`
- Receives string or array of `char`,  number of characters `num`, and `FILE` pointer to `stream` as arguments
- Reads characters from `stream` and stores them as a C string into `str` until `num`-1 characters have been read or either a newline or the end-of-file is reached

###### Example:
`file.txt`
```
Hello World! My name is Kat.
How are you?
This is now the third line of the text file.
And this is the last line!

```

```
    FILE *fp = fopen("file.txt", "r");
    int num = 50, count = 0;
    char str[num];
    if(fp == NULL){
        printf("Failed to open file.\n");
    }
    else{
        printf("Succesfully opened file.\n");
        while(fgets(str, num, fp)){
            printf("Line %d: %s", ++count, str);
        }
        
        fclose(fp);
        printf("Succesfully closed file.\n");
    }
```

`Output`:
```
Succesfully opened file.
Line 1: Hello World! My name is Kat.
Line 2: How are you?
Line 3: This is now the third line of the text file.
Line 4: And this is the last line!
Succesfully closed file.
```

## File Streams Provided by `stdio.h`:
- `stdin`: pointer of type `FILE *` used to receive input from the user or another program
	- Example: `scanf()`, `getchar()`, `fgets()`
```
    char name[50];
    printf("Enter your name: ");
    fgets(name, 50, stdin);  // Read input from stdin (keyboard by default)
    printf("Hello, %s", name);
```

- `stdout`: pointer of type `FILE *` send output to the user (via terminal) or another program
	- Example: `printf()`, `puts`
	
- `stderr`: pointer of type `FILE *` used to send error messages or diagnostic output
```
    FILE *file = fopen("nonexistent.txt", "r");
    if (file == NULL) {
	    // Prints error to stderr
        fprintf(stderr, "Error: Could not open file.\n");  
        return 1;
    }
    fclose(file);
```

## Other Notes:
- `\0`: specifier used to determine the end of a string
 Example:
```
    const char str[20] = "Hello World!";
    int i = 0;
    while(str[i] != '\0'){
        printf("str[%d] = %c\n", i, str[i]);
        i++;
    }
```

`Output`:
```
str[0] = H
str[1] = e
str[2] = l
str[3] = l
str[4] = o
str[5] =  
str[6] = W
str[7] = o
str[8] = r
str[9] = l
str[10] = d
str[11] = !
```

- `EOF`: specifier used to determine the end of a file
 Example:
```
	while(myChar = fget(fp) != EOF){
		// Code for processing file
	}
```

- `FEOF`: file end of file
Example: 
```
	while(!feof(fp)){
		// Code for processing file
	}
```