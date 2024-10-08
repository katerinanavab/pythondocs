---
layout: default
title: "🐞 Debugging Tips" 
parent: References
nav_order: 2
---

# 🐞 Debugging Scenarios & Solutions
{:.no_toc}

<a name="top"></a>

### Quick debugging tips:
{:.no_toc}
* Read the error message and look at the line that it refers to.
    * Sometimes the issue is at the line just ⬆ **above** the line that was listed in the error.
    * If enabled, pay close attention to the **syntax highlighting** in your editor, which can point at where the error might be happening.
* Use `print()` statements to display the type and value of your variable.
* Go back to the instructions and carefully re-read them.
* Use [Python Tutor to visualize your code](https://pythontutor.com/visualize.html#mode=edit).
* Use the [Rubber Duck Debugging](https://rubberduckdebugging.com) to walk yourself through the logic of your code.
* If you are having trouble with your output not matching what is expected, use an online text comparison tool, e.g. <https://text-compare.com> or <https://contenttool.io/text-difference-checker>.

---

#### Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Common Error Messages

### `AttributeError: '...' object has no attribute '...'`

Example errors:
* `AttributeError: 'int' object has no attribute 'isdigit'`
* `AttributeError: 'list' object has no attribute 'split'`

*   Example erroneous code:
```py
my_int = 42
if my_int.isdigit():
    my_float = float(my_int)
```
*   **Cause**: A variable of one type is trying to use a method from a different (incompatible) type.
*   **Check**: verify the type of the object that is listed before the `.` in the `.method()` call.
    * Either change it to the type that the method works with (see example)
    * Use another method/solution that works with the original object type (e.g., for strings stored in a list, you might need to iterate through each element of a list and use `split()` on the string element

*   Corrected line of code: 
```py
my_int = "42"
if my_int.isdigit():
    my_float = float(my_int)
```

---

### `EOFError: EOF when reading a line`

* **Cause**: 
    * Python is expecting an input but there is no input to provide. 
    * Alternatively, there might be a missing closing parenthesis (see [`SyntaxError: unexpected EOF while parsing`](#syntaxerror-unexpected-eof-while-parsing)). 
    * If the error is produced when using a loop, check that you do not have an infinite loop. Look closely at the loop's conditions and verify that the loop stops, especially, in the edge cases.
    * In almost all cases, `input()` should be included inside the **main program**, _not_ inside the functions.

* The program instructions might be providing 1 input value, but you have an extra `input()` in your code.
```py
num_items = int(input())
item = input()
```
but the input is just a single number, there's no `item` to provide via `input()`.

* An infinite loop example - `num_items` doesn't get updated _within the loop_, so the condition stays always `True` (unless `num_items == 0` and the loop is not executed):
```py
num_items = int(input())
items = []
while num_items:
    item = input("Enter an item: ")
    items.append(item)
```

[⬆️ BACK TO TOP](#top)

---

### `SyntaxError: unexpected EOF while parsing`

*   **Cause**:  Missing a closing parenthesis `)`.
*   Example erroneous code:
```py
print('Hello, World'
```
*   Corrected line of code: 
```py
print("Hello, World")
```

[⬆️ BACK TO TOP](#top)

---

### `EOL while scanning string literal`

*   **Cause**:   Missing a **closing** quotation mark or a mismatched quotation mark (incorrectly placed quotation can also cause it).
*   Example erroneous code:
```py
print('Hello, World) # missing a quotation mark
```
or
```py
print('Hello, World") # mismatched quotation marks
```

[⬆️ BACK TO TOP](#top)

---

### `IndentationError: unexpected indent`
*   Example erroneous code:
```py
print("Hello world!")
    print("What a nice day!")
```
*   **Cause**:   The code is either indented even though it is not necessary or is missing an indentation. The line number in the error points at where the mismatch happened.
*   Correct code: 
```py
print("Hello world!")
print("What a nice day!")
```

[⬆️ BACK TO TOP](#top)

---

### `IndentationError: expected an indented block`

*   Example erroneous code:
```py
def print_hello():
"""Print a simple greeting."""
print("Hello!")
```

* **Cause**: This error occurs if the previous line ended with a colon `:` and did not have a properly indented line of code underneath it. It is likely that the issue occured at the line directly above the line reported in the error.
*   Correct code (notice the indentation after the line that ends with a colon):
```py
def print_hello():
    """Print a simple greeting."""
    print("Hello!")
```

[⬆️ BACK TO TOP](#top)

---

### `IndexError: ... index out of range`

Example errors:
* `IndexError: string index out of range`
* `IndexError: list index out of range`

* Example code that causes the error:

```py
my_str = ""
print("The first symbol is", my_str[0])
print("The last symbol is", my_str[-1])
```

* **Cause**: The string/list is being indexed at a location that does not exist.
* **Check**: Print the length of the string/list to check its maximum index (remember that Python indexing starts at 0).

* Correct code that won't cause the error: 

```py
my_str = ""
if len(my_str) != 0: # my_str != ""
    print("The first symbol is", my_str[0])
    print("The last symbol is", my_str[-1])
```

[⬆️ BACK TO TOP](#top)

---

### `KeyError: ...` with a dictionary

This error occurs when working with dictionaries. The line above the error shows which line caused the incorrect retrieval.

* Example erroneous code:

```py
month_names = {
    "1": "January",
    "2": "February",
}
print("First month is", month_names[1]) # KeyError: 1
```

Alternatively, you wouldn't get an error but would get an undesired output that displays `None` if using `.get()`:

```py
print("First month is", month_names.get(1)) # results in "First month is None"
```

*   **Cause**: This error occurrs when trying to retrieve a value using a key that doesn't exist in the dictionary. Possible causes:
    * the dictionary does not store the correct key-value pairs (did you add all necessary items? what about the edge cases?)
    * the key is stored / retrieved as an incorrect type (see the example)

* Correct code (alternative options): 

```py
...
print("First month is", month_names["1"])
print("First month is", month_names.get("1"))
print("First month is", month_names[str(1)])
```

[⬆️ BACK TO TOP](#top)

---

### `NameError: name '...' is not defined`

Python would replace the ellipsis `...` with the name of the variable that it's unable to find.
*   **Cause**:   Generally, this error happens when a function name or a variable name 
    * is misspelled 
    * has not been properly defined first

For example:

`NameError: name 'Print' is not defined`
* Example erroneous code:
```py
Print('Hello, World')
```
*   **Cause**:   In this case, the function name is "misspelled" - an accidentally capitalized name of the function makes Python look for a variable called `Print`.    


This error can also be caused if there is a **single word** (or comma-separated words) inside the `print()` that needed to be displayed as the literal text but does not include quotation marks around it (similar to the `SyntaxError: invalid syntax`).

*   Example erroneous code: 
```
print(Hello)
print(Hello, World)
```
generates the same error (`NameError: name 'Hello' is not defined`), since Python is now looking for a variable called `Hello` - it doesn’t know that we just forgot to put quotation marks around the text.

[⬆️ BACK TO TOP](#top)

---

### `NameError` with a dictionary

*   `NameError: name 'A' is not defined`
*   Example erroneous code:
```py
dict1 = {"A":1, "B":2, "C":3}
print(dict1[A])
```
*   **Cause**:  Missing quotation marks (`" "`) when indexing a key from the dictionary.

*   Correct code: 
```py
dict1 = {"A":1, "B":2, "C":3}
print(dict1["A"])
```

[⬆️ BACK TO TOP](#top)

---

### Positional Arguments Errors

Let's first look at the case where too many arguments were provided in the function call.
In that case, the error would be something like: `print_name takes 0 positional arguments but 1 was given`.

* Example erroneous code:

```py
def print_name():
    print("Sam")

if __name__ == '__main__':
    print_name("Sam")
```

* **Cause**: The function `print_name()` does not take any parameters but when calling the function one parameter is being passed. This error signifies that there is a mismatch between the number of parameteres in the function defintion and the number of arguments in the function call. 

* Correct code: 

```py
def print_name():
    print("Sam")

if __name__ == '__main__':
    print_name()
```

This also works the other way around if you are missing arguments in the function call. For example, the function below results in an error: `get_largest() missing 1 required positional argument: 'y'`.

* Example erroneous code:

```py
def get_largest(x, y):
    return max(x, y)

if __name__ == '__main__':
    x = int(input())
    y = int(input())
    print(get_largest((x, y)))
```

* **Cause**: The function `get_largest()` takes in _two_ parameters but when calling the function only _one_ is passed in (i.e., a _tuple_ with two elements). This error likewise signifies that there is a mismatch between the number of parameteres in the function defintion and the number of arguments in the function call. 
* Correct code: 

```py
def get_largest(x, y):
    return max(x, y)

if __name__ == '__main__':
    x = int(input())
    y = int(input())
    print(get_largest(x, y))
  
```

[⬆️ BACK TO TOP](#top)

---
### `RecursionError: maximum recursion depth exceeded`

* **Cause**: This error usually occurs due to an **infinite recursion**, which typically happens when there is ...
    * <span style="color:red">no base case</span>
    * <span style="color:red">an invalid base case</span>
    * <span style="color:red">a missing base case</span>
    * <span style="color:red">an incorrect recursive call</span>
    * <span style="color:red">a missing `return`</span>

* **Check**: The following actions suggest what you can check when debugging an infinite recursion - make sure to add `print()` statements to _each_ branch, so that you can trace _which case_ is being called and with _which arguments_. Check the cases in the provided order:
    *  <span style="color:red">No base case</span>: 
        - does the recursive **function definition** contain an `if` statement that compares if the **input parameter** is a **_specific value_**, which corresponds to the base case?
        - do the instructions mention any specific value that can be turned into a base case? what action needs to happen in that case?
        - Common base cases are typically: an empty list/string; a count/length of 0 or 1; a minimum/maximum allowed value; 
    *  <span style="color:red">An invalid base case</span>: does the `if` statement compare the **input parameter** to the **correct value** of the **correct type**?
    *  <span style="color:red">A missing base case</span>: 
        - does there need to be another `if`/`elif` statement that should check if the **input parameter** corresponds to an _additional_ **correct value** of the **correct type** (remember the Fibbonacchi numbers example)? 
        - Ask yourself: is there another case when the function _does not need to do any computation/processing_ (so that it can easily produce the answer)? what action needs to happen in that case?
        - Common additional base cases: finding a match in a list/string; a single-element list/string
    *  <span style="color:red">An incorrect recursive call</span>: 
        - are the **arguments** in the recursive function call (_within the function itself_) being **reduced** / **increased** so that they **get closer to the value in the base case**? (use `print()` to verify/visualize their values)
        - Plug-in **_the next simplest case_** that would occur immediately **_after the base case_** and check whether the recursive call correctly triggers the base case (e.g., if the base case is an empty list, check if the function call with a single-element list would end up calling the base case).
        - Check the instructions - are the input values supposed to be from a specific range (e.g., non-negative? is 0 included? are letters/strings accepted?)
    *  <span style="color:red">A missing `return`</span>: Verify that if the function is supposed to **return** its result, then _each branch_ contains the `return` keyword. In the recursive case/branch, it is common to `return` **the result of calling the recursive function** (i.e., the recursive call). 

#### Example erroneous code illustrating the above recursion issues

Starting from the first case, we illustrate the potential issues by building on the first example:

* <span style="color:red">No base case</span>

```py
def fib(n):
    """
    param: n (int) - the ordinal value of the Fibonacchi
           sequence; expected to be > 0.
    The function recursively computes the n-th Fibonacchi
    number, starting from the 1st one.
    returns: the computed Fibonacchi value (int)
    """
    # missing a base case here - no `if` branch
    return fib(n - 1) + fib(n - 2)

if __name__ == "__main__":
    print(fib(3))
```
    
* <span style="color:red">An invalid base case</span>

```py
def fib(n):
    """
    param: n (int) - the ordinal value of the Fibonacchi
           sequence; expected to be > 0.
    The function recursively computes the n-th Fibonacchi
    number, starting from the 1st one.
    returns: the computed Fibonacchi value (int)
    """
    if n == '1': # incorrect type of the base case
        return 1
    return fib(n - 1) + fib(n - 2)

if __name__ == "__main__":
    print(fib(3))
```

* <span style="color:red">A missing base case</span>

```py
def fib(n):
    """
    param: n (int) - the ordinal value of the Fibonacchi
           sequence; expected to be > 0.
    The function recursively computes the n-th Fibonacchi
    number, starting from the 1st one.
    returns: the computed Fibonacchi value (int)
    """
    if n == 1: # correct type of the base case
        return 1 # correct return, correct value, correct type
    # need another base case, for the 2nd Fibonacchi n
    return fib(n - 1) + fib(n - 2)

if __name__ == "__main__":
    print(fib(3))
```


* <span style="color:red">An incorrect recursive call</span>

```py
def fib(n):
    """
    param: n (int) - the ordinal value of the Fibonacchi
           sequence; expected to be > 0.
    The function recursively computes the n-th Fibonacchi
    number, starting from the 1st one.
    returns: the computed Fibonacchi value (int)
    """
    if n == 1:
        return 1
    if n == 2:
        return 1
    return fib(n) + fib(n - 2) # the first function call doesn't decrement n

if __name__ == "__main__":
    print(fib(3))
    print(fib(0)) # also, the function call is not supposed to work for n <= 0
```


* <span style="color:red">A missing `return`</span>

```py
def fib(n):
    """
    param: n (int) - the ordinal value of the Fibonacchi
           sequence; expected to be > 0.
    The function recursively computes the n-th Fibonacchi
    number, starting from the 1st one.
    returns: the computed Fibonacchi value (int)
    """
    if n == 1:
        print ( 1 ) # missing a correct return
    if n == 2:
        print( 1 ) # incorrect return value
    return fib(n - 1) + fib(n - 2)

if __name__ == "__main__":
    print(fib(3))
```


[⬆️ BACK TO TOP](#top)

---


## Syntax Errors

### `SyntaxError: invalid character in identifier`

*   **Cause**:   Either quotations around the text or some other symbol is not from the standard Latin alphabet used by Python. The error typically occurs when writing code in a text processor (e.g., Word), typing on a mobile device that has autocorrect enabled, or (rarely) when accidentally switching the keyboard language layout.

*   Example erroneous code:
```py
print(‘Hello!’) # invalid quotations
```



### `SyntaxError: invalid syntax`

This is a general error that occurs when the syntax is not correct and a "Python sentence" is broken.
    If enabled, pay close attention to the syntax highlighting, which can point at where the error might be happening.

Below are sample Python syntax rules:
1. A function call must start and end with a parenthesis; the number of open and closed parentheses must match.
1. The literal text has to be enclosed within the quotation marks.
1. Variables must first be defined (created) before being used.

<br/>

*   **Cause**:   Missing **opening** quotation mark or **opening** parenthesis or quotations around the text.
*   Example erroneous code:
```py
print(Hello World')
print'Hello World  
print(Hello World) # see also NameError
```

[⬆️ BACK TO TOP](#top)

---

### `SyntaxError: unmatched ')'`
*   **Cause**:  an extra **closing** parenthesis `)` that does not have a matching **opening** paren `(`.
*   Example erroneous code:
```py
print('Hello, World'))
```

[⬆️ BACK TO TOP](#top)

---

## Type Errors

### `TypeError: argument of type 'int' is not iterable`

Related error: [`TypeError: 'list' object cannot be interpreted as an integer`](#typeerror-list-object-cannot-be-interpreted-as-an-integer)

* Example erroneous code:

```py
total = 42
sum(total)

# another alternative that would case such error
for i in total: # `in` requires a range/collection, not an integer
    print(i)
```

*   **Cause**: The error usually occurs when a built-in Python function that is intended for a sequence/collection is applied to an integer instead.
*   **Check**: Take a look at the line that is causing an error and verify that you are using a proper collection (i.e., a list or a range). 

* Correct code:

```py
total = [42]
sum(total)

for i in total: # `in` requires a range/collection, not an integer
    print(i)

# alternatively, if `total` needed to stay as an integer
total = 42
for i in range(total):
    print(i)
```

[⬆️ BACK TO TOP](#top)

---

### `TypeError: argument of type 'NoneType' is not iterable`

* Example erroneous code:

```py
val = None
if "a" in val:
    print("Found it!")
```

*   **Cause**: The error usually occurs when the `in` operator in trying to index a `None` value instead of the sequence/collection. 
    * Check the type/value of the object that is used after the `in` operator - if that object is a result of the function's return value, verify that the function is returning the correct object or that your `if` branches are set up correctly to not try to index a `None`.
    * Do not store the result of `print()` and attempt to index it. Just like the methods that modify lists directly (since lists are mutable), `print()` does not return anything other than `None`.

* Correct code:

```py
val = None
if val != None:
    if "a" in val:
        print("Found it!")
```

or

```py
val = "aeou" # correct object provided
if "a" in val:
    print("Found it!")
```

[⬆️ BACK TO TOP](#top)

---

### `TypeError: can only concatenate str (not "int") to str`
* Example erroneous code:

```py
num = 6
print("I would like " + num + " tacos please.")
```

*   **Cause**:  You can only concatenate a string with a string, not a numeric type. Check the types of the variables that you are using in the concatenation.

* Correct code and alternatives: 

```py
num = 6
print("I would like " + str(num) + " tacos please.") # proper string concatenation
print("I would like", num, "tacos please.") # using print defaults
print(f"I would like {num} tacos please.") # using f-strings
```

[⬆️ BACK TO TOP](#top)

---

### `TypeError: 'list' object cannot be interpreted as an integer`

* Example erroneous code:

```py
total = [42]
for i in range(total):
	print(i)
```

*   **Cause**: The `range()` function requires an **integer argument** but a list is given instead.
*   **Check**: 
   * Is the current argument given to the `range()` supposed to be a list? Are you trying to print its _values_? If so, why do you need to use a `range()`, which helps print _indices_?
   * Do you need to print indices of a list? If so, do you have `len()` of a list as an input to the `range()`?
   * Do you need to generate a bunch of numbers and you accidentally stored the total as a list, instead of as an integer? 

* Depending on what you need to do, the potential solutions to the above error could be:

```py
# `total` needs to be an integer, not a list
total = 42
for i in range(total):
	print(i) # prints the numbers from 0 to 42 (value in total)

# or, alternatively
# `total` stays as a list but
# the range() needs to be provided a proper integer, e.g., the length of the list
total = [42]
for i in range(len(total)):
	print(i) # prints the indices of the list, which is just 0
```

[⬆️ BACK TO TOP](#top)

---

### `TypeError: object of type '...' has no len()`

Examples include the errors
```
TypeError: object of type 'int' has no len()
TypeError: object of type 'float' has no len()
```

* Example erroneous code:

```py
len(42)
```

*   **Cause**: The error usually occurs when you think that you are asking for a length of a collection (e.g., a list, string, dictionary) but in reality the argument is an integer. Examine the value that is being provided as an argument into the `len()` function.

* Correct code: 
```py
len([42]) 
```

[⬆️ BACK TO TOP](#top)

---

### `TypeError: ... takes exactly one argument (... given)`

Some examples of this error:
```
TypeError: len() takes exactly one argument (2 given)
```

* Example erroneous code:

```py
len(42, 33)
```

*   **Cause**: The error usually occurs when 
    * a built-in Python function is being applied to an incorrect object.
    * the function is not given the required number of arguments.

* Correct code: 
```py
len([42, 33]) 
```

[⬆️ BACK TO TOP](#top)

---

### `TypeError: '...' not supported between instances of '...' and '...'`

Some specific instances of this error:
* `TypeError: '<=' not supported between instances of 'int' and 'str'`
* `TypeError: '<' not supported between instances of 'str' and 'int'`

Similar error: `TypeError: unsupported operand type(s) ...`

*   **Causes**: The code is trying to compare incompatible types. The listed types are on the left and ithe right side of the provided operator respectively.
*   **Check**: Does either or both of the operands need to be converted into a numeric type?

* Erroneous code:
```py
my_var = input() 
if my_var < 5:
   print(my_var)
```

* Correct code: 

```py
my_var = int(input()) 
if my_var < 5:
   print(my_var)
```

[⬆️ BACK TO TOP](#top)

---

### `TypeError: unsupported operand type(s) for +: 'int' and 'list'`

Similar error: `TypeError: '...' not supported between instances of 'int' and 'str'`

* Example erroneous code:

```py
nested_list = [[5, 10, 6], [7, 8, 9]]
total_sum = sum(nested_list)
```

*   **Cause**: The error can occur when trying to apply a built-in Python method to an unsupported type, e.g., to sum up a nested list, instead of its individual elements.

* Correct code: 

```py
nested_list = [[5, 10, 6], [7, 8, 9]]
total_sum = 0
for item in nested_list:
    item_sum = sum(item)
    total_sum += item_sum
```


[⬆️ BACK TO TOP](#top)

---

### `ValueError: invalid literal for int() with base 10`
*   Example erroneous code:
```py
current_year = '1792.99'
current_year = int(current_year)
print(current_year)
```
*   **Cause**:  Float, represented as a string, cannot be directly converted into an integer. If you do want to pass a string representation of a float to an int,  you need to convert to a float first, then to an integer.

*   Correct code: 
```py
current_year = '1792.99'
current_year = float(current_year)
current_year = int(current_year)
print(current_year)
```

[⬆️ BACK TO TOP](#top)

---

### `ZeroDivisionError: division by zero`

* Example erroneous code:
```py
print(1 / 0)
# or
my_list = []
print("The average value of the list is", sum(my_list) / len(my_list))
```
*   **Cause**:  The denominator in a division is 0.

*   Correct code: 
```py
my_list = []
if my_list != []: # len(my_list) != 0
    print("The average value of the list is", sum(my_list) / len(my_list))
```


[⬆️ BACK TO TOP](#top)

---

## Undesirable Results

### Output printing `None`

* `None` is printed even though you don't want it to be there 
* Example erroneous code: 

```py
def print_hello():
    print("hello")

if __name__ == '__main__':
    print(print_hello())
```

* **Cause**: The function `print_hello()` does not return anything (it has no `return` statement) so when you call `print(print_hello())` you are printing its return value which is `None`. 
* Correct code: 

```py
def print_hello():
    print("hello")

if __name__ == '__main__':
    print_hello()
```

[⬆️ BACK TO TOP](#top)

---

### Function returns `None` but a different value is needed

* Example erroneous code: 

```py
def get_hello():
    print("hello")

if __name__ == '__main__':
    print(get_hello())
```

* **Cause**: The function `get_hello()` does not return anything (it has no `return` statement) so when you call `print(get_hello())` you are printing its return value which is `None`. 
* **Check**: Sometimes, this behavior can occur when your code has nested `if`/`elif` branches, which contain a `return` inside of them. If one or more of the conditions are not set up correctly, the correct return statement would not be triggered. 
    * Verify the accuracy of the conditions, check the edge cases, especially with the `==` (e.g., is it supposed to be `<` or `<=`).
    * Note what condition needs to fail for your code to return `None`. 
    * Debug your code by adding print statements and/or add an `else: return 42` to see which branches get executed/skipped. 

* Correct code: 

```py
def get_hello():
    return "hello"

if __name__ == '__main__':
    print(get_hello())
    assert get_hello() == "hello" # to check the return value
```

[⬆️ BACK TO TOP](#top)

---


### Logic Errors
* Sometimes, we get a logic error, when the output does not match what we expect.
* Example erroneous code: 
```py
def get_largest(x,y):
    if x > y: 
      return y
    else: 
      return x
```
* **Cause**: Although the syntax of this function is correct and the function will produce no errors, the result will be incorrect. This is simply due to a logical error - an incorrect value is being returned (or, the `if` condition needs to be changed). 

* Correct code: 
```py
def get_largest(x,y):
    if x > y: 
      return x
    else: 
      return y
```

[⬆️ BACK TO TOP](#top)

---

### Function address is printed `<function function_name at 0x....> `
*   Function Address gets printed - `<function function_name at 0x....> `
*   Example erroneous code:

```py
def area(radius):
    return 3.14 * radius**2

if __name__ == '__main__':   
    radius = float(input())
    print(f"Circle has area {area} inches squared.")
```

*   **Cause**:  Instead of the function call, which requires the parentheses (and the arguments, if necessary), only the name of the function is used. 
*   Correct code: 
```py
    ...
    print(f"Circle has area {area(radius)} inches squared.")
``` 

---

**Acknowledgement**

Content on this page is adapted from [Yekaterina Kharitonova](ucsb-csw8.github.io)
{: .fs-2 }
