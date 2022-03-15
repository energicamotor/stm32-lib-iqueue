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
- Create a `iqueue_t` instance.
- Initialize the queue using `iqueue_init`
   

## Example

This example uses a NUCLEO-H745ZI-Q. In thi exmple the library is used to better handle a CANBus communication (taken from [EN.W.009784/tsk_app.c](https://github.com/energicamotor/EN.W.009784/blob/main/stm-source-code/CM7/AppCode/tsk_app.c) )
```C
iqueue_t q_canbus;  
static void cb_canbus(canbus_frame_t *frame)              //callback of a receiving CAN-Bus frame
{
	iqueue_enqueue(&q_canbus, frame);                     //iqueue_enqueue() is taking two args: 1. iqueue handler of the CAN-Bus
}

[...]

if(iqueue_dequeue(&q_canbus,&cbus_frame_rx) != I_EMPTY)
		{
			ser_dt[0] = (cbus_frame_rx.id & 0xFF00) >> 8;
			ser_dt[1] = (cbus_frame_rx.id & 0x00FF) >> 0;
			ser_dt[2] = cbus_frame_rx.dlc;
			ser_dt[3] = cbus_frame_rx.id_type;
			ser_dt[4] =	cbus_frame_rx.fr_format;
			ser_dt[5] = cbus_frame_rx.dt[0];
			ser_dt[6] = cbus_frame_rx.dt[1];
			ser_dt[7] = cbus_frame_rx.dt[2];
			ser_dt[8] = cbus_frame_rx.dt[3];
			ser_dt[9] = cbus_frame_rx.dt[4];
			ser_dt[10] = cbus_frame_rx.dt[5];
			ser_dt[11] = cbus_frame_rx.dt[6];
			ser_dt[12] = cbus_frame_rx.dt[7];

			uint32_t b64_sz = base64_encode(ser_dt, 13, can_base64_dt);
			uart_send_message(&uart_comm_rpb, can_base64_dt, b64_sz);
		}
```

