---
layout: notes
title: "📓1.1: Python Basics" 
parent: "1️⃣ Python Bootcamp"
nav_order: 1
---

## Table of Contents
{: .no_toc .text-delta }

{: .fs-2 }
- TOC
{:toc}

---

## Introduction to Python
### What is Python?

Python is a programming language created by Guido Van Rossum in the late 1980s. Python the language is [open source](https://github.com/python/cpython).

Python has a wide variety of **real-world applications** such as:

- AI/ML
    - SciPi
    - NumPy
    - Pandas
    - PyTorch
- Hardware & Micro-controllers
    - Raspberry Pi
    - MicroPython
    - CircuitPython
- Web Development
    - Django
    - Flask
- Scripting
    - DevOps
    Configuration scripts

Python has an incredibly rich fully featured [standard library](https://docs.python.org/3/library/), as well as the [PyPI Package Index](https://pypi.org/) for 3rd party packages, which as of February 2019 contains 167,107 packages.

Python is considered to be a "batteries included" language, because the standard library contains a majority of the libraries and packages you'll need in a standard application.

#### PEP8 STYLE GUIDELINES
{:.no_toc}

[PEP8](https://pep8.org/) is a Python  **coding standard**, that sets guidelines for how our Python code should look like.

---
## Basic Data Types

First, make sure you have a blank Python program to take notes and code along as we dive into the lesson.

<div class="setup" markdown="block">

1. GITHUB NOTES FILE

</div>

### Variables

**Variables** in Python allow us to store information and give it a label that we can use to retrieve that information later. We can use variables to store numbers, strings (a sequence of characters), or even more complex data types like lists and dictionaries.

We assign _values_ to _variables_ by putting the _value_ to the right of an equal sign.

Because Python is a *dynamic* language, we **don't need to declare the type** of the variables before we store data in them.

That means that this is valid Python code:

```python
>>> x = 42
```

Unlike typed languages, the type of what's contained in Python variables can change at any time.

For example, the below is perfectly valid Python code:

```python
>>> x = 42
>>> x = "hello"
```

Here, the value of the variable `x` changed from a number to a string.

#### Naming Variables
{: .no_toc }

When creating variables in Python, there are a few best practices you should follow. The [PEP8 guidelines](https://www.python.org/dev/peps/pep-0008/#naming-conventions) specify the following convention for naming variables: 

{: .highlight }
Python variable names are entirely **lowercase**, with multiple words separated by **underscores** `_`. 

> Unlike other languages that name multi-word variables with **camelCase** (like `Java`).

Because Python is a** dynamic language** and you don't have type hints to explain what's stored inside a variable while reading code, you should do your best naming your variables to describe what is stored inside of them.

It's ok to be _verbose_. For example, `n` is a poor variable name, while `numbers` is a better one. If you're storing a collection of items, name your variable as a plural.

<div class="warn" markdown="block">

* You can't start your variable name with a numerical digit, although your variable name can end in a digit. 
* Your variable name can't contain special characters, such as `!`,  `@`,  `#`, `$`,  `%` and more.
* There are some things that you can't name your variables, such as `and`, `if`, `True`, or `False`. That's because Python uses these names for program control structure.
* 💣 Python will let you override built-in methods and types without a warning so don't name your Python variables things like `list`, `str`, or `int`.
    * If you notice your program behaving oddly and you can't find the source of the bug, double check the list of [built-in functions](https://docs.python.org/3/library/functions.html) and [built-in types](https://docs.python.org/3/library/stdtypes.html) to make sure that your variable names don't conflict.

</div>

### The `type()` Function

Python has a very easy way of determining the type of something, with the `type()` function.

```python
>>> num = 42
>>> type(num)
```

The output in this case would be: `<class 'int'>`.

#### No-Value, `None`, or Null Value
{: .no_toc }

There's a special type in Python that signifies no value at all. In other languages, it might be called Null. In Python, it's called `None`.

If you try to examine a variable on the REPL that's been set to `None`, you won't see any output. We'll talk more about the `None` type later in the class.

```python
>>> x = None
>>> x
```

### Numbers
There are three different types of numbers in Python: `int` for Integer, Float, and Complex.

```python
# These are all integers
x = 4
y = -193394
z = 0
```

```python
# These are all floats
x = 5.0
y = -3983.2
z = 0.
```

```python
# This is a complex number
x = 42j
```

In Python, Integers and other simple data types are just **objects** under the hood. That means that you can create new ones by calling methods. You can provide either a number, or a string. This will come in handy later on in the course.

```python
x = int(4)
y = int('4')
z = float(5.0)
```

Python also provides a `decimal` library, which has certain benefits over the `float` datatype. For more information, refer to the [Python documentation](https://docs.python.org/3/library/decimal.html).

### Mathematical Operations
{: .no_toc }

Numbers can be added together. If you add a `float` and an `int`, the resulting type will be a `float`.

If you divide two `int`s (integers), the result will be of type `float`.

### Booleans
{: .no_toc }

In Python, Booleans are of type `bool`. Surprisingly, the boolean types `True` and `False` are also numbers under the hood.

* `True` is `1` under the hood.
* `False` is `0` under the hood.

That means you can do silly things, like add two Boolean numbers together, but I'll cover why this is a useful Python feature later in the course.

### Strings

Strings in Python can be enclosed either with single quotes like `'hello'` or double quotes, like `"hello"`.

Strings can also be **concatenated** (added together) using the `+` operator to combine an arbitrary number of Strings. For example:

<pre><code class="plaintext">1334</code></pre>

```python
salutation = "Hello "
name = "Nina"
greeting = salutation + name
# The value of greeting will be "Hello Nina"
```

To use the same type of quote within a string, that quote needs to be **escaped** with a `\` - backwards slash.

```python
greeting = 'Hello, it\'s Nina'
```

Alternately, mixed quotes can be present in a Python string without escaping.

```python
# Notice that the single quote ' is surrounded by
# double quotes, ""
greeting = "Hello, it's Nina"
```

Long multi-line strings can be represented in between `"""` (triple quotes), but the whitespace will be part of the string.

```python
long_greeting = """
                Greetings and salutations, dear Nina.
                I'm superfluous with my words,
                and require more space to say Hello!"
                """
```

### The `print()` Function

Strings can be printed out using the `print()` function in Python.

To use the `print()` function, call it with a regular or formatted string.

```python
>>> print("Hello")
Hello
>>> name = "Nina"
>>> print(name)
Nina
```

#### String Formatting
{: .no_toc }

There are several types of string formatting in Python.

If you're using Python 3.7 and above you can use my favorite type of string formatting, and the one I'll be using for the course called **f-strings**.

```python
>>> name = "Nina"
>>> greeting = f"Hello, {name}"

>>> print(greeting)
Hello, Nina
```

**f-strings** allow you to simply and easily reference variables in your code, and as a bonus, they're *much* faster.

### Common Mistakes

There are a few common errors that you'll encounter when working with Strings and numbers. In Python programs, errors are called `Exceptions`. By going over what they are, you'll be able to recognize them immediately.

#### Scenario 1: Mismatched string quotes
{: .no_toc }

{:.highlight}
Mismatched string quotes will result in a `SyntaxError`

When we try to start a String with one type of quote, and end with another, we'll see a syntax error.

For example, starting the string Hello with a double quote, and ending in a single quote, like this:

```python
>>> name = 'Hello"
  File "<stdin>", line 1
    name = "Hello'
                 ^
SyntaxError: EOL while scanning string literal
```

**Solution:** use matching quote types for defining your strings. Either single quotes `'Hello'` or double quotes `"Hello"`.

#### Scenario 2: Trying to print a String and a number with concatenation using the "+" symbol.
{: .no_toc }

{:.highlight}
Trying to add or concatenate a String and a number will result in a `TypeError`


If you add try to add (or concatenate) a String and a number, you'll get an error saying that adding the two types together isn't possible.

```python
>>> print(3 + " Three")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

**Solutions:**

There are two possible solutions here, for two different scenarios.

1. In the first scenario, you'd like to add a number to a string via **concatenation**. In order to do that, you must first convert the number to a string via the `str()` method.

```python
>>> my_num = 3
>>> print(str(my_num) + " Three")
3 Three
```

2. In the second scenario, you'd like to a convert a number that's contained in a string (ex: `"3"`) into an Integer, so you can use it like any other number. In this case, you'd like to convert it to an Integer, with the `int()` method.

```python
>>> str_num = "3"
>>> print(int(str_num) + 5)
8
```

### ⭐️ Practice

#### Types
{: .no_toc }

<html>
<div class="task" markdown="block">

List the type of the following variables using the `type()` function.

```python
>>> x = 42
>>> y = 3 / 4
>>> z = int('7')
>>> a = float(5)
>>> name = "Nina"
```

</div>
</html>

#### Numbers
{: .no_toc }

<div class="task" markdown="block">

Calculate the amount of rent you pay daily, by taking your monthly rent and diving it by 30.

```python
>>> rent = 480
>>> per_day = rent / 30
>>> print(per_day)
16.0
```

</div>

#### Strings
{: .no_toc }

<div class=“task” markdown="block">

Try printing some things:

```python
>>> print("Hello world")
Hello world
>>> name = "Nina"
>>> print("My name is", name)
My name is Nina
```
</div>

The current recommended way to format string is with **f-Strings**. f-Strings are much more readable and easier to maintain than the previous methods. 

{:.highlight}
With f-Strings, your string is prepended with the letter `f` and your **variables** or **expressions to interpret** are placed in `{brackets}`.

```python
>>> name = "Nina"
>>> print(f"Hello, my name is {name} and I pay ${rent / 30} in rent per day")
Hello, my name is Nina and I pay $16.0 in rent per day
```

#### Helper Functions
{: .no_toc }

Python has a few built-in functions to help you if you get stuck. `type()` tells you what an object's type is, for example a string (`str`) or integer (`int`). `dir()` returns a list of valid attributes for an object, so you can quickly see what variables an object has or what functions you can call on it. `help()` brings up helpful documentation on any object. You can also type `help()` on its own to bring an interactive help console.

<div class=“task” markdown="block">
 Try it out: 
    
```python
>>> x = 42
>>> y = 3 / 4
>>> name = "Nina"
>>> type(x)
>>> type(y)
>>> type(name)
```
</div>

---
## Functions

The purpose of functions in Python are to **create reusable code**. If we find ourselves copying and pasting the same code multiple times, that's a good sign that a function might help!

### Defining Functions

<div class=“imp” markdown="block">

This is the recipe for defining a Python function:

1. `def`: the `def` keyword, telling Python we're about to start a function definition
1. a name for the function
1. `(`: opening parenthesis
1. (optional) the **names** of one or more arguments, separated with `,`
1. (optional) the **names** and **values** of one or more default arguments, separated with (`,`) *note: we'll see these in the next section*
1. `)` closing parenthesis
1. `:` a colon

</div>

{:.highlight}
A function in Python is defined with the `def` keyword, followed by the function names, zero or more argument names contained in parenthesis `()`, and a colon `:` to indicate the start of the function. The contents of the function then follow. Then, an *optional* `return` statement can follow, if the function plans on passing data back to the caller.

```python
# A Basic Function that accepts no arguments and returns nothing.
def hello_world():
    print("Hello, World!")


# A Function that accepts two arguments, and returns the value of
# those numbers added together.
def add_numbers(x, y):
    return x + y
```

{:.highlight}
If you **forget** the recipe while trying to create a function, Python will help you remember with a `SyntaxError`.

For example, trying to create a function without the colon `:`:

```python
>>> def hello_world()
  File "<stdin>", line 1
    def hello_world()
                    ^
SyntaxError: invalid syntax
```

And trying to create a function without the parenthesis `()`:

```python
>>> def hello_world:
  File "<stdin>", line 1
    def hello_world:
                   ^
SyntaxError: invalid syntax
```

### Function Contents
{: .no_toc }

<div class=“imp” markdown="block">

The recipe for **function contents**:

1. a new line
1. indentation (press tab on your keyboard)
1. one or more lines
1. (optional) a `return` statement

</div>

#### `return` statement
{: .no_toc }

A `return` statement is a way to "short-circuit" the function.

Using a `return` statement, you can optionally pass back data to the caller of your function.

#### with no `return` statement
{: .no_toc }

If a function doesn't have a return statement, it implicitly returns `None`.

```python
>>> def foo():
...     x = 5
...
>>> val = foo()
>>> type(val)
```

#### with a `return` statement, but no value
{: .no_toc }

If a function has a return statement, but no value, it also returns `None`. This is typically used to control the flow of a program.

```python
>>> def foo():
...     x = 5
...     return
...
>>> val = foo()
>>> type(val)
```

#### with a `return` statement and a value
{: .no_toc }

To return a value from a function, just type it after the `return` statement. You can return anything from a Python function, including other functions! For today, we'll focus on simple and complex data types.

```python
>>> def foo():
...     x = 5
...     return x
...
>>> val = foo()
>>> val
5
```

As we explore simple functions, our `return` statements will usually be at the end of the function, but that's not the only way they can be used. A function can have multiple `return` statements, and those `return` statements can be used to help control the flow of the program.


### Indentation

One of the most important aspects of functions is **indentation**. Remember, Python doesn't use curly braces to figure out what's inside a function like other languages you've seen like JavaScript or Java.

Python knows what code is related to a function by how it's indented. Anything that's indented one level deep under the function declaration is part of the function, no matter how many spaces there are between lines.

To add a level of indentation, just press the **Tab** key on your keyboard after entering a new line.

If you're using the REPL, once you're done entering your function, you'll need to press enter an additional time, to mark the end of the function. You know you're done defining your function when you see the 3 input arrows `>>>` again.

Let's try it together. Type the following code in your REPL. Note that the 3 dots '...' indicate that those lines are *indented* in the REPL. If you type your code in a Python file, you won't see the `...` dots.

<div class=“task” markdown="block">

```python
>>> def add_numbers(x, y):
...     return x + y
...
```

</div>

<html>
<details>
<summary><strong>🆘 Getting an error? Expand this section:</strong></summary>
<div markdown="block"> 
    
**Note:** If you get an `IndentationError`, that means that you didn't correctly indent your code after your function definition. Try typing your function into the REPL one more time.

```python
# The error you'll see if you didn't indent your function correctly.
>>> def add_numbers(x, y):
... return x + y
File "<stdin>", line 2
    return x + y
        ^
IndentationError: expected an indented block
```
</div>
</details>
</html>

### Arguments & Calling Functions

#### With no arguments
{: .no_toc }

Once you've defined a function, you can call it from your Python code as many times as you'd like.

To call a Python function, type in it's name, along with parenthesis, and any *required* arguments to the function. Let's try it now, with a function that doesn't require arguments.

```python
>>> def hello_world():
...     print("Hello, World!")
...
>>> hello_world()
Hello, World!
```

#### With arguments
{: .no_toc }

Let's try it again, this time with a function that does accept arguments.

{:.highlight}
Here, note that the function accepts **names** for the arguments. But, when we call the function, we're passing in **values**.

```python
>>> def add_numbers(x, y):
...     return x + y
...
>>> add_numbers(3, 5)
8
>>>
```

#### Storing the `return`ed value of a function.
{: .no_toc }

Storing the `return`ed value of a function is easy. All you need to do is assign it to a variable.

```python
>>> def add_numbers(x, y):
...     return x + y
...
>>> new_number = add_numbers(3, 5)
>>> new_number
8
```

The variable `new_number` now contains the result of running our `add_numbers` function with our arguments `3` and `5`.

### Arguments in Practice
{: .no_toc }

#### Positional arguments are required
{: .no_toc }

Positional arguments are all required, and must be given in the order they are declared.

For example, this function doesn't do what we expected, because we passed in our arguments in the wrong order.

```python
>>> def say_greeting(name, greeting):
...     print(f"{greeting}, {name}.")
...
>>> say_greeting("Hello!", "Nina")
Nina, Hello!.
```

#### Keyword arguments with default values
{: .no_toc }

Functions can accept two types of named arguments, ones without default values, and ones with default values. Arguments that have default values are called **keyword arguments**. The nice thing about defaults is they can be overridden when needed.

Let's see this in practice, by writing two functions that print out a greeting. One function will have a default argument to make things easier for us.

```python
# No default arguments
def say_greeting(greeting, name):
    print(f"{greeting}, {name}.")

# Default argument - greeting will always be
# Hello, if one isn't provided.
def say_greeting_with_default(name, greeting="Hello", punctuation="!"):
    print(f"{greeting}, {name}{punctuation}")
```

#### Without default arguments
{: .no_toc }

Now, let's try calling our function with no default arguments:

```python
>>> # No Default arguments
>>> def say_greeting(greeting, name):
...     print(f"{greeting}, {name}.")
...
>>> say_greeting("Good Day", "Nina")
Good Day, Nina.
```

#### Using default arguments
{: .no_toc }

Let's make a new function, `say_greeting_with_default` that accepts two arguments -- `name`, and a now **optional** argument, `greeting`. If `greeting` is not passed in, it will default to `Hello`.

```python
>>> # With Default Arguments
>>> def say_greeting_with_default(name, greeting="Hello", punctuation="!"):
...     print(f"{greeting}, {name}{punctuation}")
...
>>> say_greeting_with_default("Nina")
Hello, Nina!
>>> say_greeting_with_default("Nina", "Good Day")
Good Day, Nina!
```

#### Order matters!
{: .no_toc }

A function can accept all of one type or the other, but **arguments need to go in a specific order**.

All of the *required arguments go first*. They are then *followed by the optional keyword arguments*.

What happens when we try to define our arguments out of order? If you guessed a `SyntaxError`, you're correct!

```python
>>> def say_greeting_bad(greeting="Hello", name):
...     print("Oops, this won't work!")
...
  File "<stdin>", line 1
SyntaxError: non-default argument follows default argument
```

### Calling functions with arguments
{: .no_toc }

There are a few important things to know about calling functions with arguments.

#### Arguments without defaults are **required**!
{: .no_toc }

Arguments without default values are **required** by Python. Otherwise your function wouldn't know what to do! If you don't pass in all the required arguments, you'll get a `TypeError`.

In the REPL:
```python
>>> def say_greeting(name, greeting):
...     print(f"{greeting}, {name}.")
...
>>> say_greeting("Nina")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: say_greeting() missing 1 required positional argument: 'greeting'
```

#### You can pass in none, some, or all of the keyword arguments.
{: .no_toc }

If your function takes keyword arguments, you can provide zero, one, or all of them when you call it. You don't need to pass these arguments in order either.

```python
>>> def create_query(language="JavaScipt", num_stars=50, sort="desc"):
...     return f"language:{language} num_stars:{num_stars} sort:{sort}"
...
>>> create_query()
'language:JavaScipt num_stars:50 sort:desc'
>>> create_query(language="Ruby")
'language:Ruby num_stars:50 sort:desc'
>>> create_query(num_stars=1, language="Python", sort="asc")
'language:Python num_stars:1 sort:asc'
```

#### You can pass in required parameters by keyword.
{: .no_toc }

Even if your function arguments don't have keyword arguments with defaults, you can still pass values in to the function by name. This is especially helpful if you want to be extra clear about what you're passing in.

```python
>>> def say_greeting(name, greeting):
...     print(f"{greeting}, {name}.")
...
>>> say_greeting("Nina", "Hello")
Hello, Nina.
>>> say_greeting(name="Max", greeting="Bonjour")
Bonjour, Max.
```

### Arguments Danger Zone
{: .no_toc }

{:.warning}
Never use **mutable** types, like `list`s, as a default argument.

We'll talk more about `list`s and mutability in the coming chapter, but for the time being remember to never use an empty list as a default value to a function.

Why? Because it won't work like you'd expect it to.

```python
>>> # Don't do this!
>>> def add_five_to_list(my_list=[]):
...     my_list.append(5)
...     return my_list
...
>>> # This works like we expected it to.
>>> add_five_to_list()
[5]
>>> # Huh?
>>> add_five_to_list()
[5, 5]
>>> # We see that the original `my_list` is still being modified.
>>> add_five_to_list()
[5, 5, 5]
```

If you need to use a mutable type, like a `list` as a default, use a *marker* instead. We'll cover this technique when we talk about `list`s in the next chapter.

In Python, default arguments are evaluated only once -- when the function is defined. Not each time the function is called. That means if you use a value that can be changed, it won't behave like you'd expect it to.

### Naming Functions and Arguments
{: .no_toc }

Because Python is a dynamic language (sometimes called duck-typed) we use names as cues for what our function does, the arguments it accepts, and the values it returns.

This is especially important because we generally don't declare *types* for our programs when we're first starting out. *Note: Python does support Type hinting, but it's more of an intermediate feature. Make sure you have the basics down before learning more about it.*

{:.highlight}
Try to avoid single character names for your functions and variables, unless they have meaning in math.

For example, in this function, `x` and `y` are common names used when referring to points, so it's OK to use single-letter names in this scenario.

```python
def add_points(x1, y1, x2, y2):
    return x1 + x2, y1 + y2
```

For sequences, like `list`s, it's appropriate to name them in the plural.

For example, I'd expect a variable called `name` to be a single string, and a variable called `names` to be a list of strings.

{:.highlight}
A great resource to help you figure out the best naming conventions to use in your production Python code is a talk by Brandon Rhodes, called ["The Naming of Ducks: Where Dynamic Types Meet Smart Conventions"](https://www.youtube.com/watch?v=YklKUuDpX5c).

### Function Scope

Inside of a function in Python, the **scope** changes.

Think about it this way: scoping in Python happens with **whitespace**. When we delineate the code a function contains by indenting it under a function definition, it's scope **changes** to a new internal scope. It has access to the variables defined outside of it, but it can't change them.

Once the function is done running, its scope goes away, as do its defined variables.

```python
>>> def twitter_info():
...     twitter_account = "nnja"
...     print(f"Account inside function: {twitter_account}")
...
>>> twitter_info()
Account inside function: nnja
>>> print(f"Account outside of function: {twitter_account}")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'twitter_account' is not defined
```

We get a `NameError` when trying to access the `twitter_account` variable outside of the function. That's because it's out of scope, exactly like we expected it to be.


#### Using variables defined outside of the function
{: .no_toc }

Generally, we want to be careful when using variables defined outside of our function.

Note, that if we try to change the value of a variable defined outside of our function, we'll see the changes in the function, but not outside of it.

You can't change variables defined outside of the function inside of the function. If you try to, your changes will only apply while the function is running. Once the function is done running, the value goes back to what it was before your function ran.

A little confusing, but let's see it in action:

```python
>>> name = "Nina"
>>> print(f"Name outside of function: {name}")
Name outside of function: Nina
>>>
>>> def try_change_name():
...     name = "Max"
...     print(f"Name inside of function: {name}")
...
>>> try_change_name()
Name inside of function: Max
>>> print(f"Name outside of function: {name}")
Name outside of function: Nina
```

If we didn't know what to look for, the program might not behave how we'd expect it to. A good rule of thumb is to name our variables clearly, and minimize how many variables we declare outside of functions and classes, which you'll learn about in day two.


{:.highlight}
An appropriate use is when using a **constant**, a variable defined in all caps, with the words separated by underscores. A constant is a value that we expect to use several times within our program, but we never expect to change it programmatically.

For example:

```python
>>> ROOT_API_URL =  "https://api.github.com"
>>> def api_search_repos_url():
...     return f"{ROOT_API_URL}/search/repositories"
...
>>> api_search_repos_url()
'https://api.github.com/search/repositories'
>>>
```

### ⭐️ Practice

#### Functions
{: .no_toc }

<div class=“task” markdown="block">

Let's try creating a basic function. Use tab to indent the second line, and press enter on an empty line to finish the function.

```python
>>> def add_numbers(x, y):
...     return x + y
... # Press Enter
```

Now let's try our new function. Type this into your REPL:

```python
>>> add_numbers(1, 2)
# Let's use the string formatting we learned in the last chapter
>>> print(f"The sum of 1 and 2 is {add_numbers(1, 2)}")
```

</div>

<html>
<details>
<summary><strong>✅ Check your result after testing (no peeking!):</strong></summary>
<div markdown="block"> 
    
```python
>>> add_numbers(1, 2)
3
# Let's use the string formatting we learned in the last chapter
>>> print(f"The sum of 1 and 2 is {add_numbers(1, 2)}")
The sum of 1 and 2 is 3
```

</div>
</details>
</html>


#### The Importance of Whitespace
{: .no_toc }

Here's an error that you'll become very familiar with during your career as a Pythonista, the `IndentationError`. Whitespace is important for defining function scope in python, so missing or extra indentations or spaces will cause the runtime to throw this error. Let's redefine our `add_numbers` function, but we'll forget to indent the second line, `return x + y`. Notice that the second line is directly under (at the same indentation level) as the `def`:

```python
>>> def add_numbers(x, y):
... return x + y
  File "<stdin>", line 2
    return x + y
         ^
IndentationError: expected an indented block
```

Notice how the runtime tells us the line that failed (`line 2`), gives you a copy of the line with an arrow pointing to the offending error (`return x + y`), and then tells you the error (`IndentationError`) with additional information (`expected an indented block`).

#### Function Scope
{: .no_toc }

As we saw earlier, scoping in Python happens with whitespace. Let's see this in action:

```python
>>> x = 1
>>> y = 2
>>> def add_numbers(x, y):
...     print(f"Inside the function, x = {x} and y = {y}")
...     return x + y
...
>>> print(f"Outside the function, x = {x} and y = {y}")
>>> print(f"The sum of 5 and 6 is {add_numbers(5, 6)}")
```

<html>
<details>
<summary><strong>✅ Check your result after testing (no peeking!):</strong></summary>
<div markdown="block"> 
    
```python
>>> x = 1
>>> y = 2
>>> def add_numbers(x, y):
...     print(f"Inside the function, x = {x} and y = {y}")
...     return x + y
...
>>> print(f"Outside the function, x = {x} and y = {y}")
Outside the function, x = 1 and y = 2
>>>
>>> print(f"The sum of 5 and 6 is {add_numbers(5, 6)}")
Inside the function, x = 5 and y = 6
The sum of 5 and 6 is 11
```

</div>
</details>
</html>

#### Positional Arguments vs Keyword Arguments
{: .no_toc }

The `x` and `y` arguments for our `add_numbers()` function are called positional arguments. Python also lets us declare *keyword* arguments. Keyword arguments are great for setting default values, because passing them is optional. Just remember that keyword arguments must come *after* any positional arguments. 

<div class=“task” markdown="block">

Let's define a more generic function for doing math:

```python
>>> def calculate_numbers(x, y, operation="add"):
...     if operation == "add":
...         return x + y
...     elif operation == "subtract":
...         return x - y
...
# Let's try our new function. Remember, if we don't pass the operation keyword argument, the default is "add"
>>> calculate_numbers(2, 3)
# You can pass a keyword argument as a normal positional argument
>>> calculate_numbers(2, 3, "subtract")
# You can also use the argument's keyword. This helps with readability
>>> calculate_numbers(2, 3, operation="subtract")
```

</div>

<html>
<details>
<summary><strong>✅ Check your result after testing (no peeking!):</strong></summary>
<div markdown="block"> 
    
```python
>>> def calculate_numbers(x, y, operation="add"):
...     if operation == "add":
...         return x + y
...     elif operation == "subtract":
...         return x - y
...
# Let's try our new function. Remember, if we don't pass the operation keyword argument, the default is "add"
>>> calculate_numbers(2, 3)
5
# You can pass a keyword argument as a normal positional argument
>>> calculate_numbers(2, 3, "subtract")
-1
# You can also use the argument's keyword. This helps with readability
>>> calculate_numbers(2, 3, operation="subtract")
-1
```

</div>
</details>
</html>

---
## Advanced Data Types

### Lists
Lists are one of the most powerful data types in Python. Generally, they're container objects used to **store related items together**.

#### `list` cheat sheet
{: .no_toc }

| type             	| `list`                                                                                	|
|------------------	|---------------------------------------------------------------------------------------	|
| use              	| Used for storing similar items, and in cases where items need to be added or removed. 	|
| creation         	| `[]` or `list()` for empty list, or `[1, 2, 3]` for a list with items.                            	|
| search methods   	| `my_list.index(item)` or `item in my_list`                                                                           	|
| search speed     	| Searching in an item in a large list is slow. Each item must be checked.                               	|
| common methods   	| `len(my_list)`, `append(item)` to add, `insert(index, item)` to insert in the middle, `pop()` to remove.         	|
| order preserved? 	| Yes. Items can be accessed by index.                                                  	|
| mutable?         	| Yes                                                                                   	|
| in-place sortable?        	| Yes. `my_list.sort()` will sort the list in-place. `my_list.sort(reverse=True)` will sort the list in-place in *descending* order. `my_list.reverse()` will *reverse the items* in `my_list` in-place.           	|


Let's create a few lists to see how they work.

An empty list can be created in two ways. The first, by calling the `list()` method. More commonly, it's created with two empty brackets `[]`. Don't forget to check the type of the list with the `type` built-in function.

```python
>>> list()
[]
>>> []
[]
>>> type(list())
<class 'list'>
>>> type([])
<class 'list'>
```

Let's create our list with a few items in it. Let's say we want to keep track of a list of names. We add items to our list, and separate them with commas `,`.

```python
>>> names = ["Nina", "Max", "Jane"]
```

We can check its length with the built-in `len()` method, like so:

```python
>>> len(names)
3
```

### Indexes and Indices
{: .no_toc }

**Lists retain the order** of the items in them. In the next section, you'll learn about some data structures that don't.

In order to *access* items in a list, we'll need to use an *index*. (Multiple indexes are sometimes also called indices). The index for the item you want to access is *an integer* put in *square brackets* after the list.

{:.highlight}
**Indexes start at** `0` in Python and most other programming languages.

<div class=“task” markdown="block">

```python
>>> names = ["Nina", "Max", "Jane"]
>>> names[0]
>>> names[1]
>>> names[2]
```

</div>

#### Updating an item in a list
{: .no_toc }

To update a particular item in a `list` use square-bracket notion and assign a new value. `my_list[pos] = new_value`

<div class=“task” markdown="block">

```python
>>> names = ["Nina", "Max", "Jane"]
>>> names[2] = "Floyd"
>>> names
```
</div>

{:.highlight}
If you try to access an index that is greater than or equal to (>=) the length of the list, you'll get an `IndexError`.

```python
>>> names = ["Nina", "Max", "Jane"]
>>> len(names)
3
>>> names[3]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list index out of range
```

#### Formatting
{: .no_toc }

{:.highlight}
We can *optionally* add new lines after the commas. This helps with readability for more complex list items.

Notice that we can also *optionally* add a trailing comma after the last item. A trailing comma isn't required to create a valid list, but it does help minimize version control differences when working on a Python codebase with a team.

```python
>>> names = [
... "Nina",
... "Max",
... "Jane",
... ]
```


### Common Mistakes
{: .no_toc }

{:.highlight}
If you forget to include commas between your items, you'll get a `SyntaxError`.

```python
>>> numbers = [1, 2 3]
  File "<stdin>", line 1
    numbers = [1, 2 3]
                    ^
SyntaxError: invalid syntax
```

The REPL makes it difficult to forget the closing bracket, but if you forget it while writing code in a Python file, you'll see a `SyntaxError` with a different name. It'll say: `SyntaxError: unexpected EOF while parsing` or `SyntaxError: invalid syntax`.

For example:

```python
# Python file: program.py
names = ["Nina",
x = 5
```

Notice how the `SyntaxError` points to a completely valid line of Python code. In these cases, you also need to check the line of code **before** the line with the `SyntaxError`. There, we'll notice that we forgot the closing bracket of our `names` list.

```bash
# In a shell
(env) $ python program.py
  File "/Users/nina/Desktop/program.py", line 2
    x = 5
      ^
SyntaxError: invalid syntax
```

### Sorting
{: .no_toc }

Sorting sounds complicated, but in practice, it's just one method call away!

#### Sorting a Copy Of Your List
{: .no_toc }

If you'd like sort to return a brand new copy of your list, instead of modifying your original copy, you can use the built-in `sorted(my_list)` function on your list to return a *new* `list`, sorted in increasing (ascending) order. Or use `sorted(my_list, reverse=True)` to create a new `list` sorted backwards, in decreasing (or descending) order. This operation will **not modify** the underlying list.

Either of these operations will return a *new* list.

```python
>>> lottery_numbers = [1, 4, 32423, 2, 45, 11]
>>> sorted(lottery_numbers)
[1, 2, 4, 11, 45, 32423]
>>> lottery_numbers
[1, 4, 32423, 2, 45, 11]
>>> sorted(lottery_numbers, reverse=True)
[32423, 45, 11, 4, 2, 1]
>>> lottery_numbers
[1, 4, 32423, 2, 45, 11]
```

#### Sorting the list in-place
{: .no_toc }

You can call `my_list.sort()` on your list to sort it in increasing (ascending) order, or `my_list.sort(reverse=True)` on the list to sort it backwards, in decreasing (or descending) order. This operation will modify the underlying list, and *doesn't return a value*.

```python
>>> lottery_numbers = [1, 4, 32423, 2, 45, 11]
>>> lottery_numbers.sort()
>>> lottery_numbers
[1, 2, 4, 11, 45, 32423]

>>> lottery_numbers.sort(reverse=True)
>>> lottery_numbers
[32423, 45, 11, 4, 2, 1]

>>> words = ["Umbrella", "Fox", "Apple"]
>>> words.sort()
>>> words
['Apple', 'Fox', 'Umbrella']
```

#### Reverse the list in-place
{: .no_toc }

To reverse the items of a list in-place, call `my_list.reverse()` on it.

```python
>>> lottery_numbers = [1, 4, 32423, 2, 45, 11]
>>> lottery_numbers.reverse()
>>> lottery_numbers
[11, 45, 2, 32423, 4, 1]
```

### Finding Methods
{: .no_toc }

Remember, if you ever forget which methods are available on `list`, just call `dir` on it. Ignore the methods that start with underscores. If you need help remembering what a method does, you can call `help()` on it. For example, for append, call `help(list.append)`.

#### Adding, Removing, Changing, and Finding Items in `list`s cheat sheet
{: .no_toc }


| action                                           	| method                                	| returns           	| possible errors                            	|
|--------------------------------------------------	|---------------------------------------	|-------------------	|--------------------------------------------	|
| check length                                     	| `len(my_list)`                        	| `int`             	|                                            	|
| **add:** to the end                              	| `my_list.append(item)`                	| -                 	|                                            	|
| **insert:** at position                          	| `my_list.insert(pos, item)`           	| -                 	|                                            	|
| **update:** at position                          	| `my_list[pos] = item`          	| -        -         	| `IndexError` if `pos` is >= `len(my_list)`                                          	|
| **extend:** add items from another list          	| `my_list.extend(other_list)`          	| -                 	|                                            	|
| is item in list?                                 	| `item in my_list`                     	| `True` or `False` 	|                                            	|
| **index** of item                                	| `my_list.index(item)`                 	| `int`             	| `ValueError` if `item` is not in `my_list` 	|
| **count** of item                                	| `my_list.count(item)`                 	| `int`             	|                                            	|
| **remove** an item                               	| `my_list.remove(item)`                	| -                 	| `ValueError` if `item` not in `my_list`    	|
| **remove** the last item, or an item at an index 	| `my_list.pop()` or `my_list.pop(pos)` 	| `item`            	| `IndexError` if `pos` >= `len(my_list)`    	|


#### Checking Length
{: .no_toc }

Before we add or remove items, it's usually a good idea to check a list's length. We do that with the `len` built in function. We can even use the `len` built in function to check the lengths of other types, like strings.

Let's see it in action on a names `list` with two items, and a name `str`ing with four characters.

```python
>>> len(names)
2
>>> name = "Nina"
>>> len(name)
4
```

### Adding Items
{: .no_toc }

Let's start with a list of two names.

```python
>>> names = ["Nina", "Max"]
```

##### `my_list.append(item)` adds to the end of `my_list`
{: .no_toc }

We can use `my_list.append(item)` to add an additional item to the end of the list.

```python
>>> names.append("John")
>>> names
['Nina', 'Max', 'John']
```

##### `my_list.insert(pos, item)` inserts an item into `my_list` at the given position
{: .no_toc }

Use `my_list.insert(pos, item)` to insert items in an arbitrary position in the list. If the position is 0, we'll insert at the beginning of the list.

```python
>>> names.insert(0, "Rose")
>>> names
['Rose', 'Nina', 'Max', 'John']
```

You can call `dir()` on our names list to verify that it's actually of type `list`. If you forget which order insert is called in, don't forget you can always use the `help()` function on the REPL. **Remember: Press `q` to quit the help screen.** Let's try it now:

```python
>>> type(names)
<class 'list'>
>>> help(names.insert)

Help on method_descriptor:

insert(self, index, object, /)
    Insert object before index.
```

You can also call help on `names.insert`. Because `names` is already of type `list`, it achieves the same result.

##### `my_list.extend(other_list)` adds all the contents of `other_list` to `my_list`
{: .no_toc }

```python
>>> names = ["Nina", "Max"]
>>> colors = ["Red", "Blue"]
>>> names
['Nina', 'Max']
>>> names.extend(colors)
>>> names
['Nina', 'Max', 'Red', 'Blue']
```

### Looking for Items
{: .no_toc }

Looking for items in a list is *slow*. Each item needs to be checked in order to find a match.

This doesn't matter much when you're just getting started, unless your data set is large, or if you're building high-performance systems. If you want to quickly search for an item, you'll need to use a `set` or a `dict`ionary instead.

There are a few ways to determine if an item is in the list, and at which position. Let's try this on our list of names.

```python
names = ["Nina", "Max", "Phillip", "Nina"]
```

##### Use the `in` keyword to determine if an item is present or not.
{: .no_toc }

```python
>>> "Nina" in names
True
>>> "Rose" in names
False
```

##### Use the `my_list.index(item)` method to find the **first** index of a potential match.
{: .no_toc }

Notice that only the *first* index of the string `"Nina"` is returned. We'll learn more about what an index is in the next chapter.

{:.highlight}
If the item we're looking for *is not* in the list, Python will throw a `ValueError`.

You'll learn how to deal with exceptions later. For now, you can use the `in` operator to check if an item is present in the list before finding its index.

```python
>>> names.index("Nina")
0
>>> names.index("Rose")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: 'Rose' is not in list
```

##### Use the `my_list.count(item)` method to find out how many times an item appears in a list.
{: .no_toc }

```python
>>> names.count("Nina")
2
>>> names.count("Rose")
0
```

### Updating Items
{: .no_toc }

To update items in a list, use the *position* of the item you'd like to change using square bracket `[]` syntax. Like: `my_list[pos] = new_item`

For example:

```python
>>> names = ["Nina", "Max"]
>>> names[0] = "Rose"
>>> names
['Rose', 'Max']
```

Or, when used with `my_list.index(item)`:

```python
>>> names = ["Nina", "Max"]
>>> pos = names.index("Max")
>>> names[pos] = "Rose"
>>> names
['Nina', 'Rose']
```

{:.highlight}
You'll see a `IndexError: list assignment index out of range` if you try to update an item in a position that doesn't exist, that is *if the position is greater than or equal to `>=` the length of the list*.

```python
>>> names = ["Nina", "Max"]
>>> len(names)
2
>>> names[2] = "Rose"
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list assignment index out of range
```

### Removing Items
{: .no_toc }

There are a few ways to remove items from a list.

##### Use `my_list.remove(item)` to remove the *first* instance of the item
{: .no_toc }

Be careful. `remove()` only removes the first instance of the item from the list, which isn't always what we want to do.

```python
>>> names = ["Nina", "Max", "Rose"]
>>> names.remove("Nina")
>>> names
['Max', 'Rose']
>>>
>>>
>>> names = ["Nina", "Max", "Nina"]
>>> names.remove("Nina")
>>> names
['Max', 'Nina']
```

{:.highlight}
If we try to remove an item that's not in the list, we'll get a `ValueError: list.remove(x): x not in list`.

```python
>>> names = ["Nina"]
>>> names.remove("Max")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: list.remove(x): x not in list
```

##### Use `my_list.pop()` to remove the last item, or `my_list.pop(index)` to remove the item at that index
{: .no_toc }

Using `pop()` will also **return** the item that was in that position. That's useful if we want to save the item.

```python
>>> names = ["Nina", "Max", "Rose"]
>>> names.pop()
'Rose'
>>> names
['Nina', 'Max']
>>> names.pop(1)
'Max'
>>> names
['Nina']
```

{:.highlight}
If we try to pop an item from an index that is longer than or equal to the length of the list, we'll get an `IndexError: pop index out of range`.

```python
>>> names = ["Nina"]
>>> len(names)
1
>>> names.pop(1)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: pop index out of range
```

### Tuples
Tuples are light-weight collections used to keep track of related, but different items. Tuples are **immutable**, meaning that once a tuple has been created, the items in it can't change.

You might ask, why tuples when Python already has lists? Tuples are different in a few ways. While lists are generally used to store collections of similar items together, tuples, by contrast, can be used to contain a snapshot of data. They can't be continually changed, added or removed from like you could with a list.

#### `tuple` cheat sheet
{: .no_toc }

| type               	| `tuple`                                                                                                 	|
|--------------------	|---------------------------------------------------------------------------------------------------------	|
| use                	| Used for storing a snapshot of related items when we don't plan on modifying, adding, or removing data. 	|
| creation           	| `()` or `tuple()` for empty tuple. `(1, )` for one item, or `(1, 2, 3)` for a tuple with items.         	|
| search methods     	| `my_tuple.index(item)` or `item in my_tuple`                                                            	|
| search speed       	| Searching for an item in a large tuple is slow. Each item must be checked.                              	|
| common methods     	| Can't add or remove from tuples.                                                                        	|
| order preserved?   	| Yes. Items can be accessed by index.                                                                    	|
| mutable?           	| **No**                                                                                                  	|
| in-place sortable? 	| **No**                                                                                                  	|

#### Uses
{: .no_toc }
A good use of a `tuple` might be for storing the information for a *row* in a spreadsheet. That data is information only. We don't necessarily care about updating or manipulating that data. We just want a read-only snapshot.


Tuples are an interesting and powerful datatype, and one of the more unique aspects of Python. Most other programming languages have ways of representing lists and dictionaries, but only a small subset contain tuples. Use them to your advantage.

### Examples
{: .no_toc }

#### Empty and one-item `tuple`s
{: .no_toc }

One important thing to note about tuples, is there's a quirk to their creation. Let's check the type of an empty `tuple` created with `()`.
```python
>>> a = ()
>>> type(a)
<class 'tuple'>
```

That looks like we'd expect it to. What about if we *tried* to create a one-item `tuple` using the same syntax?

```python
>>> b = (1)
>>> type(b)
<class 'int'>
```

It didn't work! `type((1))` is an `int`eger. In order to create a one-item tuple, you'll need to include a trailing comma.

```python
>>> c = (1, )
>>> type(c)
<class 'tuple'>
```

{:.highlight}
If you're creating a one-item tuple, you **must** include a trailing comma, like this: `(1, )`

#### Creation
{: .no_toc }

Let's say we have a spreadsheet of students, and we'd like to represent each row as a tuple.

```python
>>> student = ("Marcy", 8, "History", 3.5)
```

#### Access by index
{: .no_toc }

We can access items in the `tuple` by index, but we **can't change them**.

```python
>>> student = ("Marcy", 8, "History", 3.5)
>>> student[0]
'Marcy'
>>> student[0] = "Bob"
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
```

{:.highlight}
We'll see `TypeError: 'tuple' object does not support item assignment` if we try to change the items in a tuple.

`tuple`s also don't have an `append` or `extend` method available on them like lists do, because they can't be changed.

### `tuple` unpacking.
{: .no_toc }

Sounds like a lot of work for not a lot of benefit, right? Not so. `tuple`s are great when you depend on your data staying unchanged. Because of this guarantee, we can use `tuples` in other types of containers like `set`s and `dict`ionaries.

It's also a great way to quickly consolidate information.

You can also use `tuples` for something called unpacking. Let's see it in action:

```python
>>> student = ("Marcy", 8, "History", 3.5)
>>>
>>> name, age, subject, grade = student
>>> name
'Marcy'
>>> age
8
>>> subject
'History'
>>> grade
3.5
```

You can return tuples from functions, and use unpacking.

```python
>>> def http_status_code():
...     return 200, "OK"
...
>>> code, value = http_status_code()
>>> code
200
>>> value
'OK'
```

### Sets
Sets are a datatype that allows you to store other **immutable** types in an unsorted way. An item can only be contained in a set once. There are no duplicates allowed. The benefits of a set are: very fast membership testing along with being able to use powerful set operations, like `union`, `difference`, and `intersection`.

#### `set` cheat sheet
{: .no_toc }

| type               	| `set`                                                                                                                         	|
|--------------------	|-------------------------------------------------------------------------------------------------------------------------------	|
| use                	| Used for storing immutable data types uniquely. Easy to compare the items in `set`s.                                          	|
| creation           	| `set()` for an empty set (`{}` makes an empty `dict`) and `{1, 2, 3}` for a set with items in it                              	|
| search methods     	| `item in my_set`                                                                                                              	|
| search speed       	| Searching for an item in a large set is very fast.                                                                            	|
| common methods     	| `my_set.add(item)`, `my_set.discard(item)` to remove the item if it's present, `my_set.update(other_set)` 	|
| order preserved?   	| **No**. Items *can't* be accessed by index.                                                                                   	|
| mutable?           	| **Yes**. Can add to or remove from `set`s.                                                                                    	|
| in-place sortable? 	| **No**, because items aren't ordered.                                                                                                                        	|

### Examples
{: .no_toc }

#### Empty `set`s
{: .no_toc }

Let's create our first few sets.

The first thing we might try to do is create an empty set with `{}`, but we'll come across a hurdle.

```python
>>> my_new_set = {}
>>> type(my_new_set)
<class 'dict'>
>>> my_set = set()
>>> type(my_set)
<class 'set'>
```

{:.highlight}
You can't create an empty `set` with `{}`. That creates a `dict`. Create an empty set with `set()` instead.

{:.highlight}
While you're learning Python, it's useful to use `type()`, `dir()` and `help()` as often as possible.

#### `set`s with items
{: .no_toc }

Now, let's make a new set with some items in it, and test out important set concepts.

#### `set`s can't contain duplicate values
{: .no_toc }

```python
>>> names = {"Nina", "Max", "Nina"}
>>> names
{'Max', 'Nina'}
>>> len(names)
2
```

#### `set`s can't contain mutable types
{: .no_toc }

The way that `set`s allow you to quickly check if an item is contained in them or not is with an algorithm called a hash. I won't cover the details, but an algorithm is a way of representing an immutable data type with a unique numerical representation. In Python, there's a built-in `hash()` function.

The `hash()` function only works on immutable data types. That means, data types where the contents can't be changed after creation.

```python
>>> hash("Nina")
3509074130763756174
>>> hash([])
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
```

{:.highlight}
You'll see a `TypeError: unhashable type: 'list'` if you try to add a mutable data type (like a `list`) to a set.

If you try to add a mutable data type (like a `list`) to a set, you'll see the same `TypeError`, complaining about an `unhashable type`.

```python
>>> {"Nina"}
{'Nina'}
>>> {[]}
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
```

#### `set`s can be used to de-duplicate the items in a list
{: .no_toc }

**Tip:** *If you don't care about order*, you can quickly de-duplicate the items in a `list` by passing the `list` into the `set` constructor.

```python
>>> colors = ["Red", "Yellow", "Red", "Green", "Green", "Green"]
>>> set(colors)
{'Red', 'Green', 'Yellow'}
```

#### `set`s don't have an order
{: .no_toc }

Sets don't have an order. That means that when you print them, the items won't be displayed in the order they were entered in the list.

```python
>>> my_set = {1, "a", 2, "b", "cat"}
>>> my_set
{1, 2, 'cat', 'a', 'b'}
```

It also means that you *can't* access items in the `set` by position in subscript `[]` notation.

```python
>>> my_set = {"Red", "Green", "Blue"}
>>> my_set[0]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'set' object does not support indexing
```

{:.highlight}
You'll see `TypeError: 'set' object does not support indexing` if you try to access the items in a `set` by index with `my_set[pos]`

**Tip:** If your set contains items of the same type, and you want to sort the items, you'll need to convert the `set` to a `list` first. Or, you can use the built-in `sorted(sequence)` method, which will do the conversion for you.

```python
>>> my_set = {"a", "b", "cat", "dog", "red"}
>>> my_set
{'b', 'red', 'a', 'cat', 'dog'}
>>> sorted(my_set)
['a', 'b', 'cat', 'dog', 'red']
```

#### adding to and removing from `set`s
{: .no_toc }

Since a set has no order, we can't add or remove items to it by index. We need to call the operations with the item itself.

#### Add items to a set with `my_set.add(item)`.
{: .no_toc }

```python
>>> colors = {"Red", "Green", "Blue"}
>>> colors.add("Orange")
>>> colors
{'Orange', 'Green', 'Blue', 'Red'}
```

#### Remove items with `my_set.discard(item)`
{: .no_toc }

You can remove an item from a `set` if it's present with `my_set.discard(item)`. If the set doesn't contain the item, no error occurs.

```python
>>> colors = {"Red", "Green", "Blue"}
>>> colors.discard("Green")
>>> colors
{'Blue', 'Red'}
>>> colors.discard("Green")
>>> colors
{'Blue', 'Red'}
```

You can also remove items from a `set` with `my_set.remove(item)`, which will raise a `KeyError` if the item doesn't exist.


#### Update a set with another sequence using `my_set.update(sequence)`
{: .no_toc }

You can update a `set` by passing in another sequence, meaning another `set`, `list`, or `tuple`.

```python
>>> colors = {"Red", "Green"}
>>> numbers = {1, 3, 5}
>>> colors.update(numbers)
>>> colors
{1, 3, 'Red', 5, 'Green'}
```

{:.highlight}
Be careful passing in a `str`ing to `my_set.update(sequence)`. That's because a `str`ing is *also* a sequence. It's a sequence of characters.

```python
>>> numbers = {1, 3, 5}
>>> numbers.update("hello")
>>> numbers
{1, 3, 'h', 5, 'o', 'e', 'l'}
```

Your set will update with each character of the `str`ing, which was probably not your intended result.

### `set` operations
{: .no_toc }

`sets` allow quick and easy operations to compare items between two sets.

#### `set` operations cheat sheet
{: .no_toc }

 method operation    	| symbol operation 	| result                                                                        	|
|---------------------	|------------------	|-------------------------------------------------------------------------------	|
| `s.union(t)`        	| <code>s &#124; t</code> | creates a new set with all the items **from both `s` and `t`**             |
| `s.intersection(t)` 	| `s & t`          	| creates a new set containing *only* items that are **both in `s` and in `t`** 	|
| `s.difference(t)`    	| `s ^ t`          	| creates a new set containing items that are **not in both `s` and in `t`**                        	|

#### examples
{: .no_toc }

Let's see it in action.

We have two sets, `rainbow_colors`, which contain the colors of the rainbow, and `favorite_colors`, which contain my favorite colors.

```python
>>> rainbow_colors = {"Red", "Orange", "Yellow", "Green", "Blue", "Violet"}
>>> favorite_colors = {"Blue", "Pink", "Black"}
```

First, let's combine the sets and create a new `set` that contains all of the items from `rainbow_colors` and `favorite_colors` using the union operation. You can use the `my_set.union(other_set)` method, or you can just use the symbol for union `|=` from the table above.

```python
>>> rainbow_colors | favorite_colors
{'Orange', 'Red', 'Yellow', 'Green', 'Violet', 'Blue', 'Black', 'Pink'}
```

Next, let's find the intersection. We'll create a new `set` with *only* the items in both `set`s.

```python
>>> rainbow_colors & favorite_colors
{'Blue'}
```

Lastly, We can also find the difference. Create a new set with the items that are in in one, but not the other. We'll see that `"Blue"` is missing from the list.

```python
>>> rainbow_colors ^ favorite_colors
{'Orange', 'Red', 'Yellow', 'Green', 'Violet', 'Black', 'Pink'}
```

There are other useful operations available on `set`s, such as checking if one set is a subset, a superset, and more, but I don't have time to cover them all. Python also has a `frozenset` type, if you need the functionality of a `set` in an immutable package (meaning that the contents can't be changed after creation).

Find out more by reading the [documentation](https://docs.python.org/3/library/stdtypes.html#set), or calling `help()` on `set`.

### Dictionaries
Dictionaries are a useful type that allow us to store our data in key, value pairs. Dictionaries themselves are **mutable**, *but*, dictionary keys can only be **immutable** types.

We use dictionaries when we want to be able to quickly access additional data associated with a particular key. A great practical application for dictionaries is memoization. Let's say you want to save computing power, and store the result for a function called with particular arguments. The arguments could be the key, with the result stored as the value. Next time someone calls your function, you can check your dictionary to see if the answer is pre-computed.

Looking for a key in a large dictionary is extremely fast. Unlike lists, we don't have to check every item for a match.

### `dict`ionary cheat sheet
{: .no_toc }

| type               	| `dict`                                                                                                                                             	|
|--------------------	|----------------------------------------------------------------------------------------------------------------------------------------------------	|
| use                	| Use for storing data in key, value pairs. Keys used must be **immutable** data types.                                                              	|
| creation           	| `{}` or `dict()` for an empty `dict`. `{1: "one", 2: "two"}` for a `dict` with items.                                                              	|
| search methods     	| `key in my_dict`                                                                                                                                   	|
| search speed       	| Searching for a key in a large dictionary is fast.                                                                                                 	|
| common methods     	| `my_dict[key]` to get the value by `key`, and throw a `KeyError` if `key` is not in the dictionary. Use `my_dict.get(key)` to fail silently if `key` is not in `my_dict`. `my_dict.items()` for all key, value pairs, `my_dict.keys()` for all keys, and `my_dict.values()` for all values. 	|
| order preserved?   	| **Sort of**. As of Python 3.6 a `dict` is sorted by insertion order. Items *can't* be accessed by index, only by key.                              	|
| mutable?           	| **Yes**. Can add or remove keys from `dict`s.                                                                                                      	|
| in-place sortable? 	| **No**. `dict`s don't have an index, only keys.                                                                                                    	|

### Examples
{: .no_toc }

#### Empty `dict`s
{: .no_toc }

We already learned one of the methods of creating an empty `dict` when we tried (and failed) to create an empty set with `{}`. The other way is to use the `dict()` method.

```python
>>> my_dict = {}
>>> type(my_dict)
<class 'dict'>

>>> my_dict = dict()
>>> type(my_dict)
<class 'dict'>
```

#### Creating `dict`s with items
{: .no_toc }

If we want to create `dict`s with items in them, we need to pass in key, value pairs. A `dict` is declared with curly braces `{}`, followed by a key and a value, separated with a colon `:`. Multiple key and value pairs are separated with commas `,`.


We can call familiar methods on our dictionary, like finding out how many key / value pairs it contains with the built-in `len(my_dict)` method.

```python
>>> nums = {1: "one", 2: "two", 3: "three"}

>>> len(nums)
3
```

#### Side note: What can be used as keys?
{: .no_toc }

Any type of object, mutable or immutable, can be used as a value but just like `set`s, `dict`ionaries can only use immutable types as keys. That means you can use `int`, `str`, or even `tuple` as a key, but **not** a `set`, `list`, or other `dict`ionary.

The follow is OK:

```python
>>> my_dict = {1: 1}
>>> my_dict = {1: []}
```

{:.highlight}
You'll see a `TypeError: unhashable type: 'list'` if you try to use a mutable type, like a `list` as a `dict`ionary key.

```python
>>> my_dict = {[]: 1}
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
```

#### Accessing
{: .no_toc }

Our `dict` contains `key`, `value` pairs. Because a `dict`ionary isn't ordered, we *can't access the items in it by position*. Instead, to access the items in it, we use square-bracket `my_dict[key]` notation, similar to how we access items in a list with square bracket notation containing the position.

```python
>>> nums = {1: "one", 2: "two", 3: "three"}
>>> nums[1]
'one'
>>> nums[2]
'two'
```

Q: What happens when we try to access a key in a `dict`ionary with square bracket notation, but the key isn't present?

{:.highlight}
We'll get a `KeyError: key` if we try to access `my_dict[key]` with square bracket notation, but `key` isn't in the dictionary.

```python
>>> nums = {1: "one", 2: "two", 3: "three"}
>>> nums[4]

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 4
```

One way to get around this is to use the `my_dict.get(key)` method. Using this method, if the key isn't present, no error is thrown, and no value (aka the `None` type) is returned.

```python
>>> nums = {1: "one", 2: "two", 3: "three"}
>>> nums.get(4)

>>> result = nums.get(4)
>>> type(result)
<class 'NoneType'>
```

If we want to provide a *default value* if the key is missing, we also pass an *optional* argument to the `my_dict.get(key)` method like so: `my_dict.get(key, default_val)`

```python
>>> nums = {1: "one", 2: "two", 3: "three"}
>>> nums.get(4, "default")
'default'
```

#### Adding, Removing
{: .no_toc }

To add a new key value pair to the dictionary, you'll use square-bracket notation.

If you try to put a key into a dictionary that's already there, you'll just end up replacing it. To avoid subtle bugs, you can check if a particular key is in a dictionary with the `in` keyword. We'll cover that technique in Chapter 6 - Control Statements and Looping.

```python
>>> nums = {1: "one", 2: "two", 3: "three"}
>>> nums[8] = "eight"

>>> nums
{1: 'one', 2: 'two', 3: 'three', 8: 'eight'}

>>> nums[8] = "oops, overwritten"
>>> nums
{1: 'one', 2: 'two', 3: 'three', 8: 'oops, overwritten'}
>>> 8 in nums
True
```

#### Updating
{: .no_toc }

Just like with `list`s an `set`s, you can update the items in a dictionary with the items from another dictionary.

```python
>>> colors = {"r": "Red", "g": "Green"}
>>> numbers = {1: "one", 2: "two"}
>>> colors.update(numbers)
>>> colors
{'r': 'Red', 'g': 'Green', 1: 'one', 2: 'two'}
```

### Complex Dictionaries
{: .no_toc }

One incredibly useful scenario for dictionaries is storing the values in a `list` or other sequence. Going into too much detail is outside of the scope of the class, but I'll show you a quick example:

```python
>>> colors = {"Green": ["Spinach"]}
>>> colors
{'Green': ['Spinach']}
>>> colors["Green"].append("Apples")
>>> colors
{'Green': ['Spinach', 'Apples']}
```

### Working with `items`, `keys`, and `values`
{: .no_toc }

There are three useful methods you need to remember about `dict`ionary access:

1. `my_dict.keys()`
2. `my_dict.values()`
3. `my_dict.items()`

#### 1. `my_dict.keys()` Getting all the keys in a dictionary
{: .no_toc }

```python
>>> nums = {1: 'one', 2: 'two', 3: 'three', 8: 'eight'}
>>> nums.keys()
dict_keys([1, 2, 3, 8])
```

#### 2. `my_dict.values()` Getting all the values in a dictionary.
{: .no_toc }

```python
>>> nums = {1: 'one', 2: 'two', 3: 'three', 8: 'eight'}
>>> nums.values()
dict_values(['one', 'two', 'three', 'eight'])
```

#### 3. `my_dict.items()` Getting all the items (key, value pairs) in a dictionary
{: .no_toc }

Notice that `my_dict.items()` returns a type that looks like a list. It contains two-item `tuple`s containing the key, value pairs.

```python
>>> nums = {1: 'one', 2: 'two', 3: 'three', 8: 'eight'}
>>> nums.items()
dict_items([(1, 'one'), (2, 'two'), (3, 'three'), (8, 'eight')])
```

### Mutability

Mutability, simply put: the contents of a mutable object can be changed, while the contents of an immutable object cannot be.

#### Simple Types
{: .no_toc }

All of the simple data types we covered first are **immutable**

| type                      	| use                     	| mutable? 	|
|---------------------------	|-------------------------	|----------	|
| `int`, `float`, `decimal` 	| store numbers           	| **no**   	|
| `str`                     	| store strings           	| **no**   	|
| `bool`                    	| store `True` or `False` 	| **no**   	|

#### Container Types
{: .no_toc }

For the mutability of the container types we covered in this chapter, check this helpful list:

| container type 	| use                                                                                                     	| mutable? 	|
|----------------	|---------------------------------------------------------------------------------------------------------	|----------	|
| `list`         	| ordered group of items, accessible by position                                                          	| **yes**  	|
| `set`          	| mutable unordered group consisting only of immutable items. useful for set operations (membership, intersection, difference, etc) 	| **yes**  	|
| `tuple`        	| contain ordered groups of items in an **immutable** collection                                          	| **no**   	|
| `dict`         	| contains key value pairs                                                                                	| **yes**  	|


### ⭐️ Practice

### Lists
{: .no_toc }

Lists are great for storing an ordered sequence of objects. 

<div class=“task” markdown="block">

Remember that you can see the current state of your list at any time by typing the name of your list by itself. Check your list after every operation to see if it has changed.

```python
>>> my_list = ["h", "e", "l", "l", "o"]
# Let's look at our list:
>>> my_list
# Let's add to my_list:
>>> my_list.append("!")
# Now let's see it again:
>>> my_list
```
</div>

<div class=“task” markdown="block">

Let's play with slices. How do we get the last two elements of our list?

```python
# We know the number of items in our list is 6...
>>> len(my_list)
6
# So the last two indexes are 4 and 5. Since the first number in the slice is inclusive, and the second number is exclusive, we can ask for everything between index 4 and 6
>>> my_list[4:6]
# We can also say "Give me everything after index 4
>>> my_list[4:]
# Or, we can ask for just the last two items without caring how big the list is. This means "give me everything starting from two before the end":
>>> my_list[-2:]
```
</div>

<div class=“task” markdown="block">

There are many other ways to interact with our lists as well:

```python
# Remove the first L:
>>> my_list.remove("l")
# Let's put it back at index 2
>>> my_list.insert(2, "l")

# Delete any element
>>> del my_list[0]
# Remove and return the last element. Useful for queues!
>>> last_item = my_list.pop()
>>> last_item

# We can also look at individual items my using an index:
>>> my_list[2]
# Or we can see if a certain value exists in the list:
>>> "!" in my_list
# Let's sort our list in reverse order
>>> my_list.sort(reverse=True)
>>> my_list
# Note that sort() doesn't return anything, it sorts the list in-place
# You can also use the sorted() function to return a new, sorted list without modifying the old one
>>> sorted(my_list, reverse=False)
>>> my_list
```
</div>

<html>
<details>
<summary><strong>✅ Check your result after testing (no peeking!):</strong></summary>
<div markdown="block"> 

```python
>>> my_list = ["h", "e", "l", "l", "o"]
>>> my_list
['h', 'e', 'l', 'l', 'o']
>>> my_list.append("!")
>>> my_list
['h', 'e', 'l', 'l', 'o', '!']

>>> len(my_list)
6
>>> my_list[4:6]
['o', '!']
>>> my_list[4:]
['o', '!']
>>> my_list[-2:]
['o', '!']

>>> my_list.remove("l")
>>> my_list.insert(2, "l")
>>> del my_list[0]
>>> last_item = my_list.pop()
>>> last_item
'o'
>>> my_list[2]
'l'
>>> "!" in my_list
False
>>> my_list.sort(reverse=True)
>>> my_list
['o', 'l', 'l', 'h', 'e', '!']
>>> sorted(my_list, reverse=False)
['!', 'e', 'h', 'l', 'l', 'o']
```

</div>
</details>
</html>

### Sets
{: .no_toc }

Sets are a great data type for storing unique data - you can only have one of any given object in a set. Sets are unordered, thus you can't access them with `[]` indexing syntax, but they do have some handy functions.

<div class=“task” markdown="block">

Let's play with some set operations:

```python
# Create an empty set
>>> my_set = {}
>>> type(my_set)
# Gotcha: using {} actually creates an empty dictionary. To create an empty set, use set()
>>> my_set = set()
>>> my_set

# Let's create a non-empty set
>>> my_set = {1, 2, 3}
# We can add and remove items from the set
>>> my_set.add(4)
>>> my_set.remove(2)
# We can test if an item exists in the set
>>> 2 in my_set

# Unlike lists, every item in a set must be unique
>>> my_set
>>> my_set.add(3)
>>> my_set
# There is still only one 3 in the set

>>> my_set
# my_set should equal {1, 3, 4}
>>> my_other_set = {1, 2, 3}
# We can combine two sets
>>> my_set.union(my_other_set)
# We can get the intersection of two sets
>>> my_set.intersection(my_other_set)
# We can get the difference of two sets
>>> my_set.difference(my_other_set)

```
</div>

<html>
<details>
<summary><strong>✅ Check your result after testing (no peeking!):</strong></summary>
<div markdown="block"> 
    
```python
>>> my_set = {}
>>> type(my_set)
<class 'dict'>
>>> my_set = set()
>>> type(my_set)
<class 'set'>

>>> my_set = {1, 2, 3}
>>> my_set.add(4)
>>> my_set.remove(2)
>>> 2 in my_set
False

>>> my_set
{1, 3, 4}
>>> my_set.add(3)
>>> my_set
{1, 3, 4}

>>> my_other_set = {1, 2, 3}
>>> my_set.union(my_other_set)
{1, 2, 3, 4}
>>> my_set.intersection(my_other_set)
{1, 3}
>>> my_set.difference(my_other_set)
{4}
```

</div>
</details>
</html>

### Tuples
{: .no_toc }

Tuples are a lightweight way to hold information that describes something, like a person - their name, age, and hometown. You can think about it kind of like a row in a spreadsheet. Tuples are represented inside parentheses, however parentheses are not required to create a tuple, just a sequence of objects followed by commas.

<div class=“task” markdown="block">

Try this:

```python
>>> my_tuple = 1,
>>> my_tuple
# Let's add to our tuple
>>> my_tuple[1] = 2
```

</div>

Oops! Remember that tuples are immutable, so you can't change them once they've been created. Tuples are great for moving data around in a lightweight way, because you can unpack them easily into multiple variables.

<div class=“task” markdown="block">
Try this:
    
```python
>>> person = ('Jim', 29, 'Austin, TX')
>>> name, age, hometown = person
>>> name
>>> age
>>> hometown
```

</div>

<html>
<details>
<summary><strong>✅ Check your result after testing (no peeking!):</strong></summary>
<div markdown="block"> 
    
```python
>>> my_tuple = 1,
>>> my_tuple
(1,)
>>> my_tuple[1] = 2
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
```

```python
>>> person = ('Jim', 29, 'Austin, TX')
>>> name, age, hometown = person
>>> name
'Jim'
>>> age
29
>>> hometown
'Austin, TX'
```

</div>
</details>
</html>

### Dictionaries
{: .no_toc }

Dictionaries are great for storing data that you can index with keys. The keys must be unique, and the dictionaries *are* stored in the order you inserted items, however this is only guaranteed as of Python 3.7.

<div class=“task” markdown="block">

Try this:
    
```python
>>> my_dict = {"key": "value"}
# Remember, dictionaries don't have numerical indexes like lists, so if you try to use an index number...
# Unless 0 happens to be a key.
>>> my_dict[0]
# You'll get a KeyError!

# Let's put some more things into our dictionary
>>> my_dict["hello"] = "world"
>>> my_dict["foo"] = "bar"
>>> my_dict

# What was the value for "hello" again?
>>> my_dict["hello"]
# You can also use get() to get a key
>>> my_dict.get("hello")
# What if the key you want doesn't exist?
>>> my_dict["baz"]
# If you're not sure if a key exists, you can ask:
>>> "baz" in my_dict
# Or you can use a default value. If "baz" doesn't exist, return "boo":
>>> my_dict.get("baz", "boo")

# Let's try separating the dictionary into lists of keys and values:
>>> my_dict.keys()
>>> my_dict.values()

# What if we want to iterate over a dictionary's items? We can use the items() function to get a list of tuples:
>>> my_dict.items()
```
</div>

<html>
<details>
<summary><strong>✅ Check your result after testing (no peeking!):</strong></summary>
<div markdown="block"> 
    
```python
>>> my_dict = {"key": "value"}
>>> my_dict[0]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 0

>>> my_dict["hello"] = "world"
>>> my_dict["foo"] = "bar"
>>> my_dict
{'foo': 'bar', 'hello': 'world', 'key': 'value'}

>>> my_dict["hello"]
'world'
>>> my_dict.get("hello")
'world'
>>> my_dict["baz"]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'baz'
>>> "baz" in my_dict
False
>>> my_dict.get("baz", "default response")
'default response'

>>> my_dict.keys()
['foo', 'hello', 'key']
>>> my_dict.values()
['bar', 'world', 'value']

>>> my_dict.items()
[('foo', 'bar'), ('hello', 'world'), ('key', 'value')]
```

</div>
</details>
</html>

### Mutability
{: .no_toc }

Remember, in Python, some data types are **immutable** -- that means that once they're created, their contents can't be changed. Tuples are immutable - once you make one, you can't alter it, you can only make a new one. Conversely, lists, dictionaries, and sets are mutable - you can change them without making new ones.

<div class=“task” markdown="block">

Let's see this in practice:

```python
# Lists are mutable
>>> my_list = [1, 2, 3]
>>> my_list[0] = 'a'
>>> my_list

# Dictionaries are also mutable
>>> my_dict = {"hello": "world"}
>>> my_dict["foo"] = "bar"
>>> my_dict

# Sets are mutable, but don't support indexing or item assignment, so you have to use add() and remove()
>>> my_set = {1, 2, 3}
>>> my_set[0] = 'a' # This will throw a TypeError
>>> my_set.add('a')
>>> my_set

# Tuples are immutable
>>> my_tuple = (1, 2, 3)
>>> my_tuple[0] = 'a' # This will throw a TypeError
```
</div>

<html>
<details>
<summary><strong>✅ Check your result after testing (no peeking!):</strong></summary>
<div markdown="block"> 
    
```python
>>> my_list = [1, 2, 3]
>>> my_list[0] = 'a'
>>> my_list
['a', 2, 3]

>>> my_dict = {"hello": "world"}
>>> my_dict["foo"] = "bar"
>>> my_dict
{'hello': 'world', 'foo': 'bar'}

>>> my_set = {1, 2, 3}
>>> my_set[0] = 'a'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'set' object does not support item assignment
>>> my_set.add('a')
>>> my_set
{1, 2, 3, 'a'}

>>> my_tuple = (1, 2, 3)
>>> my_tuple[0] = 'a'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
```

</div>
</details>
</html>


---

#### Acknowledgement
{: .no_toc }

Content on this page is adapted from [LearnPython - Nina Zakharenko](https://www.learnpython.dev/).
{: .fs-2 }
