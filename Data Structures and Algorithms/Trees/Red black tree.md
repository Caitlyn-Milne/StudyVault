A red black tree is a form of self balancing [[Bineary Search Trees]]. It assigns every node a red or a black value, where there are 4 rules to maintain. 

1. A node is either red or black
2. The root and leaves are considered black. (We consider the leaves to be pointers to null in this case)
3. If a node is red, then its children are black.
4. All paths from a node to its leaves (null) contain the same number of black nodes

## Rotations
The red and black tree uses a concept called rotations in a few of its algorithms. Lets say we want to rotate a tree left around node `x`. Lets declare `y` to be `x.right` at the start. `y` becomes the parent of `x` on the left. The previous `y.left` becomes the right of `x`. If `x` was the root, update the new root to be `y`. 
Change `x` parent to now point to `y`
### Complexity
Rotations take O(1) time complexity, unless we first have to find the node, in which cause it will take O(logn) time.
Space is O(1)


The following code should not be used as an example as it is incomplete
```kt

fun main() {
    val rbt = MyRBT()
    rbt.insert(4)
    rbt.insert(2)
    rbt.insert(6)
    rbt.insert(1)
    rbt.insert(3)
    rbt.insert(5)
    rbt.insert(7)
    println("rbt\n$rbt")
    
    rbt.rotateLeft(6)
    println("rbt\n$rbt")
    
    rbt.rotateRight(7)
    println("rbt\n$rbt")
}

data class RBTNode(
    val value : Int,
    var parent : RBTNode?,
    var left : RBTNode?,
    var right : RBTNode?,
    var red : Boolean
) {
    override fun toString() : String {
        return value.toString()
    }
}

class MyRBT {
    var root : RBTNode? = null
    
    fun insert(value : Int) {
        val node = basicInsert(value)
    }
    
    private fun basicInsert(value : Int) : RBTNode {
    	val node = RBTNode(value, null, null, null, true)
        val (found, parent) = search(value)
        if (found != null) throw Exception("Cannot enter duplicate value")
        
        if(parent == null) {
            root = node
            return node
        }
        
        node.parent = parent
        if (value < parent.value) {
            parent.left = node
            return node
        }
        parent.right = node
        return node
    }
    
    private fun contains(target : Int) : Boolean {
        val (node, _) = search(target)
        return node != null
    }
    
    private fun search(target : Int) : Pair<RBTNode?, RBTNode?> {
        if (root == null) return Pair(null, null)
    	var node = root
        var previous : RBTNode? = null
        while (node != null) {
            if (target == node.value)
            	return Pair(node, previous)
            previous = node
            if (target < node.value) {
            	node = node.left
                continue
            }
            node = node.right 
        }
        return Pair(node, previous)
    }

    fun rotateLeft(around : Int) {
        val (node, _) = search(around)
        if(node == null) throw Exception("")
        rotateLeft(node)
    }
    
    private fun rotateLeft(around : RBTNode) {
        val other = around.right
        if (other == null) return
        val temp = other.left
        other.left = around
      	around.right = temp

        around.parent?.let{ parent ->
            if(parent.left == around) {
           		parent.left = other 
                other.parent = parent
                return@let
        	}
            parent.right = other 
            other.parent = parent
        } ?: run { root = other }
        around.parent = other
        temp?.apply {parent = around}
    }
    
   	fun rotateRight(around : Int) {
        val (node, _) = search(around)
        if (node == null) return
        rotateRight(node)
    }
    
    private fun rotateRight(around : RBTNode) {
        val other = around.left
        if (other == null) return
        val temp = other.right
        other.right = around
        around.left = temp
        around.parent?.let { parent ->
            if (parent.left == around) {
                parent.left = other 
                other.parent = parent
                return@let
            }
            parent.right = other
            other.parent = parent
        } ?: run { root = other }
        around.parent = other
        temp?.apply {parent = around}
    }
    
    override fun toString() : String {
        if (root == null) return "empty"
        val sb = StringBuilder()
        fun inOrder(node : RBTNode?, ident : Int) {
            if (node == null) return
            inOrder(node.left, ident + 1)
            val redTxt = if(node.red) "red" else "black"
            for(i in 0 until ident) { sb.append("|") }
            val parentTxt = node?.parent?.value ?: "root"
            sb.append("${node.value} (${redTxt}) {$parentTxt}\n")
            inOrder(node.right, ident + 1)
        }
        inOrder(root, 0)
        return sb.toString()
    }
}
```