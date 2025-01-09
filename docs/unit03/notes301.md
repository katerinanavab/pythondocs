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
  <dt>Web Application</dt>
  <dd>
  </dd>
</dl>
</html>

Flask is a lightweight [WSGI] web application framework. It is designed to make
getting started quick and easy, with the ability to scale up to complex
applications. It began as a simple wrapper around [Werkzeug] and [Jinja] and has
become one of the most popular Python web application frameworks.

Flask offers suggestions, but doesn't enforce any dependencies or project
layout. It is up to the developer to choose the tools and libraries they want to
use. There are many extensions provided by the community that make adding new
functionality easy.

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

###  

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

Content on this page is adapted from [The Flask Mega-Tutorial - Miguel Grinberg](https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).
{: .fs-2 }
