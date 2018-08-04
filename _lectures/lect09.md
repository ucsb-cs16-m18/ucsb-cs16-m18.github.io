---
num: "Lecture 9"
desc: "Structs and Reference Variables"
ready: true
date: 2018-07-31 11:00:00.00-7:00
---

# Structs

* Structs are a programmer-defined type containing a set of associated values with possibly varying types.
* C++ gives us a lot of tools and types to work with out-of-the-box.
	* However, it’s impossible for a programming language to give us all possible types of abstractions
	* Programmers can organize data into types that fit the needs of an application.

## Defining a struct

```
struct Student { // Student is now a new defined type
	string name;
	int perm;
	double tuition;
}; // Syntactically, a ‘;’ is needed at the end of a struct definition.
```

* You can use the ‘.’ operator to assign values to and access values from a member of a struct type.

## Example

```
int main() {
	Student s1; // defining a variable containing the struct type Student
	s1.name = "Chris Gaucho";
	s1.perm = 1234567;
	s1.tuition = 3000.50;

	cout << "Name: " << s1.name << ", perm: " << s1.perm
		 << ", tuition: " << s1.tuition << endl;

	return 0;
}
```

* We can use this representation to do more interesting things like keep collections of students in a class, department, university, etc.

## Struct values as pointers

* A pointer can point to any C++ type, including structs!

```
Student* s2 = &s1; // OK
s2.name = "Mr. E"; // ERROR! Why?
```

* The code above won’t work because s2 is a pointer containing an address to a Student struct.
	* Remember, pointers contain memory addresses to a type!
	* If we wanted to modify a memory address, we would have to dereference the pointer.

```
*s2.name = "Mr. E"; // Still contains an error!
```

* In this case, the ‘.’ operator has precedence over the ‘*’ operator.
	* So it’s still trying to access the name field from a pointer variable without dereferencing it.
* One way to correct this is to dereference the variable first, then access the struct’s variable.

```
(*s2).name = "Mr. E"; // OK. Pointer is dereferenced first, then name is accessed
```

* When dealing with pointers, this mechanism is so common that there is a shortcut to do this.
* The ‘->’ operator is used.

```
s2->name = "Mr. E"; // OK. Same as (*s2).name
```

## A larger example: courses with students

```
struct Student {
	string name;
	int perm;
	double tuition;
};
struct Course {
	string name;
	int enrolled;
	Student roster[100];
};

void printStudentInfo(Student s) {
	cout << "\tStudent Name: " << s.name << ", PERM: " <<
	s.perm << ", tuition: " << s.tuition << endl;
	return;
}

void printCourseInfo(Course c) {
	cout << "Course Name: " << c.name << ", Enrolled: " <<
	c.enrolled << endl;

	for (int i = 0; i < c.enrolled; i++) {
		printStudentInfo(c.roster[i]);
	}
	return;
}

int main() {

	Student s0;
	s0.name = "Chris Gaucho";
	s0.perm = 1234567;
	s0.tuition = 3000.50;

	Student s1;
	s1.name = "Jane Doe";
	s1.perm = 7654321;
	s1.tuition = 0;
	Student s2;
	s2.name = "John Doe";
	s2.perm = 5555555;
	s2.tuition = 10000;

	Course cs16;
	cs16.name = "CMPSC 16";
	cs16.enrolled = 3;
	cs16.roster[0] = s0;
	cs16.roster[1] = s1;
	cs16.roster[2] = s2;

	printCourseInfo(cs16);

	return 0;
}
```

* We can also write additional functionality for our data such as calculating min,max,average tuition...

```
double calculateTuitionAverage(Course c) {
	double totalTuition = 0;

	for (int i = 0; i < c.enrolled; i++) {
		totalTuition += c.roster[i].tuition;
	}

	return totalTuition / c.enrolled;
}

double calculateTuitionAverage(Course* c) {
	double totalTuition = 0;

	for (int i = 0; i < c->enrolled; i++) {
		totalTuition += c->roster[i].tuition;
	}

	return totalTuition / c->enrolled;
}

int main() {
// …
	cout << calculateTuitionAverage(cs16) << endl;
	cout << calculateTuitionAverage(&cs16) << endl;
}
```

# Reference Variables

* Reference variables are considered another alias to a variable that was assigned to it.
	* Any changes to either variable are reflected in both variables.

```
int x = 100;
int& y = x; // y references x

cout << x << ", " << y << endl;
x = 500;
cout << x << ", " << y << endl;
x = 200;
cout << x << ", " << y << endl;
```

## Some differences between reference variables and pointers

* Reference variables may not change after it was assigned to reference another variable.
	* Pointers can change what it’s pointing to.
* Reference variables must be initialized.
	* Pointers can be uninitialized.
* Reference variables cannot refer to other reference variables
	* Pointers can have pointers to pointers to pointers …
* Reference variables’ address is the same address as the variable it binds to.
	* Pointers’ values have the address it points to, but occupies its own space on the stack and has its own memory address.
	* So when we pass-by-reference, we are technically using reference variables that are using the same memory address as the function caller’s parameter variables.

## Example (observe the addresses)

```
int a = 10;
int* p = &a;
int& r = a;

cout << "a = " << a << endl;
cout << "&a = " << &a << endl;
cout << "p = " << p << endl;
cout << "&p = " << &p << endl;
cout << "r = " << r << endl;
cout << "&r = " << &r << endl;
```

![Memory Diagram](memory.png)
