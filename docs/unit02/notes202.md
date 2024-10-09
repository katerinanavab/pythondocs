---
layout: notes
title: "📓2.2: Matplotlib" 
parent: "2️⃣ Data Science"
nav_order: 2
---

## Table of Contents
{: .no_toc .text-delta }

{: .fs-2 }
- TOC
{:toc}

---
## What is Data Visualization?

First, discuss: [One Dataset, Visualized 25 Ways](https://flowingdata.com/2017/01/24/one-dataset-visualized-25-ways/)

We'll now take an in-depth look at the `Matplotlib` package for **visualization** in Python. Matplotlib is a multiplatform data visualization library built on `NumPy` arrays and designed to work with the broader `SciPy` stack.

* It was conceived by John Hunter in 2002, originally as a patch to IPython for enabling interactive MATLAB-style plotting via `gnuplot` from the IPython command line.
* IPython's creator, Fernando Perez, was at the time scrambling to finish his PhD, and let John know he wouldn’t have time to review the patch for several months.
* John took this as a cue to set out on his own, and the Matplotlib package was born, with version 0.1 released in 2003.
* It received an early boost when it was adopted as the plotting package of choice of the Space Telescope Science Institute (the folks behind the **Hubble Telescope**), which financially supported Matplotlib’s development and greatly expanded its capabilities.

---

## General Matplotlib Tips

Before we dive into the details of creating visualizations with Matplotlib, there are a few useful things you should know about using the package.

### Importing Matplotlib

Just as we use the `np` shorthand for NumPy and the `pd` shorthand for Pandas, we will use some standard shorthands for Matplotlib imports:

```python
import matplotlib as mpl
import matplotlib.pyplot as plt
```

The `plt` interface is what we will use most often, as you shall see throughout this part of the book.

### Setting Styles

We will use the `plt.style` directive to choose appropriate aesthetic styles for our figures. Here we will set the `classic` style, which ensures that the plots we create use the classic Matplotlib style:

```python
plt.style.use('classic')
```

For more information on stylesheets, see [Styling Matplotlib]().

### How to Display Your Plots

A visualization you can't see won't be of much use!

If you are using Matplotlib from within a script, the function `plt.show` is your friend.
`plt.show` starts an event loop, looks for all currently active `Figure` objects, and opens one or more interactive windows that display your figure or figures.

So, for example, you may have a file containing the following:

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 10, 100)

plt.plot(x, np.sin(x))
plt.plot(x, np.cos(x))

plt.show()
```

The `plt.show` command does a lot under the hood, as it must interact with your system's interactive graphical backend.
The details of this operation can vary greatly from system to system and even installation to installation, but Matplotlib does its best to hide all these details from you.

One thing to be aware of: the `plt.show` command should be used *only once* per Python session, and is most often seen at the very end of the script.
Multiple `show` commands can lead to unpredictable backend-dependent behavior, and should mostly be avoided.

### Saving Figures to File

One nice feature of Matplotlib is the ability to save figures in a wide variety of formats.
Saving a figure can be done using the `savefig` command.
For example, to save the previous figure as a PNG file, we can run this:


```python
fig.savefig('my_figure.png')
```

We now have a file called *my_figure.png* in the current working directory.

In `savefig`, the file format is inferred from the extension of the given filename.

Note that when saving your figure, it is not necessary to use `plt.show` or related commands discussed earlier.


---

#### Acknowledgement
{: .no_toc }

Content on this page is adapted from [Python Data Science Handbook - Jake VanderPlas](https://jakevdp.github.io/PythonDataScienceHandbook).
{: .fs-2 }
