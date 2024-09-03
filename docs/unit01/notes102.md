---
layout: notes
title: "📓1.2: Control Structures" 
parent: "1️⃣ Python Bootcamp"
nav_order: 2
---

## Table of Contents
{: .no_toc .text-delta }

{: .fs-2 }
- TOC
{:toc}

---

## Control Structures: Conditionals & Loops

### The `if` Statement and Conditionals

`if` in Python means: **only run the rest of this code once, *if* the condition evaluates to `True`.** Don't run the rest of the code at all if it's not.

Anatomy of an `if` statement: Start with the `if` keyword, followed by a boolean value, an expression that evaluates to `True`, or a value with "Truthiness". Add a colon `:`, a new line, and write the code that will run if the statement is `True` under a level of indentation.

{{% notice note %}}
Remember, just like with functions, we know that code is associated with an `if` statement *by it's level of indentation*. All the lines indented under the `if` statement will run if it evaluates to `True`.
{{% /notice %}}

```python
>>> if 3 < 5:
...     print("Hello, World!")
...
Hello, World!
```

{{% notice tip %}}
Remember, your `if` statements only run if the expression in them evaluates to `True` and just like with functions, you'll need to enter an extra space in the REPL to run it.
{{% /notice %}}

#### Using `not` With `if` Statements

If you only want your code to run if the expression is `False`, use the `not` keyword.

```python
>>> b = False
>>> if not b:
...     print("Negation in action!")
...
Negation in action!
```

### `if` Statements and Truthiness

`if` statements also work with items that have a "truthiness" to them.

For example:

 * The number 0 is False-y, any other number (including negatives) is Truth-y
 * An empty `list`, `set`, `tuple` or `dict` is False-y
 * Any of those structures with items in it is Truth-y

```python
>>> message = "Hi there."

>>> a = 0
>>> if a:   # 0 is False-y
...     print(message)
...

>>> b = -1
>>> if b:  # -1 is Truth-y
...     print(message)
...
Hi there.

>>> c = []
>>> if c:  # Empty list is False-y
...     print(message)
...

>>> d = [1, 2, 3]
>>> if d:  # List with items is Truth-y
...     print(message)
...
Hi there.
```

### `if` Statements and Functions

You can easily declare `if` statements in your functions, you just need to mindful of the level of indentation. Notice how the code belonging to the `if` statement is indented at *two levels*.

```python
>>> def modify_name(name):
...    if len(name) < 5:
...         return name.upper()
...    else:
...         return name.lower()
...
>>> name = "Nina"
>>> modify_name(name)
'NINA'
```

#### Nested `if` Statements

Using the same technique, you can also *nest* your `if` statements.

```python
>>> def num_info(num):
...    if num > 0:
...        print("Greater than zero")
...        if num > 10:
...            print("Also greater than 10.")
...
>>> num_info(1)
Greater than zero
>>> num_info(15)
Greater than zero
Also greater than 10.
```


#### How *Not* To Use `if` Statements

Remember, comparisons in Python evaluate to `True` or `False`. With conditional statements, we check for that value *implicitly*. In Python, we **do not** want to compare to `True` or `False` with `==`.

{{% notice warning %}}
Warning - pay attention, because the code below shows what you **shouldn't** do.
{{% /notice %}}

```python
# Warning: Don't do this!
>>> if (3 < 5) == True: # Warning: Don't do this!
...     print("Hello")
...
Hello

# Warning: Don't do this!
>>> if (3 < 5) is True: # Warning: Don't do this!
...     print("Hello")
...
Hello
```

{{% notice tip %}}
Do this instead:
{{% /notice %}}

```python
>>> if 3 < 5:
...     print("Hello")
...
Hello
```

If we want to explicitly check if the value is explicitly set to `True` or `False`, we can use the `is` keyword.

