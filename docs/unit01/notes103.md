---
layout: notes
title: "📓1.3: Files, Libraries, & APIs" 
parent: "1️⃣ Python Bootcamp"
nav_order: 3
---

## Table of Contents
{: .no_toc .text-delta }

{: .fs-2 }
- TOC
{:toc}

---
## The Main Method
Once you start writing more comprehensive Python programs, you'll want to include a `main` method in your code.

The purpose of checking for the `main` method is to make sure that the code in your `main` method is only run when it's executed as a stand-alone program. Because of how Python's import system works, if someone else imports your Python program, any code in it is executed on import.

We'll talk more about imports and modules on day two, but let's look at a quick example.

Let's say we had a Python file named `name_lib.py`

```python
def name_length(name):
    return len(name)

def upper_case_name(name):
    return name.upper()

def lower_case_name(name):
    return name.lower()

name = "Nina"
length = name_length(name)
upper_case = upper_case_name(name)

print(f"The length is {length} and the uppercase version is: {upper_case}")
```

If we ran this code, we'd see exactly what we expect.

```bash
(env) $ python name_lib.py
name_lib.py
The length is 4 and the uppercase version is: NINA
```

### Writing Reusable Code

We went through all this trouble of writing a useful name library. What if someone else wanted to use our library in their own code by `import`ing it?

Let's say someone else wrote their own program, in `other_program.py`

```python
import name_lib

my_name = "Fred"

my_length = name_lib.name_length(my_name)
my_lower_case = name_lib.lower_case_name(my_name)

print(f"In my code, my length is {my_length} and my lower case name is: {my_lower_case}")
```

If we ran this, we'd see the following result:

```bash
(env) $ python other_program.py

The length is 4 and the uppercase version is: NINA
In my code, my length is 4 and my lower case name is: fred
```

If I'm Fred, I just wanted to use this cool library. But all of a sudden, I'm seeing information about Nina!

To prevent this from happening, we want to write a conditional that will only run *our* code if we're the ones running the program directly.

To do that, we'll need to check if `__name__ == __main__`.

Let's unwrap that.

`__name__` is a special variable that's set by Python that tells it where it was called from. We can tell it's a special variable because it starts and ends with `__`. That's a hint that you don't want to *change* the value of this variable, or it could adversely affect the execution of your Python program.

{{% notice tip %}}
In Python, `__` is also called double underscore, or *dunder*.
{{% /notice %}}

Let's comment out our original `print`, and add the following line to the end of `name_lib.py`:

```python
# Note: add to the bottom of name_lib.py

# print(f"The length is {length} and the uppercase version is: {upper_case}")
print(f"The value of __name__ is: {__name__}")
```

Now, let's run `name_lib.py` again. We should see:

```bash
(env) $ python name_lib.py
The value of __name__ is: __main__
```

We're getting somewhere. When we run this file directly, we'll see that `__name__` has the *value* of `__main__`.

What if we run our other program again?

```bash
(env) $ python other_program.py
The value of __name__ is: name_lib
```

When we "run" our library by importing it, we'll see that it's `__name__` is set to the name of the file that it's in, minus the `.py` extension. In this case, `__name__` is set to `name_lib`.

### Putting Code in a `main` Conditional

To avoid running our code when it's imported by other modules, we put it in a conditional statement, and explicitly check `if __name__ == "__main__"`.

Let's update `name_lib.py`, and put our own code inside of the conditional check.

```python
def name_length(name):
    return len(name)

def upper_case_name(name):
    return name.upper()

def lower_case_name(name):
    return name.lower()

if __name__ == "__main__":
    name = "Nina"
    length = name_length(name)
    upper_case = upper_case_name(name)

    print(f"The length is {length} and the uppercase version is: {upper_case}")
```

Now, if we run `other_program.py`, we'll see:

```bash
(env) $ python other_program.py
In my code, my length is 4 and my lower case name is: fred
```

Much better!

{{% notice note %}}
Using a `main` method is a common pattern that you’ll see in Python programs, and it comes in handy for being able to write programs that work both on their own and when imported into other programs.
{{% /notice %}}

---
## File Handling

Python provides a built-in function for opening files, cleverly titled `open()`. The `open()` method will return an object that you can `read()` to get the data. By default, `open()` will open a file in read-only mode, however you can change this by passing a mode parameter. The list of optional modes is here:

