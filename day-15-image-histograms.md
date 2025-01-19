# Day 15: Image Histograms
#image-processing-fundamentals 

Note: Need to update image processing sections, currently working out of 
https://github.com/klabuguen/c-dsp/tree/main/image-processing 

## 1. Histogram Equalization
An image histogram is used to determine the relative frequency in which each pixel value occurs in the image. This helps determine relevant statistics such as the average intensity, minimum, and maximum values. *Histogram equalization* is a method used to distribute intensities within an image more equally. 
### Theory
The idea behind *histogram equalization* is finding an intensity mapping function $f(I)$ such that the resulting histogram is flat, as shown in the image below:

![[./images/histogram_equalization.png]]

In order to find the mapping function $f(I)$, one method involves computing the *cumulative distribution function* (CDF), $c(I)$, by integrating the pixel distribution $h(I)$:
$$
Equation\ 2.1: \ c(I)=\frac{1}{N}\sum_{i=0}^{I}{h(i)=c(I-1)+\frac{1}{N}h(I)}
$$
where $N$ is the number of pixel within the image and $I$ is the intensity of each pixel. 

### Example
##### 1. Computing the Histogram
For a grayscale image, each of the pixels contains an intensity value between 0 and 255. To compute the histogram of this image, I simply count how many pixel values contain each intensity value. For example, the `histogram` variable stores 256 buckets, one for each intensity level, 0 to 255. Each of the buckets, will count how many pixels in the image have that intensity.

Thus, in the function `computeHistogram()`, I loop through each pixel in the image, and store the amount of times an intensity value occurs in `**histogram`.  I then write the histogram to the file `histogram_data.txt`.

```
int computeHistogram(unsigned char *buffer, int width, int height, float **histogram){

	FILE *histOut = fopen("./images/write/histogram_data.txt", "w");
	
	if(histOut == NULL){
		printf("Failed to open file for writing. Exiting..\n");
		return 1;
	}
	else{
		printf("Successfully opened file for writing!\n");
	}
	int imgSize = width*height, intensity = 0;
	for(int y = 0; y < height; y++){
	
		for(int x = 0; x < width; x++){
		// find intensity for each pixel in the image
		intensity = *(buffer + x + y * width);
		printf("ptr = %p\n", (buffer + x + y * width));
		printf("ptr val = %d\n", intensity);
		(*histogram)[intensity]+=1;
		printf("histogram[%d] = %d\n", intensity, (*histogram)[intensity]);
		}
	}
	printf("Writing histogram data to file.\n");
	for(int i = 0; i < MAX_INTENSITY; i++){
		(*histogram)[i] = (*histogram)[i] / (float)imgSize;
		printf("(*histogram)[%d] = %f\n", i, (*histogram)[i]);
		fprintf(histOut, "\n%f", (*histogram)[i]);
	}
	printf("Compute histogram successfully completed.\n");
	fclose(histOut);
}
```

To see the output of this function, take a look at `./data/histogram_data.txt`!

After plotting the histogram data using GNU Plot, I get the following:
![[./images/histogram_example.png]]

## 3. Equalizing an Image

