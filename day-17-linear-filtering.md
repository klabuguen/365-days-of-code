# Day 17: Linear Filtering
#image-processing-fundamentals 
## Linear Filtering Theory
Linear filtering operators use fixed weighted combinations of pixels in small neighbors to apply enhancements to an image. Linear filters are the most widely used type of neighborhood operators and may be described using the following equation:
$$
g(i,j)=\sum_{k,l}f(i+k,j+l)h(k,l)
$$
The weight kernel $h(k,l)$ contains the filter coefficients (or weights) used in linear filtering. The equation above, known, as the *correlation operator* is also described as:
$$
g=f\otimes h
$$The formula may also be written as:
$$
g(i,j)=\sum_{k,l}f(i-k,j-l)h(k,l)=\sum_{k,l}f(k,l)h(i-k,j-l)
$$
where $f$ is now a function of $i-k, j-l$. This is known as the convolution operator:
$$
g=f\ast h
$$
where $h$ is the *impulse response function*. 

## Examples
### 1. 2D Moving Average Filter
Applying a 3x3 moving average kernel to a 2D 5x5 array.
###### 5x5 array:
```
  1   2   3   4   5
  6   7   8   9  10
 11  12  13  14  15
 16  17  18  19  20
 21  22  23  24  25
```
###### 3x3 kernel:
```
 1/9  1/9  1/9
 1/9  1/9  1/9
 1/9  1/9  1/9
```

#### Steps:
1. The first step is to apply the kernel to the top-left 3x3 neighborhood, or sub-matrix. 
```
[1   2   3 ]  4   5 
[6   7   8 ]  9  10 
[11  12  13] 14  15 
 16  17  18  19  20 
 21  22  23  24  25 
```
$Sum = \frac{1}{9}*1+\frac{1}{9}*2+\frac{1}{9}*3+\frac{1}{9}*6+\frac{1}{9}*7+\frac{1}{9}*8+\frac{1}{9}*11+\frac{1}{9}*12+\frac{1}{9}*13$
or
$Sum=\frac{1}{9}(1+2+3+6+7+8+11+12+13)=\frac{63}{9}=7$

2. Next, slide right and apply the kernel to the next neighborhood to the right of the current neighborhood.
```
 1   [2   3   4]   5 
 6   [7   8   9]  10 
 11  [12  13 14]  15 
 16  17  18  19   20 
 21  22  23  24   25 
```
$Sum = \frac{1}{9}*2+\frac{1}{9}*3+\frac{1}{9}*4+\frac{1}{9}*7+\frac{1}{9}*8+\frac{1}{9}*9+\frac{1}{9}*12+\frac{1}{9}*13+\frac{1}{9}*14$
or
$Sum=\frac{1}{9}(1+2+3+6+7+8+11+12+13)=\frac{72}{9}=8$

The process will then repeat for the entire matrix. The final result is:
```
  7   8   9 
 12  13  14 
 17  18  19 
```

#### Code:
Code goes here

### 2. Sepia Filter

