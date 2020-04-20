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

There are two main strategies to deal with errors:
1. Look before you leap (LBYL)
2. Easier to ask for forgiveness than permission (EAFP)

[LBYL]({{ page.root }}/reference/#LBYL) strategy is generally used in low-level programming languages and consist in checking 
the variables for potential errors in later functions before the error actually happens.
Then, according to the estimated error proceed.

[EAFP]({{ page.root }}/reference/#EAFP), on the other hand, lets the code to fail, and then, instead of stopping the execution,
check the error and proceed accordingly to it.   

In python, the most common strategy is EAFP. This strategy has several advantages respect to LBYL.
- Simplicity: By not consider all possible failures the code (at high level) becomes simpler and 
easier to read
- Modularity: If the error occurs in one of the modules, the error is risen and the top script
can capture it and decide how to handle it, centralizing (or encapsulating) error handling at 
one section instead of being spread along the code.

Error handling is done using `try` and `except` clauses. These allows to capture an error and write and alternative
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

Also, multiple types of exceptions can be handled by an unique `except` clause, by grouping
them in a tuple:

~~~
string_input = input("Enter a number: ")

try:
    number = float(string_input)
    division = 1/number
    print('result: ', division)
except (ZeroDivisionError, ValueError):
    print('some error occurred')
~~~
{: .language-python}

> ## Keep in mind
>
> The main objective of having multiple types of exceptions is to have more control over
> the different causes of errors the program may have. It is good practice to be as restrictive
> as possible handling the exceptions by using short `try` blocks and using specific `except`clauses.
> This is in order to not overlook unexpected errors. 
{: .callout}


## Raising custom errors
In long programs it is useful to be able to rise exceptions by ourselves if certain conditions
are met. This advertises the rest of the program that a particular error has ben produced so other
part of the code can handle it. This is done using the keyword `raise`. 

~~~
def inverse(num)
    if num < 6:
        raise ValueError('The value should be greater than 5')
    return 1/num

string_input = float(input("Enter a number greater than 5: "))
division = inverse(num)
print('result: ', division)

~~~
{: .language-python}

In the last example `raise` is set inside the inverse function. This allows to combine with the clauses
`try` and `except` to properly handle the exception as in the previous examples.

~~~
def inverse(num)
    if num < 6:
        raise ValueError('The value should be greater than 5')
    return 1/num

string_input = float(input("Enter a number greater than 5: "))
try:
    division = inverse(num)
except ValueError:
    print('Adding 6 to satisfy condition')
    num = abs(num) + 6
    division = inverse(num)
    
print('result: ', division)
~~~
{: .language-python}

{% include links.md %}
