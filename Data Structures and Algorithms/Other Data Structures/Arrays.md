An array data structure stores a collection of elements, and can be indexed. The data in an array is stored in conceqitive spaces in memory. This means they have a fixed size, because they occupy a fixed space in memory. 

## In [[C Sharp]]

An array can be created via the following syntax
```cs
int[] array = new int[3];
```
The above is an array of 3, and will use the default value for int as the placeholder value. 

To initialize an array with values you can use the following syntax
```cs
int[] array = new int[]{ 1, 2, 3 }
```
When initializing an array here we do not need to specify the length, because its implied through the constructor

Note an array in C# is considered an object and therefore is allocated on the [[Heap (Memory)|heap]].

There is away to allocate it on the [[Stack (Memory)|stack]] instead, watch this space. 

## In [[Java]]

Like in c# an array can be created using the following syntax
```java
int[] array = new int[3];
```

To initialize an array with values you can use the following syntax
```java
int[] array = { 1, 2, 3 }
```
When initializing an array here we do not need to specify the length, because its implied through the constructor

Simular to C# this will be allocated on the [[Heap (Memory)|heap]]. 

## In [[Kotlin]]

This is where we start to get caviats. 

In kotlin there is a distiniction between object and primitive arrays. 

Object arrays in Kotlin are defined the following way
```kt
val arr = Array<Foo?>(3) { null }
```
Inside the [[Lambda|lambda]] we can return a default value for an item in the array

To initialize an array with values we can do the following
```kt
val foo1 = new Foo(1)
val foo3 = new Foo(3)
val arr = arrayOf<Foo?>(foo1, null, foo3)
```

In Kotlin, [[Primitives|primitives]] have there own array types.

This means to create an array of integers in kotlin we do the following.
```kt
val arr = IntArray(3)
//or
val arr = intArrayOf(1, 2, 3)
```

and its simular for the other primitives, `ShortArray`, `FloatArray`, `BooleanArray`.

Why is this the case? 
Kotlin trys to hide java's complexity when it comes to dealing with primitives and autoboxing (watch the space for a page about that).
Because of this `Int` in kotlin can be `Integer` in java or `int` depending on the usage. Because of this an `Array<Int>` is equalient to a `Integer[]` in java, and an `IntArray` is equalient to an `int[]` in java. 

### In [[C++]]
In C++ we can create an array on the [[Stack (Memory)|stack]] using the following syntax
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

Becareful not to do this on a heap allocated `array` as its just a pointer to the first space in memory, and the compiler does not know about the length of the array. Do not do the following.
```diff
- int* arr = new int[4] {1, 2, 3 , 4};
- int arr_size = sizeof(arr) / sizeof(int); //arr_size equals 2
```

Because of this, in my opinion I believe this to be a code smell. 