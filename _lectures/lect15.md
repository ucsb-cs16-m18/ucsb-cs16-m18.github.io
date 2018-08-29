---
num: "Lecture 15"
desc: "Standard Library and Vectors"
ready: true
date: 2018-08-23 11:00:00.00-7:00
---

# Standard Library

* It’s rare if a programming language provides all of the necessary tools to accomplish a task "out of the box."
	* Programmers usually use provided building blocks to create something specific to fit their needs.
	* Programmers are also able to build additional building blocks to build upon as well.
* These libraries usually come standard with the language
	* You don’t have to download separate components.
	* The libraries should be cross-platform compatible (you shouldn’t have to code differently based on running it with Windows, Mac, or Linux)
* Implementing and maintaining libraries come with a cost
	* Python has a dedicated organization called the Python Software Foundation.
	* Java was developed and maintained by Sun Microsystems, which has been bought by Oracle.
	* C++ isn’t "owned" by anyone really.
* C++ isn’t a product of a large organization and is kinda organized like opensource
	* http://isocpp.org/, http://www.open-std.org/
	* Individual C++ compilers are then implemented based on the specifications.
		* g++ / clang++ for UNIX
		* Visual Studio for Microsoft
	* There isn’t any guarantee that these behave EXACTLY the same, but do for the most part based on the specifications.
	* In this class, we’ll assume we’re using the C++11 specification unless stated otherwise.

# std::vector
	
* So far, we've been writing and maintaining arrays on the stack and the heap.
* std::vector is a container class using arrays and is part of the standard library.
* Conceptually, a vector is a sequence of objects that are stored one after the other just like arrays.
	* But all of the maintenance of this container are managed for us (i.e. dynamicaly memory manage arrays under-the-hood).
* Vectors are implemented with templates, so you can store one data type in the vector container.
	* For now, think of defining the template type in the "< >" brackets.
	* Details of templates are outside the scope of this course.

## Example

```
#include<vector>

using namespace std;

int main() {
	vector<int> v; // a vector containing int elements
	return 0;
}
```

* The <int> syntax defines the data type the vector variable v will store.
* Under-the-hood, vectors are implemented using arrays and behave similar to arrays.
	* Vectors can be indexed starting from 0 to size – 1
* Yet they’re different than arrays…
	* Vectors are dynamically-resizable
	* Vectors have a size() method associated with it.
		* Arrays do not know their size and the programmer must be aware of it.
	* Vectors do not need an initial capacity when defining it.

## Example: Adding to vectors

```
vector<int> v;
for (int i = 0; i < 5; i++) // adding five elements
	v.push_back(i);
}

// Can access elements in vectors with [] similar to arrays
for (int i = 0; i < v.size(); i++) {
	v[i] *= 2;
}

for (int i = 0; i < v.size(); i++) {
	cout << "v[" << i << "] = " << v[i] << endl;
}
```

* Like arrays, if you index a vector element that is out of range, you will probably get junk data or make your program crash.

## Range based loop

* Syntax shortcut for looping through containers in C++.

```
int arr[] = {1,2,3};

for (int x : arr) { // C++11 range-based loop extension
	cout << x << endl;
}

// Loops through the entire array, note if we change
// arr[] to arr[10], then the range based loop will
// loop through the ENTIRE array structure (even through
// values we did not define in { }).

// also can be used with vectors

int index = 0;
for (int i : v) {
	cout << "v[" << index << "] = " << i << endl;
	index++;
}
```

## Vector Initialization

* push_back is just one way to create elements in a vector.
	* You can declare a vector with a size initially
	* You can also initialize a vector with a size and default values.

```
vector<int> v1(100); // initializes vector with 100 elements = 0
vector<int> v2(100, 1); //initializes vector with 100 elements = 1
```

## Pointer to Vectors

* You can create a vector structure on the heap and have a pointer point to this.
	* Vectors are considered a type and we can allocate any type on the heap with "new"

```
vector<int>* v = new vector<int>(10,1);
cout << v->size() << endl;
```










