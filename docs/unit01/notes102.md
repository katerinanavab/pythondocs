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

#### USING A GITHUB CODESPACE TO TAKE CLASS NOTES
{:.no_toc}

<div class="setup" markdown="block">

1. Go to GitHub and click on your picture in the _TOP RIGHT_ corner
2. Select `Your repositories`
3. Open `CS3-Unit1-Notes`
5. Now on your repository, click <button type="button" name="button" class="btn btn-green"> < > Code </button> and select the `Codespaces` tab
6. Click `Create Codespace on main` (unless you already have one listed there), wait for the environment to load, _then you're ready to code_!
7. 📝 Take notes in this Codespace during class, coding along with the instructor.

</div>

<br>

<div class="warn" markdown="block">

🛑 When class ends, don't forget to **SAVE YOUR WORK**! _There are multiple steps to saving in GitHub:_

1. Navigate to the `Source Control` menu on the _LEFT_ sidebar
2. Click the <button type="button" name="button" class="btn btn-green">commit changes</button> button on the _LEFT_ menu
3. Type a brief **commit message** at the top of the file that opens, for example: `updated main.py`
4. Click the small `✔️` **checkmark** in the _TOP RIGHT_ corner
5. Click the <button type="button" name="button" class="btn btn-green">sync changes</button> button on the _LEFT_ menu
6. _Finally you can close your Codespace!_

</div>


## Boolean Logic

### Truthiness
{:.no_toc}

Evaluating an expression to be `True` or `False` will help us control the flow of our program.


| type                                        	| truthiness                                                                     	|  
|---------------------------------------------	|--------------------------------------------------------------------------------	|
| `int`                                       	| `0` is `False`, all other numbers are `True` (including negative)              	|   	
| containers - `list`, `tuple`, `set`, `dict` 	| empty container evaluates to `False`, container with items evaluates to `True`) |   	
| `None`                                      	| `False`                                                                        	|   	

We talked about `boolean` types, `True` and `False` earlier. `True` and `False` are keywords in Python, so make sure you don't name your variables the same thing.

Sometimes the truth is obvious. For example `3 < 5` is always `True`. Other times, in Python, the truth value might surprise you. Let's review. First, let's start with an expression we know is always `True`.

```python
>>> 3 < 5
True
```

{:.highlight}
**TIP:** If you want to test your assumptions about an expression that returns `True` or `False`, you can pass it into the **constructor** for `bool`eans: `bool(expression)`.

### Numbers
{:.no_toc}

In Python, the integer `0` is always `False`, while every other number, *including negative numbers*, are `True`. In fact, under the hood, `bool`eans inherit from `int`egers.

```python
>>> bool(0)
False
>>> bool(1)
True
>>> bool(-1)
True
```

### Sequences
{:.no_toc}

Empty sequences in Python always evaluate to `False`, **including empty `str`ings.**

```python
>>> bool("")    # String
False
>>> bool([])    # Empty List
False
>>> bool(set()) # Empty Set
False
>>> bool({})    # Empty Dictionary
False
>>> bool(())    # Empty Tuple
False
```

Sequences with at least one value will evaluate to `True`.

```python
>>> bool("Hello")   # String
True
>>> bool([1])       # List
True
>>> bool({1})       # Set
True
>>> bool({1: 1})    # Dictionary
True
>>> bool((1,))      # Tuple
True
```

### `None`
{:.no_toc}

The `None` type in Python represents nothing. No returned value. It shouldn't come as a surprise that the truthiness of `None` is `False`.

```python
>>> bool(None)
False
```

`None` is commonly used as a placeholder to mean *"I haven't set this value yet."* Since empty `str`ings and sequence evaluate to `False`, we need to be very careful when we're checking if a sequence has been *declared* or not, or if it's *empty*.   We'll review this concept again when talking about `if` statements later in the day.

