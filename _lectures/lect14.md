---
num: "Lecture 14"
desc: "Recursion"
ready: true
date: 2018-08-21 11:00:00.00-7:00
---

# Recursion

* When a function contains a call to itself.
* We’re mostly familiar with writing code in an iterative fashion (i.e. one statement after the other).
	* Several programming languages exist where it’s based purely on recursion.
* Useful for problems that can be solved by using the results of similar sub problems.

## Properties of Recursion
* One or more base cases that providing the "stopping" condition
* One or more recursive calls, where the arguments are "closer" to the base case than the function input.
* Any recursive function can be done in an iterative way and any iterative function can be done in a recursive way.

## Example: Factorial

* N! = N * (N-1) * (N-2) * ... * 3 * 2 * 1
	* Note: 0! = 1, 1! = 1

```
int factorial (int n) {
	if (n == 1) // base case
		return 1;

	return n * factorial(n – 1);
}
---
int main() {
	cout << factorial(4) << endl; // 24	
}

```

* Evaluation of factorial(4)

```
factorial(4) = 4 * factorial(3)
                   3 * factorial(2)
                       2 * factorial(1)
                           1
                       2 * 1
                   3 * 2
               4 * 6
               24
```

## Example: Fibonacci

* A fibonacci sequence is when nth number in the sequence is the sum of the previous two (i.e. f(n) = f(n-1) + f(n-2)).
* f(n) = f(n-1) + f(n-2))
* f(0) = 0, f(1) = 1, f(2) = 1, f(3) = 2, f(4) = 3, f(5) = 5, f(6) = 8, … , f(n) = f(n-2) + f(n-1)

```
int fibonacci(int n) {
	if (n == 1) {
		return 1;
	}
	if (n == 0) {
		return 0;
	}
	retrun fibonacci(n-2) + fibonacci(n-1);
}
-----
int main() {
	cout << fibonacci(4) << endl; 3
}
```

* Evaluation of fibonacci(4)

```
fib(4)
fib(2)          + fib(3)
fib(0) + fib(1) + fib(3)
0      + 1      + fib(3)
1               + fib(1) + fib(2)
1               + 1      + fib(2)
1               + 1      + fib(0) + fib(1)
1               + 1      + 0      + 1
3
```

## Example: Recursively find the length of a C-string

```
int recLength(char* s) {
	char temp = *s;

	if (temp != '\0') {
		return 1 + recLength(&s[1]);
	} else {
		return 0;
	}
}
----
char s1[] = {'a', '\0'};
char s2[] = {'\0'};
char s3[] = {'a', 'a', 'a', '\0'};

cout << recLength(s1) << endl;
cout << recLength(s2) << endl;
cout << recLength(s3) << endl;
```

## Example: Recursively search through a Linked List

* Assuming we are using the linkedListFuncs.h and linkedList.h from lab08

```
bool recExists(Node* n, int value) {
	if (n == NULL) {
		return false;
	}

	if (n->data == value) {
		return true;
	}

	return recExists(n->next, value);
}
---
#include "linkedListFuncs.h"

int main() {
	int arr1[3]={73,57,61};
	LinkedList* list1 = arrayToLinkedList(arr1,3);

	cout << recExists(list1->head, 57) << endl; // 1
	cout << recExists(list1->head, 60) << endl; // 0
	cout << recExists(list1->head, 73) << endl; // 1
}
```

## Recursion Performance

* Recursion consumes more memory than an iterative solution since it keeps adding memory to the call stack.
* Recursion can sometimes be simply written vs an iterative algorithm (more readable).

## Stack Overflow

* An event that happens when a program crashes due to running out of memory in its call stack.
	* Usually happens when there is an infinite loop of recursive calls.
	* For example, forgetting to provide a base case may result in an infinite number of recursive calls.

```
int factorial (int n) {
/* REMOVE BASE CASE
	if (n == 1) // base case
		return 1;
*/

	cout << n << endl;
	return n * factorial(n – 1);
}
```
