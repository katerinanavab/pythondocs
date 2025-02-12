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

### What is SQL? 
{:.no_toc}

**SQL** ([Structured Query Language](https://www.w3schools.com/sql/)) is the standard language for interacting with **relational databases**. It allows users to _create_, _retrieve_, _update_, and _delete_ data stored in a structured format using **tables**. SQL databases, such as `SQLite`, `PostgreSQL`, and `MySQL`, are widely used in web applications to ensure efficient data management.

`SQLite` is a lightweight, _serverless_ SQL **database engine** that is built into `Python` and commonly used for small to medium-sized applications. 
> Unlike other database systems that require a separate server process, SQLite operates as a simple file on disk, making it an excellent choice for local development and small-scale web applications.

### CRUD: Create, Read, Update, Delete

![image](https://repository-images.githubusercontent.com/589202470/23a403ef-85c3-493f-881a-ffa186b043cb)

<div class="imp" markdown="block">
    
💿 **CRUD** represents the four fundamental _operations_ performed on a database. Each operation corresponds to a _SQL statement_.

1. **Create** – Inserting new records into the database.
   > _SQL:_ `INSERT INTO table_name (column1, column2) VALUES (value1, value2);`
3. **Read** – Retrieving and displaying stored data.
   > _SQL:_ `SELECT * FROM table_name;`
5. **Update** – Modifying existing records.
   > _SQL:_ `UPDATE table_name SET column1 = value1 WHERE condition;`
7. **Delete** – Removing records from the database.
   > _SQL:_ `DELETE FROM table_name WHERE condition;`

</div>

#### EXAMPLE: Crud Operations in Python
{:.no_toc}

In a `Flask` app using `SQLAlchemy`, these operations translate into Python *methods*.

```python
# Create
task = Todo(content="Complete Flask tutorial")
db.session.add(task)
db.session.commit()

# Read
tasks = Todo.query.all()

# Update
task = Todo.query.get(1)
task.content = "Updated task"
db.session.commit()

# Delete
db.session.delete(task)
db.session.commit()
```

---

## Tutorial: SQLite + Flask

In this tutorial, we will walk through the process of integrating an `SQLite` database into a `Flask` **web application**. We will use `SQLAlchemy`, Flask's **ORM** ([Object-Relational Mapper](https://www.freecodecamp.org/news/what-is-an-orm-the-meaning-of-object-relational-mapping-database-tools/)), to manage the database. By the end of this tutorial, you will have a working to-do list web application that allows users to add and delete tasks, all stored in an SQLite database.

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

### Step 2: Creating the Database Model

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
    {% raw %}{% block head %}{% endblock %}{% endraw %}
</head>
<body>
    {% raw %}{% block body %}{% endblock %}{% endraw %}
</body>
</html>
```

#### Main Page (`templates/index.html`)
{:.no_toc}

```html
{% raw %}
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
{% endraw %}
```

---

## Next Steps: Advanced SQLite

As your applications grow, you may need to implement advanced SQLite features for better performance and scalability.

### Indexing for Performance Optimization

An **index** is a data structure that improves the _speed_ of data retrieval operations. Without an index, a database must scan every row to find matching records, which can be slow for large datasets.

#### Example: Creating an Index
{:.no_toc}

```sql
CREATE INDEX idx_task_content ON Todo(content);
```
> This index allows faster lookups when searching for tasks by content.

### Foreign Keys for Relational Data

**Foreign keys** enforce relationships between tables, ensuring data integrity. They prevent orphaned records and help structure data _logically_.

#### Example: Defining Foreign Keys in SQLAlchemy
{:.no_toc}

```python
class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(80), unique=True, nullable=False)

class Task(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    content = db.Column(db.String(200), nullable=False)
    user_id = db.Column(db.Integer, db.ForeignKey('user.id'), nullable=False)
    user = db.relationship('User', backref=db.backref('tasks', lazy=True))
```
> Here, each **task** is associated with a **specific user**, ensuring structured data relationships.

### Transactions for Data Integrity

A database **transaction** is a sequence of operations that must all be executed successfully or none at all. This ensures _consistency_ in case of failures.

#### Example: Using Transactions in SQLAlchemy
{:.no_toc}

```python
try:
    db.session.begin()
    db.session.add(task1)
    db.session.add(task2)
    db.session.commit()
except:
    db.session.rollback()
```
> If an error occurs while adding `task1` or `task2`, the rollback prevents partial data corruption.



---

#### Acknowledgement
{: .no_toc }

Content on this page is adapted from []().
{: .fs-2 }
