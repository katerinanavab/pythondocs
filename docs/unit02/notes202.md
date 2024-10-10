---
layout: notes
title: "📓2.2: Matplotlib Plotting" 
parent: "2️⃣ Data Science"
nav_order: 2
---

## Table of Contents
{: .no_toc .text-delta }

{: .fs-2 }
- TOC
{:toc}

---
## What is Data Visualization? 📈📊📉

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
{:.no_toc}

Just as we use the `np` shorthand for NumPy and the `pd` shorthand for Pandas, we will use some standard shorthands for Matplotlib imports:

```python
import matplotlib as mpl
import matplotlib.pyplot as plt
```

The `plt` interface is what we will use most often, as you shall see throughout this part of the book.

### Setting Styles
{:.no_toc}

We will use the `plt.style` directive to choose appropriate aesthetic styles for our figures. Here we will set the `classic` style, which ensures that the plots we create use the classic Matplotlib style:

```python
plt.style.use('classic')
```

For more information on stylesheets, see [Styling Matplotlib](https://coderina.dev/pythondocs/docs/unit02/notes203.html).

### How to Display Your Plots
{:.no_toc}

A visualization you can't see won't be of much use!

If you are using Matplotlib from within a script, the function `plt.show` is your friend.
`plt.show` starts an event loop, looks for all currently active `Figure` objects, and opens one or more interactive windows that display your figure or figures.

So, for example, you may have a file containing the following:

```python
# Generate values to plot
x = np.linspace(0, 10, 100)

plt.plot(x, np.sin(x))
plt.plot(x, np.cos(x))

plt.show()
```

The `plt.show` command does a lot under the hood, as it must interact with your system's interactive graphical backend.
The details of this operation can vary greatly from system to system and even installation to installation, but Matplotlib does its best to hide all these details from you.

One thing to be aware of: the `plt.show` command should be used *only once* per Python session, and is most often seen at the very end of the script.
Multiple `show` commands can lead to unpredictable backend-dependent behavior, and should mostly be avoided.

### Saving Figures to Files
{:.no_toc}

One nice feature of Matplotlib is the ability to save figures in a wide variety of formats.

Saving a figure can be done using the `savefig` command.
For example, to save the previous figure as a `PNG` file, we can run this:

```python
fig.savefig('my_figure.png')
```

We now have a file called *my_figure.png* in the current working directory.

In `savefig`, the file format is inferred from the extension of the given filename.

{:.highlight}
Note that when saving your figure, it is not necessary to use `plt.show` or related commands discussed earlier.

---
## Line Plots

Perhaps the simplest of all plots is the visualization of a single function `y = f(x)`.

<div class="task" markdown="block">

Create a new python script called `lineplots.py` in your working directory and set it up as follows:

```python
import numpy as np
import matplotlib.pyplot as plt
plt.style.use('seaborn-whitegrid')

fig = plt.figure()
ax = plt.axes()
```

</div>

For all Matplotlib plots, we start by creating a `figure` object and `axes`.

* In Matplotlib, the *figure* (an instance of the class `plt.Figure`) can be thought of as a single container that contains all the objects representing axes, graphics, text, and labels.
* The *axes* (an instance of the class `plt.Axes`) is what we see above: a bounding box with ticks, grids, and labels, which will eventually contain the plot elements that make up our visualization.

Throughout this part of the book, I'll commonly use the variable name `fig` to refer to a figure instance and `ax` to refer to an axes instance or group of axes instances.

Once we have created an axes, we can use the `ax.plot` method to plot some data. Let's start with a simple sinusoid, as shown in the following figure:


```python
x = np.linspace(0, 10, 1000)
ax.plot(x, np.sin(x))
```

### Line Colors and Styles

🎨 The first adjustment you might wish to make to a plot is to control the line colors and styles. The `plt.plot` function takes additional arguments that can be used to specify these.

To adjust the color, you can use the `color` keyword, which accepts a string argument representing virtually any imaginable color:

```python
plt.plot(x, np.sin(x - 0), color='blue')        # specify color by name
plt.plot(x, np.sin(x - 1), color='g')           # short color code (rgbcmyk)
plt.plot(x, np.sin(x - 2), color='0.75')        # grayscale between 0 and 1
plt.plot(x, np.sin(x - 3), color='#FFDD44')     # hex code (RRGGBB, 00 to FF)
plt.plot(x, np.sin(x - 4), color=(1.0,0.2,0.3)) # RGB tuple, values 0 to 1
plt.plot(x, np.sin(x - 5), color='chartreuse'); # HTML color names supported
```

{:.highlight}
If no color is specified, Matplotlib will automatically cycle through a set of default colors for multiple lines.

Similarly, the line style can be adjusted using the `linestyle` keyword (see the following figure):

```python
plt.plot(x, x + 0, linestyle='solid')
plt.plot(x, x + 1, linestyle='dashed')
plt.plot(x, x + 2, linestyle='dashdot')
plt.plot(x, x + 3, linestyle='dotted');

# For short, you can use the following codes:
plt.plot(x, x + 4, linestyle='-')  # solid
plt.plot(x, x + 5, linestyle='--') # dashed
plt.plot(x, x + 6, linestyle='-.') # dashdot
plt.plot(x, x + 7, linestyle=':');  # dotted
```

Though it may be less clear to someone reading your code, you can save some keystrokes by combining these `linestyle` and `color` codes into a single non-keyword argument to the `plt.plot` function; the following figure shows the result:

```python
plt.plot(x, x + 0, '-g')   # solid green
plt.plot(x, x + 1, '--c')  # dashed cyan
plt.plot(x, x + 2, '-.k')  # dashdot black
plt.plot(x, x + 3, ':r');  # dotted red
```
> These single-character color codes reflect the standard abbreviations in the **RGB (Red/Green/Blue)** and **CMYK (Cyan/Magenta/Yellow/blacK)** color systems, commonly used for digital color graphics.

### Axes Limits

Matplotlib does a decent job of choosing default axes limits for your plot, but sometimes it's nice to have finer control.

The most basic way to adjust the limits is to use the `plt.xlim` and `plt.ylim` functions:

```python
plt.plot(x, np.sin(x))

plt.xlim(-1, 11)
plt.ylim(-1.5, 1.5);
```

If for some reason you'd like either axis to be displayed in _reverse_, you can simply reverse the order of the arguments:

```python
plt.plot(x, np.sin(x))

plt.xlim(10, 0)
plt.ylim(1.2, -1.2);
```

A useful related method is `plt.axis` (note here the potential confusion between *axes* with an *e*, and *axis* with an *i*), which allows more qualitative specifications of axis limits. For example, you can automatically tighten the bounds around the current content, as shown in the following figure:

```python
plt.plot(x, np.sin(x))
plt.axis('tight')
```

Or you can specify that you want an equal axis ratio, such that one unit in `x` is visually equivalent to one unit in `y`, as seen in the following figure:

```python
plt.plot(x, np.sin(x))
plt.axis('equal')
```

Other axis options include `'on'`, `'off'`, `'square'`, `'image'`, and more. For more information on these, refer to the `plt.axis` docstring.

### Labeling Plots

As the last piece of this chapter, we'll briefly look at the _labeling_ of plots: titles, axis labels, and simple legends.

**Titles** and **axis labels** are the simplest such labels—there are methods that can be used to quickly set them (see the following figure):


```python
plt.plot(x, np.sin(x))
plt.title("A Sine Curve")
plt.xlabel("x")
plt.ylabel("sin(x)")
```

The position, size, and style of these labels can be adjusted using optional arguments to the functions, described in the docstrings.

When multiple lines are being shown within a single axes, it can be useful to create a **plot legend** that labels each line type.

Again, Matplotlib has a built-in way of quickly creating such a legend; it is done via the (you guessed it) `plt.legend` method.

Though there are several valid ways of using this, I find it easiest to specify the label of each line using the `label` keyword of the `plot` function (see the following figure):

```python
plt.plot(x, np.sin(x), '-g', label='sin(x)')
plt.plot(x, np.cos(x), ':b', label='cos(x)')
plt.axis('equal')

plt.legend()
```

---

## Scatter Plots

Another commonly used plot type is the **simple scatter plot**, a close cousin of the line plot. Instead of points being joined by line segments, here the points are represented individually with a **dot**, **circle**, or other shape.

<div class="task" markdown="block">

Create a new python script called `scatterplots.py` in your working directory and set it up as follows:

```python
import numpy as np
import matplotlib.pyplot as plt
plt.style.use('seaborn-whitegrid')
```

</div>

### Scatter Plots with plt.plot

In the previous chapter we looked at using `plt.plot`/`ax.plot` to produce line plots.
It turns out that this same function can produce scatter plots as well:

```python
x = np.linspace(0, 10, 30)
y = np.sin(x)

plt.plot(x, y, 'o', color='black')
```

The third argument in the function call is a character that represents the type of symbol used for the plotting. Just as you can specify options such as `'-'` or `'--'` to control the line style, the marker style has its own set of short string codes. The full list of available symbols can be seen in the documentation of `plt.plot`, or in Matplotlib's [online documentation](https://matplotlib.org/stable/api/_as_gen/matplotlib.markers.MarkerStyle.html). 

```python
rng = np.random.default_rng(0)
for marker in ['o', '.', ',', 'x', '+', 'v', '^', '<', '>', 's', 'd']:
    plt.plot(rng.random(2), rng.random(2), marker, color='black',
             label="marker='{0}'".format(marker))
plt.legend(numpoints=1, fontsize=13)
plt.xlim(0, 1.8)
```

For even more possibilities, these character codes can be used together with line and color codes to plot points along with a line connecting them (see the following figure):

```python
plt.plot(x, y, '-ok');
```

Additional keyword arguments to `plt.plot` specify a wide range of properties of the lines and markers, as you can see in the following figure:

```python
plt.plot(x, y, '-p', color='gray',
         markersize=15, linewidth=4,
         markerfacecolor='white',
         markeredgecolor='gray',
         markeredgewidth=2)
plt.ylim(-1.2, 1.2);
```

These kinds of options make `plt.plot` the **primary workhorse for two-dimensional plots** in Matplotlib.

For a full description of the options available, refer to the [`plt.plot` documentation](https://matplotlib.org/3.5.0/api/_as_gen/matplotlib.pyplot.plot.html).

### Scatter Plots with plt.scatter

A second, more powerful method of creating scatter plots is the `plt.scatter` function, which can be used very similarly to the `plt.plot` function (see the following figure):

```python
plt.scatter(x, y, marker='o');
```    

The primary difference of `plt.scatter` from `plt.plot` is that it can be used to create scatter plots where the properties of each individual point (size, face color, edge color, etc.) can be individually controlled or mapped to data.

Let's show this by creating a random scatter plot with points of many colors and sizes.
In order to better see the overlapping results, we'll also use the `alpha` keyword to adjust the transparency level (see the following figure):


```python
rng = np.random.default_rng(0)
x = rng.normal(size=100)
y = rng.normal(size=100)
colors = rng.random(100)
sizes = 1000 * rng.random(100)

plt.scatter(x, y, c=colors, s=sizes, alpha=0.3)
plt.colorbar();  # show color scale
```

Notice that the color argument is automatically mapped to a color scale (shown here by the `colorbar` command), and that the size argument is given in pixels.
In this way, the color and size of points can be used to convey information in the visualization, in order to visualize multidimensional data.

For example, we might use the Iris dataset from Scikit-Learn, where each sample is one of three types of flowers that has had the size of its petals and sepals carefully measured:

```python
from sklearn.datasets import load_iris
iris = load_iris()
features = iris.data.T

plt.scatter(features[0], features[1], alpha=0.4,
            s=100*features[3], c=iris.target, cmap='viridis')
plt.xlabel(iris.feature_names[0])
plt.ylabel(iris.feature_names[1])
```  

We can see that this scatter plot has given us the ability to simultaneously explore **four different dimensions** of the data:

* the (*x*, *y*) **location** of each point corresponds to the sepal length and width
* the **size** of the point is related to the petal width
* the **color** is related to the particular species of flower


---

## Histograms, Binning, and Density

A simple histogram can be a great first step in understanding a dataset. Matplotlib's `hist` function creates a basic histogram in one line.

<div class="task" markdown="block">

Create a new python script called `histograms.py` in your working directory and set it up as follows:

```python
import numpy as np
import matplotlib.pyplot as plt
plt.style.use('seaborn-whitegrid')

rng = np.random.default_rng(1701)
data = rng.normal(size=1000)

plt.hist(data)
```

</div>


The `hist` function has many options to tune both the calculation and the display;
here's an example of a more customized histogram, shown in the following figure:


```python
plt.hist(data, bins=30, density=True, alpha=0.5,
         histtype='stepfilled', color='steelblue',
         edgecolor='none');
```

The `plt.hist` docstring has more information on other available customization options.
I find this combination of `histtype='stepfilled'` along with some transparency `alpha` to be helpful when comparing histograms of several distributions (see the following figure):


```python
x1 = rng.normal(0, 0.8, 1000)
x2 = rng.normal(-2, 1, 1000)
x3 = rng.normal(3, 2, 1000)

kwargs = dict(histtype='stepfilled', alpha=0.3, density=True, bins=40)

plt.hist(x1, **kwargs)
plt.hist(x2, **kwargs)
plt.hist(x3, **kwargs);
```

Just as we create histograms in one dimension by dividing the number line into bins, we can also create histograms in two dimensions by dividing points among two-dimensional bins.

We'll start by defining some data—an `x` and `y` array drawn from a multivariate Gaussian distribution:

```python
mean = [0, 0]
cov = [[1, 1], [1, 2]]
x, y = rng.multivariate_normal(mean, cov, 10000).T
```

### plt.hist2d: Two-dimensional histogram

One straightforward way to plot a two-dimensional histogram is to use Matplotlib's `plt.hist2d` function (see the following figure):


```python
plt.hist2d(x, y, bins=30)
cb = plt.colorbar()
cb.set_label('counts in bin')
```

 


Just like `plt.hist`, `plt.hist2d` has a number of extra options to fine-tune the plot and the binning, which are nicely outlined in the function docstring.
Further, just as `plt.hist` has a counterpart in `np.histogram`, `plt.hist2d` has a counterpart in `np.histogram2d`:

```python
counts, xedges, yedges = np.histogram2d(x, y, bins=30)
print(counts.shape)
```

For the generalization of this histogram binning when there are more than two dimensions, see the `np.histogramdd` function.

### plt.hexbin: Hexagonal binnings

The two-dimensional histogram creates a tesselation of squares across the axes.
Another natural shape for such a tesselation is the regular hexagon.
For this purpose, Matplotlib provides the `plt.hexbin` routine, which represents a two-dimensional dataset binned within a grid of hexagons (see the following figure):


```python
plt.hexbin(x, y, gridsize=30)
cb = plt.colorbar(label='count in bin')
```


`plt.hexbin` has a number of additional options, including the ability to specify weights for each point and to change the output in each bin to any NumPy aggregate (mean of weights, standard deviation of weights, etc.).


---

#### Acknowledgement
{: .no_toc }

Content on this page is adapted from [Python Data Science Handbook - Jake VanderPlas](https://jakevdp.github.io/PythonDataScienceHandbook).
{: .fs-2 }