```python
>>> my_name = None
>>> bool(my_name)
False
>>> my_name = ""
>>> bool(my_name)
False

>>> my_list = None
>>> bool(my_list)
False
>>> my_list = []
>>> bool(my_list)
False
```

### Comparison Operators: `<`, `<=`,`>`, `>=`

|Operator|Means|
|---|---|
|`<`|less-than|
|`<=`|less-than-or-equal-to|
|`>`|greater-than|
|`>=`|greater-than-or-equal-to|

In Python, comparing numbers is pretty straight forward.

<div class="task" markdown="block">

Test the following operations: 

```python
>>> 10 > 5
>>> 5 > 10
>>> 10 > 10
>>> 10 >= 10
>>> 5 < 10
>>> 5 < 5
>>> 5 <= 5
>>> 5 == 5
>>> 5 != 10
```

</div>

<html>
<details>
<summary><strong>✅ Check your result after testing (no peeking!):</strong></summary>
<div markdown="block"> 
  
```python
>>> 10 > 5
True
>>> 5 > 10
False
>>> 10 > 10
False
>>> 10 >= 10
True
>>> 5 < 10
True
>>> 5 < 5
False
>>> 5 <= 5
True
>>> 5 == 5
True
>>> 5 != 10
True
```

</div>
</details>
</html>

Things get interesting when you try to compare strings. Strings are compared lexicographically. That means by the ASCII value of the character. You don't need to know much about ASCII, besides that capital letters come before lower case ones.

Each character in the two strings is checked one by one, until a character is found that is of a different value. That determines the order. Under the hood, this allows Python to sort strings by comparing them to each other.

```python
>>> "T" < "t"  # Upper case letters are "lower" valued.
True
>>> "a" < "b"
True
>>> "bat" < "cat"
True
```

### Checking Equality: `==`, `!=`

|Operator|Means|
|---|---|
|`==`|equals|
|`!=`|not-equals|

