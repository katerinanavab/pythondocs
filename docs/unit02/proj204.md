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
  - Provide a _link_ to the dataset you chose. You may use platforms like Kaggle, UCI Machine Learning Repository, or government open data portals.
  > Note that in `markdown`, you can format links like this: `[Link text](Link address)` 
- [ ] **Column Descriptions**:
  - Write a brief description of each column in your dataset. Include data types and potential values.
- [ ] **Hypotheses/Questions**:
  - List at least 5 questions you want to explore using your dataset. 
    - _Is there a correlation between two variables?_
    - _How do values in a specific column change over time or categories?_
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
  - See the [Example Graph Gallery](https://python-graph-gallery.com/) for inspiration
  - Ensure each visualization is well-labeled with titles, axis labels, and legends.
  - Visualizations should be clear, informative, and appropriate for the data (_see guidelines below_)
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
  - Cite the dataset and any external resources (_research on the topic for your poster's Introduction and/or Discussion sections_).

---

### Choosing Appropriate Visualizations

{:.highlight}
💡 Choosing the right type of visualization is crucial for effectively communicating your findings. Below are some **guidelines** to help you decide. Check out this resource from [UC Berkeley](https://guides.lib.berkeley.edu/data-visualization/about) for additional tips.

1. **Understand the Nature of Your Data**
  - **Categorical Data**:
    - Use **bar plots** or **pie charts** to show proportions or comparisons between categories.
  - **Numerical Data**:
    - Use **histograms** or **box plots** to display distributions.
    - Use **scatter plots** to show relationships between two numerical variables.
  - **Time-Series Data**:
    - Use **line plots** to show trends over time.
2. **Match the Visualization to Your Question**
  - **Comparisons Across Groups**:
    - Bar plots or grouped bar plots work well.
    - Consider box plots if comparing distributions between groups.
  - **Relationships Between Variables**:
    - Scatter plots are ideal for two numerical variables.
    - Heatmaps can show correlations between multiple variables.
  - **Proportions**:
    - Pie charts or stacked bar plots can highlight proportions within a whole.
  - **Trends**:
    - Line plots are best for visualizing trends over time or sequential events.
3. **Highlight Key Insights**
    - Use color and annotations sparingly but effectively to emphasize critical points.
    - Avoid clutter by focusing on the most relevant data.
4. **Keep Accessibility in Mind**
    - Ensure your visualizations are easy to interpret:
      - Include clear titles, axis labels, and legends.
      - Choose color palettes that are colorblind-friendly (e.g., Seaborn's default palette).

#### Example Chart Selection Table

| **Question Type**              | **Recommended Chart Type**       |
|--------------------------------|----------------------------------|
| Proportions                    | Pie chart, Stacked bar plot      |
| Trends over time               | Line plot                        |
| Distribution of a variable     | Histogram, Box plot              |
| Comparison across categories   | Bar plot, Grouped bar plot (catplot)      |
| Relationships between variables| Scatter plot, Heatmap            |

![image](data-viz-cheatsheet.jpeg)

