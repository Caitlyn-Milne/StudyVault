
## Iterators
Alot of the datastructures in the c++ std library have iterators that generally can be retrieved with the `begin` and `end`.

`begin` returns the iterator at the begining of the list, while `end` returns an iterator beyond the end of the datastructure. You can progress the datastructure by using the `++` operator.

```cpp
vector<int> vec = { 1, 2, 3, 4 };
vector<int>::iterator it = vec.begin();
int value = *it; //1
++it;
value = *it; //2
```

```cpp
//in combination with a for loop
vector<int> vec = { 1, 2, 3, 4 };
 = vec.begin();
for(auto it = vec.begin(); it != vec.end(); ++it){
	cout << *it << endl
}
/* output
1
2
3
4 */
```
Some datastructures may also provide reverse iterators that traverse the datastructure backwards which can be accessed with `rbegin` and `rend` functions. 

Simularly if you want an iterator that cannot modify the data it points to, you can use a constant iterator, that are accessed with the `cbegin` and `cend` functions.