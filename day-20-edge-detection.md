# Day 20: Edge Detection
#image-processing-fundamentals 
## Introduction
In image processing, an **edge** is generally defined as a region within an image where there are discontinuities, corresponding to significant changes in pixel intensity. **Edge detection** is a method used to identify the boundaries between different objects in an image. In the next few days of this week, I'll be going more in-depth about common edge detection techniques, such as the Sobel operator, Prewitt operator, Robinson operator, Kirsch operator, Laplacian operator, and Robert operator. 

Today, I reviewed a simple example and implemented it in C: the Line detector. 
## Line Detection Operator
The line detection operator relies on the four kernels below (tuned for light lines against dark backgrounds), necessary for detecting 1) horizontal, 2) +45 degree, 3) vertical, and 4) -45 degree lines. The operator is applied by convolving an image with each of the kernels. 

```
horizontal          +45           vertical          -45
[-1 -1 -1]      [-1  2 -1]       [-1 -1  2]      [ 2 -1 -1]
[ 2  2  2]      [-1  2 -1]       [-1  2 -1]      [-1  2 -1]
[-1 -1 -1]      [-1  2 -1]       [ 2 -1 -1]      [-1 -1  2]
```

Description
```
TODO: Add working code in here
```


