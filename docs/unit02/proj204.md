---
layout: project
title: "💻 PROJECT #2.4"
projectname: "Exploratory Data Analysis"
parent: "2️⃣ Data Science"
nav_order: 8
---

### Overview & Setup


<div class="setup" markdown="block">

1. Go to the `CS3 Project 2.4` assignment on **Blackbaud** and follow the provided **GitHub Classroom** link.
  > 📁 Clicking the link generates a **private repository** for your project with the appropriate starter code. Note that **projects** are stored within the [BWL-CS Organization](https://github.com/BWL-CS), so you _cannot_ access it from the "Your Repositories" page!
2. Open the repository in a **Codespace** whenever you spend time working on the program, in class or at home. 
  > ⚠️ Always remember to `commit changes` after every coding session!
3. When your project is complete, **submit the link to your repository** in the `CS3 Project 2.4` assignment on Blackbaud.

</div>

This is a cumulative project focusing on **Exploratory Data Analysis (EDA)** using Python's `pandas`, `matplotlib`, and `seaborn` libraries. The project aims to demonstrate skills in data wrangling, visualization, and communication of findings through a scientific conference-style poster. You will work with a large, real-world dataset of your choice to perform EDA. The long-term project consists of THREE main deliverables:

1. A descriptive **markdown** text file
2. A **python** code script
3. An academic conference-style **poster** 
> 📰 Make a copy of this [Google Slide Template](https://docs.google.com/presentation/d/1IkrIYBNTEBLFIO7kqUJWvrWhzRuiYhXyX7lxNZglkpU/edit?usp=sharing) for the poster!

#### Dataset Sources:
- [Kaggle](https://www.kaggle.com/)
- [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/index.php)
- [Data.gov](https://www.data.gov/)

---

### Instructions & Requirements

#### ① Markdown file:

- [ ] **Dataset**:
  - Provide a _link_ to the dataset you chose. 
    > In `markdown` syntax, you can format links like this: `[Link text](Link address)` 
- [ ] **Column Descriptions**:
  - Write a brief description of each column in your dataset. Include data types and potential values.
- [ ] **Hypotheses/Questions**:
  - List at least 5 questions you want to explore using your dataset. 
    > _Is there a correlation between two variables?_
    > _How do values in a specific column change over time or categories?_
- [ ] **Visualization Plan**:
  - Explain how you will use visualizations to test your hypotheses. Include the type of chart you plan to use for each question.

#### ② Python script:

Your `main.py` script should be well-organized and demonstrate that you performed meaningful data analysis and generated diverse visualizations.

- [ ] **Load & process the dataset**
  - Handle missing values.
  - Rename columns if necessary for clarity.
  - Convert data types if needed.
  - Filter and/or group data for focused analysis.
- [ ] Contain code for at least **4 different types of visualizations**
  - Ensure each visualization is well-labeled with titles, axis labels, and legends.
  - Visualizations should be clear, informative, and appropriate for the data (_see guidelines below_)
  > See the [Example Graph Gallery](https://python-graph-gallery.com/) for inspiration.
- [ ] Be thoroughly **commented**
  - Explain the purpose of each section of the code.
  - Use functions for reusable components of your code.

#### ③ Poster: 

A scientific poster for an academic conference must effectively communicate **key findings**. All captions and text should be concise and relevant.
  
- [ ] **Introduction**
  - Context for the dataset and why it is interesting/relevant.
  - Clearly state your research questions or hypotheses.
- [ ] **Methods**
  - Describe your process for cleaning and analyzing the data.
  - Include screenshots of key Python code snippets.
- [ ] **Results**
  - Present 2–3 visualizations from your analysis.
  - Provide clear captions for each figure.
- [ ] **Discussion**
  - Interpret your findings and discuss patterns or trends observed in the data.
  - Mention any limitations of your analysis.
- [ ] **Conclusions**
  - Summarize key takeaways.
  - Suggest potential areas for future research or data exploration.
- [ ] **References**
  - Cite the dataset and any external resources
  > 📚 Conduct _research_ on the topic to enhance your poster's **Introduction** and/or **Discussion** sections!

---

### Choosing Appropriate Visualizations

{:.highlight}
💡 Choosing the right type of visualization is crucial for effectively communicating your findings. Below are some **guidelines** to help you decide. Check out this resource from [UC Berkeley](https://guides.lib.berkeley.edu/data-visualization/about) for additional tips.

#### Example Chart Selection Table

| **Question Type**              | **Recommended Chart Type**       |
|--------------------------------|----------------------------------|
| Proportions within a whole                    | Pie chart, Stacked bar plot, Word cloud      |
| Trends over time, sequential events              | Line plot, Animated plots                        |
| Distribution of a variable     | Histogram, Box plot (comparing between groups)             |
| Comparison across categories   | Bar plot, Grouped bar plot (catplot)      |
| Relationships between variables| Scatter plot (two variables), Heatmap (multiple variables)            |

![image](data-viz-cheatsheet.jpeg)