```python
>>> a = True        # a is set to True
>>> b = [1, 2, 3]   # b is a list with items, is "truthy"
>>>
>>> if a and b:     # this is True, a is True, b is "truthy"
...     print("Hello")
...
Hello
>>> if a is True:   # we can explicitly check if a is True
...     print("Hello")
...
Hello
>>> if b is True:   # b does not contain the actual value of True.
...     print("Hello")
...
>>>
```

### `else`

The `else` statement is what you want to run **if and only if** your `if` statement wasn't triggered.

An `else` statement is part of an `if` statement. If your `if` statement ran, your `else` statement will never run.


```python
>>> a = True
>>> if a:
...     print("Hello")
... else:
...     print("Goodbye")
...
Hello
```

And vice-versa.

```python
>>> a = False
>>> if a:
...     print("Hello")
... else:
...     print("Goodbye")
...
Goodbye
```

In the REPL it must be written on the line after your last line of indented code. In Python code in a file, there can't be any other code between the `if` and the `else`.

{{% notice info %}}
You'll see `SyntaxError: invalid syntax` if you try to write an `else` statement on its own, or put extra code between the `if` and the `else` in a Python file.
{{% /notice %}}

```python
>>> if a:
...     print("Hello")
...
Hello
>>> else:
  File "<stdin>", line 1
    else:
       ^
SyntaxError: invalid syntax
```

### `elif` Means Else, If.

`elif` means *else if*. It means, **if** this `if` statement isn't considered `True`, try this **instead.**

You can have as many `elif` statements in your code as you want. They get evaluated in the order that they're declared **until** Python finds one that's `True`. That runs the code defined in that `elif`, and skips the rest.

```python
>>> a = 5
>>> if a > 10:
...     print("Greater than 10")
... elif a < 10:
...     print("Less than 10")
... elif a < 20:
...     print("Less than 20")
... else:
...     print("Dunno")
...
Less than 10
```

### While Loops
`while` loops are a special type of loop in Python. Instead of running just once when a condition is met, like an `if` statement, they run **forever** until a condition is *no longer* met.

`while` loops usually need to be accompanied by an always changing sentinel value.

```python
>>> counter = 0
>>> max = 4
>>>
>>> while counter < max:
...     print(f"The count is: {counter}")
...     counter = counter + 1
...
The count is: 0
The count is: 1
The count is: 2
The count is: 3
```

{{% notice warning %}}
Our loop will run forever if we forget to *update* the sentinel value. **Press Ctrl-C to exit the infinite loop.**
{{% /notice %}}


```python
# Warning: don't copy and paste this example.

>>> counter = 0
>>> max = 4

>>> while counter < max:
...     print(f"The count is: {counter}")
...
# What happens if we don't update counter?
The count is: 0
The count is: 0
The count is: 0
The count is: 0
# An infinite loop repeated until we hit Ctrl-C
The count ^CTraceback (most recent call last):
  File "<stdin>", line 2, in <module>
KeyboardInterrupt
```

### For Loops
Looping in Python doesn't look like looping in other languages.

If you write JavaScript, Java, or other languages, you might have seen code that looks something like this code, that keeps track of 3 things: the starting index, the condition the loop will run until, and which action to take (in this case, incrementing the variable `i` by 1) until the condition is met.

```javascript
for (i = 0; i < 5; i++) {
  text += "The number is " + i + "<br>";
}
```

In fact, before these languages introduced something called a `for each` loop, that was also the clunky way you'd loop through items in a sequence.

### Looping in Python

Looping in Python is a simpler, cleaner process because the Python language prides itself on readability.

Remember you used the `in` keyword to test if an item was in a sequence? When combined with the `for` keyword, `in` can be used to indicate looping over each item in the sequence. The syntax is: `for single_item in items`, followed by a colon `:`, followed by a new line, a level of indentation, and the code you'd like to consider as the *body* of the loop. That is, the code that'll run multiple times, until there are no more items in the collection.

Let's see it in action.