The equality operators `val1 == val2` *(`val1` equals `val2`)* and `val1 != val2` *(`val1` doesn't equal `val2`)* compare the contents of two different values and return a `bool`ean.

Equality works like you'd expect it to for simple data types.

```python
>>> a = 1
>>> b = 1
>>> a == b
True
>>> a != b
False

>>> a = "Nina"
>>> b = "Nina"
>>> a == b
True
>>> a != b
False
```

Equality for container types is interesting. Even though `a` and `b` are two different `list`s, their contents are still the same. So compared two lists containing the same values with `==` will return `True`.

```python
>>> a = [1, 2, 3]
>>> b = [1, 2, 3]
>>> a == b
True
>>> a != b
False
```

### Checking Identity: `is`, `is not`

|Operator|Means|
|---|---|
|`is`| *is* the same object in memory? (not equality!)|
|`is not`| *is not* the same object in memory? (not equality!)|

{:.highlight}
This is something that trips up Python beginners, so make sure you remember that *equality* (`==`, `!=`) **is not** the same as *identity* (`is`, `not is`).

The `is` keywords tests if the two compared objects are stored in the same memory location. I won't go into too much detail into why, but remember **not** to use `is` when what you actually want to check for is equality.

```python
>>> a = [1, 2, 3]
>>> b = [1, 2, 3]

>>> a == b  # Testing for equality. a and b contain the same values
True
>>> a is b  # Testing for identity. a and b are NOT the same object.
False
```

{:.highlight}
When you're first starting out, the only place you'll want to use the `is` keyword is to explicitly compare a value to the built-in types of `None`, `True`, or `False`.

```python
>>> a = True
>>> a is True
True

>>> b = False
>>> b is False
True
>>> b is not True   # Opposite of is b True. aka is b False?
True

>>> c = None
>>> c is None
True
>>> c is not None
False
```

### Compound Operators: `and`, `or`, `not`
`and`, `or`, and `not` are the three basic types of boolean operators that are present in math, programming, and database logic.

In other programming languages, you might have seen the concept of `and` represented with `&&`, `or`, represented with `||`, and `not` represented by `!`. The Python language is instead focused on readability. So we'll use the english `and` instead of trying to remember fancy symbols. Python still uses the `&`, `|` and `!` expressions, but they're used for bitwise operations.

You can use them to compare one (or more expressions) and determine if they evaluate to `True` or `False`.

Thankfully, you don't have to be a computer scientist to understand them if you use this handy table.

|Operation|Result|
|---|---|
|`a or b`|if a is False, then b, else a|
|`a and b`|if a is False, then a, else b|
|`not a`|if a is false, then `True`, else `False`|


#### `and` table
{:.no_toc}

<!--
| a       	| b       	| a `and` b  	|
|---------	|---------	|------------	|
| `True`  	| `True`  	| **`True`** 	|
| `True`  	| False 	| False    	|
| False 	| `True`  	| False    	|
| False 	| False 	| False    	|
-->

{:.highlight}
For `a and b`, if a is false, a is returned. Otherwise b is returned.
*If `a and b` are both `bool`ean values, the expression evaluates to`True` if both a and b are `True`.*

```python
>>> a = True    # a is True
>>> b = True
>>> a and b     # True is returned. (value of b)
True

>>> a = False   # a is False
>>> b = True
>>> a and b     # False is returned. (value of a)
False

>>> a = False   # a is False
>>> b = False
>>> a and b     # False is returned. (value of a)
False
```

Notice what happens when do the same thing to values that have a "truthiness" to them.

```python
>>> bool(0) # Verify that zero is "falsey"
False
>>> bool(1) # Verify that one is "truthy"
True
>>> 0 and 1 # 0 is False. 0 is returned.
0
```

#### `or` table
{:.no_toc}

| a       	| b       	| a `or` b   	|
|---------	|---------	|------------	|
| `True`  	| `True`  	| **`True`** 	|
| `True`  	| `False` 	| **`True`** 	|
| `False` 	| `True`  	| **`True`** 	|
| `False` 	| `False` 	| **`False`** |


{:.highlight}
For `a or b`, if a is false, b is returned. If a is true, a is returned.
*`a or b` evaluates to `True` if either (or both) of the expressions are true.*

```python
>>> a = True    # a is true
>>> b = True
>>> a or b      # True is returned (value of a)
True

>>> a = False   # a is false
>>> b = True
>>> a or b      # True is returned (value of b)
True

>>> 0 or 1      # 0 is false. Return 1.
1
```

#### `not` table
{:.no_toc}

| a       	| `not` a    	|
|---------	|------------	|
| true  	| False    	|
| false 	| **`True`** 	|


{:.highlight}
`not a` reverses the `bool`ean value of `a`. If it *was* true, it will return `False`. If it was false, it will return `True`.

```python
>>> a = True
>>> not a  # not returns the opposite. True -> False
False

>>> a = False
>>> not a  # not returns the opposite. False -> True
True
```

And again, with numbers. Remember, zero is considered `False`, any other number is considered `True`.

```python
>>> bool(1)
True
>>> not 1
False
>>> bool(0)
False
>>> not 0
True
```

#### In Combination
{:.no_toc}

When combining multiple boolean operators, you can add optional parenthesis for readability.

```python
>>> a = True
>>> b = True
>>> c = False

>>> a and (b or c)
True
```

You can combine multiple operators to test complex assumptions. For example, to return `True` only if *both* values are `False`, we can use the `not` negation operation on the result of an `or`.

```python
>>> a = False
>>> b = False

>>> a or b  # False because both are False.
False

>>> not (a or b)  # True - checking if both are False.
True
```

#### With "truthiness"
{:.no_toc}

Remember, we learned that some values in Python are *falsey* like the number zero, and some are *truthy* like any number *expect* for zero.

It's a little counter intuitive, but when we compare values other than `bool`eans, our code behaves a little differently.

|Operation|Result|
|---|---|
|`x or y`|if x is false, then y, else x|
|`x and y`|if x is false, then x, else y|

Let's see it in action. First, lets test our assumptions again.

```python
>>> bool(0)     # Truthiness of 0 is False
False

>>> bool(1)     # Truthiness of 1 is True
True

>>> bool(None)  # Truthiness of None type is False
False

>>> 1 or 0      # Returns 1, the True value
1

>>> 1 and 0     # Returns 0, the False value
0

>>> 0 or None   # Neither are True. Returns nothing (None)
```

### ⭐️ Practice

#### Truthiness
{:.no_toc}

Different languages have different ideas of what is "truthy" and "falsy." In Python, all objects can be tested for truth, and an object is considered True unless except under certain circumstances that we talked about earlier in the chapter. Remember that checking if an object is "equal" to another object doesn't necessarily mean the same thing. An object is considered "truthy" if it satisfies the check performed by `if` or `while` statements.

<div class="task" markdown="block">

Let's try a few of these out:

```python
>>> 5 == True
>>> # The number 5 does not equal True, but...
>>> if 5:
...     print("The number 5 is truthy!")
...
>>> # The number 5 is truthy for an if test!
```

`True` and `False` can also be represented by 1 and 0:

```python
>>> 1 == True
>>> 0 == False
```

</div>

<html>
<details>
<summary><strong>✅ Check your result after testing (no peeking!):</strong></summary>
<div markdown="block"> 
  
```python
>>> 5 == True
False
>>> # The number 5 does not equal True, but...
>>> if 5:
...     print("The number 5 is truthy!")
...
The number 5 is truthy!
>>> # The number 5 is truthy for an if test!
```

```python
>>> 1 == True
True
>>> 0 == False
True
```
</div>
</details>
</html>

#### Boolean Operators
{:.no_toc}

Python also supports boolean operators, although they're a little different than the comparison operators. Remember that `or` and `and` return one of their operands, rather than `True` or `False`.

|Operation|Result|
|---|---|
|`x or y`|if x is false, then y, else x|
|`x and y`|if x is false, then x, else y|
|`not x`|if x is false, then `True`, else `False`|

<div class="task" markdown="block">

Test the following operations: 

```python
>>> True or False
>>> [] or [1, 2, 3]
>>> "Hello" or None
```

```python
>>> True and False
>>> 5 and 0
>>> [1] and [1, 2, 3]
>>> "Hello" and None
```

```python
# Of course, you can use `and` and `or` aren't limited to two operands
>>> a = False
>>> b = False
>>> c = False
>>> a or b or c
>>> b = True
>>> a or b or c

>>> a and b and c
>>> a = True
>>> c = True
>>> a and b and c
```

</div>

<html>
<details>
<summary><strong>✅ Check your result after testing (no peeking!):</strong></summary>
<div markdown="block"> 

```python
>>> True or False
True
>>> [] or [1, 2, 3]
[1, 2, 3]
>>> "Hello" or None
'Hello'
```

```python
>>> True and False
False
>>> 5 and 0
0
>>> [1] and [1, 2, 3]
[1, 2, 3]
>>> "Hello" and None
>>> # No output, since the result was None
```

```python
>>> a = False
>>> b = False
>>> c = False
>>> a or b or c
False
>>> b = True
>>> a or b or c
True

>>> a and b and c
False
>>> a = True
>>> c = True
>>> a and b and c
True
```

</div>
</details>
</html>

---

## Control Structures: Conditionals

### The `if` Statement and Conditionals
{:.no_toc}

`if` in Python means: **only run the rest of this code once, *if* the condition evaluates to `True`.** Don't run the rest of the code at all if it's not.

Anatomy of an `if` statement: Start with the `if` keyword, followed by a boolean value, an expression that evaluates to `True`, or a value with "Truthiness". Add a colon `:`, a new line, and write the code that will run if the statement is `True` under a level of indentation.

{:.highlight}
Remember, just like with functions, we know that code is associated with an `if` statement *by it's level of indentation*. All the lines indented under the `if` statement will run if it evaluates to `True`.

```python
>>> if 3 < 5:
...     print("Hello, World!")
...
Hello, World!
```

{:.highlight}
Remember, your `if` statements only run if the expression in them evaluates to `True` and just like with functions, you'll need to enter an extra space in the REPL to run it.

#### Using `not` with `if` Statements
{:.no_toc}

If you only want your code to run if the expression is `False`, use the `not` keyword.

```python
>>> b = False
>>> if not b:
...     print("Negation in action!")
...
Negation in action!
```

### `if` Statements and Truthiness
{:.no_toc}

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

### `if` Statements inside Functions

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
{:.no_toc}

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
{:.no_toc}

Remember, comparisons in Python evaluate to `True` or `False`. With conditional statements, we check for that value *implicitly*. In Python, we **do not** want to compare to `True` or `False` with `==`.

{:.warning}
Watch out, because the code below shows what you **SHOULD NOT** do!

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

{:.highlight}
Do this instead:

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

### `else` Statements

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

{:.highlight}
You'll see `SyntaxError: invalid syntax` if you try to write an `else` statement on its own, or put extra code between the `if` and the `else` in a Python file.

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

### `elif` (Else, If) Statements

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

---

## Control Structures: Iteration

### `while` Loops
`while` loops are a special type of loop in Python. Instead of running just once when a condition is met, like an `if` statement, they run **forever** until a condition is *no longer* met.

`while` loops usually need to be accompanied by an **always-changing sentinel value**, which acts like a flag 🚩.

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

{:.warning}
♾️ A loop will run forever if we forget to *update* the sentinel value, like we did with `counter = counter + 1`. 

### `for in` Loops
Looping in Python doesn't look like looping in other languages.

If you write JavaScript, Java, or other languages, you might have seen code that looks something like this code below, that keeps track of 3 things: the **starting** **index**, the **condition** the loop will run until, and which **action** to take (in this case, incrementing the variable `i` by 1) until the condition is met.

```javascript
for (i = 0; i < 5; i++) {
  text += "The number is " + i + "<br>";
}
```

> In fact, before these languages introduced something called a `for each` loop, that was also the clunky way you'd loop through items in a sequence.

Looping in Python is a simpler, cleaner process because the Python language prides itself on **readability**.

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

#### Looping over a `range()` of numbers

Let's say we wanted to duplicate the code in the example JavaScript above, that prints out the numbers from 0 to 4.

In order to do this, we'll need to use a built-in function called `range()`. The range function in python produces a sequence of integers from an optional and inclusive start, to a defined and exclusive finish.

> In Python2, this function created a list of each number in that sequence. As you can imagine, it was horribly inefficient for large ranges. In Python3, the `range()` function returns a new optimized data type. It's great for optimization, but it's harder for debugging.

{:.highlight}
If you want to explicitly see what a call to `range()` produces for debugging purposes, you can pass the result into the `list()` method to see all the values at once. For example: `list(range(5))`. Remember that this is inefficient, so use it for testing, not in production code.

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

{:.highlight}
If you can't remember how to use range, don't forget to call `help(range)` from the command line.

#### Looping over items with the index using `enumerate()`

In Python, we avoid writing code like the JavaScript `for` loop at the top, but sometimes it's unavoidable, and we need a way to access the index of the items we're looping through. To do that we use a special function called `enumerate()`. The function takes a sequence, like a `list`, and it *returns* a `list` of tuples, containing the index of the item in the sequence, and the sequence itself.

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

{:.highlight}
Remember, indicies in Python start at zero.

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

{:.warning}
Remember, a dictionary is composed of `key, value` pairs. When we loop over a dictionary with the `for item in my_dict` syntax, we'll end up looping over **just** the keys.

In this example, notice how we're looping over the wrong thing:

```python
>>> for color in hex_colors:
...     print(f"The value of color is actually: {color}")
...
The value of color is actually: Red
The value of color is actually: Green
The value of color is actually: Blue
```

{:.highlight}
If we want to loop over the key, value pairs in a dictionary, we'll want to call `my_dict.items()`.

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
{:.no_toc}

What if you try to loop over key, value pairs, and forget to use `my_dict.items()`?

```python
>>> for color, hex_value in hex_colors:
...     print(f"For color {color}, the hex value is: {hex_value}")
...
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: too many values to unpack (expected 2)
```

{:.highlight}
You'll see `ValueError: too many values to unpack (expected 2)` if you *forget* to call `my_dict.items()`, and try to loop over what you'd expect to be key, value pairs.

### Using `break` and `continue`

`break` and `continue` allow you to control the flow of your loops. They're a concept that beginners to Python tend to misunderstand, so pay careful attention.

#### Using `break`
{:.no_toc}

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

{:.highlight}
`break` completely **breaks out** of the loop.

#### Using `continue`
{:.no_toc}

`continue` works a little differently. Instead, it goes back to the start of the loop, skipping over any other statements contained within the loop.

```python
>>> for name in names:
...     if name != "Nina":
...         continue
...     print(f"Hello, {name}")
...
Hello, Nina
```

{:.highlight}
`continue` continues to the **start of the loop**

#### `break` and `continue` visualized
{:.no_toc}

<div class="task" markdown="block">

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

</div>

<html>
<details>
<summary><strong>✅ Check your result after testing (no peeking!):</strong></summary>
<div markdown="block"> 

```bash
(env) $ python names.py

Hello, Rose
Hello, Nina
Done!
```
</div>
</details>
</html>

### Using `break` and `continue` in nested loops
{:.no_toc}

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

{:.highlight}
`break` in the inner loop only breaks out of the inner loop! The outer loop continues to run.

#### Loop Control in `while` loops
{:.no_toc}

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

{:.highlight}
Be careful that your condition will eventually be met, or else your program will get stuck in an infinite loop. For production use, it's better to use asynchronous programming.

#### Loops and the `return` statement
{:.no_toc}

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

### ⭐️ Practice

#### `if`, `else`, and `elif`
{:.no_toc}

Let's practice our branching statements. Remember that `elif` (short for `else if`) is an optional branch that will let you add another `if` test, and `else` is an optional branch that will catch anything not previously caught by `if` or `elif`.

<div class="task" markdown="block">

Test the following code: 

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

</div>

<html>
<details>
<summary><strong>✅ Check your result after testing (no peeking!):</strong></summary>
<div markdown="block"> 
  
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
</div>
</details>
</html>

You can also have **multiple conditions** in an if statement. This function prints "Fizzbuzz!" if the number is divisible by both 3 and 5 (the `%` or modulo operator returns the remainder from the division of two numbers):

<div class="task" markdown="block">

Test the following code: 

```python
>>> def fizzbuzz(number):
...     if number % 3 == 0 and number % 5 == 0:
...         print("Fizzbuzz!")
...
>>> fizzbuzz(3)
>>> fizzbuzz(5)
>>> fizzbuzz(15)
```

</div>

<html>
<details>
<summary><strong>✅ Check your result after testing (no peeking!):</strong></summary>
<div markdown="block"> 

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
</div>
</details>
</html>

#### The `for` loop, `range()` and `enumerate()`
{:.no_toc}

<div class="task" markdown="block">

Let's try making a list and looping over it:

```python
>>> my_list = [0, 1, 2]
>>> for num in my_list:
...     print(f"Next value: {num}")
...
```

</div>

<div class="task" markdown="block">

If we're just interested in looping over a list of numbers, we can use the `range()` function instead. Remember that the first argument is inclusive and the second is exclusive:

```python
>>> for num in range(0, 3):
...     print(f"Next value: {num}")
...
```

</div>

Another useful function is `enumerate()`, which iterates over an iterable (like a list) and also gives you an automatic counter. `enumerate()` returns a tuple in the form of (`counter`, `item`).

```python
>>> my_list = ["foo", "bar", "baz"]
>>> for index, item in enumerate(my_list):
...     print(f"Item {index}: {item}")
...
```

<div class="task" markdown="block">

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

</div>

<div class="task" markdown="block">

The `keys()` method returns the dictionary's keys as a list, which you can then iterate over as you would any other list. This also works for `values()`

```python
>>> for value in my_dict.values():
...     print(f"Value: {value}")
...
```

</div>

<div class="task" markdown="block">

The most useful function, however, is `items()`, which returns the dictionary's items as tuples in the form of `(key, value)`:

```python
>>> for key, value in my_dict.items():
...     print(f"Item {key} = {value}")
...
```

</div>

<html>
<details>
<summary><strong>✅ Check your result after testing (no peeking!):</strong></summary>
<div markdown="block"> 
  
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

</div>
</details>
</html>

#### `break`, `continue`, and `return`
{:.no_toc}

`break` and `continue` are important functions for controlling the program flow inside loops. `break` ends the loop immediately and continues executing from outside the loop's scope, and `continue` skips the remainder of the loop and continues executing from the next round of the loop. 

<div class="task" markdown="block">

Let's practice:

```python
>>> for num in range(0, 100):
...     print(f"Testing number {num}")
...     if num == 3:
...         print("Found number 3!")
...         break
...     print("Not yet...")
...
```

</div>

> Notice that "Not yet..." doesn't get printed for number 3, because we `break` out of the loop first. Let's try a `continue`:

<div class="task" markdown="block">
Try this:
  
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

</div>

> Notice that "Not yet..." doesn't get printed at all until the number is 3, because the `continue` short-circuits the loop back to the beginning. Then we `break` when we hit 5.

<div class="task" markdown="block">

You can also use the `return` keyword to break out of a loop within a function, while optionally returning a value:

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

</div>

> Notice that our function `is_number_in_list` checks all the numbers in `my_list` on the first run, but on the next run, stops immediately when it hits 3 and returns `True`.

<html>
<details>
<summary><strong>✅ Check your result after testing (no peeking!):</strong></summary>
<div markdown="block"> 
  
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
</div>
</details>
</html>

#### `while` loop
{:.no_toc}

Instead of looping over a sequence, `while` loops continue looping while a certain condition is met (or not met). The condition is checked at the beginning every iteration.

<div class="task" markdown="block">
Try this code:
  
```python
>>> counter = 0
>>> while counter < 3:
...     print(f"Counter = {counter}")
...     counter += 1
```

> Notice that the loop ends once `counter` 3, and the remainder of the loop is bypassed. You can also loop forever by using `while True` or `while False`, but you should make sure you have solid `break` conditions, or your program will just loop forever (unless that's what you want).

<div class="task" markdown="block">

Try this code:

```python
>>> counter = 0
>>> while True:
...     print(f"Counter = {counter}")
...     if counter == 3:
...         break
...     counter += 1
```

</div>

<html>
<details>
<summary><strong>✅ Check your result after testing (no peeking!):</strong></summary>
<div markdown="block"> 
  
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

</div>
</details>
</html>

#### Nested Loops
{:.no_toc}

Nesting loops is often necessary and sometimes tricky. The `break` keyword will only get you out of whichever loop you're `break`ing. The only way to exit all loops is with multiple `break` statements (at each level), or the `return` keyword (inside a function). For example:

<div class="task" markdown="block">

Practice nesting loops:

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

</div>

> Notice how the inner `y` loop never gets above 2, whereas the outer `x` loop continues until the end of its range.

<html>
<details>
<summary><strong>✅ Check your result after testing (no peeking!):</strong></summary>
<div markdown="block"> 

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

</div>
</details>
</html>

---

#### Acknowledgement
{: .no_toc }

Content on this page is adapted from [LearnPython - Nina Zakharenko](https://www.learnpython.dev/).
{: .fs-2 }
