---
layout: notes
title: "📓3.1: Intro to Flask" 
parent: "3️⃣ Flask Web Apps"
nav_order: 1
---

## Table of Contents
{: .no_toc .text-delta }

{: .fs-2 }
- TOC
{:toc}

---
## Introduction to Flask Web Applications

<html>
<dl>
  <dt>🧪Flask</dt>
  <dd>A lightweight Python framework for <strong>web applications</strong> that provides the basics for URL routing and page rendering with HTML templates.
  </dd>
</dl>
</html>

Flask is a lightweight [WSGI] web application framework. It is designed to make
getting started quick and easy, with the ability to scale up to complex
applications. It began as a simple wrapper around [Werkzeug] and [Jinja] and has
become one of the most popular Python web application frameworks.

[WSGI]: https://peps.python.org/pep-3333/
[Werkzeug]: werkzeug.md
[Jinja]: jinja.md

```python
# app.py
from flask import Flask

app = Flask(__name__)

@app.route("/")
def greet():
    return "Hello, World!"
```

```
$ flask run
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

#### Using a GitHub Template for class notes
{:.no_toc}

<div class="setup" markdown="block">

1. Go to the public template **repository** for our class: [BWL-CS Python Template](https://github.com/BWL-CS/python-template)
2. Click the <button type="button" name="button" class="btn btn-green">Use this template</button> button above the list of files then select `Create a new repository`
3. Specify the **repository name**: `CS3-Unit-3-Notes`
4. Click <button type="button" name="button" class="btn btn-green">Create repository</button>
    > Now you have **your own personal copy** of this starter code that you can always access under the `Your repositories` section of GitHub! 
5. Now on your repository, click <button type="button" name="button" class="btn btn-green"> < > Code </button> and select the `Codespaces` tab
6. Click `Create Codespace on main` and wait for the environment to load, _then you're ready to code_!
7. 📝 Take notes in this Codespace during class, coding along with the instructor.

</div>

--- 

## Flask Basics Tutorial

Flask is called a "micro" framework because it doesn't directly provide features like form validation, database abstraction, authentication, and so on. Such features are instead provided by special Python packages called Flask extensions. The extensions integrate seamlessly with Flask so that they appear as if they were part of Flask itself. For example, Flask doesn't provide a page template engine, but installing Flask includes the Jinja templating engine by default. For convenience, we typically speak of these defaults as part of Flask.

In this Flask tutorial, you create a simple Flask app with three pages that use a common base template. Along the way, you experience a number of features of Visual Studio Code including using the terminal, the editor, the debugger, code snippets, and more.

### Create and run a minimal Flask app
{:.no_toc}

1. Install Flask in the virtual environment by running the following command in the VS Code Terminal:

    ```bash
    python -m pip install flask
    ```
    
1. In VS Code, create a new file in your project folder named `app.py` using either **File** > **New** from the menu, pressing `Ctrl+N`, or using the new file icon in the Explorer View (shown below).

    ![image](figures/new-file-icon.png)

1. In `app.py`, add code to import Flask and create an instance of the Flask object. If you type the code below (instead of using copy-paste), you can observe VS Code's [IntelliSense and auto-completions](/docs/python/editing.md#autocomplete-and-intellisense):

    ```python
    from flask import Flask
    app = Flask(__name__)
    ```

1. Also in `app.py`, add a function that returns content, in this case a simple string, and use Flask's `app.route` **decorator** to map the URL route `/` to that function:

    ```python
    @app.route("/")
    def home():
        return "Hello, Flask!"
    ```

    > **Tip**: You can use multiple decorators on the same function, one per line, depending on how many different routes you want to map to the same function.

1. Save the `app.py` file.

1. In the Integrated Terminal, run the app by entering `flask run`, which runs the Flask development server. The development server looks for `app.py` by default. When you run Flask, you should see output similar to the following:

    ```bash
     * Environment: production
       WARNING: Do not use the development server in a production environment.
       Use a production WSGI server instead.
     * Debug mode: off
     * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
    ```

{:.warning}
If you see an error that the Flask module cannot be found, make sure you've run `python -m pip install flask` in your virtual environment as described at the end of the previous section. 

{:.highlight}
Also, if you want to run the development server on a different IP address or port, use the host and port command-line arguments, as with `--host=0.0.0.0 --port=80`.

1. To open your default browser to the rendered page, `Ctrl+click` the `http://127.0.0.1:5000/` URL in the terminal.

    ![image](figures/app-in-browser-01.png)

