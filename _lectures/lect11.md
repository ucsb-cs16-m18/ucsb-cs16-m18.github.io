---
num: "Lecture 11"
desc: "C++ Memory Model, Dynamic Memory"
ready: true
date: 2018-08-07 11:00:00.00-7:00
---

# Dynamic Memory Management

* So far, we have been working exclusively with static allocation and stack memory.
* ... but there are situations where knowing the exact size BEFORE runtime is limiting.
* It’s not feasible to store dynamically growing / shrinking objects on the stack!
* For dynamically allocating memory during the execution of a program, there’s the free store, or more commonly known as the heap.

# Heap
* The heap allows users to manually decide when, how much, and what will be stored in it.
* On the flip side, you must also decide when memory will be deallocated (deleted) in order to reuse it.
* <b>Q:</b> What happens if you forget to delete stuff from the heap?
	* Memory leaks! Memory space is finite and eventually your program will crash if unused memory is not being deleted.
* <b>Q:</b> But we can store strings of different sizes on the stack... what’s up with that?
	* On the stack, strings are a fixed size containing fields such as the length of the string, and a memory address to the sequence of characters on the heap.
	* Note that a memory address and integer size ARE of fixed length (as well as other information the string class may have).
	* Behind the scenes, as strings may grow and shrink on the heap, the address that points to the sequence of chars on the heap can change.
* The programmer manages heap memory space manually.

## "new" operator

* The primary use for pointers are to access objects that have been dynamically allocated on the heap.
* The result of "new" is a pointer to the object that was allocated on the heap.

## Example
```
int* p = new int(10);	// allocate an int on the heap and point p to it
*p = 2;			// sets the int value to 2 (without address change)
int& q = *p;		// q refers to the value that p points to
q = 4;			// change int value to 4

cout << *p << endl;	// prints 4

int* r = &q;		// make r point to the address that q refers to
*r = 6;			// change int value that r points to to 6

cout << *p << endl;	// prints 6
cout << q << endl;	// prints 6
cout << *r << endl;	// prints 6
```

![new example](newExample.png)

## "delete" operator

* Anytime you use the “new” operator, consider if you need to eventually delete the memory it consumes.
	* Otherwise, your program will have memory leaks and eventually crash!

## Example of memory leaks

```
void g(int x) {
	int* p = new int(x);	// memory leak!
	delete p;		// remove this and see application size grow!
	return;
}

int main() {
for (int i = 0; i < 100000000; i++)
		g(i);
}
```

* since int* p in g() is a local variable, this gets removed from the stack, BUT THE VALUE ON THE HEAP REMAINS.
	* Once the variable is removed when the function exits, there is no way to remove this from the heap.
		* This is a memory leak!
* "delete" is the opposite of new
	* "new" creates an object on the heap and returns a pointer to it.
	* "delete" takes a pointer and removes the data from the heap.
		* "delete p;" doesn’t delete the variable p, it deletes what p points to on the heap!
		* "delete" only works for values that exist on the heap.

# Dangling Pointers
* After a pointer’s memory is deleted, the pointer itself is still available to use.
* BUT, you should never use a dangling pointer (the behavior of it is undefined).
	* And why would you want to use a pointer to something that shouldn’t be there?

## Dangling Pointers Example

```
int g(int x) {
	double* p = new double(x);
	delete p;	// delete value from the heap
	return *p; 	// p is a dangling pointer since heap contents were removed!
			// Results in undefined behavior. Shouldn’t do this!
}
```

# Dynamically allocating arrays
* We have been allocating arrays on the stack, but we can also do this on the heap!
	* Actually, we SHOULD do this on the heap if our array size is not known during compile time.
	* Example of declaring and deleting an array on the heap. 

```
int* arr = new int[10];	// create an array of 10 integers on the heap
delete [] arr;		// removes the array from the heap. Note the [] syntax for deleting arrays from the heap.
```

* Some compilers may have extended functionality to support dynamically allocating arrays using the syntax for statically allocating arrays.
	* For example, g++/clang++ allows this, but VisualStudio currently does not:

```
int x;
cout << "Enter a positive number: ";
cin >> x;
// int intArray[x]; // ERROR IN VisualStudio, NOT g++ / clang++
int* intArray = new int[x]; // LEGAL IN BOTH
for (int i = 0; i < x; i++) {
	intArray[i] = i;
	cout << intArray[i] << endl;
}

// Note: to delete an array on the heap, use delete [] intArray;
delete [] intArray;
```

