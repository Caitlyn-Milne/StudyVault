Because a tree is a graph, we can use graph traversal algorithms on a tree, such as [[Depth-first search|DFS]] and [[Breath-first Search|BFS]]. Because it is imposible for a loop to be made, we do not need to keep track of what nodes have been seen.

![[Tree 2.png]]
## Pre Order
Doing a [[Depth-first search|DFS]] and visiting a node before we visit the left and right child gives us a preorder traversal. 
```kt
fun preOrderTraversal(node : TreeNode?, result : MutableList<TreeNode>) {
	if (node == null) return
	result.add(node)
	preOrderTraversal(node.leftChild, result)
	preOrderTraversal(node.rightChild, result)
}
```
[Kotlin playground](https://pl.kotl.in/1FOTNo-oG?theme=darcula)
## In Order
Doing a [[Depth-first search|DFS]] and visiting a node inbetween the left and right child gives us a in order traversal. 
```kt
fun inOrderTraversal(node : TreeNode?, result : MutableList<TreeNode>) {
	if (node == null) return
	inOrderTraversal(node.leftChild, result)
    result.add(node)
	inOrderTraversal(node.rightChild, result)
}
```
[Kotlin playground](https://pl.kotl.in/1FOTNo-oG?theme=darcula)
## Post Order
Doing a [[Depth-first search|DFS]] and visiting a node after we visit the left and right child gives us a postorder traversal. 
```kt
fun postOrderTraversal(node : TreeNode?, result : MutableList<TreeNode>) {
	if (node == null) return
	postOrderTraversal(node.leftChild, result)
	postOrderTraversal(node.rightChild, result)
    result.add(node)
}
```
[Kotlin playground](https://pl.kotl.in/1FOTNo-oG?theme=darcula)
## Level Order
Doing a [[Breath-first Search|BFS]] gives us a level order traversal. Here we visit nodes one level at a time.
```kt
fun levelOrderTraversal(root : TreeNode?, result : MutableList<TreeNode>) {
	if (root == null) return
    val queue = ArrayDeque<TreeNode>()
    queue.addLast(root)
    while (queue.size > 0) {
        val node = queue.removeFirst()
        result.add(node)
        if (node.leftChild != null) {
        	queue.addLast(node.leftChild)
        }
        if (node.rightChild != null) {
        	queue.addLast(node.rightChild)
        }
    }
}
```
[Kotlin playground](https://pl.kotl.in/1FOTNo-oG?theme=darcula)

## Complexity
For all of these algorithms the time complexity is O(n) and the space O(n)

## Full Example
```kt
import kotlin.test.*

data class TreeNode(
    val value : Int,
    val leftChild : TreeNode?,
    val rightChild : TreeNode?
) {
    override fun toString() : String {
        return value.toString()
    }

}

fun printTree(node : TreeNode?, indent : Int = 0) {
    if (node == null) return
    val prefix = String(CharArray(indent) {'-'})
    println("$prefix$node")
    printTree(node.leftChild, indent + 1)
    printTree(node.rightChild, indent + 1)
}

fun main() {
    val root = TreeNode(1,
                    TreeNode(2,
                        TreeNode(4,null,null),
                        TreeNode(5,
                            TreeNode(6,null,null), null)),
                    TreeNode(3,null,null))
    println("Tree")
    printTree(root)
    println("--------------------------------------")
    val result = mutableListOf<TreeNode>()
    preOrderTraversal(root, result)
    println("preorder ${result.joinToString()}")
    
    result.clear()
    
   	inOrderTraversal(root, result)
    println("inOrder ${result.joinToString()}")
    
    result.clear()
    
	postOrderTraversal(root, result)
    println("postOrder ${result.joinToString()}")
    
    result.clear()
    
	levelOrderTraversal(root, result)
    println("levelOrder ${result.joinToString()}")
    
}

fun preOrderTraversal(node : TreeNode?, result : MutableList<TreeNode>) {
	if (node == null) return
	result.add(node)
	preOrderTraversal(node.leftChild, result)
	preOrderTraversal(node.rightChild, result)
}

fun inOrderTraversal(node : TreeNode?, result : MutableList<TreeNode>) {
	if (node == null) return
	inOrderTraversal(node.leftChild, result)
    result.add(node)
	inOrderTraversal(node.rightChild, result)
}

fun postOrderTraversal(node : TreeNode?, result : MutableList<TreeNode>) {
	if (node == null) return
	postOrderTraversal(node.leftChild, result)
	postOrderTraversal(node.rightChild, result)
    result.add(node)
}

fun levelOrderTraversal(root : TreeNode?, result : MutableList<TreeNode>) {
	if (root == null) return
    val queue = ArrayDeque<TreeNode>()
    queue.addLast(root)
    while (queue.size > 0) {
        val node = queue.removeFirst()
        result.add(node)
        if (node.leftChild != null) {
        	queue.addLast(node.leftChild)
        }
        if (node.rightChild != null) {
        	queue.addLast(node.rightChild)
        }
    }
}
```
[Kotlin playground](https://pl.kotl.in/1FOTNo-oG?theme=darcula)

