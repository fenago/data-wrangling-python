Lab 2: Advanced Operations on Built-In Data Structures
======================================================


#### Pre-reqs:
- Google Chrome (Recommended)

#### Lab Environment
Notebooks are ready to run. All packages have been installed. There is no requirement for any setup.

All notebooks are present in `~/work/data-wrangling-python/lab02` folder.


Advanced Data Structures
========================

Before we jump into constructing data structures, we\'ll look at a few
methods to manipulate them.

Iterator
--------

Let\'s learn about the various functions we can use with
`itertools`. As you execute each line of the code after the
`import` statement, you will be able to see details about what
that particular function does and how to use it:

```
from itertools import (permutations, combinations, \
                       dropwhile, repeat, zip_longest)
permutations?
combinations?
dropwhile?
repeat?
zip_longest?
```


For example, after executing `zip_longest?`, we\'ll see the
following output:



![](./images/B15780_02_01.jpg)


The preceding screenshot shows how the `zip_longest` function
could be used from the `itertools` module.

**Note:**

To look up the definition of any function, type the function name,
followed by *?*, and then press *Shift* + *Enter* in a Jupyter Notebook.

Let\'s go through the following exercise to understand how to use an
iterator to iterate through a list.


Exercise 2.01: Introducing to the Iterator
------------------------------------------

In this exercise, we\'re going to generate a long list containing
numbers. We will first check the memory occupied by the generated list.
We will then check how we can use the `iterator` module to
reduce memory utilization, and finally, we will use this iterator to
loop over the list. To do this, let\'s go through the following steps:

1.  Open a new Jupyter Notebook and generate a list that will contain
    `10000000` ones. Then, store this list in a variable
    called `big_list_of_numbers`:

    
    ```
    big_list_of_numbers = [1 for x in range (0, 10000000)] 
    big_list_of_numbers
    ```

    The output (partially shown) is as follows:

    
    ```
    [1,
     1,
     1,
     1,
     1,
     1,
     1,
     1,
     1,
     1,
    ```

2.  Check the size of this variable:

    
    ```
    from sys import getsizeof
    getsizeof(big_list_of_numbers)
    ```

    The output should be as follows:

    
    ```
    81528056
    ```

    The value shown is `81528056` (in bytes). This is a huge
    chunk of memory occupied by the list. And the
    `big_list_of_numbers` variable is only available once the
    list comprehension is over. It can also overflow the available
    system memory if you try too big a number.

3.  Let\'s use the `repeat()` method from
    `itertools` to get the same number but with less memory:

    
    ```
    from itertools import repeat
    small_list_of_numbers = repeat(1, times=10000000)
    getsizeof(small_list_of_numbers)
    ```

    The output should be:

    
    ```
    56
    ```

    The last line shows that our list `small_list_of_numbers`
    is only `56` bytes in size. Also, it is a lazy method, a
    technique used in functional programming that will delay the
    execution of a method or a function by a few seconds. In this case,
    Python will not generate all the elements initially. It will,
    instead, generate them one by one when asked, thus saving us time.
    In fact, if you omit the `times` keyword argument in the
    `repeat()` method in the preceding code, then you can
    practically generate an infinite number of ones.

4.  Loop over the newly generated iterator:

    
    ```
    for i, x in enumerate(small_list_of_numbers): 
        print(x)
        if i > 10:
            break
    ```

    The output is as follows:

    
    ```
    1
    1
    1
    1
    1
    1
    1
    1
    1
    1
    1
    1
    ```

We use the `enumerate` function so that we get the loop
counter, along with the values. This will help us break the loop once we
reach a certain number (`10`, for example).

**Note:**

To access the source code for this specific section, please refer to
<https://github.com/fenago/data-wrangling-python>.



In this exercise, we first learned how to use the iterator function to
reduce memory usage. Then, we used an iterator to loop over a list. Now,
we\'ll see how to create stacks.



Stacks
------

