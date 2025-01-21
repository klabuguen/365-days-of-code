# Day 19: Gray Level Transformation
#image-processing-fundamentals 
## What is Gray Level Transformation?
Gray level transformation (or intensity transformation) is used to adjust the contrast, brightness, and/or the overall appearance of a grayscale image by modifying the intensity of its pixel values. 

The gray level image contains 256 levels of intensity for all pixels within the image, ranging from 0 (black) to 255 (white). The gray level transformation applies a function to each of these pixels to modify the intensities and generate a new image. In a majority of the past few image processing related posts, I've already used gray level transformation to modify many of the images. 

## Types of Gray Level Transformation
### 1. Linear (Contrast Stretching)
A linear transformation modifies the brightness and contrast of an image using the following formula:
$$
s=a\cdot r+b
$$
where $s$ is the *transformed pixel value*, $a$ is the *contrast factor*, $r$ is the *original pixel value*, and $b$ is the *brightness offset*. 
### 2. Logarithmic
A logarithmic transformation magnifies pixels in darker regions while compressing brighter areas, and is defined by the following formula: 

$$
s = c*\log(r+1)
$$
where $s$ is the *transformed pixel value*, $c$ is an *arbitrary constant*, and $r$ is the *original pixel value*.

### 3. Power-Law (Gamma)
The power-law (gamma) transformation adjusts brightness based on a power function defined by:
$$
s = c \cdot r^\gamma
$$
where $s$ is the *transformed pixel value*, $c$ is an arbitrary constant, $r$ is the original pixel value, and $\gamma$ is a positive constant value that determines how intensity levels are mapped. When $\gamma < 1$, the image becomes brighter as darker pixels are more enhanced - thus, lower gamma values are commonly used to brighten underexposed images. If $\gamma > 1$, the image becomes darker, and brighter pixels are emphasized less.

## Example
### 1. Negative Transformation of a Grayscale Image
This is an example of a negative linear transformation, where each pixel value in the image is subtracted from 255. I use the formula: $s=r-255$, where $r$ is the original pixel, to determine $s$, which will form the new image.

In the code below, I simply loop through each pixel in the image, and subtract 255 by its intensity value.

```
for(int y = 0; y < height; y++){
	for(int x = 0; x < width; x++){
		bufferOut[x + y * width] = 255 - buffer[x + y * width];
	}
}
```

`Input test image`:
![[Pasted image 20250120151922.png]]
`Output image:`
![[Pasted image 20250120151908.png]]