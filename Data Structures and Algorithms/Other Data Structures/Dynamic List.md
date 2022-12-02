A dynamic list, also known as an ArrayList (Java), MutableList (Kotlin),  List (C#), vector (C++), is a datastructure that holds a collection, but its size is dynamic and can be changed upon adding items to it. 

Behind the scenes a list has an [[Arrays|array]], and a pointer to the current end of the list. 

When an item is added to the dynamic list, it is added in the next avaliable space towards the end of the list. If there is no space left, a resize occurs. 

## Resize
During a resize, the array is copied to a new array with double the capacity. 

The size of the underlying array is called the capacity.

## Shuffle
A shuffle occurs when a item is removed that is not the last item in the dynamic list.

This causes a gap inside the list, and items are moved down 1 by 1 to fill in the gap. 

## Time Complexity
Adding to the list has time complexity of O(1) normally, but O(n) during a resize.

Removing has a time complexity of O(n). This is because removing an element that isnt last causes a shuffle.

Indexing the array has a complexity of O(1)

### Removing multiple items
Where you are removing multiple items it is wise to use a function that allows remove multiple items before a shuffle operation. This is because shuffle is a O(n) operation and would be done for each remove `r` number of times, where `r` is the number of removed items, making the over all time complexity O(nr). 

You might need to subiment this by copying the remove collection into a hashset as many of these such methods call contain methods, which have different complexities depending on the used datastructure. 

The following code shows the execution times of two approaches as n increases. The first for calling `.removeAll` on a `MutableList`; and the second copying the same list to a `HashSet` and calling `.removeAll` on that.
```kt
import kotlin.test.*
import kotlin.system.*

fun main(){
	runTests(10)
    runTests(1000)
    runTests(100000)
}

fun runTests(n : Int){
   	var list = mutableListOf<Int>()
    var removeItems = mutableListOf<Int>()
    setUpLists(n,list, removeItems)
    var time = measureTimeMillis {
        removeAll_Normal(list,removeItems)
    }
    println("(n = $n) normal remove all ${time}ms")
    time = measureTimeMillis {
        removeAll_Set(list,removeItems)
    }
    println("(n = $n) set remove all ${time}ms")
}

fun setUpLists(n : Int,list : MutableList<Int>, removeItems : MutableList<Int>) {
    for(i in 0..n) {
        list.add(i);
        if(i % 2 == 0){
            removeItems.add(i);
        }
    }
}

fun removeAll_Normal(list : MutableList<Int>, removeItems : MutableList<Int>){
    list.removeAll(removeItems);
}

fun removeAll_Set(list : MutableList<Int>, removeItems : MutableList<Int>){
    var s = removeItems.toHashSet()
    list.removeAll(s);
}
```
[open in playground](https://pl.kotl.in/W6bS6vrR8)

## Usage
### In [[C Sharp]]
In c sharp a dynamic list is called a `List`.
```cs
//define a list
List<int> list = new List<int>(capacity);
//add items to a list
list.Add(5);
list.Add(10);
list.Add(15);
//index list
int index1 = list[1]; //index1 = 10
//index list backwards
int last = list[^1]; //last = 15
//remove items from the list
list.Remove(10); //removes the element 10 from the list
list.RemoveAt(0); //removes item at index 1 from list
```

Remove multiple items
```cs
var list = new List<int>() { 1, 2, 3 };
HashSet<int> s = new HashSet<int>() { 1 , 3 };
list.RemoveAll((i) => s.Contains(i));
```

### In [[Kotlin]]
In kotlin a dynamic list is called a MutableList or an ArrayList.


```kt
//defining an mutable list
var list = mutableListOf<Int>()
//add items
list.add(5)
list.add(10)
list.add(15)
//index list
var index1 = list[1] //index1 = 10
var last = list.last() //last = 15
//remove items
list.remove(10) //removes the element 10 from the list
list.removeAt(1) //removes item at index 1 from list
```

Kotlin has a remove all function, but don't be fooled, its time complexity is based on the collection type you pass it. Copying the remove item collection into a hashset can seriously reduce the time complexity, if you dont mind the increased memory usage. 
```kt
fun removeAll_Normal(list : MutableList<Int>, removeItems : MutableList<Int>){
    list.removeAll(removeItems);
} //O(n^2), space O(1)
```

```kt
fun removeAll_Normal(list : MutableList<Int>, removeItems : MutableList<Int>){
    list.removeAll(removeItems);
} //time O(n), space O(n)
```