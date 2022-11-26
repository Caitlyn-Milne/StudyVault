A for loop allows for a block of code multiple times, frequently a for loop is used to iterate through a sequence such as [[Arrays]].

Because of the frequency of using a for loop for iterating through a sequence, alot of languages support foreach, that runs the code block for each item in the sequence.

## For
### In [[C Sharp|C#]] , [[C++]] and [[Java]]

In C# and C++ for loops are written the same way.

*for 0 inclusive to 10 exclusive*
```cpp
for (int i = 0; i < 10; i++)
```
```cs
for (int i = 0; i < 10; i++)
```
```java
for (int i = 0; i < 10; i++)
```

The for loop is made up of 3 statemenets
```cpp
for (statement1; statement2; statement3)
{
	//code here
}
```

statement1 is executed once before the code block
statement2 defines a condition for executing the code block
statement3 executes everytime after the code block

Normally statement1 is used for definiting a varible to be used as an iterator, statement2 is used for defining the condition for when the block excutes and statement 3 normally changes the iterator. 

### In [[Kotlin]]
To create a for loop inside kotlin, you create a range, and you iterate through that instead. 

*for 0 inclusive to 10 inclusive*
```kt
for (i in 0..10)
```

to change the step in the range, you can use the `step`

*for 0 inclusive to 10 inclusive, only even numbers*
```kt
for (i in 0..10 step 2)
```

if you want dont want to include the upper bound you can use until instead of `..`

*for 0 inclusive to 10 exclusive*
```kt
for (i in 0 until 10)
```

if you want to reverse a range you can use the `reversed` method

*for 10 inclusive to 0 inclusive*
```kt
for (i in (0..10).reversed())
```

alternatively you can use downTo

*for 10 inclusive to 0 inclusive*
```kt
for (i in 10 downTo 0)
```

## Foreach

### In [[C Sharp]]

In C# we can use the foreach to iterate through anything that is `IEnumerable<T>`.

```cs
int num = new int[] { 1, 2, 3 };
foreach (int num in nums) 
{
	//code
}
```

### In [[C++]]

In C++ arrays are not stored with a size. This means that we do not know how long an array is with out storing it seperately under normal conditions, meaning a foreach is not possible. However if the compiler knows the length of the array you can write a foreach loop the following way.

```cpp
int nums[] = { 1, 2, 3 };
for (const int num : nums)
{
	//code
}
```

behind the scenes this will create a for loop like the following
```cpp
for (auto begin = nums, end = nums + 3; begin != end; ++begin)
{
   auto num = *begin;
   //code
}
```

If the compiler cannot get the information for the length of the array, as well you pass a pointer, instead of reference to a function, you can not use a foreach loop.

### In [[Kotlin]]

In kotlin to iterate over a sequence you using a normal for loop with the following syntax

*iterates over sequence nums*
```kt
for (num in nums) {
	//code
}
```

Alteratively you can use forEach methods

```kt
nums.forEach { num ->
	//code
}
```

if you want an index while using a forEach you can use forEachIndexed

```kt
nums.forEachIndexed { index, num -> 
	//code
}
```

both forEach and forEachIndex are [[Kotlin Inline|inline functions]]
