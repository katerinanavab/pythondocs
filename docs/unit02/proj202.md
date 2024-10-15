---
layout: project
title: "💻 PROJECT #2.2"
projectname: "Visualize Our Class"
parent: "2️⃣ Data Science"
nav_order: 6
---

### Overview & Setup

In this project, you will work together to create a Pandas DataFrame containing data on each member of the class, which you will later use to create data visualizations using `matplotlib`. This assignment has two parts: 

1. **Collaborative Data Collection**: You will work together as a class to design and collect data into a single DataFrame.
2. **Independent Visualization**: You will choose an aspect of the data to create your own data visualization using `matplotlib`.


<div class="setup" markdown="block">

1. Go to the `CS3 Project 2.2` assignment on **Blackbaud** and follow the provided **GitHub Classroom** link.
  > 📁 Clicking the link generates a **private repository** for your project with the appropriate starter code. Note that **projects** are stored within the [BWL-CS Organization](https://github.com/BWL-CS), so you _cannot_ access it from the "Your Repositories" page!
2. Open the repository in a **Codespace** whenever you spend time working on the program, in class or at home. 
  > ⚠️ Always remember to `commit changes` after every coding session!
3. When your project is complete, **submit the link to your repository** in the `CS3 Project 2.2` assignment on Blackbaud.

</div>

### Instructions


#### 🐼 Part A: Collaborative Data Collection

In this part, the class will work together to design a Pandas DataFrame that contains data on each student. You will be interviewing your classmates to gather this data.

<div class="task" markdown="block">

1. **Choose the Columns for the DataFrame**: 
    - Decide as a class what kinds of data to collect. This could include basic information such as:
      - Name
      - Age
      - Favorite Subject
      - Number of Siblings
      - Favorite Movie Genre
      - Hours Spent on Hobbies per Week
      - GPA
      - Favorite Sports Team
      - Any other creative data you come up with as a class!
2. **Conduct Interviews**: 
    - Each student will interview the rest of the classmates to fill in the data for the DataFrame.
    - Make sure you are accurate and respectful when collecting information.
3. **Create the DataFrame**:
    - Once all the data is collected, combine it into a Pandas DataFrame. This can be done by sharing the data and using Python code to structure it.
    - _Example of creating a simple DataFrame:_
      ```python      
      data = {
          'Name': ['Alice', 'Bob', 'Charlie'],
          'Age': [17, 18, 17],
          'Favorite Subject': ['Math', 'History', 'Biology']
      }
      df = pd.DataFrame(data)
      ```
4. **Save the DataFrame**:
    - Save the class DataFrame into a CSV file that everyone can access.
    - _Example of saving the DataFrame to a file:_
      ```python
      df.to_csv('class_data.csv', index=False)
      ```
</div>

#### 📊 Part B: Independent Data Visualization

Now that we have a class DataFrame, you will each work independently to create your own **unique** data visualizations. You will choose any subset of the data to visualize using `matplotlib`. You are free to explore any kind of visualization that helps you understand the data better.

<div class="imp" markdown="block">

Here are some common types of visualizations that `matplotlib` can create:
- **Bar Chart**: Useful for comparing categories of data.
- **Line Plot**: Great for showing trends over time or continuous data.
- **Scatter Plot**: Useful for showing the relationship between two variables.
- **Pie Chart**: Ideal for showing parts of a whole (distribution of categories).
- **Histogram**: Perfect for showing the distribution of a single variable.

</div>

<br>

<div class="task" markdown="block">
  
1. **Choose Your Focus**:
    - Decide what part of the class DataFrame you want to visualize. This could be:
      - A comparison of favorite subjects.
      - A bar chart showing the average GPA of students by their favorite sports teams.
      - A line plot tracking the number of siblings each student has by age.
      - A pie chart showing the distribution of favorite movie genres.
2. **Create Your Visualization**:
    - Using `matplotlib`, create your visualization.
      - You can _clean_ or _filter_ the data as needed.
      - Use `plt.savefig('figure1.png', bbox_inches='tight')` to _save your figure_ as a PNG. 
    - Feel free to explore and create as many figures as you want, but check with me to make sure you generate **at least ONE type of visualization** that no one else in the class is doing!!!
3. **Interpret the Visualization**:
    - In a `''' multi-line comment '''`, write a few sentences about what your visualization tells you about the data.
    - What _trends_, _patterns_, or _insights_ can you gather from your chart?


</div>


---

#### Acknowledgement
{: .no_toc }

Content on this page is adapted from [How to Think Like a Data Scientist on Runestone Academy - Brad Miller, Jacqueline Boggs, and Jan Pearce](https://runestone.academy/ns/books/published/httlads/index.html?mode=browsing).
{: .fs-2 }
