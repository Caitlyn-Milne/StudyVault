Quick Sort is a [[Sorting Algorithms|sorting algorithm]] that is also a [[Divide and conquer algorithm|divide and conquer algorithm]] it works by selecting a pivot element from the collection (commonly an [[Arrays|array]]) and partitioning the other elements into two sub arrays that it can then recursively do the same on.

## Partition Algorithms

## Complexity
On average quick sort has a [[Complexity|time complexity]] of O(nlogn) 
At worst quick sort has a [[Complexity|time complexity]] of O(n<sup>2</sup>) 
At quick sort has a [[Complexity|space complexity]] of O(logn) because of the stack frames .

See [[Big O notation|big o notation]] and [[Complexity|complexity]] for context on what this means.

## Example
here is an example of quick sort

```kt
fun main() {
	val arr = intArrayOf(3,4,9,1,7,0,5,2,6,8)
    quickSort(arr)
    println(arr.joinToString())
}

fun quickSort(arr : IntArray) = 
    quickSort(arr,0, arr.size-1)
    
fun quickSort(arr : IntArray, left : Int, right : Int){
    if(left >= right) return
    val pivot = partition(arr, left, right)
    quickSort(arr, left, pivot -1)
    quickSort(arr, pivot + 1, right)
}

fun partition(arr : IntArray, left : Int, right : Int) : Int {
    var pivot = arr[right]
    var split = left - 1
    for(scan in left until right){
        if(arr[scan] > pivot) continue
        swap(arr, ++split, scan)        
    }
    swap(arr, ++split, right)
    return split
}

fun swap(arr : IntArray, indexA : Int, indexB : Int){
    val temp = arr[indexA]
    arr[indexA] = arr[indexB]
    arr[indexB] = temp
}

```
[kotlin playground](https://pl.kotl.in/g40m9cpsv?theme=darcula)

