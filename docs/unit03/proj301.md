---
layout: project
title: "💻 PROJECT #3.1"
projectname: "Flask"
parent: "3️⃣ Flask Web Apps"
nav_order: 5
---

### Overview & Setup

<div class="setup" markdown="block">

1. Go to the `CS3 Project 3.1` assignment on **Blackbaud** and follow the provided **GitHub Classroom** link.
  > 📁 Clicking the link generates a **private repository** for your project with the appropriate starter code. Note that **projects** are stored within the [BWL-CS Organization](https://github.com/BWL-CS), so you _cannot_ access it from the "Your Repositories" page!
2. Open the repository in a **Codespace** whenever you spend time working on the program, in class or at home. 
  > ⚠️ Always remember to `commit changes` after every coding session!
3. When your project is complete, **submit the link to your repository** in the `CS3 Project 3.1` assignment on Blackbaud.

</div>

For your project, you will create a **custom Flask web application** that demonstrates your mastery of Flask, Jinja templates, and the concepts covered in the tutorial. The project is intentionally open-ended to encourage creativity. Choose a theme that interests you and build an app that is interactive, visually appealing, and functional.

#### Project Goal
Design and develop a **themed Flask web application** with at least **three interconnected pages**, using templates, routing, static files, and basic control structures. The app should showcase your skills in creating a dynamic and engaging user experience.

---

### Project Instructions

#### 1. Choose a Theme
Pick a theme for your app that excites you! Examples:
- **Interactive Museum**: A virtual tour showcasing exhibits with descriptions and images.
- **Game Hub**: A hub featuring game stats, leaderboards, or interactive minigames.
- **Fantasy World Explorer**: A site where users can "travel" to different realms, each with unique features.
- **Adventure Guide**: A site with a map of fictional destinations. Each destination page dynamically displays weather, activities, and history.
- **Recipe Book**: A site with recipes and an interactive ingredient search.
- **Music Library**: A site where users can explore albums or songs, complete with audio previews.

#### 2. Create Your Flask App
1. **App Structure**: Organize your app into the following folders and files:
    ```
    project/
    ├── static/
    │   ├── style.css
    │   ├── script.js
    │   └── (images, additional assets)
    ├── templates/
    │   ├── layout.html
    │   ├── (your HTML pages)
    ├── app.py
    └── data.json (optional)
    ```

2. **Routes**:
   - Create routes for at least **three pages**, such as:
     - A **home page** introducing your theme.
     - An **interactive page** where users can input or interact with content.
     - A **customized page** that changes dynamically (e.g., based on URL parameters or user input).

3. **Templates**:
   - Use **template inheritance** to create a shared base layout (e.g., `layout.html`).
   - Include navigation links to all pages.
   - Use Jinja placeholders and control structures for dynamic content.

#### 3. Add Styling and Interactivity
- **CSS**: Style your app to match the theme using custom CSS in the `static/style.css` file.
- **JavaScript** (optional): Add simple interactivity, like a button that displays a message or a dynamic clock.
- **Images and Icons**: Add images or icons in the `static` folder for visual appeal.

#### 4. Showcase Flask Features
Incorporate the following features:
- **Dynamic Data**: Use variables, URL parameters, or data from a JSON file to populate your pages.
- **Control Structures**: Use `if` statements, loops, or conditions in your templates.
- **Static Files**: Include at least one custom CSS file and one image.
- **API Endpoint**: Create a route that serves a JSON response.

---

### Minimum Requirements
1. **Pages**: A minimum of three HTML pages, extending a base template.
2. **Dynamic Content**:
   - At least one page must dynamically change based on input or URL parameters.
   - Use a JSON file or dictionary for a collection of data.
3. **Styling**: A custom CSS file to style your pages.
5. **Static Files**: Use at least one image and one stylesheet.
6. **Documentation**: Include comments in your code explaining key sections.

---

### Bonus Challenges
- Use HTML **forms** to gather user input. 
- Add **user authentication** (e.g., login/logout with dummy data).
- Incorporate **JavaScript** to enhance interactivity.
- Use Flask's `flash` or `session` for notifications or user session data.
- Implement a basic database with `Flask-SQLAlchemy`.

---

#### Acknowledgement
{: .no_toc }

Content on this page is adapted from []().
{: .fs-2 }
