In [[C++ ]] arrays can be created in a simular way to [[C Progamming Language|C]] using whats called a static array (also known as C style arrays)

In [[C++]] we can create an array on the [[Stack (Memory)|stack]] using the following syntax
```cpp
int arr[3];
//or
int arr[] { 1, 2, 3 };
```

and on the heap using the following syntax

```cpp
int* arr = new int[3];
//or 
int* arr = new int[3] {1, 2, 3};
```
In both cases we actually have a pointer the first element inside the array. 

## Size of array
C++ does not store the length of the array alongside it, instead to get the size we frequently store the length along it in a seperate variable, or use a datastructure that does the same. 

```cpp
int* arr = new int[3] {1, 2, 3};
int arr_size = 3;
```

If the compiler knows about the length of the array we can get the length of the array by dividing the size of the array by the size of an element inside the array

```cpp
int arr[3] {1, 2, 3};
int arr_size = sizeof(arr) / sizeof(int);
```

Becareful not to do this on a heap allocated `array` as its just a pointer to the first space in memory, and therefore your going to get the size of the pointer.
```diff
- int* arr = new int[4] {1, 2, 3 , 4};
- int arr_size = sizeof(arr) / sizeof(int); //arr_size equals 2
```

Because of this, in my opinion I believe this to be a code smell. 

## See Also
Frequently its better to use [[C++ std array]]