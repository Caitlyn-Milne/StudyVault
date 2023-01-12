A string (text) in C++ is just an array of characters. Just like arrays in C++ creating a string returns a char* as seen below

```cpp
char* foo = "Bar"
```

Although we have a pointer here we do not need to call delete to deallocate the memory because we did not call `new`. 

Strings in both C++ and C use a null termination character, a character with a value of 0 to indicate the end of the string. The above example would therefore look more like this in memory

```
B,a,r,\0
```

Of course each char has a value so it would look more like the following

```
42 61 72 00
```

To work out the size of the string we can start from the first char (which will be at the pointer) and increase a count as we go along the memory untill we find the null termination character. 

A built in function can be used for this, called strlen
```cpp
const char* str = "text";
const size_t length = strlen(str);
```

theres also a function called `strcpy_s` that copies a string into new memory location. 

```cpp
const char* foo = "baz";
char bar[4];
strcpy_s(bar, foo);
```

notice how the bar char array is of size 4 not 3 as it contains the null termination character. 