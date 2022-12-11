A trie is a [[Trees|tree]] datastructure in which paths along a tree indicate valid sequences of data, oftern used for words, and text phrases. 

Each node of a tree contains some data (normally a `char`), and can have multiple children. 

To indicate the end of a sequence (or `word`), each node can store an boolean indicating weather a sequence ends there. Alternatively you can store a child that signals the end of a sequence. 

Where there is an overlap with how sequences start, tries can reduce repeated storage. For example, `Cait`, `Can`, `Candy`, all start with `Ca`. It would be inefficent to store `Ca` multiple times. You can imagine over thousand of words, how this advantage could scale. This is one of the main advantages of using a trie. 

One note of a trie, is the root does not conain the data.

## Search
When searching for a sequnce, we can start at the root. For every index, we can see if our node contains that element, if it does we can move to that node. If it doesn't the sequence is not in the Trie. When we get to the last element of sequence, if that node is marked as the end of a sequence, the sequence has been found. If it is not marked as the end of a sequence, it is not in the trie.

### Example
*The below checks a trie for a sequence, in this case the sequence is a word*
```kt
fun containsWord(word : String) : Boolean {
	if (word.length == 0) return false
    var node = root
    word.forEach { char ->
        val lChar = char.lowercaseChar()
        if(!node.children.containsKey(lChar)) 
        	return false
        node = node.children.getValue(lChar)
    }
    return node.isWord
}
```

### Complexity
Time O(n)
Space O(1)

## Add Sequence
To add a sequence we can start at the root and the first element of the sequence. For the current element, we can see if the node contains the element in its children, if it does we can move to this node, and goto the next element. If it does not we can create a new node with this element as the data and move to the new node and next element. 

### Example
*The below example adds a sequence to a trie, in this case the sequence is a word*
```kt
fun addWord(word : String) { 
    if (word.length == 0) return
	var node = root
    word.forEach { char ->
        val lChar = char.lowercaseChar()
        node = node.children.getOrPut(lChar) { TrieNode(lChar, false) }     	
    }
    node.isWord = true
}
```

### Complexity
Time O(n)
Space O(1)

## Remove Sequence
To remove a sequence we recurse down the tree along the path of the sequence. For the end of the sequence, we can remove the end of the sequence flag. Then to remove the data from the tree, we can remove any nodes that have no children on the way back up the tree. Because we start at the end of the sequence for the removals any children belonging to this sequence only will of been removed already. Because of that we know if we have any children we must be also apart of another sequence. 

### Example
*The below example removes a sequence from a trie, in this case a sequence is a word*
```kt
fun removeWord(word : String) { 
	if (word.length == 0) return
    fun dfs(node : TrieNode?, parent : TrieNode?, index : Int) {
        if (node == null || index >= word.length) return
        if (index == word.length - 1) {
            node.isWord = false
        }
        var nChar = word.getOrElse(index + 1) { '\u0000' }
        nChar = nChar.lowercaseChar()
        val child = node.children[nChar]
        dfs(child, node, index + 1)
        
        if(node.children.size == 0) {
            parent?.children?.remove(node.character)
        }
    }
    dfs(root, null, -1)  
}
```
The above code works by finding the next node for the sequence and recursing down the tree. 
The base case is when the node is null.

If the element is the last element of the sequence, we remove the end of sequence flag. In this code that is called `.isWord`

Finally we can remove this node from the tree by removing it from the parent's children. In this code I passed the parent down during the recursion for this purpose. 

### Complexity
Time O(n)
Space O(n)

## Maintaining State between Calls
With Tries we may want to remember where we are in the tree between calls. Imagine we are using a trie to give suggested valid words. We could suggest words based on the possible words that end below a certain node. As the user types more, we can progress this node downwards, as the possble words it could be strinks. It would be inefficent to start back from the top and go back down the tree to give more suggestions. For this you can return and keep reference to the node itself. Or you create an iterator class that manages this functionality. 

In the code examples, I created a wrapper class  `MyTrie` that protects the root, and doesn't expose the Nodes. This is because when I write code I oftern want to write code that is closed for modification and can't be broken by a consumer of my code. With many trie problems however this approach may not be desired. Or as I previously mentioned, you could create an iterator class. 

## Full example
```kt
fun main() {
    val trie = MyTrie()
	println("Add")
    println("-----------------------------")
    trie.addWord("Cait")
    println("added word Cait\n$trie")

    trie.addWord("Candy")
    println("added word Candy\n$trie")

    trie.addWord("Can")
    println("added word Can\n$trie")
    
	println("Contains")
    println("-----------------------------")
    println("contains word Can ${trie.containsWord("Can")}")
    println("contains word Cait ${trie.containsWord("Cait")}")
    println("contains word cait ${trie.containsWord("cait")}")
    println("contains word Cai ${trie.containsWord("Cai")}")
    println("contains word Kai ${trie.containsWord("Kai")}")
    
    println("Remove")
    println("-----------------------------")
    trie.removeWord("Can")
    println("remove word Can\n$trie")
    trie.removeWord("Candy")
    println("remove word Candy\n$trie")
    trie.removeWord("Cait")
    println("remove word Cait\n$trie")
}

class TrieNode(
    val character : Char,
    var isWord : Boolean
) {
    val children = hashMapOf<Char,TrieNode>()
    
    override fun toString() : String {
        return if (isWord) "$character*"
        else character.toString() 
    }
}

class MyTrie {
    
    private val root = TrieNode('\u0000', false)
    
    fun addWord(word : String) { 
        if (word.length == 0) return
    	var node = root
        word.forEach { char ->
            val lChar = char.lowercaseChar()
            node = node.children.getOrPut(lChar) { TrieNode(lChar, false) }     	
        }
        node.isWord = true
    }
    
    fun removeWord(word : String) { 
		if (word.length == 0) return
        fun dfs(node : TrieNode?, parent : TrieNode?, index : Int) {
            if (node == null || index >= word.length) return
            if (index == word.length - 1) {
                node.isWord = false
            }
            var nChar = word.getOrElse(index + 1) { '\u0000' }
            nChar = nChar.lowercaseChar()
            val child = node.children[nChar]
            dfs(child, node, index + 1)
            
            if(node.children.size == 0) {
                parent?.children?.remove(node.character)
            }
        }
        dfs(root, null, -1)  
    }
    
    fun containsWord(word : String) : Boolean {
		if (word.length == 0) return false
        var node = root
        word.forEach { char ->
            val lChar = char.lowercaseChar()
            if(!node.children.containsKey(lChar)) 
            	return false
            node = node.children.getValue(lChar)
        }
        return node.isWord
    }
    
    
    override fun toString() : String {
        val sb = StringBuilder()
        fun preOrder(node : TrieNode?, indent : Int) {
            if(node == null) return
            
            for(i in 0 until indent) { sb.append('|') }
            
            if(node == root) {
                sb.append('+')
            }
            else{
                sb.append(node.toString())
            }
            sb.append('\n')
            
            node.children.forEach { kvp -> 
            	val (_, childNode) = kvp
                preOrder(childNode, indent + 1)
            }
        }
        preOrder(root, 0)
        return sb.toString()
    }
}
```