# Advancing with Python

## Importing libraries and drawing random numbers

- Sometimes it will be helpful to use functionality that's not part of the core python functionality.
- Thankfully, python has a built-in way to import new functions that other people have written to extend the core functions
- Once you know the name of a library, you can use the `import` command to load it (if it's already been installed).
- One library that we're going to use today is called `random`.
- Once it's loaded, you'll need to precede any of its functions with `random.` in order to use them.
- Try this:
    - `import random`
    - `random.random()` - Do this a few times
    - `random.uniform(0,1)` - Do this a few times
    - `random.uniform(0,5)` - Do this a few times
    - `random.choice([5,6,7,8])` - Do this a few times
    - `firstList`
    - `random.shuffle(firstList)`
    - `firstList`
    - `random.shuffle(firstList)`
    - `firstList`
    - `random.shuffle(firstList)`
    - `firstList`

## Reading from files

- To read or write from a file, you'll first need to define the file name
    - e.g., `inFileName = "FileToRead.txt"`
- However, this is just a string variable with the file name. We need to create an object that can actually read the contents of a file.
- Python has a built-in function to create a file object - `open(<FILENAME>,<MODE>)`
- The `<FILENAME>` argument is just a string with the file's name (or path to the file)
- The `<MODE>` argument tells Python whether we are reading from a file (`r`), writing to a file (`w`), or appending to a file (`a`).
- To open up a new File object to read file contents, use syntax like this:
    - `inFile = open(inFileName,'r')`
- There are several useful methods associated with file objects, but one of the most commonly used is `readline()`. This method will read lines one-by-one from the file. Note that the end of line character (\n) is retained when the line is read in.
    - `firstLine = inFile.readline()`
- Files opened for reading can be used in a `for` loop, as follows, to go through all the lines in the file:

```
        for line in file:
            print("Length of line is: %d" % (len(line)))
```

- Note that `line` is just a variable name we've chosen to hold each line as we iterate through the file. You can use any variable name you choose, as with any other `for` loop.


## Writing to Files

- Writing to a file is very similar to reading from a file. First, you define an output file name
    - `outFileName = "FileToWrite.txt"`
- To create a file object to use for writing, we'll again use the `open()` function, but we'll specify `'w'` for the `<MODE>`.
    - `outFile = open(outFileName,'w')`
- To write to the file line-by-line, we can use the `.write()` method.
    - `outFile.write("This is a new sentence.\n")`
    - Note that the `write()` method does NOT, by default, add a new line character to strings. If we want to end a line, we have to explicitly include `\n`.


## Command-line Arguments
  
- As with bash scripts, Python scripts can also take advantage of command-line arguments.
- To easily deal with command-line arguments, we're going to take advantage of some functions in the `sys` library. So we'll need to start by importing that library:
    - `import sys`
- Any command-line arguments we pass to a script can then be accessed using the `sys.argv` variable.
    - `print(sys.argv[2])`
    - Which argument is printed when you run the line above? Does that make sense with the 0-based indexing in Python?
- We can also loop through all command-line arguments:
        for arg in sys.argv:
            print(arg)
- These abilities are very useful in a variety of contexts, but particularly when a set of filenames are provided as command-line arguments and you want to iteratively process each file.

## Python Custom Functions

### Introduction

The core Python library and optional modules contain a huge number of useful functions. However, as you write more specialized code, you will inevitably need/want to use a function that doesn't yet exist. Thankfully, Python and other programming languages make it easy to write your own custom functions. Any time you find yourself writing the same block of code repeatedly, you should instead put this code in a new function that can be called whenever needed. Writing your own functions makes your code shorter, more readable, more reliable, and easier to debug. The general syntax for defining a custom function looks like this

```
def myNewFunction():
    """ A text description of my function goes here."""
    
    print("Executing a custom function!")
```

The `def` keyword tells Python that we're defining a new function. That is followed by the name of our function (in this case, `myNewFunction`). The function name is then _always_ followed by parentheses - `()`. For simple functions, nothing needs to go inside the parentheses. These are then followed by a colon - `:`.

The next line should be indented and a text string should be provided inside sets of three double quotation marks - `"""`. This text is known as the _docstring_ and provides users, other programmers, or, more likely, you at some later time, with useful information about the function. Executing `help(myNewFunction)` in the Python interpreter will cause the _docstring_ to be printed for the user.

The rest of code relevant to your function should appear on subsequent indented lines after the _docstring_. Simple functions may only have 1 or 2 lines. More complicated functions may have 10s to 100s of lines. However, if the function gets much longer than that, it's probably an indication that you need to break the code up into more functions of a manageable size.

Custom functions are executed just like any core Python function. Simply type the function's name, followed by parentheses.

`myNewFunction()`

### Function Arguments

To make functions more flexible, they can be written to accept arguments. To do this, simply include a new variable name inside the parentheses when defining the function. Note that this variable name _only has meaning within the function's code_. More formally, we say that the scope of the variable is limited to the function.

```
def myFuncWithArg(userProvidedWord):
    """This example function shows how to accept and use arguments."""
    
    print("I am printing the word: %s" % userProvidedWord)

myFuncWithArg("test")
myFuncWithArg("tigers")
```

Note in the example above how we used the new variable name in the function's code, while the value of this variable changed depending on what string the user provided each time they executed the function.

Functions can take more than one argument, as long as they are specified in the function definition.

```
def complexMathThing(numOne,numTwo,numThree):
    """A complicated mathematical operation with three numbers."""

    print( pow(numOne, numTwo) - numThree )
    
complexMathThing(4,5,2)
```

### Return Statements

In the example above, the function accomplished a task (printing something to the screen), but nothing produced by this function could be saved in a variable to be used later. If we want a function to produce a value (integer, float, string, ...) that can be saved in a variable, we need to include a `return` statement. This statement defines what value a function will produce.

Here, we redefine the function above to `return` the same value that it printed before.

```
def complexMathThing(numOne,numTwo,numThree):
    """A complicated mathematical operation with three numbers."""

    return pow(numOne, numTwo) - numThree

myVar = complexMathThing(4,5,2)
```

By adding a `return` statement, we can save a value produced by the function `complexMathThing()` in a variable (in this case, `myVar`)for future use.

```
print(myVar)
myVar * 3
```

### Optional Arguments

One way that we can make code more efficient, especially for functions that are used often and have lots of arguments, is to provide default values for some of the arguments. When we do this, a user only *has to* provide values for those arguments that don't have defaults - but they can also change the defaults for the others if they want to.

We can specify default values for arguments when we define the function. Below, we're redefining the `complexMathThing()` function from above, but providing default values for arguments `numTwo` and `numThree`.

```
def complexMathThing(numOne,numTwo=5,numThree=2):
    """A complicated mathematical operation with three numbers."""

    return pow(numOne, numTwo) - numThree
```

Now we can execute `complexMathThing()` by only providing a value for `numOne`, as long as we're ok with the default values for `numTwo` and `numThree`.

`complexMathThing(4)`

However, we can also run the function by providing new values for `numTwo` and/or `numThree`.

```
# Providing values for all three arguments
complexMathThing(4,6,1)

# Providing values for numOne and numTwo, so numThree uses its default of 2.
complexMathThing(4,6)
```

If we pass the function values for arguments in the same order as they're listed in the function definition, we don't have to write their names. But let's say that we wanted to provide values for `numOne` and `numThree`, but not `numTwo`. Then we'd have to provide the argument names, so the function "knows" to skip `numTwo`.

`complexMathThing(numOne=4,numThree=4)`

Note that we *always* have to provide a value for `numOne`, because it doesn't have a default. For example, what happens when you try this function call

`complexMathThing(numTwo=5,numThree=1)`
