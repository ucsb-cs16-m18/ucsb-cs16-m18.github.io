---
num: "Lecture 2"
desc: "Basic I/O, Variable Types, Boolean Expressions, Control Flow"
ready: true
date: 2018-06-28 11:00:00.00-7:00
---

# Breaking down the Hello World Program

```
// hello.cpp
#include <iostream>

using namespace std;

int main() {
	cout << "Hello CS 16!" << endl;
	return 0;
}
```

```
#include <iostream>
```

* This line (also known as an include directive) tells our C++ program to include a library dealing with Input/Output (I/O) functionality.
	* We need the library `<iostream>` to print stuff to our terminal.

```
using namespace std;
```

* This line allows us to use parts of the iostream library without having to prepend `std::`.
	* For more context, `std` is short for "standard".
	* including libraries between angle brackets (< >) imply that this is part of the C++ Standard Library, which is part of the C++ language specification.

```
int main() { ... }
```

* The main function. Every C++ program needs to have one main function as its "starting point".

```
cout << "Hello CS 16!" << endl;
```

* `cout << [some_value]` tells the program to display some_value to the terminal.
* `<< endl;` tells the program to insert a <i>newline</i> at the end.
	* This places the next values to be written on the next line in the terminal.

```
return 0;
```

* Since main must be declared to return a value of "int" type, we are simply returning 0.
	* May get more into the relevance of this later.

# Comments

* Any commented text will be ignored by the compiler.
* Important to comment code for communication with others working with your code!
* `//` denotes a single-line comment.
* `/* */` denotes a multi-line comment.

## Example

```
// single line comment

/* multi
line
comment
*/
```

# C++ Variables and Types

* Variables are used to store data.
	* Each variable must have a type associated with it.
		* Not the case in Python where a variable can be anything
	* Variable names must
		* Start with an alpha character or underscore
		* Other characters can be alphanumeric and underscore characters, but no spaces or other special characters.
	* C++ is case-sensitive. ‘x’ and ‘X’ are considered different variables.

* Some common types:
	* int: Integers
	* double: Floating point
	* char: characters
	* string: sequence (array) of characters
	* bool: boolean

* Good practice to initialize your variables
	* Uninitialized variables may have strange side-effects.

# Initializing, Assigning, and Modifying Variables

* Example

```
int x; 			// initialize variable x of type int
int y, z;		// initialize variables x and y in one statement
x = 10; 		// assign x to an integer value 10.

int a = 10;		// initialize and assign in one statement
int b = 20, c = 30;

b = 6 + 4;

cout << a << "," << b << "," << c << "," <<
x << "," << y << "," << z << endl;
```

# Boolean Expressions
* An expression that evaluates to either true or false.
* You can build boolean expressions with relational operators comparing values:

```
==	// true if two values are equivalent
!=	// true if two values are not equivalent
<	// true if left value is less than the right value
<=	// true if left value is less than OR EQUAL to the right value
>	// true if left value is greater than the right value
>=	// true if left value is greater than OR EQUAL to the right value
```

* Integer values can be used as boolean values
	* C++ will treat the number 0 as false and any non-zero number as true.

```
bool x = 5 == 1;	// x = 0
bool x = 3 != 2;	// x = 1
```

	* Combine boolean expressions using Logical Operators

```
!	// inverts true to false or false to true
&&	// boolean AND
|| 	// boolean OR
```
	
	* Example

```
bool x = true;
bool y = true;
x = !x;			// x = false
x = x && y		// x = false
x = x || y		// x = true
```

# Control Structures

* Boolean expressions are fundamental pieces that provide control flow within your program.

## If-else statements

* Ability to execute two alternative blocks of C++ statements based on the value of a boolean expression.

```
if (BOOLEAN_EXPRESSION) {
	// code1
} else {
	// code2
}
```

* If the BOOLEAN_EXPRESSION evaluates to true, then code1 is executed. Otherwise code2 is executed.
* Example

```
int x = 4;
if ((x > 3) && (x < 6)) {
	cout << “x is either 4 or 5” << endl;
} else {
	cout << “x is not 4 or 5” << endl;
}
```

* Notice the “{ … }” . Also known as block statements. 
	* This allows many statements to be executed.
	* Without “{ … }”, only the following statement will be executed, and other statements are considered outside the block statement.
	* Example

```
int x = 4;
if ((x > 3) && (x < 6))
	cout << “x is either 4 or 5” << endl;
else
	cout << “x is not 4 or 5” << endl;
// Will have the same output as the last statement.

int x = 6;
if ((x > 3) && (x < 6))
	cout << “1” << endl;
	cout << “2” << endl; // outside if block
	cout << “3” << endl; // outside if block
```
	
	* The last two statements will always execute because it’s considered outside of the code block.
	* A syntax error will appear if you try to insert an “else” after the statements since “else” can only be used after an if code block.

# Multi-way If-else Statements

* Programs may require more than simply two paths of code execution.
* Multiple if-else statements can allow the program to execute many branches.
* Example

```
int x = 3;
if (x == 1)
	cout << “x equals 1” << endl;
else if (x == 2)
	cout << “x equals 2” << endl;
else if (x == 3)
	cout << “x equals 3” << endl;
else
	cout << “x does not equal 1, 2, or 3” << endl;
```

# Switch Statements

* Another way to write multi-way if-else statements are switch statements.
* A switch statement can use either an integer type, bool, char, or enum (more on this type later).
* Example

```
int a = 3;
switch (a) {
	case 1:
		cout << “a == 1” << endl;
		break;
	case 2:
		cout << “a == 2” << endl;
		break;
	case 3:
		cout << “a == 3” << endl;
		break; // remove this and notice code continues without break statement
	default:
		cout << “a != [1, 2, 3]” << endl;
}
```

* Notice the “case 1” keyword. This is equivalent as saying if (a == 1).
* Notice that each case does not have a { … }.
* All code between different cases will be considered as a single block.
* `default` block will execute if none of the cases match or until the end of the switch statement closed with "}".
* Notice the "break" statement. This tells the compiler that it’s the end of a case.
	* Without the "break" statement, the compiler will execute all statements until a break statement is reached.
	* It is possible to have many cases refer to the same statements.
	* Example

```
int a = 3;
switch (a) {
	case 1:
	case 2:
		cout << “x == [1,2]” << endl;
		break;
	case 3:
		cout << “x == 3” << endl;
		break;
	default:
		cout << “x != [1,2,3]” << endl;
}
// Change to a = 1, remove 1st break statement, and see "x == 3" printed in this scenario.
```

# Embedded if-else statements
* Within a block statement, other if structures can be written.
* Provides finer control of what code to execute in certain conditions.
* Example

```
int x = 7;
if (x >= 5) {
	cout << “x >= 5” << endl;
	if (x == 5) {
		cout << “x == 5” << endl;
	} else {
		cout << “x > 5” << end;
	}
}
```

