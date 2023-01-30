Intervals represent a set of numbers, oftern represented as a range between two numbers. For example the interval 5 <= x <= 10 contains any value between 5 and 10 inclusive.

## Overlapping intervals
To check if two intervals are overlapping, you can compare the start and end points of each interval. If the start or end of one interval is in the range of the other interval, the intervals are considered to be overlapping. This can be determined by comparing the just the start or end points of the intervals.
![[Overlapping intervals.png]]
```kt
fun doOverlap(a : Pair<Int,Int>, b : Pair<Int, Int>) : Boolean {
    return a.first in b.first .. b.second 
		|| b.first in a.first .. a.second
}
```

## Finding an interval
Given an unsorted collection of intervals, to determine if a value is contained within any of the intervals, all intervals must be checked (running in O(n)). However, if the collection is sorted and non-overlapping, a binary search can be used instead (running in O(logn)).

Here's an example of how to use a [[binary search]] to check if a value is within an interval of a sorted and non-overlapping collection of intervals:
```kt
fun main(){
    var intervals = arrayOf(Pair(1,3), Pair(4,6), Pair(8,12), Pair(16,17), Pair(20,24), Pair(27,29))
    val result = getInterval(intervals, 22)
}

fun isInInterval(intervals : Array<Pair<Int,Int>>, value : Int) : Boolean {
    var left = 0
    var right = intervals.size - 1
    while (left <= right) {
        val pivot = (left + right) / 2
        val interval = intervals[pivot]
        if (value in interval.first .. interval.second){
	        return true
        } 
        if (value < interval.first) {
            right = pivot - 1
            continue
        }
        left = pivot + 1
    }
    return false
}
```

The reason you cannot use binary search in the case of overlapping intervals is because of the case where in two or more intervals have matching start locations, and the value is in at least one but not all of these intervals. Here the value could be in any of these intervals.

Take trying to search the following intervals
```
0 <= x <= 4
1 <= x <= 2
4 <= x <= 5
```
if we are to check if `3` are included in these intervals using a binary search, we first come across `1 <= x <= 2` , `3` is larger then the start location so then we will imedary rule out the interval `0 <= x <= 4` in which `3` satifys.