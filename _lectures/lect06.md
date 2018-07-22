---
num: "Lecture 6"
desc: "C++ Build Process, Makefiles, Test-Driven Development"
ready: true
date: 2018-07-19 11:00:00.00-7:00
---

# C++ Build Process

* So far we’ve been writing and compiling small programs in a single file.
* Though typical C++ programs may be organized into small pieces where functionality is defined in separate files.

## Header Files
* A header file is a file that typically contains only declarations.
* .cpp files contains “source code" for that functionality
* Typically, each source file contains a corresponding header file with definitions you want to have accessible to other source files.
* Source files that need to use any of the functions from other source files will need to include the header file.
	* By doing this, we are declaring functions in the file (remember we must declare or define functions before using them in our code).

## Example

```
------------------------------------
// drawShapes.h
#include <string>
using namespace std;

string drawRightTriangle(int height);
string drawSquare(int length);
------------------------------------
// drawShapes.cpp
#include <string>
using namespace std;

string drawRightTriangle(int height) {
	string result = "";
	int rowLength = 1;

	for (int i = 0; i < height; i++) {
		for (int j = 0; j < rowLength; j++) {
			result += "*";
		}
		result += "\n";
		rowLength++;
	}
	return result;
}

string drawSquare(int length) {
	string result = "";

	for (int i = 0; i < length; i++) {
		for (int j = 0; j < length; j++) {
			result += "*";
		}
		result += "\n";
	}
	return result;
}
------------------------------------
//program1.cpp
#include <iostream>
#include "drawShapes.h"

int main() {
	cout << drawRightTriangle(5) << endl;
	cout << drawSquare(5) << endl;	
return 0;
}
------------------------------------
```

## What’s with the different type of #include<> or #include ""?

* Having "'#include<>'" includes libraries from the C++ Standard Library
* For our own header files, we use `#include ""`
	* For example, when we use `#include<iostream>`, all the declarations in the I/O stream library including cout, cin, endl, etc. are available for use in our file.
	* When we use `#include "drawShapes.h"`, all of the declarations in the drawShapes.h file is included in the file.	* This allows us to call these functions in our file.

Similar to how we compile C++ programs with a single file, we can compile all source (.cpp) files using:

`g++ -o program1 program1.cpp drawShapes.cpp`

* This approach works, but can be inefficient when compiling MANY files.
	* Imagine making a small change in one file, then ALL files using this command will be recompiled.

* A more efficient way would be to compile each piece separately and link all pieces together at the end.
	* This way, if only one file changed, then only that one file needs to be re-compiled.
	* Compiling a file produces a lower-level form of the file (called an object file (.o)).
	* The Linker then takes these .o files and puts them together to form the actual executable.
	* We can accomplish this as follows:

```
g++ -c -o drawShapes.o drawShapes.cpp
g++ -c -o program1.o program1.cpp
g++ -o program1 program1.o drawShapes.o
```

* If we only make a change to program1.cpp, all we need to do is recompile the program1.o file.

## C++ Build Process

1.	Preprocessing: Text-based program that runs before the compilation step. Looks for statements such as `#include` and modifies the source which is the input for compilation.
	* Think of the compiler "copying / pasting" the contents of the included file everytime `#include` is used.

2.	Compilation: Translates source code into “object code,” which is a lower-level representation optimized for executing instructions on the specific platform. Lower level representations are usually stored in a .o (object) file.

3.	Linking: Resolves dependencies and maps appropriate functions located in various object files. The output of the linker is an executable file for the specific platform.

## But what happens if we have hundreds of source files to compile?
* Manually compiling everything can be really cumbersome and error-prone.
* Makefiles are a way to automate this process by defining compilation rules.

# Makefiles

## General Format of a Makefile

```
[target]: [dependencies]
	[commands]
```

## Example

```
------
# Makefile

# Single line comments in Makefiles use '#'

program1: program1.o drawShapes.o
	g++ -o program1 program1.o drawShapes.o

clean:
	/bin/rm -f *.o program1
------
```

