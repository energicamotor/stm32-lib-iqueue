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

```C


```

