Graphs are the concept where 'verticies' are connected with 'edges' to create a network of points and connections.

*figure 1 - below is an example of a graph*
![[figure 1.png]]

You can think of each vertex as having connections (called edges) to other verticies. 

A vertex's connected vertices are called their neighbours.

## Graph in a datastructure
Storing a graph in frequently done in one of 2 ways

### Adjacency list
In an adjacency list, each vertex stores a list of connected neighbours

In figure 1 above, the adjacency list would look like the following
```json
1 [2,5]
2 [1,3,5]
3 [2,4]
4 [3,5,6]
5 [1,2,4]
6 [4]
```

### Adjacency [[Matrix|matrix]]
An adjancy matrix is a matrix where each element describes a connection or no connection. 1 is oftern used to donote a connection and 0 for no connection.

Take the graph in figure 1, when stored in an adjacency matrix it looks like the following
```json
  1 2 3 4 5 6
1 0 1 0 0 1 0
2 1 0 1 0 1 0
3 0 1 0 1 0 0
4 0 0 1 0 1 1
5 1 1 0 1 0 0
6 0 0 0 1 0 0
```

### [[#Adjacency Matrix matrix|Adjacency matrix]] vs [[#Adjacency list|Adjacency list]]
When a graph is sparse, we need less space to reperesent the graph. In this scanerio an adjacency matrix still is the size of n<sup>2</sup> meanwhile the adjacency list only stores an equaliant to E where E is the amount of edges. Because of this Adjacecy list is oftern prefered over adjacency matrix where the graph is sparse. 
