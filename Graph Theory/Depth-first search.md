A depth first search (also known as dfs) is a traversal [[Algorithm|algorithm]] that allows you to traverse all vertices of a [[Graphs|Graph]]. Simular to [[Breath-first Search|breath-first search]].

In a preorder version of a depth first search, you first visit a given vertex before visiting a neighbour. The process then repeats for that neighbour. When there is no more unvisited neighbours for a given vertex, it will backtrack exploring any unvisted neighbours on the way back. This means in dfs it will explore a neighbour's neighbour before another neighbour unlike [[Breath-first Search]].

*figure 2 - a graph drawn in paint*
![[figure 2.png]]

Basically In depth first search the traversal moves in one direction until it cant anymore, before searching any paths it missed.

Depth first search uses a [[Stack (Datastructure)|stack]] inside it's algorithm, whether its a stack datastructure or the [[Call stack|call stack]].

## Example
starting at vertex 2 in figure 2, a depth first search may look like
2 -> 1 -> 4 (backtrack) 2 -> 3 (backtrack) 2 -> 5 -> 6
for a result of 2,1, 4, 3, 5, 6

## Implimentations
### Recursive
In code a recursive algorithm for this may look like the following

```kt
fun dfs(
	vertex : GraphVertex) 
	: MutableList<GraphVertex>{
	
	val result = mutableListOf<GraphVertex>()
	dfs(vertex, hashSetOf<GraphVertex>(), result)
	return result
}

fun dfs(
	vertex : GraphVertex, 
	visited : HashSet<GraphVertex>,
	result : MutableList<GraphVertex>){
	
	if(visited.contains(vertex)) return
    
	visited.add(vertex)
	result.add(vertex)
	
	vertex.neighbours.forEach{ neighbour ->
		dfs(neighbour,visited,result)
	}
}
```

Learn more about recursion - [[Recursion]]


### Iterative
In code a iterative algorithm for this may look like the following

```kt
fun dfs(
	startingVertex : GraphVertex
	) : MutableList<GraphVertex>{
	
	val stack = ArrayDeque<GraphVertex>()
	stack.addLast(startingVertex)
	
	val visted = hashSetOf<GraphVertex>()
	val results = mutableListOf<GraphVertex>()
	
	while(stack.any()){
		val vertex = stack.last()
		stack.removeLast()

		if(visted.contains(vertex)) continue
		visted.add(vertex)
		results.add(vertex)

		vertex.neighbours.forEach{ neighbour -> 
			stack.addLast(neighbour)
		}
	}
	
    return results
}
```

Learn more about iteration - [[Iteration]]


## Working Example
if you want you can see dfs in action, copying this code into kotlins playground
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
    
    
    println("\nRecursion")
    val resultRecursive = dfs(v2)
    resultRecursive.forEach { vertex ->
        println(vertex.toString())
    }
    
    println("\nIteration:")
    val resultIterative = dfsIterative(v2)
    resultIterative.forEach { vertex ->
        println(vertex.toString())
    }
}


fun dfs(vertex : GraphVertex) : MutableList<GraphVertex>{
	val result = mutableListOf<GraphVertex>()
	dfs(vertex, hashSetOf<GraphVertex>(), result)
	return result
}

fun dfs(
	vertex : GraphVertex, 
	visited : HashSet<GraphVertex>,
	result : MutableList<GraphVertex>){
	
	if(visited.contains(vertex)) return
    
	visited.add(vertex)
	result.add(vertex)
	
	vertex.neighbours.forEach{ neighbour ->
		dfs(neighbour,visited,result)
	}
}

fun dfsIterative(
	startingVertex : GraphVertex
	) : MutableList<GraphVertex>{
	
	val stack = ArrayDeque<GraphVertex>()
	stack.addLast(startingVertex)
	
	val visted = hashSetOf<GraphVertex>()
	val results = mutableListOf<GraphVertex>()
	while(stack.any()){
		val vertex = stack.last()
		stack.removeLast()

		if(visted.contains(vertex)) continue
		visted.add(vertex)
		results.add(vertex)

		vertex.neighbours.forEach{ neighbour -> 
			stack.addLast(neighbour)
		}
	}
    return results
}
```