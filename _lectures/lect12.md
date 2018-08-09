---
num: "Lecture 12"
desc: "linked lists, Midterm 2 Review"
ready: true
date: 2018-08-09 11:00:00.00-7:00
---

# Linked Lists

* There are many ways to organize data (data structures)
* We’ve seen examples of stacks and arrays
	* But there are others like trees, tries, hash tables, …
* And there are many ways to IMPLEMENT these data structures
	* Some may use arrays (like arrayLists or vectors)
	* Some may use object pointers to link structures together.
		* Linked lists form a collection similar (but also very different) than an array.

* We can represent any type of data using structs.
* For example, an ITEM (Node) in a linked list can be a struct that contains some data (like a string, int, double, char, or another struct).
* The NEXT element in a linked list is a pointer to a linked list node representing the next item in the collection.
* Since we don’t know how many elements a linkedList may contain, managing this structure on the heap is essential!

## Linked List Structs

* There are many ways we can implement a linked list, but we will focus on an singly-linked list implementation with a head and tail reference.
* A LinkedList struct will contain two pointers to linked list nodes:
	* one points to the first element of the list (head)
	* the other points to the last element of the list (tail).
* A node in a linked list will contain some data, and a pointer to the next Node in the linked list collection.

```
struct Node {
	int data;
	Node* next;
};

struct LinkedList {
  Node* head;
  Node* tail;
};
```

![general list](generalList.png)

## Example of "walking down" a linked list

* Assume we have a linked list with the following nodes:

```
[10]->[20]->[30]->null
```

* We can walk down the collection and visit every node by using each Node's next pointer as long as the next pointer != NULL.

```
cout << list->head->data << endl; // 10
cout << list->head->next->data << endl; // 20
cout << list->head->next->next->data << endl; // 30
cout << list->head->next->next->next->data << endl; // seg fault!
```

* The performance of certain functionality with data structures largely depends on how the data is organized under-the-hood.
* On a high-level, arrays and linked lists are conceptually the same.
	* However, depending on what kind of operations performed on the data structure, performance may greatly differ. For example,
		* inserting to the front of a singly-linked linked list is much faster than inserting to the front of an array.
		* directly accessing an element in an array is much faster than directly accessing an element in a linked list.

## insertToFront() Linked List

* Order of pointer reassignment matters since we always want to make sure we don't "lose" the address of something we need on the heap.

1. Create new node to insert
2. Assign new node's next pointer to the current list's head.
3. Reassign the list's head to the new node.

![insertToFront](insertToFront.png)

## deleteIndex(int index)

Case 1: Remove first element

1. Reassign list head to list head's next pointer.
2. delete first element.

Case 2: Remove middle element

1. Reassign previous node's next pointer to current node's next pointer.
2. delete current node.

Case 3: Remove last element

1. Set previous node's next pointer to NULL.
2. Reassign list's tail pointer to previous node.
3. delete current node.

![delete index](deleteIndex.png)

# Linked List Implementation