```python
>>> colors = ["Red", "Green", "Blue", "Orange"]
>>> for color in colors:
...     print(f"The color is: {color}")
The color is: Red
The color is: Green
The color is: Blue
The color is: Orange
```

#### Looping over a range of numbers

Let's say we wanted to duplicate the code in the example JavaScript above, that prints out the numbers from 0 to 4.

In order to do this, we'll need to use a built-in function called `range()`. The range function in python produces a sequence of integers from an optional and inclusive start, to a defined and exclusive finish.


In Python2, this function created a list of each number in that sequence. As you can imagine, it was horribly inefficient for large ranges. In Python3, the `range()` function returns a new optimized data type. It's great for optimization, but it's harder for debugging.

{{% notice note %}}
If you want to explicitly see what a call to `range()` produces for debugging purposes, you can pass the result into the `list()` method to see all the values at once. For example: `list(range(5))`. Remember that this is inefficient, so use it for testing, not in production code.
{{% /notice %}}

If we wanted to loop over all the values from 0 to 4, we'd use the range function like this:

```python
>>> for num in range(5):
...     print(f"The number is: {num}")
...
The number is: 0
The number is: 1
The number is: 2
The number is: 3
The number is: 4
```

You'll notice that this call didn't *include* the number 5.

What if we wanted the range from 1 to 4, instead of 0 to 4? `range()` can be called with `start` and `stop` parameters, and the range will *start* from `start`.

```python
>>> for num in range(1, 5):
...     print(f"The number is: {num}")
...
The number is: 1
The number is: 2
The number is: 3
The number is: 4
```

You can also pass an a third optional `step` parameter in. Let's say I quickly wanted to print out all the even numbers from 2 to 10. I would call `range(2, 11, 2)`. Remember, 2 is where we're starting, 11 is one higher than where we're ending (10), and 2 is the step, or the amount to jump between numbers.

```python
>>> for num in range(2, 11, 2):
...     print(f"The number is: {num}")
...
The number is: 2
The number is: 4
The number is: 6
The number is: 8
The number is: 10
```

What do inclusive and exclusive mean in this context? *Exclusive* means that the end result *will not* include that number. If you'd like the numbers from 0 to 4, you would call `range(5)`. Consider 5 to the *stopping point*. *Inclusive* means the range will include the number. The `start` parameter is inclusive, meaning if you'd like the range of numbers from 1 to 4, you'd call `range(1, 5)`.

{{% notice tip %}}
If you can't remember how to use range, don't forget to call `help(range)` from the command line.
{{% /notice %}}

#### Looping over items with the index using `enumerate`.

In Python, we avoid writing code like the JavaScript `for` loop at the top, but sometimes it's unavoidable, and we need a way to access the index of the items we're looping through. To do that we use a special function called `enumerate()`. The function takes a sequence, like a `list`, and it *returns* a `list` of tuples, containing the index of the item in the sequence, and the sequence itself.

Don't worry about the list of tuples for now, but remember our tuple unpacking from earlier?

```python
>>> point = (2, 5, 11)
>>> x, y, z = point
>>> x
2
>>> y
5
>>> z
11
```

Because `enumerate()` returns a structure that looks like a list of `tuple`s under the hood, we can take advantage of tuple unpacking in the `for` loop.

```python
>>> for index, item in enumerate(colors):
...     print(f"Item: {item} is at index: {index}.")
...
Item: Red is at index: 0.
Item: Green is at index: 1.
Item: Blue is at index: 2.
Item: Orange is at index: 3.
```

{{% notice tip %}}
Remember, indicies in Python start at zero.
{{% /notice %}}

#### Looping over a dictionary

Now that we know we can use tuple unpacking in a for loop, let's go over how to loop over a dictionary.

Let's say we have a dictionary of colors to their hex color code used for HTML in websites.

