C++ is a [[Linked List]] implimentation, that provides a dynamically sized collection of data.

# Usage 

## Adding (Front and Back)
To add to the front and back respectively you can use `push_back` and `push_front` respectively
```cpp
list<int> my_list;
my_list.push_back(2); //[2]
my_list.push_back(3); //[2]->[3]
my_list.push_front(1); //[1]->[2]->[3]
```
### Time complexity 
pushing to front or back both take O(1)

## Removing (Front and Back)
To remove from the front and back respectively you can use `pop_back` and `pop_front` respectively
```cpp
list<int> my_list = { 1, 2, 3 }; //[1]->[2]->[3]
my_list.pop_first(); //[2]->[3]
my_list.pop_last(); //[2]
```
### Time complexity 
popping from front or back both take O(1)

## Iteration
Like alot of the [[C++ std library]] you can use an [[C++ std library#Iterators|iterator]] to iterate across the datastructure. 

## Adding (At iterator)
To add an element at the iterator location you can use the `insert` function.

```cpp
list<int> my_list = { 1, 4 }; //[1]->[4]
list<int>::iterator i = my_list.begin(); //i: ->[1]
++i; //i: ->[4]
my_list.insert(i, 2); //[1]->[2]->[4] //i: ->[2]
my_list.insert(i, 3); //[1]->[2]->[3]->[4]  //i: ->[3]
```
### Time complexity 
Adding an item at the iterator takes O(1), but of course the iteration itself could be worse

## Removing (At iterator)
To remove an element at an iterators location you can use the `erase` function, which not only removes an element at location, but also returns an iterator for the next location.
```cpp
list<int> my_list = { 1, 2, 3, 4 }; //my_list: [1]->[2]->[3]->[4]
list<int>::iterator it = my_list.begin(); //it: ->[1]
++it; //it: ->[2]
it = my_list.erase(it); //it: ->[3] my_list: [1]->[3]->[4]
```
### Time complexity 
Removing an item at the iterator takes O(1), but of course the iteration itself could be worse
