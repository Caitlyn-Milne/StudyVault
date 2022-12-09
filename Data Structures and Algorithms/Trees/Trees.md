A tree is a hierarchical data structure, and is made up of nodes. Each node of the tree can be connected with many children, but can only have one parent (apart from the root of the tree that has 0). Trees are a subset of [[Graphs|graph theory]], because trees are in themselves a type of graph. 

Because of the constains of a tree, trees can't have cycles.

Each child of a given node, makes a tree of its own, this is called a subtree, because of this, logic that can be applied to a tree, can also be applied to its child elements or subtrees. 

![[Tree 1.png]]

## Key terminology

### Node
An element inside the tree

### Root 
The root of a tree is the top most node on a tree. 

### Child
A child element of a node is any connected nodes below itself

### Parent
A parent element of a node is the node that points to this node.

### Leaf
A node with no children is called a leaf.

### Neighbor
A child or parent

### Path
A path is a seris of nodes, that when taken, traverse the path from one node to another

### Ancestor
Any node that is reachable in a path going up the tree from this node to the root. 

### Descendant
Any node that is reachable in the path going from this node to the leaf

### Level
A level is a group of nodes, where each node in the group has the same length path from the root node

### Width
Number of nodes in a level

### Width of a tree
Maxium width of a level

### Height
The height of a tree is the length of the longest path from the root to a leaf. 

### Degree 
For a given node, a degree is the number of children that node has. The degree of a leaf is 0. 

### Degree of a tree 
For a given tree, the degree of that tree is the maxium degree of one of its nodes.

### Forest
A collection of unconnected trees.

### Subtree
A tree that is created by treating a none root element as a tree. Every node is a subtree apart from the root is a subtree.

### Binary Tree
A tree with degree of 2