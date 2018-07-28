---
num: "Lecture 7"
desc: "Arrays and Number Representations"
ready: true
date: 2018-07-24 11:00:00.00-7:00
---

# Arrays

* An array is used to organize a collection of values of the same type.
* So far, we have been writing programs where values aren’t stored in a collection, but single variables.
* Another way to think of arrays under-the-hood is a sequence of cells that are stored <i>contiguously</i> in memory.

## Computer Memory Illustration

![Computer Memory](memory.png)

* Memory addresses are usually byte-addressable (i.e. a distinct memory location refers to eight bits of information).
* During compilation, the compiler knows how much memory to reserve for variables (including arrays) that are declared.
	* This is why we must declare all variables with a type.

## Declaring Arrays

```
int a[10];
```

* Arrays need a type defined (int), a variable name (a) and a size (10).
* We can check the size of a type using the `sizeof` function, which returns the size of a value in bytes.

```
cout << sizeof(5) << endl; // 4 (int)
cout << sizeof(11.1) << endl; // 8 (double)

char b = 'b';
cout << sizeof(b) << endl; // 1 (char)
```

* The array `a` will have a size of 10 * sizeof(int) in this case.

```
int a[10];
cout << sizeof(a) << endl; // 40
```

## Bracket Syntax
* Accessing an individual cell of an array uses a traditional `[ ]` syntax, which is indexed starting at 0.
	* The first element is a[0]. The last element is a[9].
	* Initially, each cell is undefined (may contain junk data).
		* Remember, it's important to explicitly initialize values in C++.

```
int a[100];
for (int i = 0; i < 100; i++) {
	cout << a[i] << endl;
}
```

* Notice how some elements in the array may contain random values since we didn't initialize values in the array.

## Example of reading / writing values from / to the array

```
a[0] = 1;
a[1] = -5;
a[1] = a[0]; // fetching and storing array values
```

* For all practical purposes, an element in an array can be treated as a value whose type is what the array was defined as.
* An example using `cin`:

```
int a[10];
cout << "Enter a number: ";
cin >> a[0];
cout << "a[0] = " << a[0] << endl;
```

* An example using functions

```
void passArrayValueExample(int x) {
	cout << “Parameter value: “ << x << endl;
}

int main() {
	int x[1];
	x[0] = 3;
	passArrayValueExample(a[0]); // prints 3
}
```

## Example of iterating through the entire array

```
int a[10];
for (int i = 0; i < 10; i++) {
	a[i] = i; // initializes elements using i
}
int x = a[5] + 2;
cout << x << endl; // 7
```

* Unlike some languages, C++ arrays cannot be indexed with negative numbers.
* Arrays do not know what their size is, so programmers will need to keep track of that.

## Shorthanded way to declare and initialize arrays

```
char grades[] = {‘A’, ‘B’, ‘C’, 'D', 'F'};
```

* This declares a char array named grades and initializes 5 elements with the values in between the `{ }`.

## Memory addresses of array elements

* Assuming the array `int values[] = {2,4,6,8};` is located at the memory address 100, what memory address would `values[3]` be located?

![Array address](arrayAddress.png)

# Number Representation

* Humans are used to dealing with numbers in Decimal (base 10) notation.
* Computers MUST deal with numbers in Binary (base 2) notation (0’s and 1’s)
	* Physical property of hardware stores state in positive / neutral charges.
	* Each binary value is called a bit.
	* Eight bits make up a byte.

## Converting values in different bases to base 10

* We can take the digits from the source base, and sum up the digit times the base's power (starting from 0) in ascending order from right-to-left.
* Example converting 110<sub>5</sub> = __________<sub>10</sub>

1 * 5<sup>2</sup> + 1 * 5<sup>1</sup> + 0 * 5<sup>0</sup>

= 25 + 5 + 0

= 30

* Example converting 1101<sub>2</sub> = __________<sub>10</sub>

1 * 2<sup>3</sup> + 1 * 2<sup>2</sup> + 0 * 2<sup>1</sup> + 1 * 2<sup>0</sup>

= 1 * 8 + 1 * 4 + 0 * 2 + 1 * 1

= 13

* We can compute the number of unique values n binary bits have with 2<sup>n</sup>.

* The number of unique values 4 bits can represent is:

2<sup>4</sup> = 16

* Computer applications can use binary combinations to represent values other than numbers.
	* American Standard Code for Information Interchange (ASCII) uses 1 byte to represent characters.
	* UTF-8 uses 1 - 4 bytes to contain characters for many languages.

## Converting base 10 to binary (base 2)

* We can use the "best-fit" approach using powers of 2.
	* See which largest power of two is less than that number.
	* Write a '1' in the appropriate place, and a '0' for any values that are larger.
	* Replace the value by subtracting it by the largest power of two less than the current value.
	* Repeat until the value is 0.

![Decimal to Binary](decimalToBinary.png)

## Hexadecimal Numbers

* Hexadecimal values are represented with a base 16, where each digit is represented with either [0-9] or [A-F].
* Memory addresses are usually represented in hexadecimal notation.
* A common hexadecimal notation has `0x` preceeded by the hexadecimal value.
	* We'll see this notation when printing memory addresses in our C++ programs.

```
Hex Value 	Binary Value
0 		0000
1 		0001
2 		0010
3 		0011
4 		0100
5 		0101
6 		0110
7 		0111
8 		1000
9 		1001
A 		1010
B 		1011
C 		1100
D 		1101
E 		1110
F 		1111
```

* Conversion from hexadecimal to binary simply takes the hexadecimal digit and substitutes the binary representation.
* Example: Convert 0x13C to binary.


1<sub>16</sub> = 0001

3<sub>16</sub> = 0011

C<sub>16</sub> = 1100

0x13C = 000100111100<sub>2</sub>


* Converting from binary to hexadecimal substitutes every 4 binary bits with the hexadecimal value.


0001,0011,1100

= 13C<sub>16</sub>













