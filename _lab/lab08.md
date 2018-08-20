---
layout: lab
num: lab08
ready: true
desc: "Strings and recursion"
assigned: 2018-08-22 08:00:00.00-8
due: 2018-08-26 23:59:00.00-7
---
<div markdown="1">


# Goals of this lab
This lab will have you do programming exercises with C-strings, string class objects, recursive functions, and Makefiles. You will also get more practice writing programs from scratch with little skeleton code.

This lab may be done solo, or in pairs.

Before you begin working on the lab, please decide if you will work solo or with a partner.

As stated in the previous lab, there are a few requirements you must follow if you decide to work with a partner. I will re-iterate them here:

* Your partner must be enrolled in the same lab section as you (so there is a dedicated time where you and your partner can work together).
* You and your partner must agree to work together outside of lab section in case you do not finish the lab during your lab section. You must agree to reserve at least two hours outside of lab section to work together if needed (preferrably during our TAs' office hours where you can ask them for additional help). You are responsible for exchanging contact information in case you need to reach your partner.
* If you choose to work with a partner for a future lab where pair programming is allowed, then you must choose a partner you have not worked with before.
* You MUST add your partner on Gradescope when submitting your work <strong>*<u>EACH TIME</u>*</strong> you submit a file(s). After uploading your file(s) on Gradescope, there is a "Group Members" link at the bottom (or "Add Group Member" under "Groups") where you can select the partner you are working with. Whoever uploaded the submission must make sure your partner is part of your Group. Click on "Group Members" -> "Add Member" and select your partner from the list.

Once you and your partner are in agreement, choose an initial driver and navigator.

# Step 1: Getting Started

1. Go to github and create a git repo for this lab following the naming convention specified in previous labs. If you are working with a partner only one of you needs to create the repo.

2. If you are working with a partner and you are the one who created the github repo, add your partner as a collborator on the repo

3. Driver, log on to your CSIL account.

4. Open a terminal window and log into the correct machine.

5. Change into your CS 16 directory

6. Clone your github repo in the ~/cs16/ directory. Then cd into your repo directory.

Note: Remember to push your work to github at the end of EVERY work session. That way, both partners always have access to the latest version of the code even if the code is being developed on one partner's CoE account.

# Step 2: Getting the starter code and writing the programs

* Navigate to your cs16 directory and clone the git repository you created
```
git clone git@github.com:ucsb-cs16-m18/lab08_alily_jgaucho.git
```
* cd into this new directory
```
cd lab08_alily_jgaucho
```

* Copy the starter code by typing the following command:

```
cp /cs/faculty/richert/public_html/cs16/lab08/* ./
```

Typing the list (ls) command should show you the following files in your current directory

```
$ ls
linkedListFuncs.cpp  recLinkedListFuncs.cpp  strFuncs.h
linkedListFuncs.h    recLinkedListFuncs.h    tddFuncs.cpp
linkedList.h         strFuncs.cpp            tddFuncs.h
```

This lab will have you write two functions that are specified in strFuncs.h and two functions that are specified in recLinkedListFuncs.h. You must implement these functions in strFuncs.cpp and recLinkedListFuncs.cpp. You must follow the instructions carefully. It is not enough to pass the gradescope check as the instructor and the TAs *will* be checking your submitted code to make sure your solution is using recursion.

## Program to find if two strings are anagrams
 In the file strFuncs.cpp, write a function called isAnagram that takes two strings as arguments and returns a boolean true if the two strings are anagrams, otherwise it returns false. The function should not be case sensitive and should disregard any punctuation or spaces. Two strings are anagrams if the letters can be rearranged to form each other. For example, “Eleven plus two” is an anagram of “Twelve plus one”. Each string contains one “v”, three “e’s”, two “l’s”, etc. Similarly "Rats and Mice" and "in cat's dream" are anagrams of each other. You may use any of the C-string library or string class functions to complete this code. You may **not** use built-in C++ functions that we have NOT discussed in lecture. You must follow a TDD style of coding. Write your own test code in a separate file and write a Makefile to compile the code.

---
## Program to check if an input string is a palindrome

In strFuncs.cpp you are asked to a function to check if a string is a palindrome. For example: "redivide" is not a palindrome, while "detartrated" is a palindrome. Read the instructions in the file carefully to understand the constraints specified for the function. Ignore case when comparing characters of the string.

```
bool isPalindrome(const string s1);
```
The above function takes a C++ string as input and returns true if an input string is a palindrome and false if it is not. You can do this by checking if the first character equals the last character, and so on. You may choose a recursive implementation in this case, although it is not required. If you chose a recursive implementation you may or may not choose to write a helper function. You won't need a helper function is you used the substr (substring) function appropriately in your recursive calls.

## Program to recursively find the sum of elements of a linked list

```
int recursiveSum(Node* head);
```
In recLinkedListFuncs.cpp you are asked to reimplement the sum function from last week, this time recursively. If there are no elements of the list, return the value 0;

## Program to recursively find the largest value of a linked list

```
int recursiveLargestValue(Node* head);
```

In recLinkedListFuncs.cpp you are asked to reimplement the largestValue function from last week, this time recursively. For this function, you may assume that the linked list contains at least one value. 

## Step 3: Turn in your code on Gradescope

Submit all the .cpp and .h files to Lab06 assignment on Gradescope via your github repo. Then visit Gradescope and check that you have a correct score. If you are working with a partner, make sure both of you join a team on gradescope, otherwise only one of you will get credit for the lab

* You must check that you have followed these style guidelines:

1. Indentation is neat, consistent and follows good practice (see below)
2. Variable name choice: variables should have sensible names.
	More on indentation: Your code should be indented neatly. Code that is inside braces should be indented, and code that is at the same "level" of nesting inside braces should be indented in a consistent way. Follow the examples from lecture, the sample code, and from the textbook.
3. Your solution uses recursion. You will not receive credit otherwise (even if Gradescope marks your code as correct).

* Your submission should be on-time. If you miss the deadline, you are subject to getting a zero.

Commit and push the latest version of your code on github

## Step 4: Done!

If you are in the Phelps lab or in CSIL, make sure to log out of the machine before you leave. Also, make sure to close all open programs before you log out. Some programs will not work next time if they are not closed. Remember to save all your open files before you close your text editor.

If you are logged in remotely, you can log out using the exit command:

`$ exit`
