A queue is a datastructure that follows a first in first out (FIFO). This means the first item you put inside a queue is the next item you will get out

[[Stack (Datastructure)|Stacks]] are simular to queues but follow a LIFO principle instead

## In [[C Sharp]]
In C# this is `Queue<T>` and you can add and remove items with Enqueue, Dequeue, and Peek for seeing the next item

```cs
var queue = new Queue<int>();
queue.Enqueue(2); //[2]
queue.Enqueue(3); //[2,3]
queue.Enqueue(4); //[2,3,4]
var dequeue = queue.Dequeue(); //dequeue: 2 queue:[3,4]
var peek = queue.Peek(); //peek: 3 queue:[3,4]
```
## In [[Kotlin]]
[[Kotlin]] doesnt have a Queue but does have a ArrayDeque that can have items added or removed at either end. To get the same effect as a queue you can add and remove items from different ends.

```kt
val queue = ArrayDeque<Int>()
queue.addLast(2) //[2]
queue.addLast(3) //[2,3]
queue.addLast(4) //[2,3,4]
val dequeue = queue.removeFirst() //dequeue:2 queue:[3,4]
val peek = queue.first() //peek: 3 queue:[3,4]
```
