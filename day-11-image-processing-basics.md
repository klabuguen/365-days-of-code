# Review of Image Processing Basics 
#image-processing-fundamentals

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
## 1. Opening and Copying an Image
Creating an Image Reader
Creating an Image Writer