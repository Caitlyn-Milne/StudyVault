DAG Relaxation is an algorithm for (as the name might suggest) [[Weighted Graph|weighted]] [[Directed Graph|directed]] [[Cyclic and Acyclic graphs|acyclic]] [[Graphs|graphs]] that finds the shortest path from one vertex to all other connected vertices.

It works by working storing the minium weight at a given vertex, and updating it if it finds a better weight. 

To do this we move long the graph in a [[Topological Ordering|toplogical ordering]]. The cost to a given vertex *u* via vertex *v* is inituively the cost to *v* plus the weight of E{u,v}.  Because by the time we visit a node in a topolical ordering we have visited all its parents, and therefore all the possible routes to the node, if we keep track of the lowest cost to this node, by the time we visit it, that cost we garenteed to be the lowest cost of a path to that vertex. This is the principle we exploit in DAG Relaxation

## Implimentation

The below example finds the cost of the shorted path from vertex `from` to vertex `to` by doing a DAG Relaxation algorithm until `to` is visited.

If no path is found, null is returned.
```kt
fun dagRelaxation(
    from : Int,
    to : Int,
    graph : HashMap<Int, HashMap<Int, Double>>)
: Double? {
    val topOrder = topologicalOrdering(from,graph)
    val weights = hashMapOf<Int, Double>()
    if (topOrder.size == 0) {
    	return null
    }

    for (v in topOrder) {
        weights[v] = Double.MAX_VALUE
    }
    
    weights[from] = 0.00
    
    for (vertex in topOrder) {
       val weight = weights.getValue(vertex)
       if(vertex == to) return weight
       for (kvp in graph[vertex]!!) {
           val (neighbor, neighborWeight) = kvp
           val neighborCost = weight + neighborWeight
           weights[neighbor] = Math.min(neighborCost, weights.getValue(neighbor))
       }
    } 
    return null
}
```
[Kotlin playground](https://pl.kotl.in/gL9IoHbyI?theme=darcula)

### Complexity
**Time O(v+e)** for traversing the graph (to create the topological ordering, and when iterating over the topological ordering)
**Space O(v)** for storing the topological ordering