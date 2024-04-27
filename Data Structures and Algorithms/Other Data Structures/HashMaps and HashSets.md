
```kt
class MyHashSet<T> {
	private var buckets : Array<MutableList<Any?>> = Array<MutableList<Any?>>(2) { mutableListOf<Any?>() }
    private val maxBucketSize = 4
    
    private fun increaseBuckets() {
        val oldBuckets = buckets
        buckets = Array<MutableList<Any?>>(oldBuckets.size * 2) { mutableListOf<Any?>() }
       	oldBuckets.forEach { bucket ->
            bucket.forEach { item ->
                add(item as T)
            }
        }
    }
    
    fun contains(item : T) : Boolean {
        val bucketIndex = item.hashCode() % buckets.size
        return buckets[bucketIndex].contains(item)
    }
    
    fun add(item : T) : Boolean {
    	if(contains(item)) return false
            
        var bucketIndex = item.hashCode() % buckets.size
        if(buckets[bucketIndex].size + 1 > maxBucketSize) {
        	increaseBuckets()
            bucketIndex = item.hashCode() % buckets.size
        }
        
        buckets[bucketIndex].add(item)
        return true
    }
    
    fun remove(item : T) : Boolean {
        if(!contains(item)) return false
            
    	val bucketIndex = item.hashCode() % buckets.size
        return buckets[bucketIndex].remove(item)
    }
}

```
[Open in Kotlin playground](https://pl.kotl.in/EHmxf0asK)