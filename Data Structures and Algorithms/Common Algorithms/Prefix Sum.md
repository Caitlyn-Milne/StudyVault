A prefix sum is the concept of storing the sum of all previous elements in a collection for easy access. 

For example `1,2,3,4,5` would have a prefix sum that looks like the following `0,1,3,6,10`

## Prefix
A prefix sum is created iteratively from left to right, keeping track of the sum of all previous elements.

## Postfix
A postfix sum is same instead we go right to left, keeping track of the sum of all of the next elements

## Prefix and Postfix
Creating a prefix and a postfix sum, gives you sum of all previous elements, and all future elements, adding these together you can get the sum of all elements apart of the current element. 

If you want to find the sum of all the other elements, a prefix and postfix might be an inefficent way to do this, because we can just sum up all items togethers and subtract the current element at each index. 

However take the problem where you want 
```
Given an array of numbers, replace each number with the product of all the numbers in the array except the number itself *without* using division.
```

You can use a prefix and postfix sum together, of course, in this case itll be a prefix product. 
```kt
//time O(n)
//space O(n)
fun product(nums : IntArray) {
    var product = 1
    var prefixProduct = IntArray(nums.size) { 1 }
    var postfixProduct = IntArray(nums.size) { 1 }
   	for (i in 1 until nums.size) {
        product *= nums[i - 1]
        prefixProduct[i] = product
    }
    product = 1
    for (i in nums.size - 2 downTo 0) {
		product *= nums[i + 1]
        postfixProduct[i] = product
    }
    
    for(i in 0 until nums.size) {
    	nums[i] = prefixProduct[i] * postfixProduct[i]
    }
}
```