A stack is a very useful data structure. If you know a bit about CPU
internals and how a program gets executed, then you will know that a
stack is present in many such cases. It is simply a list with one
restriction, **Last In First Out** (**LIFO**), meaning an element that
comes in last goes out first when a value is read from a stack. The
following illustration will make this a bit clearer:



![](./images/B15780_02_02.jpg)




As you can see, we have a LIFO strategy to read values from a stack. We
will implement a stack using a Python list. Python lists have a method
called `pop`, which does the exact same `pop`
operation that you can see in the preceding illustration. Basically, the
`pop` function will take an element off the stack, using the
**Last in First Out** (**LIFO**) rules. We will use that to implement a
stack in the following exercise.



Exercise 2.02: Implementing a Stack in Python
---------------------------------------------

In this exercise, we\'ll implement a stack in Python. We will first
create an empty stack and add new elements to it using the
`append` method. Next, we\'ll take out elements from the stack
using the `pop` method. Let\'s go through the following steps:

1.  Import the necessary Python library and define an empty stack:

    
    ```
    import pandas as pd
    stack = []
    ```

    **Note:**

    `pandas` is an open source data analysis library in
    Python.

2.  Use the `append` method to add multiple elements to the
    stack. Thanks to the `append` method, the element will
    always be appended at the end of the list:

    
    ```
    stack.append('my_test@test.edu')
    stack.append('rahul.subhramanian@test.edu')
    stack.append('sania.test@test.edu')
    stack.append('alec_baldwin@test.edu')
    stack.append('albert90@test.edu')
    stack.append('stewartj@test.edu')
    stack
    ```

    The output is as follows:

    
    ```
    ['my_test@test.edu',
     'rahul.subhramanian@test.edu',
     'sania.test@test.edu',
     'alec_baldwin@test.edu',
     'albert90@test.edu',
     'stewartj@test.edu']
    ```

3.  Let\'s read a value from our stack using the `pop` method.
    This method reads the current last index of the list and returns it
    to us. It also deletes the index once the read is done:

    
    ```
    tos = stack.pop()
    tos
    ```

    The output is as follows:

    
    ```
    'stewartj@test.edu'
    ```

    As you can see, the last value of the stack has been retrieved. Now,
    if we add another value to the stack, the new value will be appended
    at the end of the stack.

4.  Append `Hello@test.com` to the stack:

    
    ```
    stack.append("Hello@test.com")
    stack
    ```

    The output is as follows:

    
    ```
    ['my_test@test.edu',
     'rahul.subhramanian@test.edu',
     'sania.test@test.edu',
     'alec_baldwin@test.edu',
     'albert90@test.edu',
     'Hello@test.com']
    ```


From the exercise, we can see that the basic stack operations,
`append` and `pop`, are pretty easy to perform.

Let\'s visualize a problem where you are scraping a web page and you
want to follow each URL present there (backlinks). Let\'s split the
solution to this problem into three parts. In the first part, we would
append all the URLs scraped off the page into the stack. In the second
part, we would pop each element in the stack, and then lastly, we would
examine every URL, repeating the same process for each page. We will
examine a part of this task in the next exercise.



Exercise 2.03: Implementing a Stack Using User-Defined Methods
--------------------------------------------------------------

In this exercise, we will continue the topic of stacks from the last
exercise. This time, we will implement the `append` and
`pop` functions by creating user-defined methods. We will
implement a stack, and this time with a business use case example
(taking Wikipedia as a source). The aim of this exercise is twofold. In
the first few steps, we will extract and append the URLs scraped off a
web page in a stack, which also involves the `string` methods
discussed in the last lab. In the next few steps, we will use the
`stack_pop` function to iterate over the stack and print them.
This exercise will show us a subtle feature of Python and how it handles
passing list variables to functions. Let\'s go through the following
steps:

