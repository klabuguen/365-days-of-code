# Day 28: Implement a Circular Buffer
#c-fundamentals 

```
#include <stdio.h>
#include <stdbool.h>

#define BUFFER_SIZE 5

typedef struct cb{
	int buffer[BUFFER_SIZE];
	size_t head;
	size_t tail;
} cb_t;

bool initializeCb(cb_t *buffer){
	buffer->head = 0;
	buffer->tail = 0;
	return true;
}

bool isBufferFull(cb_t *buffer){
	return (((buffer->tail+1) % BUFFER_SIZE) == buffer->head) ? true : false;
}

bool isBufferEmpty(cb_t *buffer){
	return (buffer->head == buffer->tail) ? true : false;
}

bool push(cb_t *buffer, int value){
	if(isBufferFull(buffer)) return false;
	// make sure buffer indices wrap around
	buffer->tail = (buffer->tail+1) % BUFFER_SIZE;
	buffer->buffer[buffer->tail] = value;
	return true;
}

bool pop(cb_t *buffer){
	if(isBufferEmpty(buffer)) return false;
	// make sure buffer indices wrap around
	buffer->head = (buffer->head+1) % BUFFER_SIZE;
	return true;
}
```