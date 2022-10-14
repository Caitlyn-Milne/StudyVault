A breath first search (also known as bfs) is a traversal [[Algorithm|algorithm]] that allows you to traverse all vertices of a [[Graphs|Graph]]. Simular to [[Depth-first search|depth first search]].

In a preorder version of a breath first search, you first visit a given vertex, before visiting all its neighbours, and then all its neighbours neighbours. If a vertex has been seen before, it will not revist it.

*figure 2 - a graph drawn in paint*
![[figure 2.png]]

A way of imagining BFS is a circle getting ever larger around the starting vertex, because BFS checks nearby vertices before far away vertices.

Breath-first search uses a [[Queue|queue]] inside its algorithm

## Example
starting at vertex 1 in figure 2, a breath-first search may look like
1 -> 
|  2 -> 
|   |  3
|   |  5
|   |  6
|  4 
for a result of 1, 2, 4, 3, 5, 6

## Implimentation
Breath-first search implimentation is very simular to [[Depth-first search#Implimentations#Iterative|depth-first search iterative implimentation]] 

```kt
fun bfs(
	startingVertex : GraphVertex
	) : MutableList<GraphVertex>{
	
	val queue = ArrayDeque<GraphVertex>()
	queue.addLast(startingVertex)
	
	val visted = hashSetOf<GraphVertex>()
	val results = mutableListOf<GraphVertex>()
	
	while(queue.any()){
		val vertex = queue.first()
		queue.removeFirst()

		if(visted.contains(vertex)) continue
		visted.add(vertex)
		results.add(vertex)

		vertex.neighbours.forEach{ neighbour -> 
			queue.addLast(neighbour)
		}
	}
	
    return results
}
```

## Working example
if you want you can see bfs in action, copying this code into kotlins playground
```kt
class GraphVertex(var value : Int){
	lateinit var neighbours : List<GraphVertex>
    override fun toString() : String{
        return value.toString()
    }
}

fun main() {  
    val v1 = GraphVertex(1)
    val v2 = GraphVertex(2)
    val v3 = GraphVertex(3)
    val v4 = GraphVertex(4)
    val v5 = GraphVertex(5)
    val v6 = GraphVertex(6)
    
    v1.neighbours = listOf(v2,v4)
    v2.neighbours = listOf(v1,v3,v5,v6)
    v3.neighbours = listOf(v2)
    v4.neighbours = listOf(v1)
    v5.neighbours = listOf(v2, v6)
    v6.neighbours = listOf(v2, v5)
    
    val result = bfs(v1)
    result.forEach { vertex ->
        println(vertex.toString())
    }
}

fun bfs(
	startingVertex : GraphVertex
	) : MutableList<GraphVertex>{
	
	val queue = ArrayDeque<GraphVertex>()
	queue.addLast(startingVertex)
	
	val visted = hashSetOf<GraphVertex>()
	val results = mutableListOf<GraphVertex>()
	
	while(queue.any()){
		val vertex = queue.first()
		queue.removeFirst()

		if(visted.contains(vertex)) continue
		visted.add(vertex)
		results.add(vertex)

		vertex.neighbours.forEach{ neighbour -> 
			queue.addLast(neighbour)
		}
	}
	
    return results
}
```
