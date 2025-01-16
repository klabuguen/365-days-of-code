# Day 11: Review of Image Processing Basics 
#image-processing-fundamentals

Note: Need to update image processing sections, currently working out of
https://github.com/klabuguen/c-dsp/tree/main/image-processing 
## 1. Image Color and Resolution
notes
## 2. Image Formats and Data Types 
Image Formats
- JPG: Joint Potographic Experts Group
	- lossy compression
- GIF: Graphic Interchange Formage
	- lossless compression
	- limited to 8 bit color
- BMP: Bitmap picture
	- Basic format
	- lossless compression 
- PNG: Portable network graphics
	- Lossless compression
- TIFF: Tagged image file format
	- very flexible
	- compressed/uncompressed

Data Types
- Binary image
- Intensity of grayscale 
- RGB or true-color
- Floating-point

Working with the Bitmap Format:
- Consists of image header (54 bytes), color table (1028 bytes), image data
- Looking at image header, we can figure out image data
	- For example, at offset = 18, image width in pixels is given, offset = 22, image height in pixels
	- offset 28, number of bits per pixel is given, which is needed to determine the bit depth 
## Examples:
### 1. Reading and Copying an Image

```
    printf("Opening image files for processing.\n");
    FILE *imageIn = fopen("cameraman.bmp","rb");
    FILE *imageOut = fopen("cameraman_out.bmp","wb");
    
    if(imageIn == NULL){
        "Failed to open image files.\n";
        return 1;
    }
    
    printf("Successful opened image files!\n");
    
    unsigned char header[HEADER_SIZE], colormap[COLOR_TABLE_NUM_ELEMENTS];
    
    for(int i = 0; i < HEADER_SIZE; i++){
        header[i] = fgetc(imageIn);
    }
    
    // Obtain width, height, and depth from header
    int width = *(int*)&header[HEADER_WIDTH_POS];
    int height = *(int*)&header[HEADER_HEIGHT_POS];
    int depth = *(int*)&header[HEADER_BIT_DEPTH_POS];
    
    if(depth <= COLOR_TABLE_SIZE){
        fread(colormap, sizeof(unsigned char), COLOR_TABLE_NUM_ELEMENTS, imageIn);
    }
    
    printf("Copying image.\n");
    
    // Write `header` to imageOut
    fwrite(header, sizeof(unsigned char), HEADER_SIZE, imageOut);
    unsigned char buffer[width * height];
    // Read 1024 unsigned chars from imageIn and store the data in `buffer`
    fread(buffer, sizeof(unsigned char), width * height, imageIn);
    
    if(depth <= COLOR_TABLE_SIZE){
        // Write `colormap` to imageOut
        fwrite(colormap, sizeof(unsigned char), COLOR_TABLE_NUM_ELEMENTS, imageOut);
    }
    // Write `buffer` image data to imageOut
    fwrite(buffer, sizeof(unsigned char), height * width, imageOut);
    
    fclose(imageOut);
    fclose(imageIn);
    printf("Successfully read and copied an image!\n");
    printf("\nImage Data\nWidth: %d  Height: %d  Depth: %d\n", width, height, depth);

```

### 2. Creating an Image Reader
```

```

### 3. Creating an Image Writer
```

```

### 4. RGB to Grayscale
```

```

### 5. Image Binarization
```

```
