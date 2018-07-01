---
num: "Lecture 1"
desc: "Introduction, CSIL Policies, Course Structure"
ready: true
date: 2018-06-26 11:00:00.00-7:00
---

# Course Syllabus

Be sure to read the course syllabus for information on the logistics of this course.

<https://ucsb-cs16-m18.github.io/info/syllabus/>

# CSIL Policies

Be sure to review the CSIL policies. Slides are attached in the following Piazza post:

<https://piazza.com/class/jiqcwxay7mkdo?cid=6>

# High-level Overview of a Computer System

* Input Devices
	* keyboard, mouse, game controller, camera, etc.
* Output Devices
	* printer, monitor, speakers, etc.
* Processor
	* Hardware component that performs computations.
* Main Memory
	* Also known as "Random Access Memory" (RAM)
	* Volatile (does not persist when the system powers off)
* Secondary Memory
	* Non-volatile storage (ex: Mechanical / SSD Hard Drive)
	* Can hold large amounts of memory, but have slower access time than RAM.

# vim Editor

* We will use vim for the first few weeks this quarter.
* Important to be comfortable with a Unix-based command-line text editor.
* Be sure to understand how to do the [basic eight](https://ucsb-cs16.github.io/topics/vim_basic_eight/)functions.

# Hello World Program

```
// hello.cpp
#include <iostream>

using namespace std;

int main() {
	cout << "Hello CS 16!" << endl;
	return 0;
}
```

* Compile and execute the program

```
$ g++ -o hello hello.cpp
$ ./hello
Hello CS 16!
$
```

* `g++` is one of several C++ compilers
	* Compilers translate "source code" (i.e. the contents in the .cpp file) into a lower-level representation that is easier for computer system hardware to understand.
* `-o` is a "flag" that instructs the g++ compiler to produce an executable file called `hello`
* `hello.cpp` is the source file for g++ to use when producing the executable file.
* In order to actually run an executable file in Unix, `./[filename]` is used.

