---
layout: project
title: "💻 PROJECT #3.2"
projectname: "C.R.U.D. Web App"
parent: "3️⃣ Flask Web Apps"
nav_order: 5
---

### Overview & Setup

<div class="setup" markdown="block">

1. Go to the `CS3 Project 3.2` assignment on **Blackbaud** and follow the provided **GitHub Classroom** link.
  > 📁 Clicking the link generates a **private repository** for your project with the appropriate starter code. Note that **projects** are stored within the [BWL-CS Organization](https://github.com/BWL-CS), so you _cannot_ access it from the "Your Repositories" page!
2. Open the repository in a **Codespace** whenever you spend time working on the program, in class or at home. 
  > ⚠️ Always remember to `commit changes` after every coding session!
3. When your project is complete, **submit the link to your repository** in the `CS3 Project 3.2` assignment on Blackbaud.

</div>

---

For your project, you will create a **custom Flask web application** that demonstrates your mastery of Flask, Jinja templates, SQLAlchemy, and database management. The project is intentionally open-ended to encourage creativity. Choose a theme that interests you and build an app that is interactive, visually appealing, and functional.
This project will help you practice **full-stack development** using **Flask and SQLAlchemy**, while allowing you to explore a topic that interests you. Be creative and have fun! 🚀

---

## **Project Instructions**

### **1. Choose a Theme**
Pick a theme for your app that excites you! Your app should **store, display, and modify data** from an SQLite database. _Examples:_

- **Task Manager**: A to-do list app where users can add, edit, and delete tasks.
- **Student Directory**: A portal for managing student records (names, grades, subjects).
- **Library System**: A database of books with borrowing and returning functionality.
- **Movie Collection**: A catalog where users can add, rate, and review movies.
- **Recipe Manager**: A site where users can create, update, and delete recipes.
- **Fantasy World Explorer**: A site where users create and manage characters, locations, or quests.

### **2. Set Up Your Flask App**
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
    ├── models.py
    ├── forms.py (optional)
    ├── database.db
    ├── requirements.txt
    └── README.md
    ```

2. **Install Dependencies**:
   ```bash
   pip install flask flask-sqlalchemy
   ```

### **3. Database Setup**
- **Define a database model** in `models.py` using `Flask-SQLAlchemy`.
- Include at least **three fields** (e.g., `id`, `name`, `created_at`).
- Example:
   ```python
   from flask_sqlalchemy import SQLAlchemy
   from datetime import datetime

   db = SQLAlchemy()

   class Task(db.Model):
       id = db.Column(db.Integer, primary_key=True)
       content = db.Column(db.String(200), nullable=False)
       date_created = db.Column(db.DateTime, default=datetime.utcnow)
   ```

### **4. Implement CRUD Operations**
Your app must support the **Create, Read, Update, and Delete** operations. Below are the required features:

#### **A. Create (Add Data)**
- Use an **HTML form** to submit data.
- Store the data in an SQLite database.
- Example:
   ```python
   @app.route('/', methods=['POST'])
   def add_task():
       task_content = request.form['content']
       new_task = Task(content=task_content)
       db.session.add(new_task)
       db.session.commit()
   ```

#### **B. Read (View Data)**
- Fetch records from the database and display them using a Jinja template.
- Example:
   ```python
   @app.route('/')
   def index():
       tasks = Task.query.order_by(Task.date_created).all()
       return render_template('index.html', tasks=tasks)
   ```

#### **C. Update (Modify Data)**
- Provide an option to **edit** existing records.
- Example:
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

#### **D. Delete (Remove Data)**
- Implement a **delete button** to remove entries.
- Example:
   ```python
   @app.route('/delete/<int:id>')
   def delete(id):
       task_to_delete = Task.query.get_or_404(id)
       db.session.delete(task_to_delete)
       db.session.commit()
       return redirect('/')
   ```

### **5. Create HTML Templates**
- Use **Jinja** to dynamically display data.
- Extend a base template (`layout.html`) for consistent navigation.

**Example:** `index.html`
```html
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
```

### **6. Style Your App**
- **CSS**: Create a `static/style.css` file for styling.
- **Bootstrap (Optional)**: Use Bootstrap for a polished UI.
- **Images/Icons**: Store visuals in the `static` folder.

### **7. Serve Your App**
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

### **8. Document Your Work**
- Add **comments** to explain key parts of your code.
- Include a `README.md` file describing:
  - The purpose of your app.
  - How to install and run it.
  - Features and how to use them.

---

## **Minimum Requirements**
✅ At least **three HTML pages** extending a base template.  
✅ A **Flask-SQLAlchemy database** with at least **one model**.  
✅ **CRUD functionality** (Create, Read, Update, Delete).  
✅ A **form** to add records.  
✅ A **delete button** to remove records.  
✅ Styling using **CSS** or **Bootstrap**.  
✅ At least **one image** in the `static` folder.  
✅ Use of **template inheritance** and Jinja control structures.  

---

## **Bonus Challenges**
🎯 Add **user authentication** (login/logout).  
🎯 Implement **pagination** for large datasets.  
🎯 Use JavaScript for **live updates** or **form validation**.  
🎯 Add a **REST API endpoint** returning JSON data.  
🎯 Use Flask’s `flash` messages for user feedback.  
🎯 Connect to a **PostgreSQL** or **MySQL** database.  
