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

### Librarys you'll need
- Customtkinter
- Groq

These librarys are important for this AI
the AI needs customtkinter for the window and text boxes
and groq to acess its API to use the model.



### AI modules in Python.

Some common AI modules include:
-groq
-openai

These modules are used to allow you to access AI model's data set for your own use.
They each of there own syntax, but for groq's the syntax using tkinter with some other library's is pretty simple.
This is an example AI's message sending function using the groq module
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

Lets break it down, it starts with a function, send_message, this is the function that gets called whenever the user sends a message.
The first thing it does, set a variable called user_input.
Next, it checks for the user_input to make sure the user sent something instead of just clicking the send button with no input.
Then, it does chat_history.append, this appends/adds data to the AI's History/Memory.
The, data that it appends is the role: "user" which means the role is the person not the AI, and the content which is "user_input" is the data the person inputted.
Then, it configures the chat_output area, putting it in the normal state allowing the AI to output.
Next, it creates an image using the PIL module, this is optional and it puts an image that the user selected in front of its message.
Then, it runs chat_output.insert, and inserts the user input into the window.
Next, it sets a variable and prints it which is optional to allow saving of the chat into a file for the AI to remember even after you close the window.
The other chathistory append is also for saving, that saves it to the file.
Then, it configures the chat_output area, putting it in the disabled state allowing the AI to think. 
Next, it deletes the user input to get ready for the next one.
Then, it creates it's response, it uses the llama3 model by meta, to generate text.
Then, it appends the text to chat history with the role as assistant and the content being the AI's response.
Again, it configures the chat_output area, putting it in the normal state allowing the AI to output.
Then, it sets appendvar again to save the AI's output, Optional.
It prints appendvar again, Optional.
Then it creates an image of the AI using PIL, Optional.
Then, it inserts the AI's message.
Finally it disables the chat output again and jumps somewhere else in the AI's code.

### Common errors:
- Missing an API key, To get one create an account on groq.com, create and account, and get a key from https://console.groq.com/playground, under the API keys section.
- Forgetting to install a module.
- Using wrong type of variable Str vs Int when using numbers, which is why it uses str() method.
- Wrong python version: This AI **only** works in python 3.12.4.








