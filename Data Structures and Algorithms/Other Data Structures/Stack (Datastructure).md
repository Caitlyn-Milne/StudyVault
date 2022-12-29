A stack is a datastructure that follows a last in first out (LIFO). This means the last item you put inside a stack is the next item you will get out

[[Queue|Queues]] are simular to queues but follow a FIFO principle instead

## In [[CSharp]]
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
[[Kotlin]] does have a Stack but it is recommended to use a ArrayDeque that can have items added or removed at either end. To get the same effect as a stack you can add and remove items from the same end.
```kt
val stack = ArrayDeque<Int>()
stack.addLast(2) //[2]
stack.addLast(3) //[2,3]
stack.addLast(4) //[2,3,4]
val pop = stack.removeLast() //pop:4 stack:[2,3]
val peek = stack.last() //peek: 3 stack:[2,3]
```

## Implementations
### Array Version
```kt
public class ArrayStack<T> {
    
    public var capacity : Int = 4
    	get() = field
    	set(value) {
            field = value
        	_array = Array<Any?>(field) { _array.getOrNull(it) }
        }
        
   public var count : Int = 0
    	get() = _top
        
    private var _top = 0
    private var _array = Array<Any?>(Capacity) { null }
    
    fun push(value : T){
        if(_top >= _array.size){
            Capacity *= 2
        }
        _array[_top++] = value
    }
    
    fun pop() : T{
        if(_top <= 0) throw Exception("cannot pop from an empty stack")
        var result = _array[--_top] as T
        _array[_top] = null //you do actually need to set it to null so the garbage collector can clean up
        return result
    }
    
    fun peek() : T {
        return _array[_top - 1] as T
    }
}
```
[kotlin playgound](https://pl.kotl.in/SIDuQSR85?theme=darcula)
#### Time Complexity 
Insertion O(1) normally, but O(n) if reallocation is needed
Peek O(1) 
Pop O(1)
Count O(1)

### Linked List Version
Below is  a [[Linked List|linked list]] implimentation of a stack.
```kt
private data class MyStackNode<T>(val value : T, val next : MyStackNode<T>?){}
public class MyStack<T> {
    
    private var _head : MyStackNode<T>? = null
    public var count : Int = 0
    	get private set
    
    fun push(value : T){
        _head = MyStackNode<T>(value, _head)
        count++
    }
    
    fun pop() : T{
        if(_head == null){
            throw Exception("cannot pop from an empty stack")
        }
        var result = _head!!.value
        _head = _head!!.next
        count--
        return result
    }
    
    fun peek() : T{
        return _head!!.value
    }
}
```
[kotlin playground](https://pl.kotl.in/JeioxG6wZ?theme=darcula)
#### Time Complexity 
Insertion O(1)
Peek O(1) 
Pop O(1)
Count O(1)

### Array Vs LinkedList

This array implimentation has a inferior worse case time complexity for insertion. This is due to situation when capacity is exceeded. Here it must reallocate the array into a new array with more size.

The array implimentation can be developed to include indexing at positons along the stack with in O(1). Trying to add simular functionality to the linked list implimentation would require O(n)

The linked list implimentation creates new nodes for every item added to the stack. In garbage collected lanugages, this can cause an increase of trash needed to be collected by the garbage collector.  

The array implimentation has its values next to each other in memory due to how arrays work, allowing for less cache misses in low level languages like C++ when iterating over or pulling multiple items from the stack. (In the above example in kotlin, this is probably less applicable)


