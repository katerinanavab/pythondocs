---
layout: project
title: "💻 PROJECT #3.2"
projectname: "C.R.U.D. Web App"
parent: "3️⃣ Flask Web Apps"
nav_order: 5
---

### Project Overview

This project will help you practice **full-stack development** using `Flask` and `SQLAlchemy`, while allowing you to explore a topic that interests you. Choose a theme, be creative, and have fun! 🚀

<html>
  <details>
    <summary>📥 SETUP & SUBMISSION INSTRUCTIONS</summary>

<div class="setup" markdown="block">

1. Go to the `CS3 Project 3.2` assignment on **Blackbaud** and follow the provided **GitHub Classroom** link.
  > 📁 Clicking the link generates a **private repository** for your project with the appropriate starter code. Note that **projects** are stored within the [BWL-CS Organization](https://github.com/BWL-CS), so you _cannot_ access it from the "Your Repositories" page!
2. Open the repository in a **Codespace** whenever you spend time working on the program, in class or at home. 
  > ⚠️ Always remember to `commit changes` after every coding session!
3. When your project is complete, **submit the link to your repository** in the `CS3 Project 3.2` assignment on Blackbaud.

</div>

    
  </details>
</html>

---

### Project Instructions

#### 1. Choose a Theme
Pick a theme for your app that excites you! Your app should **store, display, and modify data** from an SQLite database. _Examples:_

- **Shopping List App**: A shopping list app where users can add, edit, and delete items.
- **Event Planner**: A portal for creating and sharing social plans with friends.
- **Library System**: A database of books with borrowing and returning functionality.
- **Movie Collection**: A catalog where users can add, rate, and review movies.
- **Recipe Manager**: A site where users can create, update, and delete recipes.
- **Fantasy World Explorer**: A site where users create and manage characters, locations, or quests.

#### 2. Set Up Your Flask App
- **App Structure**: Organize your app into the following folders and files:
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
    ```

- **Install Dependencies**:
   ```bash
   pip install flask flask-sqlalchemy
   ```

#### 3. Database Setup
- **Define a database model** in `app.py` using `Flask-SQLAlchemy`.
- Include at least **three fields** (e.g., `id`, `name`, `date_created`).
- _Example:_
   ```python
   from flask_sqlalchemy import SQLAlchemy
   from datetime import datetime, timezone

   db = SQLAlchemy()

   class Task(db.Model):
       id = db.Column(db.Integer, primary_key=True)
       content = db.Column(db.String(200), nullable=False)
       date_created = db.Column(db.DateTime, default=datetime.utcnow)
   ```

#### 4. Implement CRUD Operations

Your app must support the **Create, Read, Update, and Delete** operations. _Below are the required features:_

##### CREATE (Add Data)
- Use an HTML `<form>` to **submit data**.
- **Store** the data in an `SQLite` database.
- _Example:_
   ```python
   @app.route('/', methods=['POST'])
   def add_task():
       task_content = request.form['content']
       new_task = Task(content=task_content)
       db.session.add(new_task)
       db.session.commit()
   ```

##### READ (View Data)
- **Fetch** records from the database and **display** them using a `Jinja` template.
- _Example:_
   ```python
   @app.route('/')
   def index():
       tasks = Task.query.order_by(Task.date_created).all()
       return render_template('index.html', tasks=tasks)
   ```

##### UPDATE (Modify Data)
- Provide an option to **edit** existing records.
- _Example:_
   ```python
   @app.route('/update/<int:id>', methods=['GET', 'POST'])
   def update(id):
       task = Task.query.get_or_404(id)
       if request.method == 'POST':
           task.content = request.form['content']
           db.session.commit()
           return redirect('/')
       return render_template('update.html', task=task)
   ```

##### DELETE (Remove Data)
- Implement a **delete button** to remove entries.
- _Example:_
   ```python
   @app.route('/delete/<int:id>')
   def delete(id):
       task_to_delete = Task.query.get_or_404(id)
       db.session.delete(task_to_delete)
       db.session.commit()
       return redirect('/')
   ```

#### 5. Create HTML Templates
- Use [Jinja](https://jinja.palletsprojects.com/en/stable/) to dynamically display data.
- Extend a base template (`layout.html`) for consistent navigation.
- *Example:* `index.html`
  ```html
  {% raw %}
  {% extends "layout.html" %}
  
  {% block content %}
  <h2>Task List</h2>
  <ul>
      {% for task in tasks %}
      <li>{{ task.content }} - <a href="/update/{{task.id}}">Edit</a> | <a href="/delete/{{task.id}}">Delete</a></li>
      {% endfor %}
  </ul>
  
  <form action="/" method="POST">
      <input type="text" name="content" required>
      <button type="submit">Add Task</button>
  </form>
  {% endblock %}
  {% endraw %}
  ```

#### 6. Style Your App
- **CSS**: Create a `static/style.css` file for styling.
- **Bootstrap (Optional)**: Use [Bootstrap](https://getbootstrap.com/docs/5.3/getting-started/introduction/) for a responsive UI.
- **Images/Icons**: Store visuals in the `static` folder.

#### 7. Serve Your App
Run your Flask app:
  ```bash
  python app.py
  ```
If using Flask’s built-in development server:
  ```python
  if __name__ == "__main__":
      with app.app_context():
          db.create_all()
      app.run(debug=True)
  ```

---

### Minimum Requirements
- [ ] At least **three HTML pages** extending a base template.  
- [ ] A **Flask-SQLAlchemy database** with at least **one model**.  
- [ ] **CRUD functionality** (Create, Read, Update, Delete).  
- [ ] A **form** to add records.  
- [ ] A **delete button** to remove records.  
- [ ] Styling using **CSS** or **Bootstrap**.  
- [ ] At least **one image** in the `static` folder.  
- [ ] Use of **template inheritance** and Jinja control structures.  

---

### Bonus Challenges
- 🎯 Add **user authentication** (login/logout).  
- 🎯 Use `JavaScript` for **live updates** or **form validation**.  
- 🎯 Add a **REST API endpoint** returning `JSON` data.  
- 🎯 Use Flask’s `flash` messages for user feedback.  
