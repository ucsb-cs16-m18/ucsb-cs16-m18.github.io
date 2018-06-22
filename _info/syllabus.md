---
title: "Syllabus, CS16, Summer 2018"
layout: handout
ready: true
---

Basic Facts
-----------

* **Course Web Site**: <https://ucsb-cs16-m18.github.io/>
* **Instructor**:  [Richert Wang](http://www.cs.ucsb.edu/~richert)
   * Email is richert@ucsb.edu, BUT please use [Piazza](piazza.com/ucsb/summer2018/cmpsc16/home) for course related communication.
* **Lecture**: TuTh 12:30pm-1:45pm Phelps 3526, ATTENDANCE REQUIRED.
* **TAs**:  {{site.ta_list_full}} (contact via Piazza)
* **Lab** (75 minute lab section): Wednesdays 10:30am, 12pm, 1:30pm - Phelps 3525, ATTENDANCE REQUIRED.                                         
* **Office Hours**: Wednesdays 12:00pm - 3:00pm, Wednesdays in Phelps 3526

# Required Resources

* Textbooks:
  * "Problem Solving with C++" - Walter Savitch, 9th edition

Official UCSB Catalog Description
---------------------------------

<div style="background-color:#eee; border: 8px inset #333; font-size:90%; margin:1em; width:45em; padding: 0.5em;" markdown="1">

CMPSC 16: Problem Solving with Computers I

**Prerequisite:** Mathematics 3A with a grade of C or better (may be taken concurrently) 

**Recommended Preparation:** CS 8 or Engineering 3, or significant prior programming experience.

**Repeat Comments:** Legal repeat of CMPSC 10.

Fundamental building blocks for solving problems using computers. Topics include basic computer organization and programming constructs: memory CPU, binary arithmetic, variables, expressions, statements, conditionals, iteration, functions, parameters, recursion, primitive and composite data types, and basic operating system and debugging tools.

</div>

## A few course policies in brief

* If you are registered for another UCSB course that overlaps with this one, you MUST HAVE specific written permission from both instructors, or I am within my rights to give you a failing grade on any work you miss as a result, and will NOT make any accommodations for you.
* Collaboration is only permitted when specifically allowed for — otherwise, you must do your own work.
   * On most homework assignments you may collaborate with at most one other person (who must be named).
* Attendance is required at all lectures and labs (discussion sections).
  * I recognize that some absences (e.g. minor illnesses, mishaps, etc.) are unavoidable. Litigating whether each of these is "excused" or not isn't a good use of anyone's time, so instead we will drop the lowest two grades from everyone's homework. This way, absences (or failure to submit homework) does not unduly penalize your grade unless it becomes excessive.
* <strong>You</strong> must turn in your homework in lecture the day that it is due.
* We will use the [gradescope system](https://gradescope.com) this quarter. More instructions on gradescope will be given in lecture and lab assignments.
* Any regrade requests must be made on Gradescope and **we will not consider a regrade request one week after the assignment grades are distributed back to students.**

You may NOT: 

* Turn in homework on a day other than when it is due (early or late).
* Have someone else turn in your homework for you (that will be considered academic dishonesty).
* Drop it off with the instructor or TA to be graded later.

## What this course is about 

CS16 is the first course in a three-course sequence (CS16, CS24, CS32). The purpose of this sequence is to provide a solid foundation of algorithms and data structures.

## What you need before taking this course

CS16 assumes students already have some programming experience and have completed an introductory computer science course similar to CS8.

<p>This course will present C++ from the beginning; no prior knowledge of C++ is assumed. You should be comfortable with all of the following:</p>

<table border="1" cellspacing="1" cellpadding="1" id="topicTable">
  <tr>
    <td><ul>
      <li>Problem solving
        <ul>
            <li>breaking down a problem into a sequence of steps</li>
          <li>abstracting specific problems into general ones<br />
            and finding general solutions</li>
        </ul>
      </li>
      <li>Memory concepts
        <ul>
            <li>variables, primitive vs. reference variables, name, type, value</li>
          <li>assignment statements</li>
          <li>scope of variables</li>
        </ul>
      </li>
      <li>Control structures
        <ul>
            <li>for loops, if/else, while loops</li>
        </ul>
      </li>
      <li>Arrays (or a similar data structure, e.g. Lists in Python)
        <ul>
            <li>index vs. value, finding sum, min, max, average, count of elements matching some condition, making a new list of elements containing only those that match some condition</li>
        </ul>
      </li>
    </ul>    </td>
    <td><ul class="style11">
      <li>Functions
        <ul>
            <li>function call vs. function definition</li>
          <li>formal vs. actual parameters (arguments)</li>
        </ul>
      </li>
      <li>Testing
        <ul>
            <li>How to test your code</li>
        </ul>
      </li>
      <li>Input/output concepts
        <ul>
            <li>Writing to the terminal</li>
          <li>Reading from the keyboard</li>
          <li>Reading and writing to files</li>
          <li>Neatly formatting output</li>
        </ul>
      </li>
      <li>Program style
        <ul>
            <li>How to write code that other people can read and understand</li>
        </ul>
      </li>
    </ul>    </td>
  </tr>
</table>

<p>So, what is it that you need to know by the end of this course?   Here's the  list of just a few of the things you'll need to know to be ready for CS24 (the next programming course). You'll have the opportunity to learn all of these things (though not necessarily in this order).</p>

* A few of the basic data types of C++, including at least, int, double, char, bool, string
* The basic control structures of C++ (if/else, while, for etc.)
* Defining functions in C++, and passing parameters to functions in three different ways (by value, by pointer, and by reference)
* Scope and lifetime of variables in C++
* The use of "const" with parameters to functions
* Using arrays in C++, and C-strings (null-terminated character arrays)
* How arrays are passed to functions, and the relationship between arrays and pointers
* Defining and working with structs in C++
* Using structs to create singly linked lists where the space for the list nodes is allocated on the heap
* The difference between space allocated on the stack (e.g. local variables) and space allocated on the heap (with the new and delete operators)
* Converting from binary to decimal, octal, and hex, and back again&mdash;and how this relates to how C++ programs store various kinds of data in memory.
* The basic principles of recursion, and some idea of when a recursive solution is appropriate.

Learning the details of programming requires <strong>A LOT</strong> of practice, like learning any new skill. Making mistakes is an essential part of learning as long as you learn from them! Questions like "I wonder what will happen if I do this..." or "How will C++ behave in this case..." is a great way to investigate and observe the functionality and limitations of a programming language (there are many programming languages available to software developers and each have their specific pros and cons that may or may not be the best choice for the problems you are trying to solve).

I find the best way to practice is to <strong>rapid prototype constantly</strong>. Writing simple snippets of code to test and confirm your understanding allows you to 1) practice typing out code, which makes you more comfortable with the language and 2) solidify your understanding of the specific behavior of the programming language functionality.

