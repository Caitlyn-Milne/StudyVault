Using [[Higher-order functions]] can impose certain runtime performance penalities. 

Where a function takes in a [[Lambda|lambda]] we can improve performance with `inline`. Inline injects the code at the caller site at compile time. This means it is as if the functions code is in the location of where its being called from. 

*pre-compiled kotlin code
```kt
fun foo(){
	print("foo before")
	bar {
		println("lambda")
	}
	print("foo before")
}

inline fun bar(action : () -> Unit){
	print("bar before")
	action()
	print("bar after")
}
```

*compiled kotlin code*
```kt
fun foo(){
	print("foo before")
	//bars code is now in foo
	print("bar before")
	println("lambda")
	print("bar after")
	
	print("foo before")
}
```