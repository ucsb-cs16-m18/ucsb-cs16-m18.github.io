---
num: "Lecture 4"
desc: "Functions, print vs. return, Memory Stack"
ready: true
date: 2018-07-10 11:00:00.00-7:00
---

# Functions

* A function is a block of code that takes parameters, executes some statements, and sometimes returns a value.

* When developing software, defining functions is a way to “modularize” your code into maintainable parts.
	* Supports the DRY (Don’t Repeat Yourself) principle.
	* Better maintenance
		* If a bug exists in a function, change it once and it should fix it for everything that uses it.
	* General rule of thumb: if you find yourself writing the same code in different parts of the program, see if you can refactor that code into a function.

## Function Signatures

* Multiple functions may have the same name ONLY IF the parameter types differ.
	* Known as <b>overloading</b> a function.
	* Note that you cannot overload a function just with different return types.
* Combination of the function return type, name, and parameter types are known as the <b>function signature</b>.

# Example of Overloading Functions

```
void printAreaOfSquare(int area); // OK, first declaration of this function
double printAreaOfSquare(int area); // ERROR, only return type differs
void printAreaOfSquare(double area); // OK, parameters are different
void printAreaOfSquare(int length, double width); // OK
void printAreaOfSquare(int width, double length); // ERROR, same parameter types
```

## Function Declarations

In C++, a function declaration must occur BEFORE they are used.
	* We can write the method after it is used, we just need to declare it.

## Example: Simple Function Definition

```
#include <iostream>

using namespace std;

int areaOfSquare(int length); // declaration

int main() {
	int result = areaOfSquare(20); // call
	cout << result << endl;
	return 0;
}

int areaOfSquare(int length) { // definition
	return length * length;
}
// OK. Function declaration happens before it was used

-----------
#include <iostream>

using namespace std;

int main() {
	int result = areaOfSquare(20); // call
	cout << result << endl;
	return 0;
}

int areaOfSquare(int length) { // definition
	return length * length;
}
// ERROR! use of undeclared identifier 'areaOfSquare'

```

## Return vs. Print

* Not all functions need to return a value. Some cases may be
	* Printing something to a console
	* Simply changing a state of a variable or data structure.

## Example of printing, but not returning

```
void printAreaOfSquare(int area) {
	cout << “Area of Square: “ << area << endl;
	return; // return not necessary, will exit function when reached.
}
```

## Example: Matching function calls to overloaded functions

```
void f(int x) { cout << "f(int x)" << endl; }
void f(double x) { cout << "f(double x)" << endl; }

void g(int x) { cout << "g(int x)" << endl; }

void h(double x) { cout << "h(double x)" << endl; }

int main() {
	f(5); 		// f(int x) 
 	f(5.0);		// f(double x)
 	g(10.1);	// g(int x)
 	h(10);		// h(double x)
}
```

# Memory Stack

* Types are important in compiled languages like C++
	* Knowing exactly the amount of memory a function will occupy is essential for memory organization during execution.
	* Function calls are laid out in memory as a data structure called a <b>stack</b>.
		* Think of a stack like a canister of tennis balls.
		* You can only add to the top of the stack.
		* You can only remove an item at the top of the stack.
	* Every time a function is called, memory footprint is created and added to the top of the memory stack.
	* When the function returns a value, the memory reserved for the function is removed from the stack.
	* `int main()` is the bottom most function on the stack throughout execution.

## Example

```
#include <iostream>

using namespace std;

int doubleValue(int x) {
	return 2 * x;
}

int quadrupleValue(int x) {
	return double(x) + double(x); 
}

int main() {
	int result = quadrupleValue(4);
	cout << result << endl;
	return 0;
}
```

* Start Execution

```
|                       |
|-----------------------|
| int main()            |
|_______________________|
```

* `quadrupleValue(4)` is called

```
|                       |
|-----------------------|
| int quadrupleValue(4) |
|-----------------------|
| int main()            |
|_______________________|
```

* `double(x)` is called

```
|                       |
|-----------------------|
| int double(4)         |
|-----------------------|
| int quadrupleValue(4) |
|-----------------------|
| int main()            |
|_______________________|
```

* `double(4)` finishes executing and returns a value

```
|                       |
|-----------------------|
| int quadrupleValue(4) |
|-----------------------|
| int main()            |
|_______________________|
```

* `double(4)` is called again

```
|                       |
|-----------------------|
| int double(4)         |
|-----------------------|
| int quadrupleValue(4) |
|-----------------------|
| int main()            |
|_______________________|
```

* `double(4)` finishes executing and returns a value

```
|                       |
|-----------------------|
| int quadrupleValue(4) |
|-----------------------|
| int main()            |
|_______________________|
```

* `quadrupleValue` returns the sum of the two `double(4)` function calls

```
|                       |
|-----------------------|
| int main()            |
|_______________________|
```

* `main` prints the result of `quadrupleValue` return value. Program exits.