# Course Grades

Letter grades will be determined by the end of the course after all labs, homeworks, and exams have been computed. I can say that I will not grade harder than a traditional straight scale (90% = A-, 80% = B-, etc.). However, I will adjust the letter grades accordingly based on your overall performance at the end of the course. If you are concerned about your grade in the class, I encourage you to discuss the matter with me during my office hours. Please come talk to me sooner rather than later so there can be some time where we can help you succeed in the course.

Your course grade will be determined as follows:

| Grade Item                        | Percentage of Final Grade |
|-----------------------------------|---------------------------|
| Midterm 1 (Tues. 7/17)            | 15 %                      |
| Midterm 2 (Tues. 8/14)            | 15 %                      | 
| Final (Thurs. 8/30) 				| 30 %                      |
| Homeworks                         | 10 %                      |
| labs                              | 30 %                      | 

In general, homeworks will be assigned periodically throughout the quarter, and are due in lecture on the due date.

There will be labs assigned throughout the quarter. You will work on the labs during your assigned lab section, and most likely on your own time outside of your assigned lab section. Please be sure to check the due dates for all assignments on the course page and calendar.

# Late work

I will consider late submissions <strong>only</strong> for medical or family emergencies where documentation can be provided. This does not include overwhelming workload from other courses, scheduling conflicts, or vacation plans.

* There will not be any make ups for examinations.
* Two of the lowest homework scores will be dropped. Late homework submissions will not be accepted. However, even if you know you will not be able to submit a homework on time, I highly encourage you to complete it anyways since the homeworks will help prepare you for the examinations.
* All labs must be submitted by the due date. Depending on the case, your TA may consider grading your lab with a late penalty (and usually for cases where the submission was done very soon after the deadline). However, this is not an official policy and you risk receiving a zero for a late lab submission. 

Accommodations for disabilities
-------------------------------

Students with disabilities may request academic accommodations for exams online through the UCSB Disabled Students Program at [http://dsp.sa.ucsb.edu/](http://dsp.sa.ucsb.edu/). Please make your requests for exam accommodations through the online system as early in the quarter as possible to ensure proper arrangement.

Managing stress
---------------

Personal concerns such as stress, anxiety, relationships, depression, cultural differences, can interfere with the ability of students to succeed and thrive. For helpful resources, please contact UCSB Counseling & Psychological Services (CAPS) at 805-893-4411 or visit [http://counseling.sa.ucsb.edu/](http://counseling.sa.ucsb.edu/).

Responsible scholarship
-----------------------

Honesty and integrity in all academic work is essential for a valuable educational experience.  The Office of Judicial Affairs has policies, tips, and resources for proper citation use, recognizing actions considered to be cheating or other forms of academic theft, and students’ responsibilities, available on their website at: http://judicialaffairs.sa.ucsb.edu. **Students are responsible for educating themselves on the policies and to abide by them.**

Furthermore, for general academic support, students are encouraged to visit Campus Learning Assistance Services (CLAS) early and often. CLAS offers instructional groups, drop-in tutoring, writing and ESL services, skills workshops and one-on-one consultations. CLAS is located on the third floor of the Student Resource Building, or visit http://clas.sa.ucsb.edu

Standard Disclaimer
-------------------

This syllabus is as accurate as possible, but is subject to change at
the instructor's discretion, within the bounds of UC policy.

