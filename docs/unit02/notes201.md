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

## 🐼 Pandas with Movie Data

Data scientists have to deal with a lot of data at once. While Google Sheets and Excel are great ways to visualize and manipulate data, they are not as _versatile_ as we might want. In this chapter, you will be introduced to **data frames** and learn to use them to obtain information from data.

#### Using a GitHub Template for class notes

<div class="setup" markdown="block">

1. Go to the public template **repository** for our class: [BWL-CS Python Template](https://github.com/BWL-CS/python-template)
2. Click the <button type="button" name="button" class="btn btn-green">Use this template</button> button above the list of files then select `Create a new repository`
3. Specify the **repository name**: `CS3-Unit-2-Pandas`
4. Click <button type="button" name="button" class="btn btn-green">Create repository</button>
    > Now you have **your own personal copy** of this starter code that you can always access under the `Your repositories` section of GitHub! 
5. Now on your repository, click <button type="button" name="button" class="btn btn-green"> < > Code </button> and select the `Codespaces` tab
6. Click `Create Codespace on main` and wait for the environment to load, _then you're ready to code_!
7. 📝 Take notes in this Codespace during class, coding along with the instructor.

</div>

### Exploring the Data

We're going to be using a dataset about movies to try out processing some data with the `Pandas` library. A [Python Library](https://www.geeksforgeeks.org/libraries-in-python/) is a collection of related modules. It contains bundles of code that can be used repeatedly in different programs.

<div class="task" markdown="block">

1. We start with some standard **imports**:

```python
import pandas as pd
import numpy as np
```

2. Download the `movies_metadata.csv` file from [Kaggle](https://www.kaggle.com/rounakbanik/the-movies-dataset) and upload it to your repository. 

3. **Load** the data from a local file using `pandas`:

```python
df = pd.read_csv('movies_metadata.csv').dropna(axis=1, how='all')
df.head()
```

4. Let's see what data we have:

```python
df.shape
```

5. Twenty-three columns of data for over 45,000 movies is going be a lot to look
at, but let's start by looking at what the columns represent:

```python
df.columns
```

</div>

<html>
<details markdown="block">
<summary>Explanation of Columns</summary>
  
- **belongs_to_collection:** A stringified dictionary that identifies the
  collection that a movie belongs to (if any).
- **budget:** The budget of the movie in dollars.
- **genres:** A stringified list of dictionaries that list out all the genres
  associated with the movie.
- **homepage:** The Official Homepage of the movie.
- **id:** An arbitrary ID for the movie.
- **imdb_id:** The IMDB ID of the movie.
- **original_language:** The language in which the movie was filmed.
- **original_title:** The title of the movie in its original language.
- **overview:** A blurb of the movie.
- **popularity:** The Popularity Score assigned by TMDB.
- **poster_path:** The URL of the poster image (relative to
  http://image.TMDB.org/t/p/w185/).
- **production_companies:** A stringified list of production companies involved
  with the making of the movie.
- **production_countries:** A stringified list of countries where the movie was
  filmed or produced.
- **release_date:** Theatrical release date of the movie.
- **revenue:** World-wide revenue of the movie in dollars.
- **runtime:** Duration of the movie in minutes.
- **spoken_languages:** A stringified list of spoken languages in the film.
- **status:** Released, To Be Released, Announced, etc.
- **tagline:** The tagline of the movie.
- **title:** The official title of the movie.
- **video:** Indicates if there is a video present of the movie with TMDB.
- **vote_average:** The average rating of the movie on TMDB.
- **vote_count:** The number of votes by users, as counted by TMDB.
  
</details>
</html>

### Filtering the Data

Let’s start by only looking at films that cost over a million dollars to make.

<div class="task" markdown="block">

Create a variable called ``budget_df`` that contains all columns for the movies
whose budget was over a million dollars.
```python
budget_df = [] # fill in the brackets
budget_df.shape
```

</div>

> 💬: *How many movies have a budget over 1 million dollars?* 

With this more manageable list of 7000+ movies, I’d like to have a way to **look
up the budget** of a particular movie.

<div class="task" markdown="block">

Create a Series object called ``budget_lookup`` such that you are able to use a
call to ``budget_lookup['Dead Presidents']`` to find the budget of that movie.
```python
budget_lookup = [] # fill in the brackets
budget_lookup['Dead Presidents']
```

</div>

> 💬: *What was the budget for Dead Presidents?* 

Let's say I have figured out that the first (alphabetically) movie whose title starts with
an "A" is "A Bag of Hammers" and the last movie that starts with a "B" is
"Byzantium".

```python
# Get first movie whose title starts with A
budget_lookup[budget_lookup.index.str.startswith('A')].sort_index()[[0]]
# Get last movie whos title starts with B
budget_lookup[budget_lookup.index.str.startswith('B')].sort_index()[[-1]]
```

<div class="task" markdown="block">

Use that knowledge to create a `Series` that contains budget informations for all the movies that start with an "A" or a "B". 
> **Hint:** No need to use ``startswith`` like I did above, just use the movie **titles** to do a _slice_.

```python
budget_lookup_as_and_bs = [] # fill in the brackets
budget_lookup_as_and_bs.shape
```

</div>

> 💬: ***How many** movies with a budget of over a million dollars and whose title starts with an "A" or a "B" are there?*

### Numbers as Indices

### Dealing with Multiple DataFrames

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

Content on this page is adapted from [How to Think Like a Data Scientist on Runestone Academy - Brad Miller, Jacqueline Boggs, and Jan Pearce](https://runestone.academy/ns/books/published/httlads/index.html?mode=browsing).
{: .fs-2 }
