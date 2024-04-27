Need a quick refresher, or need to know where to start. This page give a simplified explanation of the topics in data structures and algorithms. 

## Arrays
[[Data Structures and Algorithms/Other Data Structures/Arrays]] contain multiple items in consecutive spaces in memory. For objects it holds pointers in consecutive spaces instead.

Arrays are of a predetermined size and cannot be changed after creation.

## Dynamic Lists
[[Dynamic List|Dynamic lists]] are like arrays but their size is not fixed. 

It works by copying the items of an array across into an array of double the size when there is no more space in the underlying array. 

The capacity refers to the size of underlying array. And the size refers the how full the underlying array is.

Although insertion of a dynamic list is O(1) it is important to remember deletions are O(n) time

## Linked lists
[[Linked List]] creates a list structure by storing elements with a pointer to the next element. The list ends when the next pointer points to null. 

We can append an element to the list by setting the next pointer of the last item to the new element. This allows a linked list be dynamic in size. 

## Stack
A [[Stack (Datastructure)|Stack]] can only append and remove elements at the end. This makes it a first in last out (FILO) datastructure, as the first item you put in will be the last item you get out. 

Stacks are frquently implimented using [[#Linked lists]] or a [[#Dynamic Lists]] 

## Queue
A [[Queue]] appends items to the end but removes items from the front. This makes it a first in first out (FIFO) datastructure, as the first item you put in will be the first item you get out. 

Queues are frequently implimented using [[#Linked lists]] or a [[Dynamic List]] (using a [[Circular Buffer]])

## Deque
A [[Deque]] can prepend / append or remove items from either the front or the back. This means you can use a deque like either a queue or a stack

Deques are frequently implimented using [[Linked List]] or a [[Dynamic List]] (using a [[Circular Buffer]])

## Hashmaps and sets
[[HashMaps and HashSets]] expolit hashing to be able to look up data in [[Constant time and space|constant time]]. Data can be hashed and put into different indexes of an [[#Arrays|Array]] based on this hash. 

To search for data we can then hash it, and look at that index of an array. 

HashMaps and HashSets are OP in the current meta.

## Graphs
[[Graphs]] are the concept where 'verticies' are connected with 'edges' to create a network of points and connections.

Graphs can be presented as a [[Graphs#Adjacency list|adjacency list]] or [[Graphs#Adjacency Matrix matrix|adjacency matrix]]

You can traverse all vertices of a graph in O(v + e) time using a [[Depth-first search|dfs]] or [[Breath-first Search|bfs]] traversal.

A [[Directed Graph|directed graph]] is a graph where edges can only be traversed in one direction.

An [[Cyclic and Acyclic graphs|acyclic graph]] is a graph with no cycles, while a [[Cyclic and Acyclic graphs|cyclic graph]] is one with cycles.

A [[Weighted Graph|weighted graph]] contains values called weights along each edge, oftern dictating the price of traversing that edge. 

A DAG is a nickname for a directed acyclic graph

A [[Topological Ordering]] finds an ordering of a DAG where a vertex's parents must be visted before its self. 

To find the shortest path between two nodes, theres a few different algorithms

[[BFS shortest path]] can find the shortest path in an unweighted graph using [[Breath-first Search|breath first search]] and says that the first time you find a node during BFS, that is the shortest path. 

[[DAG Relaxation]] is used for a weighted directed acyclic graph, and traverses a graph in a [[Topological Ordering]], relaxing a cost to a node with the best found cost so far. 

Dijkstra's Algorithm - watch this space

There are also a few other algorithms to note such as

Union find - watch this space

## Sorting algorithms
[[Sorting Algorithms]] are algorithms that sort a given collection into an order. The fastest algorithm we know to sort data runs in O(nlogn) time and with O(1) extra memory

### Merge sort
One sorting algorithm is [[Merge Sort|merge sort]], that breaks an array down into indivual elements, and then merges them together.

To merge two sorted collections, we take the lowest value of either collection, and move it to the output, continue until both collections are empty. 

This algorithm runs in O(nlogn), typically it uses O(n).

### Quick sort
Another sorting algorithm is [[Quick Sort|quick sort]]. Quick sort works by partioning an array so that at a given pivot, any smaller elements are on the left, and any larger elements are on the right. 

This algorithm runs in O(nlogn) on average, but can run as bad as O(n<sup>2</sup>), and uses O(logn) extra memory for recursive calls. 

## Binary search
[[Binary Search]] is away of searching through a sorted collection in O(logn) time.

We start at the center of a collection. If this is the target, we have found it. If target is smaller, we can rule out this and any larger values, simularly if the target is larger, we can rule out any smaller values. Repeat with this new section until we have either found it, or we are out of possibilities.

## Trees
[[Trees]] are datastruture made up of nodes can that point to multiple child nodes. Each child node can only have one parent. 

[[Trees]] are actually a graph, and therefore alot of the same algorithms can be used. 

Theres 4 common ways to traverse a tree. [[Tree Traversal#Pre Order|Pre-Order]] [[Tree Traversal#In Order|In-Order]] [[Tree Traversal#Post Order|Post-Order]] which use [[Depth-first search]] and [[Tree Traversal#Level Order|Level-Order]] that uses [[Breath-first Search]].

A tree is considered balanced where the difference in height between their children does not differ by more than 1.

A binary tree has a left and right node. 

### Binary Search Tree
[[Bineary Search Trees]] turns [[#Binary Search]] into a datastructure. In a binary search tree, a nodes left descendants must be smaller, and a nodes right descendants must be bigger. 

To [[Bineary Search Trees#Searching|search]] for an item, if this node is equal to the target, we have found it, if smaller search left child, if bigger search right child. This takes O(logn) for a balanced tree, but can take O(n) if the tree is unbalanced.

[[Bineary Search Trees#Adding|Inserting]] an item works by looking for where that item should be, and inserting it in that location, and runs in O(logn) to search for that location.

[[Bineary Search Trees#Delete|Deleting]] an element in a binary search tree can also take O(logn) time

[[Bineary Search Trees#Getting the order|Getting the order]] from a binary search tree is as simple as doing an In order traversal on it.

Binary search trees can become unbalanced when items are inserted at inconvient orders, with a ascending or descending order being the worst case

### Red black trees
[[Red black tree]] are a form of self balancing binary search trees that refer to each node as either red or black. Each node has to follow certain rules. Maintaining these rules keeps the tree balanced.

### Tries
A [[Trie]] is a [[#Trees|Tree]] datastructure where each node represents an element inside a sequence and are ofterned used to validate words and phrases. Tries are good at suggesting ends to sequences, as well as validating if a sequence is in a datastructure. 

Another key strength of the datastructure is reduces repeated space usage for sequences that start the same way. For example Candy and Can and Cait all start with Ca and in a trie Ca at the start will only be stored once.

## Heaps


## Prefix sum
[[Prefix Sum]] is the concept of storing the sum of previous elements in a datastructure. 

Doing it in reverse is called a postfix sum, and gives the sum of future elements. 

Combining a prefix and a postfix sum, you can get a sum of all elements apart from the current, useful when the inverse operation is unavaliable or slow. 

It doesn't have to be a sum it can be a product, or any total value

## Backtracking
[[Backtracking]] is the process of exploring every possibility of the descision tree. 

## Dynamic programming
[[Dynamic programming]] applies the concept of storing the answers to subproblems, to solve other subproblems and the problem in general. 

In memoisation we cache the results of subproblems during exploration of a decision tree, seen in [[#Backtracking]]. 

From there we can look out how this memoisation array is built up, and build it up ourselves, removing the need for calls on the call stack. 

## Greedy

## Two pointers

## Sliding window