```python
>>> hex_colors = {
...     "Red": "#FF",
...     "Green": "#008",
...     "Blue": "#0000FF",
... }
```

{{% notice warning %}}
Remember, a dictionary is composed of key, value pairs. When we loop over a dictionary with the `for item in my_dict` syntax, we'll end up looping over **just** the keys.
{{% /notice %}}

In this example, notice how we're looping over the wrong thing:

```python
>>> for color in hex_colors:
...     print(f"The value of color is actually: {color}")
...
The value of color is actually: Red
The value of color is actually: Green
The value of color is actually: Blue
```

{{% notice tip %}}
If we want to loop over the key, value pairs in a dictionary, we'll want to call `my_dict.items()`.
{{% /notice %}}

We can use tuple unpacking along with the `my_dict.items()` list to loop over both the keys and the values at the same time.

```python
>>> for color, hex_value in hex_colors.items():
...     print(f"For color {color}, the hex value is: {hex_value}")
...
For color Red, the hex value is: #FF0000
For color Green, the hex value is: #008000
For color Blue, the hex value is: #0000FF
```

##### Common Errors

What if you try to loop over key, value pairs, and forget to use `my_dict.items()`?

```python
>>> for color, hex_value in hex_colors:
...     print(f"For color {color}, the hex value is: {hex_value}")
...
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: too many values to unpack (expected 2)
```

{{% notice info %}}
You'll see `ValueError: too many values to unpack (expected 2)` if you *forget* to call `my_dict.items()`, and try to loop over what you'd expect to be key, value pairs.
{{% /notice %}}

#### Additional Resources

If you really want to be a pro at looping in a Pythonic way, I recommend watching Raymond Hettinger's talk - [Transforming Code into Beautiful, Idiomatic Python](https://www.youtube.com/watch?time_continue=1855&v=OSGv2VnC0go) after the course.

`break` and `continue` allow you to control the flow of your loops. They're a concept that beginners to Python tend to misunderstand, so pay careful attention.

### Using `break`

The `break` statement will completely break out of the *current loop*, meaning it won't run any more of the statements contained inside of it.


```python
>>> names = ["Rose", "Max", "Nina", "Phillip"]
>>> for name in names:
...     print(f"Hello, {name}")
...     if name == "Nina":
...         break
...
Hello, Rose
Hello, Max
Hello, Nina
```

{{% notice tip %}}
`break` completely **breaks out** of the loop.
{{% /notice %}}

### Using `continue`

`continue` works a little differently. Instead, it goes back to the start of the loop, skipping over any other statements contained within the loop.

```python
>>> for name in names:
...     if name != "Nina":
...         continue
...     print(f"Hello, {name}")
...
Hello, Nina
```

{{% notice tip %}}
`continue` continues to the **start of the loop**

{{% /notice %}}


### `break` and `continue` visualized

What happens when we run the code from this Python file?

```python
# Python file names.py
names = ["Jimmy", "Rose", "Max", "Nina", "Phillip"]

for name in names:
    if len(name) != 4:
        continue

    print(f"Hello, {name}")

    if name == "Nina":
        break

print("Done!")
```

![break and continue visualized](/02-introduction-to-python/110-control-statements-looping/images/break-continue.png?classes=shadow,border)

#### Results

{{%expand "See if you can guess the results before expanding this section." %}}
```bash
(env) $ python names.py

Hello, Rose
Hello, Nina
Done!
```
{{% /expand%}}

### Using `break` and `continue` in nested loops.

Remember, `break` and `continue` only work for the **current loop**. *Even though I've been programming Python for years, this is something that still trips me up!*

```python
>>> names = ["Rose", "Max", "Nina"]
>>> target_letter = 'x'
>>> for name in names:
...     print(f"{name} in outer loop")
...     for char in name:
...             if char == target_letter:
...                 print(f"Found {name} with letter: {target_letter}")
...                 print("breaking out of inner loop")
...                 break
...
Rose in outer loop
Max in outer loop
Found Max with letter: x
breaking out of inner loop
Nina in outer loop
>>>
```