1.  First, define two functions: `stack_push` and
    `stack_pop`. We renamed them so that we do not have a
    namespace conflict. Also, create a stack called
    `url_stack` for later use:

    
    ```
    def stack_push(s, value):
        return s + [value]
    def stack_pop(s):
        tos = s[-1]
        del s[-1]
        return tos
    url_stack = []
    url_stack
    ```

    The output is as follows:

    
    ```
    []
    ```

    The first function takes the already existing stack and adds the
    value at the end of it.

    **Note:**

    Notice the square brackets around the value to convert it into a
    one-element list using the `+` operation. The second
    function reads the value that\'s currently at the `-1`
    index of the stack, then uses the `del` operator to delete
    that index, and finally returns the value it read earlier.

    Now, we are going to have a string with a few URLs in it.

2.  Analyze the string so that we push the URLs in the stack one by one
    as we encounter them, and then use a `for` loop to pop
    them one by one. Let\'s take the first line from the
    `Wikipedia` article
    (<https://en.wikipedia.org/wiki/Data_mining>) about data science:

    
    ```
    wikipedia_datascience = """Data science is an interdisciplinary field that uses scientific methods, processes, algorithms and systems to extract knowledge [https://en.wikipedia.org/wiki/Knowledge] and insights from data [https://en.wikipedia.org/wiki/Data] in various forms, both structured and unstructured,similar to data mining [https://en.wikipedia.org/wiki/Data_mining]""" 
    ```

    For the sake of the simplicity of this exercise, we have kept the
    links in square brackets beside the target words.

3.  Find the length of the string:

    
    ```
    len(wikipedia_datascience) 
    ```

    The output is as follows:

    
    ```
    347
    ```

4.  Convert this string into a list by using the `split`
    method from the string, and then calculate its length:

    
    ```
    wd_list = wikipedia_datascience.split()
    wd_list
    ```

    The output is as follows (partial output):

    
    ```
    ['Data',
     'science',
     'is',
     'an',
     'interdisciplinary',
     'field',
     'that',
     'uses',
     'scientific',
     'methods,',
    ```

5.  Check the length of the list:

    
    ```
    len(wd_list)
    ```

    The output is as follows:

    
    ```
    34
    ```

6.  Use a `for` loop to go over each word and check whether it
    is a URL. To do that, we will use the `startswith` method
    from the string, and if it is a URL, then we push it into the stack:

    
    ```
    for word in wd_list:
        if word.startswith("[https://"):
            url_stack = stack_push(url_stack, word[1:-1])  
            print(word[1:-1])
    ```

    The output is as follows:

    
    ```
    https://en.wikipedia.org/wiki/Knowledge
    https://en.wikipedia.org/wiki/Data
    https://en.wikipedia.org/wiki/Data_mining
    ```

    Notice the use of string slicing to remove the surrounding double
    quotes `"[" "]"`.

7.  Print the value in `url_stack`:

    
    ```
    print(url_stack) 
    ```

    The output is as follows:

    
    ```
    ['https://en.wikipedia.org/wiki/Knowledge',
     'https://en.wikipedia.org/wiki/Data',
     'https://en.wikipedia.org/wiki/Data_mining']
    ```

8.  Iterate over the list and print the URLs one by one by using the
    `stack_pop`z function:

    
    ```
    for i in range(0, len(url_stack)):
        print(stack_pop(url_stack)) 
    ```

    The output is as follows:

    
    ![](./images/B15780_02_03.jpg)
    



9.  Print it again to make sure that the stack is empty after the final
    `for` loop:

    
    ```
    print(url_stack) 
    ```

    The output is as follows:

    
    ```
    []
    ```


In this exercise, we have noticed a strange phenomenon in the
`stack_pop` method. We passed the `list` variable
there, and we used the `del` operator inside the function in
*step 1*, but it changed the original variable by deleting the last
index each time we called the function. If you use languages like C,
C++, and Java, then this is a completely unexpected behavior as, in
those languages, this can only happen if we pass the variable by
reference, and it can lead to subtle bugs in Python code. So, be careful
when using the user-defined methods.



Lambda Expressions
------------------

Let\'s look at the following exercise to understand how we use a lambda
expression.



Exercise 2.04: Implementing a Lambda Expression
-----------------------------------------------

In this exercise, we will use a lambda expression to prove the famous
trigonometric identity:



![](./images/B15780_02_04.jpg)




Let\'s go through the following steps to do this:

1.  Import the `math` package:
    
    ```
    import math 
    ```

2.  Define two functions, `my_sine` and `my_cosine`,
    using the `def` keyword. The reason we are declaring these
    functions is the original `sin` and `cos`
    functions from the `math` package take `radians`
    as input, but we are more familiar with `degrees`. So, we
    will use a lambda expression to define a wrapper function for
    `sine` and `cosine`, then use it. This
    `lambda` function will automatically convert our degree
    input to radians and then apply `sin` or `cos`
    on it and return the value:
    
    ```
    def my_sine():
        return lambda x: math.sin(math.radians(x))
    def my_cosine():
        return lambda x: math.cos(math.radians(x)) 
    ```

3.  Define `sine` and `cosine` for our purpose:

    
    ```
    sine = my_sine()
    cosine = my_cosine()
    math.pow(sine(30), 2) + math.pow(cosine(30), 2) 
    ```

    The output is as follows:

    
    ```
    1.0
    ```

Notice that we have assigned the return value from both
`my_sine` and `my_cosine` to two variables, and then
used them directly as the functions. It is a much cleaner approach than
using them explicitly. Notice that we did not explicitly write a
`return` statement inside the lambda function; it is assumed.


Exercise 2.05: Lambda Expression for Sorting
--------------------------------------------

In this exercise, we will be exploring the `sort` function to
take advantage of the lambda function. What makes this exercise useful
is that you will be learning how to create any unique algorithm that
could be used for sorting a dataset. The syntax for a lambda function is
as follows:

```
lambda x  :   <do something with x>
```


A lambda expression can take one or more inputs. A lambda expression can
also be used to reverse sort by using the parameter of
`reverse` as `True`. We\'ll use the reverse
functionality as well in this exercise. Let\'s go through the following
steps:

1.  Let\'s store the list of tuples we want to sort in a variable called
    `capitals`:
    
    ```
    capitals = [("USA", "Washington"), ("India", "Delhi"), ("France", "Paris"), ("UK", "London")]
    ```

2.  Print the output of this list:

    
    ```
    capitals 
    ```

    The output will be as follows:

    
    ```
    [('USA', 'Washington'),
     ('India', 'Delhi'),
     ('France', 'Paris'),
     ('UK', 'London')]
    ```

3.  Sort this list by the name of the capitals of each country, using a
    simple lambda expression. The following code uses a lambda function
    as the `sort` function. It will sort based on the first
    element in each tuple:

    
    ```
    capitals.sort(key=lambda item: item[1])
    capitals 
    ```

    The output will be as follows:

    
    ```
    [('India', 'Delhi'),
     ('UK', 'London'),
     ('France', 'Paris'),
     ('USA', 'Washington')]
    ```

As we can see, lambda expressions are powerful if we master them and use
them in our data wrangling jobs. They are also
side-effect-free --- meaning that they do not change the values of the
variables that are passed to them in place.


Exercise 2.06: Multi-Element Membership Checking
------------------------------------------------

In this exercise, we will create a list of words using `for`
loop to validate that all the elements in the first list are present in
the second list. Let\'s see how:

1.  Create a `list_of_words` list with words scraped from a
    text corpus:

    
    ```
    list_of_words = ["Hello", "there.", "How", "are", "you", "doing?"] 
    list_of_words
    ```

    The output is as follows:

    
    ```
    ['Hello', 'there.', 'How', 'are', 'you', 'doing?']
    ```

2.  Define a `check_for` list, which will contain two similar
    elements of `list_of_words`:

    
    ```
    check_for = ["How", "are"] 
    check_for
    ```

    The output is as follows:

    
    ```
    ['How', 'are']
    ```

    There is an elaborate solution, which involves a `for`
    loop and a few `if`/`else` conditions (and you
    should try to write it), but there is also an elegant Pythonic
    solution to this problem, which takes one line and uses the
    `all` function. The `all` function returns
    `True` if all elements of the iterable are
    `True`.

3.  Use the `in` keyword to check membership of the elements
    in the `check_for` list in `list_of_words`:

    
    ```
    all(w in list_of_words for w in check_for) 
    ```

    The output is as follows:

    
    ```
    True
    ```


Let\'s look at the next data structure: a **queue**.


Queue
-----


**Exercise 2.07: Implementing a Queue in Python**

In this exercise, we\'ll implement a queue in Python. We\'ll use the
`append` function to add elements to the queue and use the
`pop` function to take elements out of the queue. We\'ll also
use the `deque` data structure and compare it with the queue
in order to understand the wall time required to complete the execution
of an operation. To do so, perform the following steps:

1.  Create a Python queue with the plain list methods. To record the
    time the `append` operation in the queue data structure
    takes, we use the `%%time` command:

    
    ```
    %%time
    queue = []
    for i in range(0, 100000):
        queue.append(i)
    print("Queue created")
    queue 
    ```

    **Note:**

    `%%time` is a regular built-in magic command in Python to
    capture the time required for an operation to execute.

    The output (partially shown) is as follows:

    
    ![](./images/B15780_02_06.jpg)
    

2.  If we were to use the `pop` function to empty the queue
    and check the items in it:

    
    ```
    for i in range(0, 100000):
        queue.pop(0)
    print("Queue emptied") 
    ```

    The output would be as follows:

    
    ```
    Queue emptied
    ```

    However, this time, we\'ll use the `%%time` magic command
    while executing the preceding code to see that it takes a while to
    finish:

    
    ```
    %%time
    for i in range(0, 100000):
        queue.pop(0)
    print("Queue emptied") 
    queue
    ```

    The output is as follows:

    
    ![](./images/B15780_02_07.jpg)
    



    **Note:**

    If you are working on Google Colab or other virtual environments,
    you will see an additional line indicating the CPU time present in
    the output. This is the CPU time of the server on which Google Colab
    (or any other virtual environment) is running on. However, if you
    are working on your local system, this information will not be a
    part of the output.

    In a modern MacBook, with a quad-core processor and `8` GB
    of RAM, it took around `1.20` seconds to finish. With
    Windows 10, it took around 2.24 seconds to finish. It takes this
    amount of time because of the `pop(0)` operation, which
    means every time we pop a value from the left of the list (the
    current `0` index), Python has to rearrange all the other
    elements of the list by shifting them one space left. Indeed, it is
    not a very optimized implementation.

3.  Implement the same queue using the `deque` data structure
    from Python\'s `collections` package and perform the
    `append` and `pop` functions on this data
    structure:

    
    ```
    %%time
    from collections import deque
    queue2 = deque()
    for i in range(0, 100000):
        queue2.append(i)
    print("Queue created")
    for i in range(0, 100000):
        queue2.popleft()
    print("Queue emptied") 
    ```

    The output is as follows:

    
    ![](./images/B15780_02_08.jpg)
    



With the specialized and optimized queue implementation from Python\'s
standard library, the time that this should take for both the operations
is only approximately `27.9` milliseconds. This is a huge
improvement on the previous one.

**Note:**

To access the source code for this specific section, please refer to
<https://github.com/fenago/data-wrangling-python>.



We will end the discussion on data structures here. What we discussed
here is just the tip of the iceberg. Data structures are a fascinating
subject. There are many other data structures that we did not touch on
and that, when used efficiently, can offer enormous added value. We
strongly encourage you to explore data structures more. Try to learn
about linked lists, trees, graphs, and all the different variations of
them as much as you can; you will find there are many similarities
between them and you will benefit greatly from studying them. Not only
do they offer the joy of learning, but they are also the secret
mega-weapons in the arsenal of a data practitioner that you can bring
out every time you are challenged with a difficult data wrangling job.



Activity 2.01: Permutation, Iterator, Lambda, and List
------------------------------------------------------

In this activity, we will be using `permutations` to generate
all possible three-digit numbers that can be generated using
`0`, `1`, and `2`. A permutation is a
mathematical way to represent all possible outcomes. Then, we\'ll loop
over this iterator and also use `isinstance` and
`assert` to make sure that the return types are tuples. Use a
single line of code involving `dropwhile` and
`lambda` expressions to convert all the tuples to lists while
dropping any leading zeros (for example, `(0, 1, 2)` becomes
`[1, 2]`). Finally, we will write a function that takes a list
like before and returns the actual number contained in it.

These steps will guide you as to how to solve this activity:

1.  Look up the definition of `permutations` and
    `dropwhile` from `itertools`.

2.  Write an expression to generate all the possible three-digit
    numbers, using `0`, `1`, and `2`.

3.  Loop over the iterator expression you generated before. Print each
    element returned by the iterator. Use `assert` and
    `isinstance` to make sure that the elements are of the
    tuple type.

4.  Write the loop again, using `dropwhile`, with a lambda
    expression to drop any leading zeros from the tuples. As an example,
    `(0, 1, 2)` will become `[0, 2]`. Also, cast the
    output of `dropwhile` to a list.

5.  Check the actual type that `dropwhile` returns.

6.  Combine the preceding code into one block; this time, write a
    separate function where you will pass the list generated from
    `dropwhile` and the function will return the whole number
    contained in the list. As an example, if you pass `[1, 2]`
    to the function, it will return `12`. Make sure that the
    return type is indeed a number and not a string. Although this task
    can be achieved using other tricks, treat the incoming list as a
    stack in the function and generate the number by reading the
    individual digits from the stack.

    The final output should look like this:

    
    ```
    12.0
    21.0
    102.0
    120.0
    201.0
    210.0
    ```


With this activity, we have finished this topic and will move on to the
next topic, which involves basic file-level operations.



Basic File Operations in Python
===============================

**Exercise 2.08: File Operations**

In this exercise, we will learn about the OS module of Python, and we
will also look at two very useful ways to write and read environment
variables. The power of writing and reading environment variables is
often very important when designing and developing data-wrangling
pipelines.

The purpose of the OS module is to give you ways to interact with
OS-dependent functionalities. In general, it is pretty low-level and
most of the functions from there are not useful on a day-to-day basis;
however, some are worth learning. `os.environ` is the
collection Python maintains with all the present environment variables
in your OS. It gives you the power to create new ones. The
`os.getenv` function gives you the ability to read an
environment variable:

1.  Import the `os` module.
    
    ```
    import os 
    ```

2.  Set a few environment variables:

    
    ```
    os.environ['MY_KEY'] = "MY_VAL"
    os.getenv('MY_KEY') 
    ```

    The output is as follows:

    
    ```
    'MY_VAL'
    ```

3.  Print the environment variable when it is not set:

    
    ```
    print(os.getenv('MY_KEY_NOT_SET')) 
    ```

    The output is as follows:

    
    ```
    None
    ```

4.  Print the `os` environment:

    
    ```
    print(os.environ) 
    ```

After executing the preceding code, you will be able to see that you
have successfully printed the value of `MY_KEY`, and when you
tried to print `MY_KEY_NOT_SET`, it printed `None`.
Therefore, utilizing the OS module, you will be able to set the value of
environment variables in your system.



File Handling
-------------

You can open a file for reading with the command that follows. The path
(highlighted) would need to be changed based on the location of the file
on your system.

```
fd = open("../datasets/data_temporary_files.txt")
```


We will discuss some more functions in the following section.

**Note:**

The file can be found here <https://github.com/fenago/data-wrangling-python>.

This is opened in `rt` mode (opened for the
`reading+text` mode). You can open the same file in
`binary` mode if you want. To open the file in binary mode,
use the `rb (read, byte)` mode:

```
fd = open('AA.txt',"rb")
fd
```


The output is as follows:

```
<_io.BufferedReader name='../datasets/AA.txt'>
```


**Note:**

The file can be found here: <https://github.com/fenago/data-wrangling-python>.

This is how we open a file for writing:

```
fd = open("../datasets/data_temporary_files.txt ", "w")
fd
```


The output is as follows:

```
<_io.TextIOWrapper name='../datasets/data_temporary_files.txt ' mode='w' encoding='cp1252'>
```


Let\'s practice this concept in the following exercise.



Exercise 2.09: Opening and Closing a File
-----------------------------------------

In this exercise, we will learn how to close a file after opening it.


We must close a file once we have opened it. A lot of system-level bugs
can occur due to a dangling file handler, which means the file is still
being modified, even though the application is done using it. Once we
close a file, no further operations can be performed on that file using
that specific file handler.

1.  Open a file in binary mode:

    
    ```
    fd = open("../datasets/AA.txt", "rb")
    ```

    **Note:**

    Change the highlighted path based on the location of the file on
    your system. The video of this exercise shows how to use the same
    function on a different file. There, you\'ll also get a glimpse of
    the function used to write to files, which is something you\'ll
    learn about later in the lab.

2.  Close a file using `close()`:
    
    ```
    fd.close()
    ```

Python also gives us a `closed` flag with the file handler. If
we print it before closing, then we will see `False`, whereas
if we print it after closing, then we will see `True`. If our
logic checks whether a file is properly closed or not, then this is the
flag we want to use.


Opening a File Using the with Statement
---------------------------------------

Open a file using the `with` statement:

```
with open("../datasets/AA.txt") as fd:
    print(fd.closed)
print(fd.closed) 
```


The output is as follows:

```
False
True
```


If we execute the preceding code, we will see that the first
`print` will end up printing `False`, whereas the
second one will print `True`. This means that as soon as the
control goes out of the `with` block, the file descriptor is
automatically closed.

**Note:**

This is by far the cleanest and most Pythonic way to open a file and
obtain a file descriptor for it. We encourage you to use this pattern
whenever you need to open a file by yourself.



Exercise 2.10: Reading a File Line by Line
------------------------------------------

In this exercise, we\'ll read a file line by line. Let\'s go through the
following steps to do so:

1.  Open a file and then read the file line by line and print it as we
    read it:

    
    ```
    with open("../datasets/Alice`s Adventures in Wonderland, "\
              "by Lewis Carroll", encoding="utf8") as fd: 
        for line in fd: 
            print(line)
    ```

    **Note:**

    Do not forget to change the path (highlighted) of the file based on
    its location on your system.

    The output (partially shown) is as follows:

    ![](./images/B15780_02_10.jpg)
    

2.  Duplicate the same `for` loop, just after the first one:

    
    ```
    with open("../datasets/Alice`s Adventures in Wonderland, "\
              "by Lewis Carroll", encoding="utf8") as fd: 
        for line in fd:
            print(line)
        print("Ended first loop")
        for line in fd:
            print(line)
    ```

    **Note:**

    Do not forget to change the path (highlighted) of the file based on
    its location on your system.

    The output (partially shown) is as follows:

    
    ![](./images/B15780_02_11.jpg)
    


Let\'s look at the last exercise of this lab.



Exercise 2.11: Writing to a File
--------------------------------

In this exercise, we\'ll look into file operations by showing you how to
read from a dictionary and write to a file. We will write a few lines to
a file and read the file:

**Note:**

`data_temporary_files.txt` can be found at
<https://github.com/fenago/data-wrangling-python>.

Let\'s go through the following steps:

1.  Use the `write` function from the file descriptor object:

    
    ```
    data_dict = {"India": "Delhi", "France": "Paris",\
                 "UK": "London", "USA": "Washington"}
    with open("../datasets/data_temporary_files.txt", "w") as fd:
        for country, capital in data_dict.items():
            fd.write("The capital of {} is {}\n"\
                     .format(country, capital))
    ```

    **Note:**

    Throughout this exercise, don\'t forget to change the path
    (highlighted) based on where you have stored the text file.

2.  Read the file using the following command:

    
    ```
    with open("../datasets/data_temporary_files.txt", "r") as fd:
        for line in fd:
            print(line)
    ```

    The output is as follows:

    
    ```
    The capital of India is Delhi
    The capital of France is Paris
    The capital of UK is London
    The capital of USA is Washington
    ```

3.  Use the `print` function to write to a file using the
    following command:
    
    ```
    data_dict_2 = {"China": "Beijing", "Japan": "Tokyo"}
    with open("../datasets/data_temporary_files.txt", "a") as fd:
        for country, capital in data_dict_2.items():
            print("The capital of {} is {}"\
                  .format(country, capital), file=fd)
    ```

4.  Read the file using the following command:

    
    ```
    with open("../datasets/data_temporary_files.txt", "r") as fd:
        for line in fd:
            print(line)
    ```

    The output is as follows:

    
    ```
    The capital of India is Delhi
    The capital of France is Paris
    The capital of UK is London
    The capital of USA is Washington
    The capital of China is Beijing
    The capital of Japan is Tokyo
    ```

    **Note:**

    In the second case, we did not add an extra newline character,
    `\n`, at the end of the string to be written. The
    `print` function does that automatically for us.


With this, we will end this topic. Just like the previous topics, we
have designed an activity for you to practice your newly acquired
skills.



Activity 2.02: Designing Your Own CSV Parser
--------------------------------------------

A CSV file is something you will encounter a lot in your life as a data
practitioner. A CSV file is a comma-separated file where data from a
tabular format is generally stored and separated using commas, although
other characters can also be used, such as `tab` or
`*`. Here\'s an example CSV file:



![](./images/B15780_02_12.jpg)




In this activity, we will be tasked with building our own CSV reader and
parser. Although it is a big task if we try to cover all use cases and
edge cases, along with escape characters, for the sake of this short
activity, we will keep our requirements small. We will assume that there
is no escape character---meaning that if you use a comma at any place in
your row, you are starting a new column. We will also assume that the
only function we are interested in is to be able to read a CSV file line
by line, where each read will generate a new dictionary with the column
names as keys and row names as values.

Here is an example:



![](./images/B15780_02_13.jpg)




We can convert the data in the preceding table into a Python dictionary,
which would look as follows:
`{"Name": "Bob", "Age": "24", "Location": "California"}`:

1.  Import `zip_longest` from `itertools`. Create a
    function to zip `header`, `line`, and
    `fillvalue=None`.

    Open the accompanying `sales_record.csv` file from the
    GitHub link (<https://github.com/fenago/data-wrangling-python>) by using `r`
    mode inside a `with` block and check that it is opened.

2.  Read the first line and use string methods to generate a list of all
    the column names.

3.  Start reading the file. Read it line by line.

4.  Read each line and pass that line to a function, along with the list
    of the headers. The work of the function is to construct a
    `dictionary` out of these two and fill up the
    `key:values` variables. Keep in mind that a missing value
    should result in `None`.

    The partial output of this should look like this:



![](./images/B15780_02_14.jpg)




Summary
=======


This lab covered manipulation techniques of advanced data structures
such as stacks and queues. We then focused on different methods of
functional programming, including iterators, and combined lists and
functions together. Later, we looked at OS-level functions and the
management of environment variables. We examined how, using Python, we
can open, close, and even write to local files in a variety of ways.
Knowing how to deal with files in a clean way is a critical skill in a
data wrangler\'s repertoire. Toward the end, we tested our newly learned
skills by creating our own CSV parser.

In the next lab, we will be dealing with the three most important
libraries, namely `NumPy`, `pandas`, and
`matplotlib`.
