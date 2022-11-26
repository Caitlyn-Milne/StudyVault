Something that is recursive has itself inside its definition. Inside computer science this normally means that a function calls itself. 

To create a recursive function, it can be best to imagine the problem space as a tree, with each node being apart of the [[Call stack|call stack]]. Each leaf of the tree is your base case.

Now you can first deal with the base case before worrying about the recursive case and the result.

This is just the way I've found useful to think about recursion. 