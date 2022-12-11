Backtracking is the process of exploring a decision tree for valid solutions. It works by exploring all solutions until a solution is invalid. When a solution is invalid, it explores the next possible path.

You can traverse the decision tree the same way you would explore an actual tree. [[Tree Traversal#Pre Order|Preorder]] and [[Tree Traversal#Post Order|Post Order]] are the most common ways to explore this decision tree. 

Because during backtracking we could possibly explore all possibilities of a decision tree, so the time complexity is the number of nodes in that tree. When exploring the tree using [[Depth-first search]] the time complexity is the height of said tree (with recursion). 

Because backtracking is inefficent, it is oftern a brute force approach, but for some problems there may not be a better algorithm. It can also be good to get something working that is slow, then get nothing working because of a focus on trying to get an optimal answer. 

## Example
For example, for the problem, given the array `[4,2,1,3]` find all possible solutions that add up to 6, the decision tree looks like the following. 
![[Backtracking Decision Tree 1.png]]
Along the decision tree, we keep a total so far along that path. If the path sums to 6 we have found a valid path, if we exceed 6 the path is marked as invalid. When we run out of options we also have found an invalid path.

*Not in this problem the minium value has to be 1, if values could be negative, we would have to keep searching after we exceed 6. If the values are 0 there might be valid routes after another valid answer*

