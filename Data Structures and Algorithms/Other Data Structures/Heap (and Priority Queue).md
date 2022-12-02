## Implimentation

```kt
class MinHeap() {

	private var array = IntArray(7) { 0 }

    constructor(source : IntArray) : this() {
        count = source.size
        array = source
        for(index in source.size / 2 downTo 0) {
            heapDown(index)
        }
    }
    
    var count = 0
    	get
        private set
    
    var capacity : Int
    	get() = array.size
    	private set(value : Int) {
            array = IntArray(value) { i -> if (i < array.size) array[i] else 0 }
        }
        
    fun add(item : Int) {
        if(count + 1 >= capacity) {
			capacity *= 2
        }
        array[count] = item
        heapUp(count)
        count++
    }
    
    fun pop() : Int {
        if (count == 0) throw IllegalStateException()
        var result = array[0]
        count--
        array[0] = array[count]
        array[count] = 0
        heapDown(0)
        return result
    }
    
    fun peek() : Int {
        if (count == 0) throw IllegalStateException()
        return array[0]
    }
    
    fun print() { 
    	println(array.joinToString())
    }
    
    private fun heapUp(index : Int) {
        var parent = parentIndex(index);
        if(parent == null || array[parent] <= array[index]) return
        val temp = array[parent]
        array[parent] = array[index]
        array[index] = temp
        heapUp(parent)
    }
    
    private fun heapDown(index : Int) {
        var left = leftChildIndex(index);
        var right = rightChildIndex(index);
        
        if (left == null && right == null) return
       	var swap = if (left == null) right!!
        else if (right == null) left
        else if (array[left] < array[right]) left 
        else right
        
        if (array[index] < array[swap]) return
        val temp = array[swap]
        array[swap] = array[index]
        array[index] = temp
        heapDown(swap)
    }
    
   	private fun parentIndex(index : Int) : Int? { 
    	var result = (index - 1) / 2 
        return if (result >= 0) result else null
    }
    
    private fun leftChildIndex(index : Int) : Int? { 
    	var result = index * 2 + 1
        return if (result < count) result else null
    }
    
    private fun rightChildIndex(index : Int) : Int? { 
        var result = index * 2 + 2
        return if (result < count) result else null
    }
    
}
```
[kotlin playground](https://pl.kotl.in/wRh2m08--?theme=darcula)