* If a change to a .cpp file is made, then only that .cpp file gets recompiled.
* If no changes were made, make knows not to do anything.
	* Uses timestamps to determine if a .o file needs to be recompiled.

* `make program1` will check if program1.o and drawShapes.o is present.
	* `make` will try to generate the .o files if they aren't available.
	* Once .o files are generated, the command is executed, which generates the executable by linking the .o files together.
* `make clean` will remove all .o files and the executable `program1`

## Example

```
$ make program1
c++    -c -o program1.o program1.cpp
c++    -c -o drawShapes.o drawShapes.cpp
g++ -o program1 program1.o drawShapes.o
```

* If we make a small change to program1.cpp, save the file, and run the make command again:

```
$ make program1
c++    -c -o program1.o program1.cpp
g++ -o program1 program1.o drawShapes.o
```

* Only the program1.o file is recompiled.
* `make` knows the other .cpp files haven't been updated (using timestamps) so it doesn't need to recompile these .o files.
* If we try executing `make program1` again without any changes, then nothing happens since no updates to any .o files are needed.

```
$ make program1
make: `program1' is up to date.
```

# Another Example of a Test Program

## Test-Driven Development
* Write test cases that describe what the intended behavior of a unit of software should BEFORE implementing the functionality.
	* Defines the requirements of your piece of software.
* Implement the details of the functionality with the intention of passing the tests.
	* Repeat until the tests pass.
* Imagine large software products where dozens of engineers are trying to add new features / implement optimizations all at the same time.
	* Having a “suite” of tests before deploying software to the public is essential.
	* Someone may modify changes that work for a current version, but breaks functionality in another version
	* Rigorous tests enable confidence in the stability in software.
* Gradescope system does something similar
	* It tests your submitted code and ensures functionality is correct by passing tests.

* We can define our testing functionality into `tdd.h` and `tdd.cpp`

```
------------------------------------
// tdd.h
#include <string>
using namespace std;

void assertEqual(string expected, string actual, string message="");
------------------------------------
// tdd.cpp
#include <iostream>
#include <string>
using namespace std;

void assertEqual(string expected, string actual, string message = "") {
	if (expected == actual) {
		cout << "PASSED: " << message << endl;
	} else {
		cout << "\tFAILED: " << message << endl;
		cout << "Expected: " << "[\n" << expected <<
		"\n]" << "Actual: [\n" << actual << "\n]" << endl;
	}
}
------------------------------------
//testDrawShapes.cpp
#include <iostream>
#include <string>
#include "drawShapes.h"
#include "tdd.h"
using namespace std;

void testDrawRightTriangle() {
	string expected1 =
	"*\n"
	"**\n";

	string actual1 = drawRightTriangle(2);
	assertEqual(expected1, actual1, " testHeight:2");

	string expected2 =
	"*\n"
	"**\n"
	"***\n";

	string actual2 = drawRightTriangle(3);
	assertEqual(expected2, actual2, " testHeight:3");
}

void testDrawSquare() {
	string expected1 =
	"**\n"
	"**\n";

	string actual1 = drawSquare(2);
	assertEqual(expected1, actual1, " testLength: 2");

	string expected2 =
	"***\n"
	"***\n"
	"***\n";

	string actual2 = drawSquare(3);
	assertEqual(expected2, actual2, " testLength: 3");
}

int main() {
	testDrawRightTriangle();
	testDrawSquare();
}
------------------------------------
# Makefile

testDrawShapes: testDrawShapes.o drawShapes.o tdd.o
	g++ testDrawShapes.o drawShapes.o tdd.o -o testDrawShapes

clean:
	/bin/rm -f *.o testDrawShapes
------------------------------------
```

* To use make to compile your code into an executable called testDrawShapes:

```
make testDrawShapes
```

More information on compilation / makefiles:

* <https://foo.cs.ucsb.edu/16wiki/index.php/C%2B%2B:_Separate_Compilation_and_Makefiles>












