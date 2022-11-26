## Definition

A topological sort (or ordering) of a [[Directed Graph|directed]] [[Cyclic and Acyclic graphs|acyclic]] [[Graphs|graph]] is a way of ordering its vertices such that at every edge from u to v, u comes before v in the ordering. In other terms a vertex must come before any of its children. 

## Example

## Graph 3
![[graph 3.png]]

In [[#Graph 3]] we can see a [[Directed Graph|directed]] [[Cyclic and Acyclic graphs|acyclic]] graph with vertices 1..5

One valid Toplogical ordering is 
```
[5, 1, 2, 3, 4]
```

In this ordering you can validate that we include a vertex only after we have included all its parents. For example vertex 2 is only included once both 5 and 1 have been included

## Uniqueness 
For a given [[Directed Graph|directed]] [[Cyclic and Acyclic graphs|acyclic]] [[Graphs|graph]] there can be multiple valid topological orderings. This is because there might be multiple vertices where all the parents have been visited. In the above [[#Example|example]] another valid ordering would be:
```
[1, 5, 2, 3, 4]
```

## Acyclic 
The graph must be directed and acyclic for a topoligical ordering to be possible. The reasons why a graph must be acyclic is because if a graph has a cycle, we can not visit a vertex in a cycle. This is due that vertex being an ancestor of itself, and therefore we can not visit itself, without visiting itself.

## Implimentations

In code to create a topologicalOrdering, we do a [[Depth-first search|depth first search]], keeping track of the visited vertices along the path, as well as the vertices included in the result.

We build the answer bottom up. Instead of only adding a vertex if we have already included its parent, we only add a vertex if we have already seen all its children. That way we can recursively ask if the child if it has been included or if there is a cycle.

If we have already visited a vertex we have a cycle, which is invalid. In the [[#Kotlin code]] below, we return an empty result, but you could also return null or throw an error. 

If we have already included the child we can return true to inform our parent.

If all the vertexs children have been included, we can include ourself and return true to inform our parent.

### Kotlin code
```kt
fun topologicalOrdering(startingVertex : GraphVertex) : List<GraphVertex>{
    
    var visited = hashSetOf<GraphVertex>()
    var included = hashSetOf<GraphVertex>()
    var result = mutableListOf<GraphVertex>()
    
    fun dfs(startingVertex : GraphVertex) : Boolean {
        if(visited.contains(vertex)){
            return false
        }
        if(included.contains(vertex)){
            return true
        }
        visited.add(vertex)
        vertex.neighbours.forEach{ neighbor ->
            if(!dfs(neighbor)){
                return false
            }
        }
        visited.remove(vertex)
        included.add(vertex)
        result.add(vertex)
        return true
    }
    
    return if(dfs(startingVertex)) result.reversed()
    else listOf<GraphVertex>()
}
```
[kotlin playground](https://pl.kotl.in/J6q-ZS5_f)

In this code, only vertices in the subgraph starting with *startingVertex* will be outputted. 

To return a toplogical of a whole graph, we can instead iterate over all vertices in the graph and call dfs. Because already included vertices will return true, we will not do repeated calculations on already included vertices during the now included for loop. 

```kt
fun topologicalOrdering(vertices : Array<GraphVertex>) : List<GraphVertex>{
    
    var visited = hashSetOf<GraphVertex>()
    var included = hashSetOf<GraphVertex>()
    var result = mutableListOf<GraphVertex>()
    
    fun dfs(vertex : GraphVertex) : Boolean {
        if(visited.contains(vertex)){
            return false
        }
        if(included.contains(vertex)){
            return true
        }
        visited.add(vertex)
        vertex.neighbours.forEach{ neighbor ->
            if(!dfs(neighbor)){
                return false
            }
        }
        visited.remove(vertex)
        included.add(vertex)
        result.add(vertex)
        return true
    }
    vertices.forEach{ v -> 
        if(!dfs(v)) 
        	return@topologicalOrdering listOf<GraphVertex>() 
    }
	return result.reversed()
}
```
[kotlin playground](https://pl.kotl.in/0FXMxWmiC)

### Time and space
Time O(n)
Space O(n)