```
// LinkedList.h
#ifndef LINKEDLIST_H
#define LINKEDLIST_H

struct Node {
	int data;
	Node* next;
};

struct LinkedList {
	Node* head;
	Node* tail;
};

void printList(LinkedList* list);
void insertToFront(LinkedList* list, int value);
bool exists(LinkedList* list, int value);
int length(LinkedList* list);
void deleteIndex(LinkedList* list, int index);

#endif
--------------
// LinkedList.cpp
#include <iostream>
#include "linkedList.h"
using namespace std;

void printList(LinkedList* list) {
	for (Node* i = list->head; i != NULL; i = i->next) {
		cout << "[" << i->data << "]->";
	}
	cout << "null" << endl;
}

void insertToFront(LinkedList* list, int value) {
	if (list->head == 0) {		// empty list
		Node* item = new Node;
		item->data = value;
		item->next = NULL;
		list->head = item;
		list->tail = item;
	} else { 			// not empty
		Node* item = new Node;
		item->data = value;
		item->next = list->head;
		list->head = item;
	}
}

bool exists(LinkedList* list, int value) {
	for (Node* i = list->head; i != NULL; i = i->next) {
		if (i->data == value)
			return true;
	}
	return false;
}

int length(LinkedList* list) {
	int counter = 0;
	// let's use a while loop instead of a for...
	Node* temp = list->head;
	while (temp != 0) {
		counter++;
		temp = temp->next;
	}
	return counter;
}

void deleteIndex(LinkedList* list, int index) {
	if (index >= length(list) || index < 0) {
		cerr << "Invalid index: " << index << endl;
		return;
	}

	// check if first item
	if (index == 0 && list->head != 0) {
		Node* temp = list->head;
		list->head = list->head->next;
		delete temp;
		return;
	}

	Node* prev = list->head;
	Node* curr = list->head->next;
	for (int i = 1; i < index; i++) {
		prev = prev->next;
		curr = curr->next;
	}

	// remove the current node
	prev->next = curr->next;
	delete curr;

	// re-assign list->tail if curr was the last node.
	if (index == length(list) - 1)
		list->tail = prev;

	return;
}
----------
// main.cpp
#include <iostream>
#include <string>
#include <fstream>
#include "linkedList.h"

using namespace std;

int main() {
	LinkedList* list = new LinkedList;
	list->head = 0;
	list->tail = 0;

	cout << length(list) << endl;

	insertToFront(list, 10);
	cout << length(list) << endl;
	insertToFront(list, 20);
	insertToFront(list, 30);
	printList(list);			// 30->20->10

	cout << exists(list, 15) << endl; 	// 0
	cout << exists(list, 30) << endl; 	// 1
	cout << exists(list, -1) << endl; 	// 0

	cout << length(list) << endl;		// 3

	deleteIndex(list, -1); 			// err
	deleteIndex(list, 5);			// err
	deleteIndex(list, 3);			// err
	deleteIndex(list, 2);			// OK!
	printList(list);			// 30->20->null

	return 0;
}
----------
$ g++ -o main main.cpp LinkedList.cpp
```

# Midterm 2 Review

```
- Tuesday in lecture

Logistics
	- TAs will proctor
	- Bring studentID and a writing utensil
		- Preferable ink or dark led
		- PLEASE WRITE LEGIBLY
	- No electronic devices
	- No book, no notes

Format
	- Similar to midterm 1 (more or less)
	- Possible types of questions
		- Short answers
		- Explain, describe, define, ...
		- Write some code
		- Fill in the blank
		- True / False (if false, explain)
		- Given code, write the output
	- Should take ~ 1 hour (but you have the entire lecture)
	- Covers a broad range of topics, but probably not everything.

Topics
	- Will cover everything up to Tuesday's lecture (8/7) NOT including LinkedLists.
	- Will cover material from lectures, reading, homeworks, and labs.

File IO
	- reading and writing from / to files
	- Appending to / overwriting a file.

C++ build process
	- Breaking code into multiple files (.cpp , .h)
	- Preprocessing vs. Compilation vs. Linking
	- Makefiles
		- General syntax
		- Conceptual understanding
		- Simple g++ compilation rules

TestDriven Development
	- Write a test that does ...
	- Given tests, which ones pass
	- Explain Test Driven Development ...

Arrays
	- Declaration
	- Syntax
	- Reading / writing elements

Number Conversion
	- Any base to base 10 notation
	- Binary to base 10 / Base 10 to binary
	- Hex to binary / binary to Hex

Memory concepts and pointers
	- Pointer syntax
	- Memory sizes of pointers and types
	- Arrays as pointers
	- Dereferencing
	- Pointers to pointers
	- pass by reference vs. pass by value
	- reference variables

Structs
	- Defining / declaring structures
	- pointers to structs
		- "->" operator

Pointer Arithmetic
	- compute the offset of arrays
	- Segmentation faults
	- passing a pointer by value / reference

Dynamic memory management
	- stack vs. heap
	- dynamic allocation / deallocation
		- "new" operator
		- "delete" operator
	- Dangling pointers

Good Luck!
```