1. Observe that when you visit a URL like /, a message appears in the debug terminal showing the **HTTP request**:

    ```bash
    127.0.0.1 - - [11/Jul/2018 08:40:15] "GET / HTTP/1.1" 200 -
    ```

1. Stop the app by using `Ctrl+C` in the terminal.

> **Tip**: When using a different filename than `app.py`, such as `webapp.py`, you will need to define an environment variable named FLASK_APP and set its value to your chosen file. Flask's development server then uses the value of FLASK_APP instead of the default file `app.py`. For more information, see [Flask command line interface](https://flask.palletsprojects.com/en/1.1.x/cli/).

### Use an HTML template to render a page

The app you've created so far in this tutorial generates only plain text web pages from Python code. Although it's possible to generate HTML directly in code, developers avoid such a practice because it opens the app to [cross-site scripting (XSS) attacks](https://flask.palletsprojects.com/security/#cross-site-scripting-xss). 

{:.highlight}
A much better practice is to keep `HTML` out of your python code entirely by using **templates**, so that your code is concerned only with _data values_ and not with _rendering_.

<html>
<dl>
  <dt>Template</dt>
  <dd>An <code>HTML</code> file that contains <strong>placeholders</strong> for values that the code provides at run time. The templating engine takes care of making the <strong>substitutions</strong> when rendering the page. The code, therefore, concerns itself only with <em>data values</em> and the template concerns itself only with <em>markup</em>.
  </dd>
</dl>
</html>

> The default templating engine for Flask is [Jinja](https://jinja.palletsprojects.com), which is installed automatically when you install Flask. This engine provides flexible options including automatic escaping (to prevent XSS attacks) and **template inheritance**. With inheritance, you can define a **base page** with _common markup_ and then build upon that base with _page-specific_ additions.

In this section, you create a single page using a template. In the sections that follow, you configure the app to serve static files, and then create multiple pages to the app that each contains a nav bar from a base template.

1. Inside the `hello_flask` folder, create a folder named `templates`, which is where Flask looks for templates by default.

1. In the `templates` folder, create a file named `hello_there.html` with the contents below. This template contains two placeholders named "name" and "date", which are delineated by pairs of curly braces, {% raw %}`{{`{% endraw %} and {% raw %}`}}`{% endraw %}. As you can see, you can also include formatting code in the template directly:
    ```html
    {% raw %}
        <!DOCTYPE html>
        <html>
            <head>
                <meta charset="utf-8" />
                <title>Hello, Flask</title>
            </head>
            <body>
                {% if name %}
                    <strong>Hello there, {{ name }}!</strong> It's {{ date.strftime("%A, %d %B, %Y at %X") }}.
                {% else %}
                    What's your name? Provide it after /hello/ in the URL.
                {% endif %}
            </body>
        </html>
    {% endraw %}
    ```
    > **Tip**: Flask developers often use the [flask-babel](https://pythonhosted.org/Flask-Babel/) extension for date formatting, rather than `strftime`, as flask-babel takes locales and timezones into consideration.

1. In `app.py`, import Flask's `render_template` function near the top of the file:

    ```python
    from flask import render_template
    ```

1. Also in `app.py`, modify the `hello_there` function to use `render_template` to load a template and apply the named values (and add a route to recognize the case without a name). `render_template` assumes that the first argument is relative to the `templates` folder. Typically, developers name the templates the same as the functions that use them, but matching names are not required because you always refer to the exact filename in your code.
    ```python
    @app.route("/hello/")
    @app.route("/hello/<name>")
    def hello_there(name = None):
        return render_template(
            "hello_there.html",
            name=name,
            date=datetime.now()
        )
    ```
   > The decorator used for the new URL route, `/hello/<name>`, defines an **endpoint** `/hello/` that can accept any additional value. The identifier inside `<` and `>` in the route defines a **variable** that is passed to the function and can be used in your code.

{:.warning}
URL routes are **case-sensitive**! For example, the route `/hello/<name>` is distinct from `/Hello/<name>`. If you want the same function to handle both, use decorators for each variant.


1. Start the program, navigate to a /hello/name URL, and observe the results.

1. Also try navigating to a /hello/name URL using a name like `<a%20value%20that%20could%20be%20HTML>` to see Flask's automatic escaping at work. The "name" value shows up as plain text in the browser rather than as rendering an actual element.

### Serve static files (CSS, JS, JSON)

**Static** files are of two types:
* 🎨 First are those files like **CSS stylesheets** to which a page template can just refer directly, or even a **JavaScript** file that handles real-time user interactions (button clicks, etc). 
  * Such files can live in any folder in the app, but are commonly placed within a `static` folder.
* The second type are those that you want to address in **code**, such as when you want to implement an API endpoint that returns a static file.
  * For this purpose, the Flask object contains a built-in method, `send_static_file`, which generates a response with a static file contained within the app's `static` folder.

The following sections demonstrate both types of static files.

#### Refer to static files in a template
{:.no_toc}

1. In the `hello_flask` folder, create a folder named `static`.

1. Within the `static` folder, create a file named `style.css` with the following contents. After entering this code, also observe the syntax highlighting that VS Code provides for CSS files, including a color preview:

    ```css
    .message {
        font-weight: 600;
        color: blue;
    }
    ```

1. In `templates/hello_there.html`, add the following line before the `</head>` tag, which creates a reference to the stylesheet.
    ```html
    {% raw %}
    <link rel="stylesheet" type="text/css" href="{{ url_for('static', filename='style.css')}}" />
    {% endraw %}
    ```
    > Flask's [url_for](https://flask.palletsprojects.com/api/#flask.url_for) tag that is used here, creates the appropriate path to the file. Because it can accept variables as arguments, `url_for` allows you to programmatically control the generated path, if desired.

1. Also in `templates/hello_there.html`, replace the contents `<body>` element with the following markup that uses the `message` style instead of a `<strong>` tag (and also displays a message if you just use a hello/ URL without a name):

    ```html
    {% raw %}
    {% if name %}
        <span class="message">Hello there, {{ name }}!</span> It's {{ date.strftime("%A, %d %B, %Y at %X") }}.
    {% else %}
        <span class="message">What's your name? Provide it after /hello/ in the URL.</span>
    {% endif %}
    {% endraw %}
    ```

1. Run the app, navigate to a /hello/name URL, and observe that the message renders in blue. Stop the app when you're done.

#### Serve a static file from code
{:.no_toc}

1. In the `static` folder, create a JSON data file named `data.json` with the following contents (which are meaningless sample data):

    ```json
    {
        "01": {
            "note" : "This data is very simple because we're demonstrating only the mechanism."
        }
    }
    ```

1. In `app.py`, add a function with the route /api/data that returns the static data file using the `send_static_file` method:

    ```python
    @app.route("/api/data")
    def get_data():
        return app.send_static_file("data.json")
    ```

1. Run the app and navigate to the /api/data endpoint to see that the static file is returned. Stop the app when you're done.

### Create multiple templates that extend a base template

🌐 Because most web apps have more than one page, and because those pages typically share many common elements, developers separate those common elements into a **base page template** that other page templates can then extend (this is also called _template inheritance_.)

Also, because you'll likely create many pages that extend the same template, it's helpful to create a reusable **code snippet** in VS Code with which you can quickly initialize new page templates. A snippet helps you avoid tedious and error-prone copy-paste operations!

The following sections walk through different parts of this process.

#### Create a base page template and styles
{:.no_toc}

A **base page template** in Flask contains all the shared parts of a set of pages, including references to CSS files, script files, and so forth. Base templates also define one or more **block** tags that other templates that _extend_ the base are expected to override. 

<div class="imp" markdown="block">

A **block tag** is delineated by {% raw %}`{% block <name> %}`{% endraw %} and {% raw %}`{% endblock %}`{% endraw %} in both the base template and extended templates.
  
</div>


The following steps demonstrate creating a base template.

1. In the `templates` folder, create a file named `layout.html` with the contents below, which contains blocks named "title" and "content". As you can see, the markup defines a simple nav bar structure with links to Home, About, and Contact pages, which you will create in a later section. Each link again uses Flask's `url_for` tag to generate a link at runtime for the matching route.

    ```html
    {% raw %}
    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="utf-8" />
            <title>{% block title %}{% endblock %}</title>
            <link rel="stylesheet" type="text/css" href="{{ url_for('static', filename='style.css')}}" />
        </head>

        <body>
            <div class="navbar">
                <a href="{{ url_for('index') }}" class="navbar-brand">Home</a>
                <a href="{{ url_for('about') }}" class="navbar-item">About</a>
                <a href="{{ url_for('contact') }}" class="navbar-item">Contact</a>
            </div>

            <div class="body-content">
                {% block content %}
                {% endblock %}
                <hr/>
                <footer>
                    <p>&copy; 2025</p>
                </footer>
            </div>
        </body>
    </html>
    {% endraw %}
    ```

1. Add the following styles to `static/style.css`, below the existing "message" style, and save the file. Note that this walkthrough doesn't attempt to demonstrate responsive design; these styles simply generate a reasonably interesting result.

    ```css
    .navbar {
        background-color: lightslategray;
        font-size: 1em;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
        color: white;
        padding: 8px 5px 8px 5px;
    }

    .navbar a {
        text-decoration: none;
        color: inherit;
    }

    .navbar-brand {
        font-size: 1.2em;
        font-weight: 600;
    }

    .navbar-item {
        font-variant: small-caps;
        margin-left: 30px;
    }

    .body-content {
        padding: 5px;
        font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
    ```

You can run the app at this point, but because you haven't made use of the base template anywhere and haven't changed any code files, the result is the same as the previous step. Complete the remaining sections to see the final effect.

#### Create a code snippet
{:.no_toc}

Because the three pages you create in the next section extend `layout.html`, it saves time to create a **code snippet** to initialize a new template file with the appropriate reference to the base template. A code snippet provides a consistent piece of code from a single source, which avoids errors that can creep in when using copy-paste from existing code.

1. In VS Code, select **File** > **Preferences** > **Configure Snippets**.

1. In the list that appears, select **html**. The option may appear as "html.json" in the **Existing Snippets** section of the list if you've created snippets previously.

1. After VS Code opens `html.json`, add the following entry within the existing curly braces (the explanatory comments, not shown here, describe details such as how the `$0` line indicates where VS Code places the cursor after inserting a snippet):


    ```json
    {% raw %}
    "Flask Tutorial: template extending layout.html": {
        "prefix": "flextlayout",
        "body": [
            "{% extends 'layout.html' %}",
            "{% block title %}",
            "$0",
            "{% endblock %}",
            "{% block content %}",
            "{% endblock %}"
        ],

        "description": "Boilerplate template that extends layout.html"
    },
    {% endraw %}
    ```

1. Save the `html.json` file.

1. Now, whenever you start typing the snippet's prefix, such as `flext`, VS Code provides the snippet as an autocomplete option, as shown in the next section. You can also use the **Insert Snippet** command to choose a snippet from a menu.

For more information on code snippets in general, refer to [Creating snippets](/docs/editor/userdefinedsnippets.md).

#### Use the code snippet to add pages
{:.no_toc}

With the code snippet in place, you can quickly create templates for the Home, About, and Contact pages.

1. In the `templates` folder, create a new file named `index.html`, Then start typing `flext` to see the snippet appear as a completion:

    ![image](figures/autocomplete-for-code-snippet.png)

    When you select the completion, the snippet's code appears with the cursor on the snippet's insertion point:

    ![image](figures/code-snippet-inserted.png)

1. At the insertion point in the "title" block, write `Home`, and in the "content" block, write `<p>Home page for the Visual Studio Code Flask tutorial.</p>`, then save the file. These lines are the only unique parts of the extended page template:

1. In the `templates` folder, create `about.html`, use the snippet to insert the boilerplate markup, insert `About us` and `<p>About page for the Visual Studio Code Flask tutorial.</p>` in the "title" and "content" blocks, respectively, then save the file.

1. Repeat the previous step to create `templates/contact.html` using `Contact us` and `<p>Contact page for the Visual Studio Code Flask tutorial.</p>` in the two content blocks.

1. In `app.py`, add functions for the /about/ and /contact/ routes that refer to their respective page templates. Also modify the `home` function to use the `home.html` template.

    ```python
    # Replace the existing index function with the one below
    @app.route("/")
    def index():
        return render_template("index.html")

    # New functions
    @app.route("/about/")
    def about():
        return render_template("about.html")

    @app.route("/contact/")
    def contact():
        return render_template("contact.html")
    ```

#### Run the app
{:.no_toc}

With all the page templates in place, save `app.py`, run the app, and open a browser to see the results. Navigate between the pages to verify that the page templates are properly extending the base template.

![image](figures/full-app.png)

> **Note**: If you're not seeing the latest changes, you might need to do a hard refresh on the page to avoid seeing a cached file.

### Implementing Control Structures

A **control structure** refers to all those things that control the flow of a program - conditionals (i.e. if/elif/else), for-loops, as well as things like macros and blocks. The official [Jinja Documentation](https://jinja.palletsprojects.com/en/stable/templates/#list-of-control-structures) provides examples for a variety of control structures and different data types.

Let's try out some more in our `about.html` page!

#### Conditionals

Earlier, we used **if blocks** in our templates to generate different HTML content based on whether a value exists. For multiple branches, `elif` and `else` can be used like in Python. You can use more complex Expressions there, too:

{% raw %}
```html
{% if mood == "good"  %}
    <p>Hi!!! I'm sooo happy you're here!</p>
{% elif mood == "bad" %}
    <p>Not feeling it today.</p>
{% else %}
    <p>Feeling mysterious today...</p>
{% endif %}
```
{% endraw %}

> * Jinja handles **string comparisons** like Python, so {% raw %}`{% if mood == "good" %}`{% endraw %} will evaluate to `True` when `mood` is set to "good". 
> * If `mood` is not "good" or "bad", the {% raw %}`{% else %}`{% endraw %} block will handle all other cases, which is a good fallback.

{:.highlight}
Don't forget to update `app.python` to pass in the appropriate data for this variable to render in the template!

```python
@app.route('/about/')
def about():
    current_mood = "good"  # or "bad", or some other value
    return render_template('about.html', mood=current_mood)
```

#### For Loops

Use a `for` loop to display a `list` of people provided in a variable called `friends`:

{% raw %}
```html
<h1>Best Class Ever</h1>
<ul>
{% for friend in friends %}
  <li>{{ friend }}</li>
{% endfor %}
</ul>
```
{% endraw %}

As variables in templates retain their object properties, it is possible to iterate over containers like `dict`:

{% raw %}
```html
<dl>
{% for key, value in my_dict.items() %}
    <dt>{{ key }}</dt>
    <dd>{{ value }}</dd>
{% endfor %}
</dl>
```
{% endraw %}

{:.highlight}
Don't forget to update `app.python` to pass in the appropriate data for this variable to render in the template!

--- 

## Next steps

1. Because this tutorial has only scratched the surface of page templates, refer to the [Jinja Documentation](https://jinja.palletsprojects.com) for more information about templates. The [Template Designer Documentation](https://jinja.palletsprojects.com/templates/#synopsis) contains all the details on the template language. You might also want to review the [official Flask tutorial](https://flask.palletsprojects.com/tutorial) as well as the documentation for Flask [extensions](https://flask.palletsprojects.com/extensions/).

1. The [Docker extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker) makes it easy to build, manage, and deploy containerized applications from Visual Studio Code. If you're interested in learning how to create a Python container for the Flask app developed in this tutorial, check out the [Python in a container](/docs/containers/quickstart-python.md) tutorial. 

1. To try your app on a production website, check out the tutorial [Deploy Python apps to Azure App Service using Docker Containers](https://learn.microsoft.com/azure/developer/python/tutorial-deploy-containers-01). Azure also offers a standard container, [App Service on Linux](https://learn.microsoft.com/azure/developer/python/configure-python-web-app-local-environment), to which you deploy web apps from within VS Code.

You may also want to review the following articles in the VS Code docs that are relevant to Python:

- [Editing Python code](/docs/python/editing.md)
- [Linting](/docs/python/linting.md)
- [Managing Python environments](/docs/python/environments.md)
- [Debugging Python](/docs/python/debugging.md)
- [Testing](/docs/python/testing.md)



--- 

<div class="warn" markdown="block">
 
🛑 When class ends, don't forget to **SAVE YOUR WORK**! _There are multiple steps to saving in GitHub:_

1. Navigate to the `Source Control` menu on the _LEFT_ sidebar
2. Click the <button type="button" name="button" class="btn btn-green">commit changes</button> button on the _LEFT_ menu
3. Type a brief **commit message** at the top of the file that opens, for example: `updated main.py`
4. Click the small `✔️` **checkmark** in the _TOP RIGHT_ corner
5. Click the <button type="button" name="button" class="btn btn-green">sync changes</button> button on the _LEFT_ menu
6. _Finally you can close your Codespace!_

</div>

---

#### Acknowledgement
{: .no_toc }

Content on this page is adapted from [Flask Tutorial in Visual Studio Code](https://code.visualstudio.com/docs/python/tutorial-flask).
{: .fs-2 }
