Dynamic programming is a way of making an [[Algorithm]] more efficent by storing itimidary results. 

Dynamic programming works well for [[Algorithm|algorithms]] with repetitive computations because as it prevents having to repeat the same computations again.

When can you use backtracking vs dynamic programming, view the following page [[Use Backtracking or Dynamic programming]]

## Memoise 
One way to create a dynamic programming solution is to first create the [[Backtracking|backtracking]] answer, and cache results the first time we see them. Then in future instead of recaculating the answer, we return the cached value. 

## Bottom up
Oftern in memoise youll notice the cache (or the memo) is filled bottom to top. We can skip the recusion step by instead building that result bottom up. 

The way I find easiest to come up with the bottom up approach is the design the memoise approach, and look how the memoise array (cache) is built up. 

Doing the bottom up approach removes the need [[Recursion]] and therefore [[Call stack|stack frames]]. 

Sometimes when building the bottom up approach you'll realize you don't need the cache array, but only need to keep track of a few previous values, removing the need for an array all together which can further reduce the space complexity. 

## Example

For the problem of working out a fibonachi number, you can see the following decision tree, with fib 1 and 2 as the base case with a value of 1. 

![[Fib Decision Tree.png]]
Exploring it in a tradition [[Backtracking]] way would lead to exploring the whole tree, with a time complexity of O(2<sup>n</sup>). 

However notice we calculate fib3 twice. In [[#Memoise|memoisation]] we can instead cache the value in an array the first time we see it. 
![[Fib Decision tree with memo.png]]
 *The decision tree and the memo array the second time we see fib3*
Now when we see fib3 a second time, we can just use the value from the previous time we calculated it. This turns our tree into more of a line, reducing our time complexity to O(n).

Now to get the bottom up solution we can see how memo is being built up. We can fill our base cases first of all, fib2 and fib1 equal 1. Now for every index we add previous 2 numbers together, and that becomes our result. 

Great now we have elimated the need for recursion, but theres one more thing we can optimize, because we are only looking at the last 2 numbers, we only need to store these two values, reducing our space complexity to O(1).

Wow what an adventure, we took a O(2<sup>n</sup>) time and a O(logn) space brute force approach, and converted it into a O(n) time and a O(1) space approach. 


