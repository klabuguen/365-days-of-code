# Day 18:  Neighborhood Operators
#image-processing-fundamentals 
## 1. Introduction
In yesterday's post, I reviewed image enhancement techniques applied with linear filtering operators. I briefly touched upon convolution and correlation, and gave two basic examples of applied linear filters. Today, I wanted to dive a little deeper into convolution and correlation, which are additional tools in our image processing tool box.
## 2. Correlation
Correlation is a common image/signal processing method used to determine how two functions (e.g. an image and kernel) are related to each other. Correlation is defined with the following formula:
$$
(2.1)\ \ \ g(i,j)=\sum_{k,l}f(i+k,j+l)h(k,l)
$$
where $g$ is the correlation result at position $(i,j)$, $f(i+k,j+l)$ is the *input image*, and $h(k,l)$ is the kernel. 

During correlation, a kernel is placed at different positions in the image. The values from the  kernel are multiplied with the corresponding pixel values at each position, then summed to obtain a correlation value. The process is then repeated by sliding the kernel across the entire image. Areas with a high correlation value means that the kernel has a correlation with the pixels in that part of the image. 
## 3. Convolution
Yesterday, I briefly reviewed convolution, which is defined by the formula:
$$
(3.1)\ \ \ g(i,j)=\sum_{k,l}f(k,l)h(i-k,j-l)
$$
where $g(i,j)$ is the *output image* or *convolved result*, $f(k,l)$ is the *input image*, and $h(i-k,j-l)$ is the kernel $h(k,l)$ flipped and shifted by $i$ and $j$. The function $f$ remains fixed in $(3.1)$, which then describes cross-correlation as $2.1$.

The formula for convolution may also be expressed as: 
$$
(3.2)\ \ \ g(i,j)=\sum_{k,l}f(i-k,j-l)h(k,l)
$$
Though both formulas describe convolution, and $h(k,l)$ is the *convolution kernel*. In this equation form, the kernel is flipped before it is applied to the image $f$. The image $f$ is shifted by $k$, $l$, then $h$ is applied to the shifted neighborhood. 

### Properties of Convolution
1. Commutativity, $f(t)*g(t)$:
	- The order of the two functions does not matter, since convolution produces the same result regardless of order
2. Associativity, $f(t)∗(g(t)∗h(t))=(f(t)∗g(t))∗h(t)$:
	- Grouping of operations does not affect the final result
3. Distributivity, $f(t)∗(g(t)+h(t))=f(t)∗g(t)+f(t)∗h(t)$: 
	- Convolution distributes over addition
4. Identity, $f(t)∗δ(t)=f(t)$: 
	- Convolution with the unit impulse function results in the function itself
5. Invertibility, $f(t)∗f−1(t)=δ(t)$:  
	- Convolution with the inverse of the function is the unit impulse function
6. Linearity, $a(f(t)∗g(t))+b(f(t)∗h(t))=f(t)∗(ag(t)+bh(t))$: 
	- Convolution is a linear operation
7. Shift Invariance, $f(t−t0​)∗g(t)=(f∗g)(t−t0​)$: 
	- Convolution preserves time shifts in signals
## 4. Example
```
int convolution(unsigned char *bufferIn, unsigned char *bufferOut, Mask *mask, int imgRows, int imgCols){
	int value = 0, maskRows = mask->rows, maskCols = mask->cols;
	for(int j = 0; j < imgRows; j++)
	for(int i = 0; i < imgCols; i++ ){
		for(int k = 0; k < maskRows; k++)
		for(int l = 0; l < maskCols; l++){
			if((j-k) >= 0 && (i-l) >= 0)
			value += ((signed char)mask->maskBuffer[k*maskRows+l] * bufferIn[(j-
			k)*imgRows+(i-l)]);
			}
		if(value > 255) value = 255;
		if(value < 0) value = 0;
		bufferOut[j*imgRows+i] = (unsigned char)value;
	}
	return 0;
}
```

`Input Image`:
![[./images/graylevel_in.png]]
`Output Image`:
![[Pasted image 20250124183628.png]]