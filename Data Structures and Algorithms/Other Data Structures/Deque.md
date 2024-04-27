An Deque is a data structure that allows you to append and remove items from the both of its ends. It is commonly implemented through a linked list, or an circular buffer/array. 

## Array Implementation 

The array implementation makes use of a [[Circular Buffer]]. It keeps track of a start and end position. Upon adding to either end, it inserts the data into the location the start/end pointer is at. When the start/end pointer exceeds either end of the array, it wraps around to the other end. If inserting data would exceed the capacity of the array, the array is copied to a larger one. This ensures there is always capacity for new elements, with out overriding old ones. This allows for asymptotic constant time insertions to either end of the data structure, as it just needs to put the element at the pointer with out shifting any elements. We describe the time complexity as asymptotic constant time because its tends towards a constant time operation, however because occasionally we have to resize the buffer, and copy elements across (which is a linear time operation), this is not always the case. 

With this implementation the time complexities are as shown 
- addFirst ~O(1)
- addLast ~O(1)
- first O(1)
- last O(1)
- removeFirst O(1)
- removeLast O(1)
### Example

```kt
class MyArrayDeque<T>(initialCapacity : Int = 4) {
    
    private var buffer : Array<Any?> = Array<Any?>(initialCapacity) { null }
    
    private var start = 0
    private var end = 1
    
    val capacity : Int 
    	get() = buffer.size
    
    var size : Int = 0
    	private set
    
    fun ensureCapacity(n : Int) {
        if (n <= capacity) return
        while(capacity < n) {
        	val newBuffer = Array<Any?>(capacity * 2) { null }
            var i = 0
 
        	while(size > 0) {
                newBuffer[i++] = removeFirst()
            }
            buffer = newBuffer
            end = i
            start = capacity - 1
            size = i
        }
    }
    
   	fun addFirst(item : T) {
       ensureCapacity(size + 1)
       size++
       buffer[start] = item
       if (--start < 0)
       		start = capacity - 1
   	}
   
   	fun addLast(item : T) {
       ensureCapacity(size + 1)
       size++
       buffer[end] = item
       end = (end + 1) % capacity
   	}
   
   	fun removeFirst() : T? {
        if (size == 0) return null
        size--
        start = (start + 1) % capacity
        val result = buffer[start] as T
        buffer[start] = null
        return result
    }
   
   	fun removeLast() : T? {  
       if (size == 0) return null
       size--
       if (--end < 0) end = capacity - 1
       val result = buffer[end] as T
       buffer[end] = null
       return result
   	}
    
    fun first() : T? {
        if (size == 0) return null
        return buffer[(start + 1) % capacity] as T
    }
    
    fun last() : T? {
        if (size == 0) return null
        var e = end - 1
        if (e <  0) e = capacity - 1
        return buffer[e] as T
    }
}
```
[Open in kotlin playgroud](https://pl.kotl.in/B-59oj0Lg "https://pl.kotl.in/B-59oj0Lg")

## Linked List Implementation
[[Linked List]] TODO

## Linked List vs Array Implementation 
The linked list implementation provides constant time operation insertion of data, although this is normally true for the array implementation, this is not always the case, as it sometimes copies data across to a new larger array. This is one benefit of the linked list, as it avoids these occasional performance hits. 

The array implementation however stores data next to each other in memory, which reduces the amount of cache misses. Because data is stored sequentially, it is quicker to loop through an ArrayDeque then an LinkedListDeque as computers are designed for quick reading of sequential data. 

A disadvantage of the linked list implementation is that you create nodes on the heap that need to be cleaned up. Deallocating memory on the heap can be costly especially in garbage collected languages. Although some of these issues can be relived by pooling nodes, there would still be an issue upon deallocating the deque itself as it would have to clean up nodes across memory, which can also cause other performance issues due to memory fragmentation. 

Generally ArrayDeques are preferred for the above reasons stated. 