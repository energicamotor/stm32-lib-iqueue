# IQUEUE LIBRARY

Library for creating and manage queues.

## Supported Hardware

- NUCLEO-H745ZI-Q
- NUCLEO-L552ZE-Q

## Functions Guide

- `iqueue_init`: initializes the structure.
- `iqueue_enqueue`: puts an element at the end of the queue.
- `iqueue_dequque`: takes out the first element of the queue.
- `iqueue_size`: gets the size of the queue (number of elements).
- `iqueue_advance_next`: advances a position in the queue.
- `iqueue_get_next_enqueue`: returns the next element of the queue.
- `iqueue_dequeue_fast`: returns the first element of the queue.


## How to use

- Include the header file `lib_iqueue.h`.
- Create a `iqueue_t` instance and where the data is saved:
```C
static uint8_t q_canbus_storage[128 * sizeof(canbus_frame_t)];    //buffer where the iqueue frame of the CAN-Bus are saved
iqueue_t q_canbus;                                                //instance
```
- Initialize the queue using `iqueue_init`:
```C
iqueue_init(&q_canbus, 128, sizeof(canbus_frame_t), q_canbus_storage); //example
```
- Use `iqueue_enqueue` and `iqueue_dequeue` to keep in a queue your data
   

## Example

This example uses a NUCLEO-H745ZI-Q. In thi exmple the library is used to better handle a CANBus communication (taken from [EN.W.009784/tsk_app.c](https://github.com/energicamotor/EN.W.009784/blob/main/stm-source-code/CM7/AppCode/tsk_app.c) )
```C
static uint8_t q_canbus_storage[128 * sizeof(canbus_frame_t)];
iqueue_t q_canbus; 

static void cb_canbus(canbus_frame_t *frame)            //callback of a receiving CAN-Bus frame
{
	iqueue_enqueue(&q_canbus, frame);               //keep in a queue the received frames
}

[...]

if(iqueue_dequeue(&q_canbus,&cbus_frame_rx) != I_EMPTY) //if something is waiting in the queue do something
{
[...]
}
```

