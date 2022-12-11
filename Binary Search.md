Binary search is away of searching through a sorted collection in O(logn) time.

We start at the center of a collection. If this is the target, we have found it. If target is smaller, we can rule out this and any larger values, simularly if the target is larger, we can rule out any smaller values. Repeat with this new section until we have either found it, or we are out of possibilities.

```kt
fun search (nums: IntArray, target: Int) : Int {
    var left = 0
    var right = nums.size - 1
    while (left <= right) {
        val pivot = (left + right) / 2
        if (nums[pivot] == target) return pivot
        if (target < nums[pivot]) right = pivot - 1
        else left = pivot + 1
    }
    return -1
}
```
## Complexity
Time O(logn)
Space O(1)