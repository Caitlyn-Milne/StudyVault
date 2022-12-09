[[Breath-first Search]] can be used with modification for a fairly simple shortest path algorithm. Because BFS expands out, the first time we find a vertex in BFS via a given path will be garenteed to be the fastest route to that vertex.

## Implimentation
Below is the code to find the shortestPathLength between two vertices

```kt
fun shortestPathLength (
    edges : List<List<Int>>,
    from : Int,
    to : Int
) : Int {
    val graph = edgesToAdjancency(edges)
    if(!graph.containsKey(from) || !graph.containsKey(to)) 
    	throw Exception("from and to are not in the graph") 
    val queue = ArrayDeque<Pair<Int,Int>>()
   	val seen = hashSetOf<Int>()
    queue.addLast(Pair(from,0))
    while (queue.size > 0) {
        val (vertex, distance) = queue.removeFirst()
        if (vertex == to) return distance
        if (seen.contains(vertex)) continue
        seen.add(vertex)
        graph.getValue(vertex).forEach { neighbor ->
            queue.add(Pair(neighbor, distance + 1))
        }
    }
    return -1
}
```
### Time complexity 
Time O(v+e)
Space O(v+e)

Below is the code to find the shortestPath between two vertices, and then returns it. 

It does a BFS and stores the parent we got to the given node from in a hashMap so if we find the 'to' vertex we can reconstruct the path. 
```kt
fun shortestPath (edges : List<List<Int>>, from : Int, to : Int) : List<Int> {
    val graph = edgesToAdjancency(edges)
    if(!graph.containsKey(from) || !graph.containsKey(to)) 
    	throw Exception("from and to are not in the graph") 
    val queue = ArrayDeque<Pair<Int,Int>>()
   	val seen = hashMapOf<Int,Int>()
    queue.addLast(Pair(from, -1))
    while (queue.size > 0) {
        val (vertex, parent) = queue.removeFirst()
        if (seen.containsKey(vertex)) continue
        seen.put(vertex, parent)
        if (vertex == to) break
        graph.getValue(vertex).forEach { neighbor ->
            queue.add(Pair(neighbor, vertex))
        }
    }
    var result = mutableListOf<Int>()
    var v = to
    while(seen.containsKey(v)) {
        result.add(v)
        v = seen.getValue(v)
    }
    return result  
}

```
### Time complexity 
Time O(v+e)
Space O(v+e)
[Kotlin playground](https://pl.kotl.in/OZwbJQ_Oy?theme=darcula)