---
layout: notes
title: "📓3.2: Flask HTTP Methods" 
parent: "3️⃣ Flask Web Apps"
nav_order: 2
---

## Table of Contents
{: .no_toc .text-delta }

{: .fs-2 }
- TOC
{:toc}

---
## HTTP Methods in Flask Apps

<html>
<dl>
  <dt>HTTP Method</dt>
  <dd>
  </dd>
</dl>
</html>

Flask provides support for common **HTTP methods** such as `GET`, `POST`, `PUT`, `DELETE`, and others. These methods allow developers to build RESTful APIs and handle various types of _client-server interactions_. Below is an overview of HTTP methods supported in Flask, along with simple examples for each.

### HTML Form Handling

Here is an example that demonstrates handling an **HTML form** and dynamically generating a page based on user responses.

1. An HTML page (such as `index.html`) page renders the form:
  ```html
  <form action="/submit" method="POST">
      <!-- Text Input -->
      <label for="name">Name:</label>
      <input type="text" id="name" name="name" required><br><br>
  
      <!-- Age Input -->
      <label for="age">Age:</label>
      <input type="number" id="age" name="age" required><br><br>
  
      <!-- Dropdown Menu -->
      <label for="favorite_hobby">Favorite Hobby:</label>
      <select id="favorite_hobby" name="favorite_hobby" required>
          <option value="Reading">Reading</option>
          <option value="Sports">Sports</option>
          <option value="Gaming">Gaming</option>
          <option value="Cooking">Cooking</option>
          <option value="Traveling">Traveling</option>
      </select><br><br>
  
      <!-- Text Input -->
      <label for="favorite_color">Favorite Color:</label>
      <input type="text" id="favorite_color" name="favorite_color" required><br><br>
  
      <!-- Numerical Input -->
      <label for="lucky_number">Lucky Number:</label>
      <input type="number" id="lucky_number" name="lucky_number" required><br><br>
  
      <!-- Submit Button -->
      <button type="submit">Submit</button>
  </form>
  ```
  > Note the `<form>` attributes: `action="/submit"` and `method="POST"`.
1. When the user clicks the button to submit the form, the data is sent to the `/submit` route in `app.py`:
  ```python
  @app.route('/submit', methods=['POST'])
  def submit():
      # Collect form data
      user_data = {
          'name': request.form.get('name'),
          'age': request.form.get('age'),
          'favorite_color': request.form.get('favorite_color'),
          'favorite_hobby': request.form.get('favorite_hobby'),
          'lucky_number': request.form.get('lucky_number')
      }
      return render_template('result.html', user_data=user_data)
  ```
1. The `/submit` route processes the data and passes it to another template (here, `result.html`) for display. The user sees their submitted responses on the result page.
```html
{% raw %}
{% extends 'layout.html' %}

{% block content %}
<p>Thank you for submitting your details! Here is what you entered:</p>
<ul>
    <li><strong>Name:</strong> {{ user_data.name }}</li>
    <li><strong>Age:</strong> {{ user_data.age }}</li>
    <li><strong>Favorite Hobby:</strong> {{ user_data.favorite_hobby }}</li>
    <li><strong>Favorite Color:</strong> {{ user_data.favorite_color }}</li>
    <li><strong>Lucky Number:</strong> {{ user_data.lucky_number }}</li>
</ul>
<a href="/">Go Back</a>
{% endblock %}
{% endraw }
```


---

#### Acknowledgement
{: .no_toc }

Content on this page is adapted from [Flask Tutorial in Visual Studio Code](https://code.visualstudio.com/docs/python/tutorial-flask).
{: .fs-2 }
