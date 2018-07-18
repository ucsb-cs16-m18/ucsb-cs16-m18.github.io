---
num: "Lecture 5"
desc: "File I/O, Midterm 1 Review"
ready: true
date: 2018-07-12 11:00:00.00-7:00
---

# File I/O

* The standard library contains functionality that help us deal with file I/O.
* The <fstream> library includes:
	* ifstream (input file stream)
	* ofstream (output file stream)
* In order to either read or write to a file, you must open it first. Note that
	* opening a file with ifstream on an invalid file does not crash your program.
		* you will have to check if opening the file was successful.
	* opening a file with ofstream will overwrite an existing file by default.
		* If the file does not exist, then it creates one.

## Working Directory

* The directory where you executed your program.
* <b>Absolute Path</b>: The entire path to a specific location.
* <b>Relative Path</b>: Path that starts at the current directly to a specific location.

## Example

```
// Writing to a file
#include<fstream>

using namespace std;

int main() {
	ofstream out;
	out.open(“outputExample.txt”);
	out << “Writing to file is like writing to the console”) << endl;
	out.close(); // important to close your files.
	return 0;
}
```

* Note the `close()` function. Without it, our program still works.
	* However, closing file streams is important in order to free up resources.

## Appending to a File

* When we write to a file, it overwrites it.
* We can add a parameter to the `open` method to simply append data to the file.

```
out.open("outputExample.txt", ios::app);
```

## Example of reading data from a file into the program

input.txt
```
Line 1
Line 2
Line 3
```
----
```
#include <iostream>
#include <fstream>

using namespace std;

int main() {
	// Reading from a file one line at a time.
	ifstream in;
	in.open("input.txt");
	string line = "";

	if (in.fail()) { // checks if reading the file failed…
		
		// Note: cerr is like cout, but used to display error messages.
		cerr << "Opening file failed" << endl;

		return 0;
	}


	while (!in.eof()) { // checks if we reached the end of file or not
		getline(in, line); // returns the entire line
		cout << line << endl;
	}
	in.close();
	return 0;
}

```

# Midterm 1 Review

```
Logistics

- Bring studentID and a writing utensil
	- Preferably ink or dark led
	- PLEASE WRITE LEGIBLY!
- No electronic devices
- No book
- No notes

Format
- Will be a mix of questions which may include …
	- short answers
		- Explain, describe, define, …
	- Write some code
	- Fill in the blank
	- True / False, if False explain why
	- Given some code, write the output (basically, be the computer)
- Should take ~ one hour to complete.
	- Will cover a broad range of topics, but probably not everything.

Topics
	- Will cover everything up to Tuesday’s lecture (7/10)
		- File IO will be covered on midterm 2
	- H01 - H03 and all the assigned readings, lecture notes, labs.
	- Knowing simple g++ compilation, vim commands can be on it.

<iostream>
	- cin, cout

C++ Variables and Types
	- int, double, char, string, bool
	- Initializing, assigning, and modifying variables

Boolean and Logical Expressions
	- Boolean and relational operators
	
Control Structures
	- if-else statements
	- multi-way if statements
	- switch statements
	- embedded if statements
	- Loops
		- do-while, while, for
		- continue and break statements
		- Embedded Loops

Functions
	- Declaration, definition, calling
	- Basic memory stack structure
```
