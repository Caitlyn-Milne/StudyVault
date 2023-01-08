[[Kotlin]] [[Arrays]] work the following way.

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