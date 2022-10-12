A for loop allows for a block of code multiple times, frequently a for loop is used to iterate through a sequence such as [[Arrays]].

Because of the frequency of using a for loop for iterating through a sequence, alot of languages support foreach, that runs the code block for each item in the sequence.

## For
### In [[C Sharp]]

### In [[Kotlin]]
Unfortunately jetbrains want for loops to be more complicated then needed. 

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
### In [[Kotlin]]

In kotlin to iterate over a sequence you using a normal for loop with the following syntax

*iterates over sequence nums*
```kt
for(num in nums)
```

Alteratively you can use forEach methods

```kt
nums.forEach { num ->
	//code
}
```

if you want an index while using a forEach you can use forEachIndexed

```kt
nums.forEach { index, num -> 
	//code
}
```

both forEach and forEachIndex are [[Kotlin Inline|inline functions]]
