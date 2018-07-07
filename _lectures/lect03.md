---
num: "Lecture 3"
desc: "User Input, Loops"
ready: true
date: 2018-07-03 11:00:00.00-7:00
---

# User Input

## Example of interacting with the console using the cin function

```
#include <iostream>
#include <string>

using namespace std;

int main() {	
// Example receiving a string from the user
	string name;
	cout << "What is your name? ";
	cin >> name;
	cout << "Hello " << name << endl;

	// Example receiving a number from the user
	int i;
	cout << "Enter a number: ";
	cin >> i;
	cout << "The number entered is " << i << endl;

	cout << i / 2 << endl; // what value / type is this if i == 11? 
}
```

## Example of using command line arguments

* We can pass information into a C++ program through the command line when executing the program.
* Note: You may have to convert command line argument information into the proper type (i.e. convert it to an integer type) if necessary.
* The main function will need to have the following:

```
int main(int argc, char *argv[]) {
```

* `int argc` is the number of "arguments" the program has, including the executable name.
* `char* argv[]` is the "list" of arguments passed into the program.
	* Don't worry if the syntax doesn't make too much sense for now, we'll cover this later in the quarter.

```
#include <iostream>
#include <cstdlib>

using namespace std;

int main(int argc, char *argv[]) {

	cout << "Number of arguments: " << argc << endl;

	cout << argv[0] << endl;
	cout << argv[1] << endl;
	cout << argv[2] << endl;

	// how to use these arguments as numbers?
	// We can convert them using the atoi function
	// in the cstdlib standard library

	int x = atoi(argv[1]) + atoi(argv[2]);
	cout << x << endl;
	return 0;
}
```

# Control Structures: Loops

## While Loops

General syntax of a while loop:

```
while (BOOLEAN_EXPRESSION) {
	// code
	// ...
}
```

1. Check if the BOOLEAN_EXPRESSION is true.
	* If true, the statements in loop will execute.
		* at the end of the loop, go back to 1.
	* If false, the statements in the loop will not execute.
		* the program execution after the loop continues.

## Example

```
int i = 0;
while (i < 10)
	cout << "i = " << i << endl;
	// add i++ afterwards to eliminate an infinite loop.
	// i++ → i = i + 1;
	// Remember to enclose this statement with { }
```

* Note that a single statement after a while loop (similar to an if statement) is considered part of the loop without the { }.
	* If more than one statement is part of the loop, this must be contained within the { }

## Do-while Loops

* Useful if you want to execute a block of code at least once.
* General syntax of a do-while loop:

```
do {
	// code
	// ...
} while (BOOLEAN_EXPRESSION);
```

* Note the ';' at the end of the loop. This syntax is required.

1. Execute the code in the loop
2. Check if BOOLEAN_EXPRESSION is true.
	* If true, then go back to 1.
	* If false, then exit the loop and resume program execution.

## Example

```
int i = 0;
do {
	cout << "i = " << i << endl;
	i++;
} while (i < 0);
```

* Outputs "i = 0" once regardless of what the BOOLEAN_EXPRESSION evaluates to.
* Change to `while (i < 10)` to print "i = [0 - 9]".

## For Loop

General syntax of a for loop:

```
for (INITIALIZATION; BOOLEAN_EXPRESSION; UPDATE) {
	// code
	// ...
}
```

1. Execute the INITIALIZATION statement.
2. Check if BOOLEAN_EXPRESSION is true.
	* if true, execute code in the loop.
		* execute UPDATE statement.
		* Go back to 2.
	* if false, do not execute code in the loop.
		* exit the loop and resume program execution.

## Example

```
for (int i = 0; i < 10; i++) {
	cout << “i = “ << i << endl;
}
```

## Nested Loops

Other loops within a loop can be defined.

## Example

```
for (int i = 0; i < 5; i++) {
	cout << “—“ << endl;
	cout << “i = “ << i << endl;
	for (int j = 0; j < 5; j++) {
		cout << “j = “ << j << endl;
	}
}
```

## Continue and break statements

* `continue;` can be used to stop the current iteration of a loop, perform the UPDATE statement if necessary, re-check the BOOLEAN_EXPRESSION, and continue with the next iteration of the loop.
* `break;` can be used to break out of the <i>current</i> loop and continue execution after the end of the loop.

## Example

```
for (int i = 0; i < 10; i++) {
	if (i == 4)
		continue;
	if (i == 7)
		break;
	cout << “i = “ << i << endl;
}
```

# Formatting output to the terminal

* Several ways to do this.
* We can customize the `cout` function to display floating point numbers as follows:

```
cout.setf(ios::fixed);
cout.setf(ios::showpoint);
cout.precision(2); // prints two decimal spaces for floating point values.
```	

# Example: A number guessing game

```
#include <iostream>

using namespace std;

const int ANSWER = 42; // const values cannot be modified

int main(int argc, char *argv[]) {

	int input = 0;

	do {
		cout << "Guess a number between [0 - 100]: ";
		cin >> input;
		if (input == -1)
			break;
		if (input < ANSWER) {
			cout << "Too small" << endl;
			continue;
		}
		if (input > ANSWER) {
			cout << "Too big" << endl;
			continue;
		}
		if (input == ANSWER) {
			cout << "WINNER! ANSWER = " << ANSWER << endl;
			break;
		}
	} while (true);

	cout << "Thanks for playing!" << endl;
}
```
