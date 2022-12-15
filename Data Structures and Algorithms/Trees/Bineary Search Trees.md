![[BST 1.png]]

A binary search tree is a [[Trees#Binary Tree|binary tree]] where at any given node, all left descendants are smaller than the node and all right descendants of child is bigger than the node. 

This means that if a node is smaller than its parent, but bigger then its parent's parent, its an invalid binary search tree. 

Binary search tree exploits the logic found in [[Binary Search|binary search]], and is basically binary search implimented into a datastructure. 

## Searching
To search for an 'target' element, we can start a search at the root node.
Searching at a node looks like the following. If this node is none, we couldn't find the target. If this node is the target, we have found the node. If the target is smaller than this node, search left. If the target is larger than this node search right. (If left or right node doesn't exsit, search none)
```kt
private fun search(target : Int) : SearchResult {
    var parent = dummy
    var node = root
    while (node != null) {
        if (target == node.value) 
        	return SearchResult(parent, node)
        parent = node
        if (target < node.value) {
        	node = node.leftChild
            continue
        }
        node = node.rightChild
    }
    return SearchResult(parent, node)
}
```
### Complexity 
Time complexity O(logn)
Addition space O(1)

## Adding
To add elements to BST we can complete a search, if we find the node, the operation is invalid. If we find null, we want to insert the node into this location, to do this we can keep track of the previous node (aka the parent) during an search. We create a new node and if the value is smaller then the parent / previous node, we set the parents left child to this new node, otherwise we want to set the right child instead. 
```kt
fun add(value : Int) { 
    val (parent, foundNode) = search(value)
    if (foundNode != null) throw Exception("invalid operation")
    val node = BstNode(value, null, null)
    if (value < parent.value) {
       parent.leftChild = node
        return
    }
    parent.rightChild = node   
}
```
### Complexity
Time complexity O(logn)
Additional space O(1)

## Delete 
I have implimentented a deletion algorithm in the [[#Full example]] but I am not happy with the written complexity of it. Watch this space 
### Complexity
Time O(logn)
Addition space O(1)

## Balance
Binary search trees can become unbalanced when items are inserted at inconvient orders, with a ascending or descending order being the worst case.

## Getting the order
An inorder traversal of a binary search tree returns a traversal in order.

## Full example
```kt
import kotlin.test.*

fun main() {
    val bst = MyBST()
    println("Additions:")
    println("------------------------")
    bst.add(4)
    println("add 4\n$bst")
    bst.add(2)
    println("add 2\n$bst")
    bst.add(6)
    println("add 6\n$bst")
    bst.add(1)
    println("add 1\n$bst")
    bst.add(3)
    bst.add(5)
    bst.add(7)
    bst.add(8)
   	println("add 3 5 7 8\n$bst")
    println("\nContains:")
    println("------------------------")
    println("contains 4 = ${bst.contains(4)}")
    println("contains 12 = ${bst.contains(12)}")
    
    println("\nDeletions")
    println("------------------------")
    println("before\n$bst")
    bst.remove(4)
    println("removed 4\n$bst")
    bst.remove(6)
	println("removed 6\n$bst")
    bst.remove(8)
	println("removed 8\n$bst")
}

 class BstNode(
    val value : Int,
    var leftChild : BstNode?,
    var rightChild : BstNode?
) {
    override fun toString() : String {
        return value.toString()
    }
}

class MyBST {
    var dummy : BstNode = BstNode(Int.MIN_VALUE, null, null) 
    val root : BstNode? 
    	get() = dummy.rightChild
    
     private fun search(target : Int) : SearchResult {
        var parent = dummy
        var node = root
        while (node != null) {
            if (target == node.value) 
            	return SearchResult(parent, node)
            parent = node
            if (target < node.value) {
            	node = node.leftChild
                continue
            }
            node = node.rightChild
        }
        return SearchResult(parent, node)
    }
     
    fun add(value : Int) { 
        val (parent, foundNode) = search(value)
        if (foundNode != null) throw Exception("invalid operation")
        val node = BstNode(value, null, null)
        if (value < parent.value) {
           parent.leftChild = node
            return
        }
        parent.rightChild = node   
    }
    
	fun contains(value : Int) : Boolean {
        val (_, node) = search(value)
        return node != null
    }
    
    fun remove(value : Int) { 
        var (parent,item) = search(value)
        if(item == null) return
        var numChildren = 0
        if (item.leftChild != null) numChildren++
        if (item.rightChild != null) numChildren++
        
        when (numChildren) {
        	0 -> remove0Children(parent, item)
            1 -> remove1Child(parent, item)
            2 -> remove2Children(parent, item)
        }
    }
   
   	private fun remove0Children(parent : BstNode, node : BstNode) {
       	setParentNext(parent, node, null)
    }
    
    private fun remove1Child(parent : BstNode, node : BstNode){
        setParentNext(parent, node, node.leftChild ?: node.rightChild)
    }
    
    private fun remove2Children(parent : BstNode, node : BstNode) {
        val (n2, n1) = search(node.value + 1)
        val next = n1 ?: n2
        var (swapParent, swapNode) = search(next!!.value)
        swap (parent, node, swapParent, swapNode!!)
        
        var numChildren = 0
        if (node.leftChild != null) numChildren++
        if (node.rightChild != null) numChildren++
       
        if (swapParent == node) {
            swapParent = swapNode
        }
        when (numChildren) {
        	0 -> remove0Children(swapParent, node)
            1 -> remove1Child(swapParent, node)
            else -> Exception()
        }
    }
    
    private fun setParentNext(parent : BstNode, node : BstNode, next : BstNode?) {
        if (parent == null) return
        if (parent.leftChild == node) {
        	parent.leftChild = next
        }
        else {
            parent.rightChild = next 
        }
    }
    
    private fun swap(
        aParent : BstNode,
        aNode : BstNode,
        bParent : BstNode,
        bNode: BstNode
    ) {
        setParentNext(aParent, aNode, bNode)
        setParentNext(bParent, bNode, aNode)
        
        var temp = aNode.leftChild
        aNode.leftChild = bNode.leftChild
        bNode.leftChild = temp
        
        temp = aNode.rightChild
        aNode.rightChild = bNode.rightChild
        bNode.rightChild = temp
    }
    
   override fun toString() : String {
       	val sb = StringBuilder()
       	fun dfs(node : BstNode?, indentation : Int) {
            if (node == null) return
            dfs(node.leftChild, indentation + 1)
           	val prefix = String(CharArray(indentation*2){'-'})
            sb.append("$prefix${node.value}\n")
            dfs(node.rightChild, indentation + 1)
        }
        dfs(root, 0)
        return sb.toString()
    }
    
    data class SearchResult(
        val parent : BstNode,
        val node : BstNode?
    ) {}
    
}
```
[Kotlin playground](https://pl.kotl.in/e0_kiFjkR)