C++'s `std::array` class is apart of [[C++ std|C++'s standard template library]] that provides abstraction of an underlying [[C++ static array (C style arrays)]], as well as providing key array functionality checking, as well as bound checking in debug enviroments. 

# Usage
## Definiting
To define a C++ std array we can use the following syntax
```cpp
//create an array of size 3
std::array<int,3> nums; 
```

```cpp
//creates an array of size 3, containing the values 1,2,3
std::array<int, 3> nums = { 1, 2, 3 }
```

```cpp
//creates an array on the heap, containing the values 1,2,3
std::array<int, 3>* nums = new std::array<int, 3>({ 1, 2, 3 });
```

## Function Arguments
Of course we can pass a `std::array` into a function the normal way, however what if you want to create a function that can accept an array of any length. Here we can use a [[C++ Templates|templated]] function. 

```cpp
template <std::size_t SIZE>
void print_std_array(const std::array<int, SIZE>& arr)
{
	for (const int num : arr)
	{
		std::cout << num << std::endl;
	}
}

int main()
{
	const std::array<int, 3> nums = {1,2,3};
	print_std_array(nums);
}
```

## Sort
There is a predefined sort algorithm provided in [[C++ std]] in the algorithms header file.
```cpp
#include <algorithm>
int main()
{
	std::array<int, 3> nums = { 3, 2, 1 };
	std::sort(nums.begin(), nums.end());
}
```
See [[Sorting Algorithms]]

# Performance
Because C++ std array stores the size of the array inside a [[C++ Templates|template]] argument, during run time, no space is used for storing the size of the array. 