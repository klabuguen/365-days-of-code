# Day 13: Point Operator
#image-processing-fundamentals 

Note: Need to update image processing sections, currently working out of
https://github.com/klabuguen/c-dsp/tree/main/image-processing 
## 1. Arithmetic Operations
Arithmetic operations, or *point operators*, describe image processing transforms where an output pixel value depends only on the associated input pixel value. Brightness, color correction, and contrast adjustments are examples of point operators. 

### Theory
An **operator** is a function that takes in one or more input images and produces an output image:
$$
Equation\ 1.1: \ g(x)=h(f(x)) \ or \ g(x)=g(f_0(x),...,f_n(x))
$$
where $g(x)$, $f(x)$, and $h(x)$ are continuous and $x$ is in the D-dimension (D=2 for images). 

In discrete/sampled images, the domain exists within the number of pixel locations $x = (i,j)$, in which the equation above can be written as:
$$
Equation\ 1.2: \ g(i,j)=h(f(i,j))
$$

Commonly used operators are addition and multiplication:
$$
Equation\ 1.3: \ g(x) = af(x)+ b
$$
where $a$ is referred to as the *gain* parameter which controls the *contrast*, and $b$ is the *bias* parameter that controls *brightness*. 

### Example
##### 1. Adjusting the Brightness of the Image
The code example below is one way of brightening an image.
1. Image data is read into `buffer` using `fread()`
2. I loop through each pixel and add the brightness offset to the current pixel value
3. If the sum of the current pixel value and brightness offset are greater than the max color value of 255, then I set the current buffer value to `WHITE`. Otherwise, I set the current pixel value to `tmp`

```
fread(buffer, sizeof(unsigned char), IMG_SIZE, imgIn);

printf("Applying brightness to image.\n");

for(int i = 0; i < IMG_SIZE; i++){
	unsigned char tmp = buffer[i] + BRIGHTNESS;
	buffer[i] = (tmp < WHITE) ? tmp : WHITE;
}

fwrite(buffer, sizeof(unsigned char), IMG_SIZE, imgOut);
```