|Character|Meaning|
|---|---|
|'r'|open for reading (default)|
|'w'|open for writing, truncating the file first|
|'x'|open for exclusive creation, failing if the file already exists|
|'a'|open for writing, appending to the end of the file if it exists|
|'b'|binary mode|
|'t'|text mode (default)|
|'+'|open a disk file for updating (reading and writing)|

Opening a file would look something like this:

```python
# Open a file for reading
>>> my_file = open("my_file.txt")

# Open a file for reading or writing
# This will replace any existing file
>>> my_file = open("my_file.txt", "w")

# Open a file for reading or writing
# This will append to the end of any existing file
>>> my_file = open("my_file.txt", "a")
```

Of course, you always want to call `close()` on your open file object once you're done with it, so that your program doesn't leave open file handles dangling. But what happens if your program exits or crashes before you can close a file? Use a context manager!


### Context Managers

Briefly, a Context Manager is like a wrapper around a block of code that depends on some resource. It's a safer way of handling resources than, say, using `open()` and then remembering to `close()` later (and hoping your program doesn't crash in between). It's similar to using `try... finally`, but cleaner to look at. Context managers can contain code that auto-magically provisions a resource before your code runs, and cleans up afterward. For example, the `open()` function also works as a context manager, so opening a file looks like this:

```python
>>> with open("my_file.text") as my_file:
...     contents = my_file.read()
```

You can perform all the functions that require access to the open file within the `with` scope, and once you exit the `with` scope, the context manager will automatically close your file for you, even if your code hits an exception inside the context manager.


### Working with Files

Let's try working with a simple json file. Download this [`cities.json` file](/code/cities.json), which contains a listing of the top five cities in the US by population. We'll import the `json` module to help us parse the data, and we'll use a context manager to open the file.

```python
>>> import json
>>> with open("cities.json") as cities_file:
...     cities_data = json.load(cities_file)
...     print(cities_data)
...
[{'name': 'New York', 'pop': 8550405}, {'name': 'Los Angeles', 'pop': 3971883}, {'name': 'Chicago', 'pop': 2720546}, {'name': 'Houston', 'pop': 2296224}, {'name': 'Philadelphia', 'pop': 1567442}]
```

---
## External Libraries

Working with external libraries in Python makes use of the `import` keyword. While this can go anywhere in your file, it's almost always best to import libraries at the top of each file where they're used. For example, in the last section, we were able to call upon the built-in `json` library by calling `import json` at the top of our code.

Importing modules with the `import` keyword is usually the best method, because it preserves the module's namespace. However, you can also use the `from <module> import <object>` syntax to import a specific object (function, variable, subclass, etc.) from a module into your program's namespace.

For example, if we wanted a random integer between 0 and 100, we could use `random.randint()`:

```python
>>> import random
>>> random.randint(0, 100)
42
```

Notice that the namespace is preserved (we needed to call `random.randint()`). If we use `from` instead:

```python
>>> from random import randint
>>> randint(0, 100)
64
```


### Installing the requests library with `pip`

For the next chapter, we'll be using an excellent 3rd part library called `requests` to make light work of retrieving data from web APIs. To install the `requests` library, run this on your command line:

```bash
(env) $ python -m pip install requests
```

This runs the `pip` module and asks it to find the `requests` library on PyPI.org (the Python Package Index) and install it in your local system, so that it becomes available for you to import. We'll dive a little more into this later.

