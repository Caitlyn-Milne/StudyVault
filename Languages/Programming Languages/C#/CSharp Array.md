An [[Arrays|array]] in [[CSharp]] can be created via the following syntax
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
