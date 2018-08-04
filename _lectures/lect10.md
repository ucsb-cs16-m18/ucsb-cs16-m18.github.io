---
num: "Lecture 10"
desc: "Pointer Arithmetic"
ready: true
date: 2018-08-02 11:00:00.00-7:00
---

# Pointer Arithmetic

* We’ve talked about array variables referring to the memory address of the first element in the array.
	* We can think of an array variable as a pointer!
	* We’ve seen an example where we can either pass in an array variable OR pass in a pointer when using arrays.
	* We also know that arrays must be declared with a size
		* And the size must be kept track of in order to stay within the memory bounds of the memory (avoid seg faults!).

```
// Recall
// void printArray(int* values, int size) { // can use a pointer
void printArray(int values[], int size) {
	// Note: size is passed in since we won’t know how to get the size with
	// just the array variable.

	cout << values << endl; // prints memory location of start of values[]

	for (int i = 0; i < size; i++) {
		cout << "values[" << i << "] = " << values[i] << endl;
		cout << "&values[" << i << "] = " << &values[i] << endl;
		// Note: The address values are 4 bytes away since int is 4 bytes
	}
}

int main() {
	int values[3] = { 5, 10, 15 };
	printArray(values, 3);
	return 0;
}
```

* We also know that we index arrays from [0, size – 1].
	* There is reason behind this!
	* Under-the-hood, C++ is using the index to perform pointer arithmetic!
	* When performing arithmetic to a pointer, it modifies the address by incrementing the number of bytes of the pointer’s type size.

## Example

```
int main() {
	int arr[5] = {0,1,2,3,4};
	int* x = arr;

	cout << arr << endl;
	cout << x << endl;

	cout << x + 1 << endl; // address is incremented by 1*sizeof(int)
	cout << x + 2 << endl; // address is incremented by 2*sizeof(int)
	cout << x + 3 << endl; // address is incremented by 3*sizeof(int)

	cout << *(x + 2) << endl;	// equivalent to x[2] or arr[2]
	cout << &(*(x + 2)) << endl;  // equivalent to x + 2
	return 0;
}
```

## Illustration

* The array index is the "offset" from the start of the array
* To access specific elements in the array using pointer arithmetic, the address is calculated as:

```
elementAddress = startOfArrayAddress + (i * (size of type pointer is pointing to))
```

![Array Elements](elementAddress.png)

## Example - trace the code

```
int arr[] = {10,15,20};
int* x;
x = arr;
cout << x + 1 << endl; // Address of arr[1]
cout << *x + 1 << endl; // 11
```

* x + 1 uses pointer arithmetic to calculate a memory address
* *x + 1 defeferences the array pointer and adds 1 to the first element

## Example - using [ ] and pointer arithmetic

* Assume we have a function that initializes an array:

```
void initializeArray(int* values, int size, int initialValue) {
	for (int i = 0; i < size; i++) {
		values[i] = initialValue;
		cout << values[i] << “ “;
	}
}
```

* We can also write this same algorithm using pointer arithmetic:

```
	for (int i = 0; i < size; i++) {
		*(values + i) = initialValue;
		cout << *(values + i) << " ";
	}
```

## Segmentation Faults

* If you're trying to access memory outside the range of an array, you may be accessing junk data or your program may crash with a <b>segmentation fault</b>

```
for (int i = 0; i < 1000000; i++) {
	*(values + i) = initialValue;
}
```

## Another Example - passing pointers by value / reference

```
void incrementPointer(int* p) {
	p++;
}

int main() {
	int arr[] = {10,20,30};
	int* x = arr;

	incrementPointer(x);

	cout << *x << endl; // 10
	return 0;
}
```

* Remember that even though pointers contain memory addresses, the pointer variable is a variable with its own address.
* The scenario above passes the pointer by value.
	* Any modification we make to the pointer’s address in incrementPointer is local to the incrementPointer function.

![Pointer Pass By Value](pointerValue.png)

* What can we do to actually increment the array using the incrementPointer function?

	* We can pass the pointer by reference.

```
void incrementPointer(int*& p) {
	p++;
}
```

![Pointer Pass By Reference](pointerReference.png)

	* We can pass a pointer to a pointer.

```
void incrementPointer(int** p) {
	//p++;		
	*p = *p + 1;	// need to modify the original pointer’s address
}

int main() {
	int arr[] = {1,2,3};
	int* x = arr;

	incrementPointer(&x); 	// since a pointer to a pointer expects the address of
				// a pointer to an int. 
	cout << *x << endl;
	return 0;
}
```

![Pointer to Pointer](pointerToPointer.png)

