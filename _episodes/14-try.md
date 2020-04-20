---
title: Error handling
teaching: 30
exercises: 0
questions:
- "How to capture and handle errors in python programs?"
- "How can I avoid my program to crash when errors occur?"
objectives:
- "To be able to write a code that do not crash if errors ocur and can 
   execute different algorithms according to the error type."
keypoints:
- "`Try` and `except`clauses to catch and redirect errors"
- "Easier to ask for forgiveness than permission (EAFP) vs Look before you leap (LBYL)."
---

Good programs are founded on good error handling. High level programming languages 
like python rely on a large set of libraries created by different programmers from which 
the and user may have almost no knowledge of its internal operation.
When errors occur in one of these internal libraries the program does not end the execution 
immediately, but instead it rises and exception that scales up until the top function 
before crashing. This can be seen in the error traceback.

~~~
Traceback (most recent call last):
  File "/Users/user/myprogram/myscript.py", line 4, in <module>
    internal_function(number)
  File "/Users/user/somelibrary/functionlibrary.py", line 3, in internal_function
    result = 2/number
ZeroDivisionError: division by zero

Process finished with exit code 1
~~~
{: .error}

This traceback shows that ZeroDivisionError has been raised. This particular error indicates
that some division contains a zero in its denominator as can be deduced by its name. There are 
many types of errors defined in the python language. Usually the error names are very explicit 
and its meaning can be inferred by the name. 
Using `try` and `except` clauses it is possible to capture this error and write and alternative
algorithm to handle it.

This clauses are used in fragments of code that may potentially rise an error.
In the following example the user is asked to introduce a number and the program calculates the
inverse. If a 0 is introduced a ZeroDivisionError is raised.
  
~~~
number = float(input("Enter a number: "))

try:
    division = 1/number
    print('result: ', division)
except ZeroDivisionError:
    print('This number produces an error')
   
~~~
{: .language-python}

The potentially failing step of this code is during the division calculation line.
For this reason the `try` clause contains this line. If a ZeroDivisionError is raised 
within this cause then the code within `except` clause is executed.

In case that the code within `try` clause can raise different error, it is possible to
write multiple `except` clauses. The following code is a modification of the former example
in witch the input introduced by the user if converted to float number within the `try`clause.
If the input is not a number, the conversion to float will raise a ValueError exception. In order
to capture this exception, an additional `except` clause is written. 

~~~
string_input = input("Enter a number: ")

try:
    number = float(string_input)
    division = 1/number
    print('result: ', division)
except ZeroDivisionError:
    print('This number produces an error')
except ValueError:
    print('This is not a number')
~~~
{: .language-python}

## Custom errors



{% include links.md %}