{{% notice tip %}}
`break` in the inner loop only breaks out of the inner loop! The outer loop continues to run.
{{% /notice %}}


### Loop Control in `while` loops

You can also use `break` and `continue` in `while` loops. One common scenario is running a loop forever, until a certain condition is met.

```python
>>> count = 0 
>>> while True:
...     count += 1
...     if count == 5:
...             print("Count reached")
...             break
...
Count reached
```

{{% notice note %}}
Be careful that your condition will eventually be met, or else your program will get stuck in an infinite loop. For production use, it's better to use asynchronous programming.
{{% /notice %}}

### Loops and the `return` statement

Just like in functions, consider the `return` statement the hard kill-switch of the loop.

```python
>>> def name_length(names):
...     for name in names:
...             print(name)
...             if name == "Nina":
...                     return "Found the special name"
...
>>> names = ["Max", "Nina", "Rose"]
>>> name_length(names)
Max
Nina
'Found the special name'
```

## Exercises
### `if`, `else`, and `elif`

Let's practice our branching statements. Remember that `elif` (short for `else if`) is an optional branch that will let you add another `if` test, and `else` is an optional branch that will catch anything not previously caught by `if` or `elif`.

```python
>>> def test_number(number):
...     if number < 100:
...         print("This is a pretty small number")
...     elif number == 100:
...         print("This number is alright")
...     else:
...         print("This number is huge!")
...
>>> test_number(5)
>>> test_number(99)
>>> test_number(100)
>>> test_number(8675309)
```

{{%expand "Here's what you should have seen in your REPL:" %}}
```python
>>> def test_number(number):
...     if number < 100:
...         print("This is a pretty small number")
...     elif number == 100:
...         print("This number is alright")
...     else:
...         print("This number is huge!")
...
>>> test_number(5)
This is a pretty small number
>>> test_number(99)
This is a pretty small number
>>> test_number(100)
This number is alright
>>> test_number(8675309)
This number is huge!
```
{{%/expand%}}

You can also have multiple conditions in an if statement. This function prints "Fizzbuzz!" if the number is divisible by both 3 and 5 (the `%` or modulo operator returns the remainder from the division of two numbers):

```python
>>> def fizzbuzz(number):
...     if number % 3 == 0 and number % 5 == 0:
...         print("Fizzbuzz!")
...
>>> fizzbuzz(3)
>>> fizzbuzz(5)
>>> fizzbuzz(15)
```

{{%expand "Here's what you should have seen in your REPL:" %}}
```python
>>> def fizzbuzz(number):
...     if number % 3 == 0 and number % 5 == 0:
...         print("Fizzbuzz!")
...
>>> fizzbuzz(3)
>>> fizzbuzz(5)
>>> fizzbuzz(15)
Fizzbuzz!
```
{{%/expand%}}

Let's also practice using `if` to test for an empty list. Remember that an empty list is "Falsey", or resolves to `False`. Write a function to print a list of elements, or an error message if the list is empty. Print a special message if a list item is `None`:

```python
>>> def my_func(my_list):
...     if my_list:
...         for item in my_list:
...             if item is None:
...                 print("Got None!")
...             else:
...                 print(item)
...     else:
...         print("Got an empty list!")
...
>>> my_func([1, 2, 3])
1
2
3
>>> my_func([2, None, "hello", 42])
2
Got None!
hello
42
>>> my_func([])
Got an empty list!
```


## The `for` loop, `range()` and `enumerate()`

Let's try making a list and looping over it:

```python
>>> my_list = [0, 1, 2]
>>> for num in my_list:
...     print(f"Next value: {num}")
...
```


If we're just interested in looping over a list of numbers, we can use the `range()` function instead. Remember that the first argument is inclusive and the second is exclusive:

```python
>>> for num in range(0, 3):
...     print(f"Next value: {num}")
...
```

Another useful function is `enumerate()`, which iterates over an iterable (like a list) and also gives you an automatic counter. `enumerate()` returns a tuple in the form of (`counter`, `item`).

```python
>>> my_list = ["foo", "bar", "baz"]
>>> for index, item in enumerate(my_list):
...     print(f"Item {index}: {item}")
...
```

We can also loop over a dictionary's keys and/or values. If you try to iterate over the dictionary object itself, what do you get?

```python
>>> my_dict = {"foo": "bar", "hello": "world"}
>>> for key in my_dict:
...     print(f"Key: {key}")
...
# This is equivalent to...
>>> for key in my_dict.keys():
...     print(f"Key: {key}")
...
```

The `keys()` method returns the dictionary's keys as a list, which you can then iterate over as you would any other list. This also works for `values()`

```python
>>> for value in my_dict.values():
...     print(f"Value: {value}")
...
```

The most useful function, however, is `items()`, which returns the dictionary's items as tuples in the form of (key, value):

```python
>>> for key, value in my_dict.items():
...     print(f"Item {key} = {value}")
...
```

{{%expand "Here's what you should have seen in your REPL:" %}}
```python
>>> my_list = [1, 2, 3]
>>> for num in my_list:
...     print(f"Next value: {num}")
...
Next value: 0
Next value: 1
Next value: 2
```

```python
>>> for num in range(0, 3):
...     print(f"Next value: {num}")
...
Next value: 0
Next value: 1
Next value: 2
```

```python
>>> my_list = ["foo", "bar", "baz"]
>>> for index, item in enumerate(my_list):
...     print(f"Item {index}: {item}")
...
Item 0: foo
Item 1: bar
Item 2: baz
```

```python
>>> my_dict = {"foo": "bar", "hello": "world"}
>>> for key in my_dict:
...     print(f"Key: {key}")
...
Key: foo
Key: hello

>>> for key in my_dict.keys():
...     print(f"Key: {key}")
...
Key: foo
Key: hello

>>> for value in my_dict.values():
...     print(f"Value: {value}")
...
Value: bar
Value: world

>>> for key, value in my_dict.items():
...     print(f"Item {key} = {value}")
...
Item foo = bar
Item hello = world
```

{{%/expand%}}

## `break`, `continue`, and `return`

`break` and `continue` are important functions for controlling the program flow inside loops. `break` ends the loop immediately and continues executing from outside the loop's scope, and `continue` skips the remainder of the loop and continues executing from the next round of the loop. Let's practice:

```python
>>> for num in range(0, 100):
...     print(f"Testing number {num}")
...     if num == 3:
...         print("Found number 3!")
...         break
...     print("Not yet...")
...
```

Notice that "Not yet..." doesn't get printed for number 3, because we `break` out of the loop first. Let's try a `continue`:

```python
>>> for num in range(0, 100):
...     print(f"Testing number {num}")
...     if num < 3:
...         continue
...     elif num == 5:
...         print("Found number 5!")
...         break
...     print("Not yet...")
...
```

Notice that "Not yet..." doesn't get printed at all until the number is 3, because the `continue` short-circuits the loop back to the beginning. Then we `break` when we hit 5.

You can also use the `return` keyword to break out of a loop within a function, while optionally returning a value.

```python
>>> def is_number_in_list(number_to_check, list_to_search):
...     for num in list_to_search:
...         print(f"Checking {num}...")
...         if num == number_to_check:
...             return True
...     return False
>>> my_list = [1, 2, 3, 4, 5]
>>> is_number_in_list(27, my_list)
>>> is_number_in_list(2, my_list)
```

Notice that our function `is_number_in_list` checks all the numbers in `my_list` on the first run, but on the next run, stops immediately when it hits 3 and returns `True`.

{{%expand "Here's what you should have seen in your REPL:" %}}

