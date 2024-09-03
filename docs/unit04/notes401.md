---
layout: notes
title: "📓4.1: AI Basics" 
parent: "4️⃣ Machine Learning"
nav_order: 1
---

## Table of Contents
{: .no_toc .text-delta }

{: .fs-2 }
- TOC
{:toc}

---

## Introduction to machine learning using Python!
### What is an AI?

Machine learning or AI is a way computers can learn.
AI can do many useful tasks such as:

- Writing
- Generating Images
- Send Emails

### How does AI work?

The way AI works, 
is that it gathers data from a bunch of different sources and sort of trains the AI.
Then using that data set, when you input, 
it feeds it in and the AI uses its data set to predict the next word, 
or pixel in the case of image generation.

This can lead to AI's being misled in math or science, as the AI
just predicts the answer.
So if it's never seen that math problem or science question,
it will make up something in its dataset.

#### Predictive AI

Some types of AI are based on predicting certain things like a number or text that was written by a person.
These are trained using data from things like Captcha's which you might find annoying, but it prevents bots from logging in,
but at the same time trains them to learn things like traffic signs for self-driving cars.
These use neural networks as there data set using the data as nodes with different weights.

### AI modules in Python.

Some common AI modules include:
-groq
-openai

These modules are used to allow you to access AI model's data set for your own use.
They each of there own syntax, but for groq's the syntax using tkinter(talked about in a previous lesson) with some other library's is pretty simple.

```python
def send_message():
    user_input = input_entry.get("1.0", tk.END).strip()
    if user_input:
        chat_history.append({"role": "user", "content": user_input})
        

        chat_output.config(state=tk.NORMAL)
        chat_output.image_create("current",image=image2)
        chat_output.insert(tk.END, f"User: {user_input}\n")
        appendvar2 = (f"User: {user_input}")
        print(str(appendvar2))
        chathistory.append(appendvar2)
        chat_output.config(state=tk.DISABLED)
        input_entry.delete("1.0", tk.END)

        response = client.chat.completions.create(model="llama3-8b-8192",
                                                messages=chat_history,
                                                max_tokens=100,
                                               temperature=1.2)
        chat_history.append({
            "role": "assistant",
            "content": response.choices[0].message.content
        })
        chat_output.config(state=tk.NORMAL)
        appendvar = (f"V3ectorGPT: {response.choices[0].message.content}\n")
        print(str(appendvar))
        chathistory.append(appendvar)
        chat_output.image_create("current",image=image)
        chat_output.insert(tk.END, f"V3ectorGPT: {response.choices[0].message.content}\n")
        
        chat_output.config(state=tk.DISABLED)
        
        chat_output.see(tk.END)  # Scroll to the bottom

```

Lets break it down, we start with a function, send_message, this is the function that gets called whenever it sends a message.
The first thing it does is it sets a variable called user_input.


