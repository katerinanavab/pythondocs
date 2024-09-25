---
layout: notes
title: "📓2.1: Pandas" 
parent: "2️⃣ Data Science"
nav_order: 1
---

## Table of Contents
{: .no_toc .text-delta }

{: .fs-2 }
- TOC
{:toc}

---
## What is Data Science?

<html>
<dl>
  <dt>Data Science</dt>
  <dd>An emerging, interdisciplinary field that brings together ideas that have been around for years, or even centuries about processes and systems to <strong>extract knowledge</strong> and/or to <strong>make predictions</strong> from data in various forms.
  </dd>
</dl>
</html>

In 2016 a study reported that [90% of the data in the world today has been created in the last two years alone](http://www.iflscience.com/technology/how-much-data-does-the-world-generate-every-minute).
This is the result of the _continuing acceleration of the rate_ at which we store
data. Some estimates indicate that roughly 2.5 quintillion bytes of data are
generated per day; that's 2,500,000,000,000,000,000 bytes! 
> By comparison, all the data in the Library of Congress adds up to about 200 TB, merely 200,000,000,000,000 bytes. This means that we are capturing _12,500 libraries of congress per day_!

The amount of data that Google alone stores in its servers is estimated to be 15 exabytes (15 followed by 18 zeros!). You can visualize 15 exabytes as a [pile of cards three miles high](https://what-if.xkcd.com/63/), covering all of New England. 

Everywhere you go, someone or something is collecting data about you: what you buy, what you read, where you eat, where you stay, how and when you travel, and so much more. By 2025, it is estimated that 463 exabytes of data will be created each day globally, and the entire digital universe is expected to reach 44 zettabytes by 2020. [This would mean there would be 40 times more bytes than there are stars in the observable universe](https://www.visualcapitalist.com/how-much-data-is-generated-each-day/)!

Often, this data is collected and stored with _little idea about how to use it_, because technology makes it so easy to capture. Other times, the data is collected quite intentionally. The big question is: **what does it all mean?** That's where data science comes in. 

### What does a data scientist do?

<a href="https://www.youtube.com/watch?v=X3paOmcrTjQ"><button class="btn btn-purple">📺 VIDEO: Data Science in 5 Minutes</button></a>

As an interdisciplinary field of inquiry, data science is perfect for a liberal arts college as well as many other types of universities.
Combining statistics, computer science, writing, art, and ethics, data science has application across the entire curriculum:  biology, economics, management, English, history, music, pretty much everything. The best thing about data science is that the job of a data scientist seems perfectly suited to many liberal arts students.

{:.highlight}
"The best data scientists have one thing in common: **unbelievable curiosity**." - D.J. Patil, *Chief Data Scientist of the United States from 2015 to 2017*.

![image](https://static1.squarespace.com/static/5150aec6e4b0e340ec52710a/t/51525c33e4b0b3e0d10f77ab/1364352052403/Data_Science_VD.png?format=1500w)

> The diagram above is widely used to answer the question "What is Data Science?" It also is a great illustration of the **liberal arts** nature of data science. Some computer science, some statistics, and something from one of the many majors available at a liberal arts college, all of which are looking for people with data skills!

---

## 🐼 Data Manipulation with Pandas

#### Using a GitHub Template for class notes
{:.no_toc}

<div class="setup" markdown="block">

1. Go to the public template **repository** for our class: [BWL-CS Python Template](https://github.com/BWL-CS/python-template)
2. Click the <button type="button" name="button" class="btn btn-green">Use this template</button> button above the list of files then select `Create a new repository`
3. Specify the **repository name**: `CS3-Unit-2-Notes`
4. Click <button type="button" name="button" class="btn btn-green">Create repository</button>
    > Now you have **your own personal copy** of this starter code that you can always access under the `Your repositories` section of GitHub! 
5. Now on your repository, click <button type="button" name="button" class="btn btn-green"> < > Code </button> and select the `Codespaces` tab
6. Click `Create Codespace on main` and wait for the environment to load, _then you're ready to code_!
7. 📝 Take notes in this Codespace during class, coding along with the instructor.

</div>

### From NumPy to Pandas

**NumPy** is a Python library centered around the `ndarray` object, which enables efficient storage and manipulation of dense typed arrays. **Pandas** is a newer package built on top of **NumPy** that provides an efficient implementation of a `DataFrame`, which is the main data structure offered by Pandas. 
> **NumPy**'s limitations become clear when we need more flexibility (e.g., attaching labels to data, working with missing data, etc.) and when attempting operations that do not map well to element-wise broadcasting (e.g., groupings, pivots, etc.), each of which is an important piece of analyzing the less structured data available in many forms in the world around us.

<html>
<dl>
  <dt><code>DataFrame</code></dt>
  <dd>A multidimensional array object with attached <code>row</code> and <code>column</code> labels, often containing heterogeneous types and/or missing data. The concept is similar to a <strong>spreadsheet</strong> in Excel or Google Sheets, but more versatile.</dd>
</dl>
</html>

As well as offering a convenient storage interface for labeled data, Pandas implements a number of powerful **data operations** familiar to users of both database frameworks and spreadsheet programs. Pandas, and in particular its `Series` and `DataFrame` objects, builds on the NumPy array structure and provides efficient access to these sorts of "data munging" tasks that occupy much of a data scientist's time.

As we will see during the course of this chapter, Pandas provides a host of useful tools, methods, and functionality on top of the basic data structures, but nearly everything that follows will require an understanding of what these structures are.
Thus, before we go any further, let's take a look at these three fundamental Pandas data structures: the `Series`, `DataFrame`, and `Index`.

We will start our code sessions with the standard NumPy and Pandas **imports**, under the aliases `np` and `pd`:

```python
import numpy as np
import pandas as pd
```

### The Pandas `Series` Object

<html>
<dl>
  <dt><code>Series</code></dt>
  <dd>A one-dimensional array of indexed data.</dd>
</dl>
</html>

A `Series` object can be created from a `list` or array as follows:

```python
data = pd.Series([0.25, 0.5, 0.75, 1.0])
```

The `Series` combines a sequence of **values** with an explicit sequence of **indices**, which we can access with the `values` and `index` attributes. The `values` are simply a NumPy array:
```python
data.values
```

The `index` is an array-like object of type `pd.Index`, which we'll discuss in more detail momentarily:
```python
data.index
```

Like with a NumPy array, data can be accessed by the associated index via the familiar Python square-bracket notation:

```python
data[1]
data[1:3]
```

As we will see, though, the Pandas `Series` is much more general and flexible than the one-dimensional NumPy array that it emulates.

#### Series as Generalized NumPy Array
{:.no_toc}

From what we've seen so far, the `Series` object may appear to be basically interchangeable with a one-dimensional NumPy array. The essential difference is that while the NumPy array has an *implicitly defined* integer index used to access the values, the Pandas `Series` has an *explicitly defined* index associated with the values.

This explicit index definition gives the `Series` object additional capabilities. For example, the index need not be an integer, but can consist of values of any desired type.
So, if we wish, we can use strings as an index:

```python
data = pd.Series([0.25, 0.5, 0.75, 1.0],
                 index=['a', 'b', 'c', 'd'])
print(data)
```

And the item access works as expected:

```python
print(data['b'])
```

We can even use noncontiguous or nonsequential indices:

```python
data = pd.Series([0.25, 0.5, 0.75, 1.0],
                 index=[2, 5, 3, 7])
print(data)
print(data[5])
```

#### Series as Specialized Dictionary
{:.no_toc}

In this way, you can think of a Pandas `Series` a bit like a specialization of a Python dictionary.
A dictionary is a structure that maps arbitrary keys to a set of arbitrary values, and a `Series` is a structure that maps typed keys to a set of typed values.
This typing is important: just as the type-specific compiled code behind a NumPy array makes it more efficient than a Python list for certain operations, the type information of a Pandas `Series` makes it more efficient than Python dictionaries for certain operations.

The `Series`-as-dictionary analogy can be made even more clear by constructing a `Series` object directly from a Python dictionary, here the five most populous US states according to the 2020 census:


```python
population_dict = {'California': 39538223, 'Texas': 29145505,
                   'Florida': 21538187, 'New York': 20201249,
                   'Pennsylvania': 13002700}
population = pd.Series(population_dict)
population
```

### The Pandas `DataFrame` Object


### Data Indexing and Selection


---

## ⭐️ Glossary

### Definitions
{:.no_toc}

<html>
<dl>
  <dt>Data Frame</dt>
  <dd>Data frames are multidimensional arrays taken from a larger dataset. 
They are used to implement specific data operations that may not need the entire dataset.
(In pandas it is called <code>DataFrame</code>)
  </dd>
  <dt>Explicit Index</dt>
  <dd>Uses the values (numeric or non-numeric) set as the index.  For example, if we 
set a column or row as the index then we can use values in the row or column as indices in different 
panda methods. 
  </dd>
  <dt>Implicit Index</dt> 
  <dd>Uses the location (numeric) of the indices, similar to the python style of indexing. 
  </dd>
  <dt>Index</dt>
  <dd>An Index is a value that represents a position (address) in the <code>DataFrame</code> or <code>Series</code>. 
  </dd>
  <dt>Series</dt>
  <dd>A series is an array of related data values that share a connecting factor or property.
  </dd>
</dl>
</html>

### Keywords
{:.no_toc}

* ``import``: Import lets programmers use packages, libraries or modules that have already been programmed. 

* ``<DataFrame>[<string>]``: return the series corresponding to the given column (<string>).

* ``<DataFrame>[<list of strings>]``: returns a given set of columns as a ``DataFrame``.

* ``<DataFrame>[<series/list of Boolean>]``: If the index in the given list is ``True`` then it returns the row from that same index in the ``DataFrame``.

* ``<DataFrame>.loc[ ]``: Uses explicit indexing to return a ``DataFrame`` containing those indices and the values associated with them. 

* ``<DataFrame>.loc[<string1>:<string2>]``: This takes in a range of explicit indices and returns a ``DataFrame`` containing those indices and the values associated with them.

* ``<DataFrame>.loc[<string>]``: Uses an explicit index and return the row(s) for that index value.

* ``<DataFrame>.loc[<list/series of strings>]``: Returns a new ``DataFrame`` containing the labels given in the list of strings.

* ``<DataFrame>.iloc[ ]``: Uses implicit indexing to return a ``DataFrame`` containing those indices and the values associated with them.

* ``<DataFrame>.iloc[<index, range of indices>]``: This takes in an implicit index (or a range of implicit indices) and returns a ``DataFrame`` containing those 
indices and the values associated with them.

* ``<DataFrame>.set_index [<string)>]``: Sets an existing column(s) with the <string> name as the index of the ``DataFrame``. 

* ``<DataFrame>.head(<numeric>)``: Returns the first <numeric> element(s). If no parameter (<numeric>) is set then it will return the first five elements. 

* ``<pandas>.DataFrame(<data>)``: Used to create a ``DataFrame`` with the given data.

* ``<pandas>.read_csv()``: Used to read a csv file into a ``DataFrame``.

* ``<DataFrame>.set_index(<column>)``: Gets the values of the given column and sets them as indices. The output will be sorted in accending order based on the new indices.

* ``<pandas>.to_numeric()``: Converts what is inside the parenthesis into neumeric values. 

* ``<series>.str.startswith(<string>)``: ``.str.startswith()`` (in pandas) checks if a series contains a string(s) that starts with the given prarameter (<string>), 
and returns a boolean value (True or False).
 
* ``<data frame>.sort_index()``: Sorts the different objects in the ``DataFrame``. By default, the ``DataFrame`` is sorted based on the first column in accending order.

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

---

#### Acknowledgement
{: .no_toc }

Content on this page is adapted from [How to Think Like a Data Scientist on Runestone Academy - Brad Miller, Jacqueline Boggs, and Jan Pearce](https://runestone.academy/ns/books/published/httlads/index.html?mode=browsing) and [Python Data Science Handbook - Jake VanderPlas](https://jakevdp.github.io/PythonDataScienceHandbook/).
{: .fs-2 }
