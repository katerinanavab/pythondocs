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

In a **Client-Server** architecture, there is a set of rules, called a _protocol_, using which, we can allow the clients, to communicate with the server, and, vice-versa. Here, the **Hyper Text Transfer Protocol** (HTTP) is used, through which, communication is possible. The commonly used HTTP methods are: `GET` and `POST`.
> For example: our browser passes our query to the Google server, then the Google server recieves and returns relevant suggestions.

<html>
<dl>
  <dt>HTTP Request Method</dt>
  <dd>A request that tells a server what <strong>action</strong> to perform on a given resource.
  </dd>
</dl>
</html>

Flask provides support for common **HTTP methods** such as `GET`, `POST`, `PUT`, `DELETE`, and others. These methods allow developers to build RESTful APIs and handle various types of _client-server interactions_. Below is an overview of HTTP methods supported in Flask, along with simple examples for each. Watch this <a href="https://www.youtube.com/watch?v=tkfVQK6UxDI" target="_blank"><button class="btn">📺 VIDEO</button></a> for an overview. 

---

### POST Method for handling HTML forms

The **POST** method is used to _send data_ to the server, typically to create or update resources. It is often used with forms or APIs.

Here is an example that demonstrates handling an **HTML form** and dynamically generating a page based on user responses.

An HTML page (such as `index.html`) page renders the form:

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

When the user clicks the button to submit the form, the data is sent to the `/submit` route in `app.py`:

```python
  {% raw %}
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
  {% endraw %}
```

The `/submit` route processes the data and passes it to another template (here, `result.html`) for display. The user sees their submitted responses on the result page.

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
  {% endraw %}
```

--- 

### GET Method

The **GET** method is used to _retrieve data_ from the server. It is the default method for routes in Flask and is typically used to fetch data without making changes on the server.

#### Example:
{:.no_toc}

```python
@app.route('/get_example', methods=['GET'])
def get_example():
    param = request.args.get('param', 'default value')
    return f"Received parameter: {param}"
```
> - `request.args.get('param')` retrieves query parameters from the URL (e.g., `/get_example?param=test`).

---

### PUT Method

The **PUT** method is used to _update_ an existing resource or create a new one if it doesn’t exist.

#### Example:
{:.no_toc}

```python
@app.route('/put_example/<resource_id>', methods=['PUT'])
def put_example(resource_id):
    data = request.json
    return f"Updated resource {resource_id} with data: {data}"
```
> - `request.json` retrieves JSON data sent in the body of the PUT request.
> - Typically, the resource ID is passed in the URL.

#### Example Request (Using cURL):
{:.no_toc}

```bash
{% raw %}
curl -X PUT http://127.0.0.1:5000/put_example/1 -H "Content-Type: application/json" -d '{"key": "value"}'
{% endraw %}
```

---

### DELETE Method

The **DELETE** method is used to _delete_ a resource identified by the URL.

#### Example:
{:.no_toc}

```python
@app.route('/delete_example/<resource_id>', methods=['DELETE'])
def delete_example(resource_id):
    return f"Deleted resource {resource_id}"
```
> - The resource ID is passed in the URL to identify which resource to delete.

#### Example Request (Using cURL):
{:.no_toc}
```bash
{% raw %}
curl -X DELETE http://127.0.0.1:5000/delete_example/1
{% endraw %}
```

---

## Summary of HTTP Methods

| Method      | Description                 | Use Case                  |
| ----------- | --------------------------- | ------------------------- |
| **GET**     | Retrieve data               | Fetching resources        |
| **POST**    | Send data to the server     | Creating resources        |
| **PUT**     | Create or update a resource | Updating entire resources |
| **DELETE**  | Delete a resource           | Removing resources        |
| **PATCH**   | Partially update a resource | Updating specific fields  |
| **HEAD**    | Fetch metadata              | Checking resource headers |
| **OPTIONS** | Discover allowed methods    | API method discovery      |


- Use appropriate HTTP methods for their intended purpose to ensure your API adheres to RESTful principles.
- Flask provides the flexibility to use `methods` in `@app.route` to handle multiple HTTP methods for a single route if needed.

#### Example for Multiple Methods:
{:.no_toc}

```python
{% raw %}
@app.route('/multi_example', methods=['GET', 'POST'])
def multi_example():
    if request.method == 'GET':
        return "This is a GET request"
    elif request.method == 'POST':
        return "This is a POST request"
{% endraw %}
```


---

#### Acknowledgement
{: .no_toc }

Content on this page is adapted from []().
{: .fs-2 }
