# Day 32: Quadrature Encoder
#c-fundamentals 
Given the quadrature encoder signal below for clockwise (CW) and counter-clockwise (CCW)  rotation, design an interrupt driven embedded software for the Nucleo-64 (STM32L476)  to keep count of the angular rotation of the encoder.

```
Quadrature Encoder Signal

Clockwise (CW) Rotation:
Channel A
		        +---+   +---+   +---+
		        |   |   |   |   |   |
			----+   +---+   +---+   +---

Channel B
		          +---+   +---+   +---+
				  |   |   |   |   |
			------+   +---+   +---+   

      Channel A leading B


Counter-Clockwise (CCW) Rotation:
Channel A
		          +---+   +---+   +---+
				  |   |   |   |   |
			------+   +---+   +---+   

Channel B
		        +---+   +---+   +---+
			    |   |   |   |   |   |
			----+   +---+   +---+   +---

      Channel B leading A

```


Specifications: 
- CHA connected to GPIO labeled D2 on the NucleoL476RG
- CHB connected to GPIO labeled D4 on the NucleoL476RG 

Write a C program to keep track of both CCW and CW rotation of the encoder. Configure both GPIO inputs to interrupt on both rising and falling edge. With each edge transition develop a counter to increment one count for each edge as it rotates CW and decrement by one count for each edge in the CCW direction. 

Your program should initialize and configure each GPIO properly. 

- Write all of the appropriate ISR's Include all appropriate header files. 
- Within the main background loop, the program should print the encoder count approximately every 500 ms. 