---
## APIs
{{% notice note %}}
Zapier has an *excellent* intro to APIs by by Brian Cooksey. The images and diagrams used on this page is from his post. Please read it [here](https://zapier.com/learn/apis/chapter-1-introduction-to-apis/).
{{% /notice %}}


### Requests and Responses

Working with APIs using HTTP depends on the request and response cycle. You send a request to the server, and it lets you know if your request was successful or by sending an HTTP Status Code with a special meaning, and will optionally send back data.

![](/02-introduction-to-python/190-APIs/images/request-response.jpeg?width=40pc)

### HTTP Methods

The HTTP Method (or verb) is how you tell the server which *type* of operation you'd like to perform.

- `GET` - Ask the server to get a resource.
- `POST` - Ask the server to create a resources, with the data that you've provided.
- `PUT` - Edit or update a resource.
- `DELETE` - Delete a resource.

### Headers, Body, Parameters

We can add additional to our request through headers, a body or URL parameters.

For today, we'll only be using URL parameters. They look like `https://example.com?var1=foo&var2=bar`.

### Response Types

Servers can respond in a variety of file formats, like JSON, XML, and others.

These days, JSON is the most common format. For many servers, it's the default if you don't specify a response type.

JSON is a common format of capturing data, and it's easy to read and generate from a variety of programming languages.

A JSON example:

```json
[
	{
		"name": "New York",
		"pop": 8550405
	},
	{
		"name": "Los Angeles",
		"pop": 3971883
	},
	{
		"name": "Chicago",
		"pop": 2720546
	},
	{
		"name": "Houston",
		"pop": 2296224
	},
	{
		"name": "Philadelphia",
		"pop": 1567442
	}
]
```


### HTTP Status Codes

HTTP Status Codes is a numerical response from the sever, indicating the status of your request.

They tend to fall into these categories:

- **`1xx` : Informational**
    - Not commonly used.
- **`2xx` : Success**
    - **`200 OK`** - Standard response for successful HTTP requests.
    - **`201 CREATED`** - A new resource was created successfully.
- **`3xx` : Redirection**
    - **`301 Moved Permanently`** - This and all future requests should be directed to the new URL.
- **`4xx` : A Client Error**
    - **`404 Not Found`** - An entry wasn't found based on the information the client gave.
- **`5xx` : A Server Error**
    - **`500 Internal Server Error`** - Something went wrong with the server.\


#### Because HTTP Status Codes are boring, we can try to remember them with cats instead!

| code                            	| cat                                                                                       	|
|---------------------------------	|-------------------------------------------------------------------------------------------	|
| **`200: OK`**                   	| ![](/02-introduction-to-python/190-APIs/images/200.jpeg?classes=shadow&outline&width=20pc) 	|
| **`301 Moved Permanently`**     	| ![](/02-introduction-to-python/190-APIs/images/301.jpeg?classes=shadow&outline&width=20pc) 	|
| **`404 Not Found`**             	| ![](/02-introduction-to-python/190-APIs/images/404.jpeg?classes=shadow&outline&width=20pc) 	|
| **`500 Internal Server Error`** 	| ![](/02-introduction-to-python/190-APIs/images/500.jpeg?classes=shadow&outline&width=20pc) 	|

<sub>Provided by [this awesome API](https://http.cat/).</sub>

#### Easter Egg - I'm a Teapot

One of my favorite bits of internet trivia is that in 1998 as an April fool's joke, HTTP Status Code `418 I'm a teapot`, a.k.a the Hyper Text Coffee Pot Control Protocol was implemented. You can pass the `BREW` command to it, to signal starting brewing a cup of coffee.

![](/02-introduction-to-python/190-APIs/images/Htcpcp_teapot.jpg?classes=shadow&outline&width=30pc)

### Authentication

There are several ways of authenticating to APIs, but they are out of the scope of this class.

To learn more about authentication, visit:

- (Concepts) Zapier - [Authentication Part 1](https://zapier.com/learn/apis/chapter-4-authentication-part-1/) and[Authentication Part 2](https://zapier.com/learn/apis/chapter-5-authentication-part-2/)  by Brian Cooksey
- Using [authentication in the `requests` library](http://docs.python-requests.org/en/master/user/authentication/) documentation.

### What is The `requests` Library?

Python is "batteries included", but sometimes the included libraries available in the standard library can be hard to understand. The standard library focuses on functionality, but not necessarily ease of use.

That's where external libraries come in. The external `requests` library was developed by Kenneth Reitz to make working with APIs in Python a lot easier. He calls it "HTTP, for humans." It's become of the (if not the most) popular Python library!

### Our First Request With The `requests` Library

{{% notice tip %}}
If you didn't install the `requests` library in the working with libraries chapter, you'll need to do that first before running this code. Use: `python -m pip install requests`
{{% /notice %}}

Let's make a request to shibe.online to get ourselves some dog pictures. Create a file called `shibe.py` in our `pyworkshop` directory and copy this:

```python
# First thing we'll do is import the requests library
import requests

# Define a variable with the URL of the API
api_url = "http://shibe.online/api/shibes?count=1"

# Call the root of the api with GET, store the answer in a response variable
# This call will return a list of URLs that represent dog pictures
response = requests.get(api_url)

# Get the status code for the response. Should be 200 OK
# Which means everything worked as expected
print(f"Response status code is: {response.status_code}")

# Get the result as JSON
response_json = response.json()

# Print it. We should see a list with one image URL.
print(response_json)
```

```bash
(env) $ python shibe.py
Response status code is: 200
['https://cdn.shibe.online/shibes/28d7c372ea7defdb315ef845285d4ac3906ccea4.jpg']
```

### Dealing with Errors

When dealing with HTTP requests, your first indication of error is usually the HTTP status code. You saw some of the common status codes in the last chapter. The most common status codes are probably `200` - Success, and `404` - Not found. You can find the status code in the `status_code` property of the `response` object:

```python
# Passing in a non-existant URL will result in a 404 (not found)
bad_response = requests.get("http://shibe.online/api/german-shepards")
print(f"Bad Response Status Code is: {bad_response.status_code}")  # Status code is 404, meaning that resource doesn’t exist.
```

### Passing in Parameters

```python
# We'll store our base URL here and pass in the count parameter later
api_url = "http://shibe.online/api/shibes"

params = {
   "count": 10
}

# Pass those params in with the request.
api_response = requests.get(api_url, params=params)

print(f"Shibe API Response Status Code is: {api_response.status_code}")  # should be 200 OK

json_data = api_response.json()

print("Here is a list of URLs for dog pictures:")
for url in json_data:
    print(f"\t {url}")
```

```bash
$ shibe.py
Shibe API Response Status Code is: 200
Here is a list of URLs for dog pictures:
     https://cdn.shibe.online/shibes/dfb2af0b2ac1f057750da32f0ea0e154afc160cf.jpg
     https://cdn.shibe.online/shibes/4989daad2c805ec62b0fb09a80280ba2262f1b08.jpg
     https://cdn.shibe.online/shibes/a9360b8262c586af2cf53a2d68bb6ec34b87fe25.jpg
     https://cdn.shibe.online/shibes/a168cc7f2524c73b433afd7c02f698884738daff.jpg
     https://cdn.shibe.online/shibes/3fbe49908948718c521b756f31dc155ed22941f6.jpg
     https://cdn.shibe.online/shibes/846bb52389cf9af8a54eb12f48e0e7d0883b17da.jpg
     https://cdn.shibe.online/shibes/d11ed7f57c5a882f047b921a73f0b95714626bb3.jpg
     https://cdn.shibe.online/shibes/0fd1dcc9f5866cefaa3040de1be0f8971b0530cd.jpg
     https://cdn.shibe.online/shibes/cd668ca05d0ec78863f3c30b08b9cd4ff7f5669c.jpg
     https://cdn.shibe.online/shibes/32bf0797e5a4c5bfb6fc06edc57ddfbf4e08f98f.jpg
```

#### More about `requests`

To learn more about the `requests` library *after* class, look at the [quick start](http://docs.python-requests.org/en/master/user/quickstart/).

### What are APIs?
Per the dictionary, an API is:

> a set of functions and procedures allowing the creation of applications that access the features or data of an operating system, application, or other service.

An API is a standardized way of accessing information across the web, between clients and servers. These days most APIs are *RESTful*. That means they follow a common set of paradigms and practices.

There are many types of APIs, but these days they're commonly known to refer to *web* APIs.

#### Authentication

Some, but not all APIs require you to authenticate. Methods of authentication are out of the scope of this class, but you'll be happy to know that there are plenty of free APIs available that require no authentication at all.

#### Rate Limiting

Some APIs allow unauthenticated requests, but they're usually *rate limited*. Rate limiting means prevent the same client (usually by IP address) from making too many requests at once and overloading the server. *The GitHub API allows 50 unauthenticated requests per hour per IP, or 10 unauthenticated requests to their Search API.*

Note: After the class, you can find a detailed list of APIs in this [public-apis repo](https://github.com/toddmotto/public-apis).

#### Free APIs

{{% notice note %}}
Free APIs are... free. That means that they may go down if their owner decides to drop their upkeep. If the API used in these examples doesn't work in the future, try a different one listed in the `public-apis` repo linked to above.
{{% /notice %}}


---
### Practice

Let's create a basic program that we can run as a file on the command line. We'll start with a basic framework using a `main()` function.

```python
def main():
    pass

if __name__ == "__main__":
    main()
```

Save your file as `file_exercise.py` and run it from the command line using `python file_exercise.py`. Note: we are concentrating on Python 3 for this class, so if you have Python 2 installed, you may need to explicitly use `python3 file_exercise.py`.

What happened? Because you ran the file directly, the file's `__name__` variable is set to `__main__`, which triggers the `if` statement to run the `main()` function. This is a common pattern that you'll see in Python programs, and it comes in handy for being able to write programs that work both on their own and when imported into other programs. The `pass` keyword does nothing, it's just there to keep the empty `main()` function from throwing a syntax error.

Let's start filling in our `main()` function. We have a json file named `cities.json` which contains the top five cities in the US, sorted by population. You can [download `cities.json` here](/code/cities.json). Let's open the file and load in the data.

```python
import json

def main():
    cities_file = open("cities.json")
    cities_data = json.load(cities_file)
    print(cities_data)

if __name__ == "__main__":
    main()
```

First, we imported the built-in `json` library to help us decode the json file. Then, we opened the file using the `open()` function, and passed the open file handle to the `json.load()` function. The `load()` function read our data in and spit it out as a Python representation - in this case, a list of dictionaries. We then print this list.

{{%expand "Here's what you should have seen on your command line:" %}}

```bash
(env) $ python file_execise.py
[{'name': 'New York', 'pop': 8550405}, {'name': 'Los Angeles', 'pop': 3971883}, {'name': 'Chicago', 'pop': 2720546}, {'name': 'Houston', 'pop': 2296224}, {'name': 'Philadelphia', 'pop': 1567442}]
```

{{%/expand%}}

This list is a little hard to make sense of in its raw form, let's print it a little nicer. Use `enumerate()` to go through the list and print it nicely:

```python
import json

def main():
    cities_file = open("cities.json")
    cities_data = json.load(cities_file)

    print("Largest cities in the US by population:")

    for index, entry in enumerate(cities_data):
        print(f"{index + 1}: {entry['name']} - {entry['pop']}")

if __name__ == "__main__":
    main()
```

A few new things here: first, remember that `enumerate()` outputs a tuple of (index, entry), so we use `index` and `entry` variables to capture those. Then, for every item in the list, we print the index (+ 1, because zero-indexed lists are sometimes hard to read), and we pull the name and population out of each entry dictionary using the dictionary `[]` syntax.

{{%expand "Here's what you should have seen on your command line:" %}}

```bash
(env) $ python file_execise.py
Largest cities in the US by population:
1: New York - 8550405
2: Los Angeles - 3971883
3: Chicago - 2720546
4: Houston - 2296224
5: Philadelphia - 1567442
```

{{%/expand%}}

One more thing to clean up - using the `open()` keyword on its own is frowned upon, because it won't automatically close any resources you might open. Even if you call the `close()` keyword yourself, there's no guarantee your program won't crash, leaving important resources dangling. It's safer to open files inside a context using the `with` keyword. Once your code exits the scope of the context, your file is automatically closed. Note: our reading and formatting code has shifted to the right because of the change in scope.

```python
import json

def main():
    with open("cities.json") as cities_file:
        cities_data = json.load(cities_file)

        print("Largest cities in the US by population:")
        for index, entry in enumerate(cities_data):
            print(f"{index + 1}: {entry['name']} - {entry['pop']}")

    print("The file is now closed.")

if __name__ == "__main__":
    main()
```

{{%expand "Here's what you should have seen on your command line:" %}}

```bash
(env) $ python file_execise.py
Largest cities in the US by population:
1: New York - 8550405
2: Los Angeles - 3971883
3: Chicago - 2720546
4: Houston - 2296224
5: Philadelphia - 1567442
The file is now closed.
```

{{%/expand%}}


#### Acknowledgement
{: .no_toc }

Content on this page is adapted from [LearnPython - Nina Zakharenko](https://www.learnpython.dev/).
{: .fs-2 }
