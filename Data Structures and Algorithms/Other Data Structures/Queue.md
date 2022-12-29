A queue is a datastructure that follows a first in first out (FIFO). This means the first item you put inside a queue is the next item you will get out

[[Stack (Datastructure)|Stacks]] are simular to queues but follow a LIFO principle instead

## In [[CSharp]]
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
[[Kotlin]] does have a queue called `LinkedList` but it is recommended to use an ArrayDeque that can have items added or removed at either end. To get the same effect as a queue you can add and remove items from different ends.

```kt
val queue = ArrayDeque<Int>()
queue.addLast(2) //[2]
queue.addLast(3) //[2,3]
queue.addLast(4) //[2,3,4]
val dequeue = queue.removeFirst() //dequeue:2 queue:[3,4]
val peek = queue.first() //peek: 3 queue:[3,4]
```

## Implimentation
Below is a [[Linked List#Doubly Linked Lists| doubly linked list]] implimentation of a queue data structure
```kt
private data class MyQueueNode<T>(
    val value : T,
    var next : MyQueueNode<T>?,
    var prev : MyQueueNode<T>?
){}

public class MyQueue<T> {  
    private var head : MyQueueNode<T>? = null
    private var tail : MyQueueNode<T>? = null
    public var count : Int = 0
    	get private set
    
    fun enqueue(value : T){
        count++
		val newNode = MyQueueNode<T>(value, head, null)
        head?.let{
            it.prev = newNode  
        } ?: run {
            tail = newNode
        }
        head = newNode
    }
    
    fun dequeue() : T{
        if(tail == null){
            throw Exception("queue is empty")
        }
        count--
        val result = tail!!.value
		val prev = tail!!.prev
        prev?.let{
            it.next = null
        }
        tail = prev
        return result
    }
    
    fun peek() : T = tail!!.value
}
```
[kotlin playground](https://pl.kotl.in/9wSiXSPCD?theme=darcula)
### Time Complexity
enqueue O(1)
dequeue O(1)
peek O(1)
count O(1)