```python
>>> for num in range(0, 100):
...     print(f"Testing number {num}")
...     if num == 3:
...         print("Found number 3!")
...         break
...     print("Not yet...")
...
Testing number 0
Not yet...
Testing number 1
Not yet...
Testing number 2
Not yet...
Testing number 3
Found number 3!
>>>
```

```python
>>> for num in range(0, 100):
...     print(f"Testing number {num}")
...     if num < 3:
...         continue
...     elif num == 5:
...         print("Found number 5!")
...         break
...     print("Not yet...")
...
Testing number 0
Testing number 1
Testing number 2
Testing number 3
Not yet...
Testing number 4
Not yet...
Testing number 5
Found number 5!
```

```python
>>> def is_number_in_list(number_to_check, list_to_search):
...     for num in list_to_search:
...         print(f"Checking {num}...")
...         if num == number_to_check:
...             return True
...     return False
...
>>> is_number_in_list(27, my_list)
Checking 1...
Checking 2...
Checking 3...
Checking 4...
Checking 5...
False
>>> is_number_in_list(2, my_list)
Checking 1...
Checking 2...
True
```
{{%/expand%}}

## `while` loop

Instead of looping over a sequence, `while` loops continue looping while a certain condition is met (or not met). The condition is checked at the beginning every iteration.

```python
>>> counter = 0
>>> while counter < 3:
...     print(f"Counter = {counter}")
...     counter += 1
```

Notice that the loop ends once `counter` 3, and the remainder of the loop is bypassed. You can also loop forever by using `while True` or `while False`, but you should make sure you have solid `break` conditions, or your program will just loop forever (unless that's what you want).

```python
>>> counter = 0
>>> while True:
...     print(f"Counter = {counter}")
...     if counter == 3:
...         break
...     counter += 1
```

{{%expand "Here's what you should have seen in your REPL:" %}}

```python
>>> counter = 0
>>> while counter < 3:
...     print(f"Counter = {counter}")
...     counter += 1
...
Counter = 0
Counter = 1
Counter = 2
```

```python
>>> counter = 0
>>> while True:
...     print(f"Counter = {counter}")
...     if counter == 3:
...         break
...     counter += 1
...
Counter = 0
Counter = 1
Counter = 2
Counter = 3
```

{{%/expand%}}

## Nested Loops

Nesting loops is often necessary and sometimes tricky. The `break` keyword will only get you out of whichever loop you're `break`ing. The only way to exit all loops is with multiple `break` statements (at each level), or the `return` keyword (inside a function). For example:

```python
names = ["Rose", "Max", "Nina"]
target_letter = 'x'
found = False

for name in names:
    for char in name:
            if char == target_letter:
                    found = True
                    break

    if found:
        print(f"Found {name} with letter: {target_letter}")
        break
```

Or:

```python
>>> for x in range(0, 5):
...     for y in range(0, 5):
...         print(f"x = {x}, y = {y}")
...         if y == 2:
...             break
...
```

Notice how the inner `y` loop never gets above 2, whereas the outer `x` loop continues until the end of its range.

{{%expand "Here's what you should have seen in your REPL:" %}}
```python
>>> for x in range(0, 5):
...     for y in range(0, 5):
...         print(f"x = {x}, y = {y}")
...         if y == 2:
...             break
...
x = 0, y = 0
x = 0, y = 1
x = 0, y = 2
x = 1, y = 0
x = 1, y = 1
x = 1, y = 2
x = 2, y = 0
x = 2, y = 1
x = 2, y = 2
x = 3, y = 0
x = 3, y = 1
x = 3, y = 2
x = 4, y = 0
x = 4, y = 1
x = 4, y = 2
```
{{%/expand%}}


---

#### Acknowledgement
{: .no_toc }

Content on this page is adapted from [LearnPython - Nina Zakharenko](https://www.learnpython.dev/).
{: .fs-2 }
