A stack is a datastructure that follows a last in first out (LIFO). This means the last item you put inside a stack is the next item you will get out

[[Queue|Queues]] are simular to queues but follow a FIFO principle instead

## In [[C Sharp]]
In C# this is `Stack<T>` and you can add and remove items with Push, Pop, and Peek for seeing the next item

```cs
var stack = new Stack<int>();
stack.Push(2); //[2]
stack.Push(3); //[2,3]
stack.Push(4); //[2,3,4]
var pop = stack.Pop(); //pop: 4 stack:[2,3]
var peek = stack.Peek(); //peek: 3 stack:[2,3]
```
## In [[Kotlin]]
[[Kotlin]] doesnt have a Stack but does have a ArrayDeque that can have items added or removed at either end. To get the same effect as a stack you can add and remove items from the same end

```kt
val stack = ArrayDeque<Int>()
stack.addLast(2) //[2]
stack.addLast(3) //[2,3]
stack.addLast(4) //[2,3,4]
val pop = stack.removeLast() //pop:4 stack:[2,3]
val peek = stack.last() //peek: 3 stack:[2,3]
```

