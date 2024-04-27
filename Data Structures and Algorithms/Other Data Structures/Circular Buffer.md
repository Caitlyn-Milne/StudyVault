A circular buffer is the idea in which upon exceeding the ends of a buffer, it jumps to the other end. Circular buffers have a few applications.

You can store the last k amount of live data using a circular buffer, using a pointer as a location to write data, once the buffer is full the pointer can jump back to the start and overwrite the old data. You can then unwrap the data, offsetting it by the pointer, to get the last k amount of live data. 

Circular buffers are also used for array implementations of Deques, but instead of overwriting data, the buffer can be unwrapped into a larger buffer.