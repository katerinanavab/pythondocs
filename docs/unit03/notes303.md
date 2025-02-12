---
layout: notes
title: "📓3.3: SQLite Databases" 
parent: "3️⃣ Flask Web Apps"
nav_order: 3
---

## Table of Contents
{: .no_toc .text-delta }

{: .fs-2 }
- TOC
{:toc}

---
## Databases in Python Web Apps

### CRUD: Create, Read, Update, Delete

---

## Tutorial: SQLite + Flask

In this tutorial, we will walk through the process of integrating an `SQLite` **database** into a `Flask` **web application**. We will use `SQLAlchemy`, Flask's **ORM** ([Object-Relational Mapper](https://www.freecodecamp.org/news/what-is-an-orm-the-meaning-of-object-relational-mapping-database-tools/), to manage the database. By the end of this tutorial, you will have a working to-do list web application that allows users to add and delete tasks, all stored in an SQLite database.

You can install the necessary dependencies using pip:
```bash
pip install flask flask-sqlalchemy
```

### Step 1: Setting Up the Flask Application
First, create a new Python file called `app.py` and import the necessary modules:

```python
from flask import Flask, render_template, request, redirect
from flask_sqlalchemy import SQLAlchemy
from datetime import datetime
```

Then, initialize the Flask application and configure the SQLite database:

```python
app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///tasks.db'
db = SQLAlchemy(app)
```

#### Step 2: Creating the Database Model

Next, define a database **model** that represents a task:

```python
class Todo(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    content = db.Column(db.String(200), nullable=False)
    date_created = db.Column(db.DateTime, default=datetime.utcnow)

    def __repr__(self):
        return f'<Task {self.id}>'
```

This model defines a `Todo` table with three columns:
- `id`: A unique identifier for each task
- `content`: The task description
- `date_created`: A timestamp for when the task was added

### Step 3: Creating the Database
Before running the application, create the database by adding the following code at the bottom of `app.py`:

```python
if __name__ == "__main__":
    with app.app_context():
        db.create_all()
    app.run(debug=True)
```

{:.highlight}
Run the Python script once to generate `tasks.db`.

### Step 4: Setting Up Routes

#### Route for Displaying Tasks
{:.no_toc}

Modify `app.py` to render a template displaying all tasks:

```python
@app.route('/', methods=['GET', 'POST'])
def index():
    if request.method == 'POST':
        task_content = request.form['content']
        new_task = Todo(content=task_content)
        try:
            db.session.add(new_task)
            db.session.commit()
            return redirect('/')
        except:
            return 'There was an issue adding your task'
    
    tasks = Todo.query.order_by(Todo.date_created).all()
    return render_template('index.html', tasks=tasks)
```

#### Route for Deleting Tasks
{:.no_toc}

```python
@app.route('/delete/<int:id>')
def delete(id):
    task_to_delete = Todo.query.get_or_404(id)
    try:
        db.session.delete(task_to_delete)
        db.session.commit()
        return redirect('/')
    except:
        return 'There was a problem deleting that task'
```

### Step 5: Creating HTML Templates

#### Base Template (`templates/base.html`)
{:.no_toc}

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="{{ url_for('static', filename='css/main.css') }}">
    {% block head %}{% endblock %}
</head>
<body>
    {% block body %}{% endblock %}
</body>
</html>
```

#### Main Page (`templates/index.html`)
{:.no_toc}

```html
{% extends 'base.html' %}

{% block head %}
<title>Task Master</title>
{% endblock %}

{% block body %}
<div class="content">
    <h1 style="text-align:center;">Task Master</h1>
    <table>
        <tr>
            <th>Task</th>
            <th>Added</th>
            <th>Actions</th>
        </tr>
        {% for task in tasks %}
            <tr>
                <td>{{ task.content }}</td>
                <td>{{ task.date_created.date() }}</td>
                <td>
                    <a href="/delete/{{task.id}}">Delete</a>
                </td>
            </tr>
        {% endfor %}
    </table>
    <div class="form">
        <form action="/" method="POST">
            <input type="text" name="content" id="content" required>
            <input type="submit" value="Add Task">
        </form>
    </div>
</div>
{% endblock %}
```

---

## Next Steps: Advanced SQLite



---

#### Acknowledgement
{: .no_toc }

Content on this page is adapted from []().
{: .fs-2 }
