Sliding window algorithms aim to help find run computations on [[Subarray|subarrays]]. 

Take the problem, whats the highest sum of a [[Subarray|subarray]] of length k with in a given array. 

In a native approach we could create every possible subarray of length k and calculate the sum, returning the highest

*example of what that would look like*
```
input: [4,2,5,3,6,1] k:4
----------------------------
[4,2,5,3] 4 + 2 + 5 + 3 = 14
[2,5,3,6] 2 + 5 + 3 + 6 = 16
[5,3,6,1] 5 + 3 + 6 + 1 = 15
```

But doing this we have to add k numbers for every subarray inside the input. This givens a [[Complexity|time complexity]] of O(nk) or sometimes refered to as O(n<sup>k</sup>)

Instead we can can start at the first subarray, and include the next item, and remove the last item. Doing this allows the majority of the comutation to stay the same.

Because this causes the computation to slide across the input array, it has been given the name sliding window.