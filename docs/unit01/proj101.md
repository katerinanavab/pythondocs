---
layout: project
title: "💻 PROJECT #1.1"
projectname: "Trivia Quiz App"
parent: "1️⃣ Python Bootcamp"
nav_order: 4
---

### Overview & Setup
In this project, students will demonstrate their understanding of Python programming basics, including variables, data types, functions, loops, conditionals, dictionaries, and lists, by creating an interactive quiz. The quiz should take input from the user, process that input, and provide appropriate feedback based on the user’s responses.

- **Project Goal:** Develop an interactive trivia quiz in Python that tests the user’s knowledge on a topic of your choice (e.g., general knowledge, mathematics, history, etc.).
- You are encouraged to be creative with the quiz topics and question types.
- Testing your program thoroughly before submission is crucial to ensure it handles different inputs and scenarios effectively.
- Collaboration with classmates is allowed, but each student must submit their unique quiz project.

<div class="setup" markdown="block">

1. GITHUB SETUP INSTRUCTIONS GO HERE

</div>

### Instructions & Requirements

<div class="task" markdown="block">

#### Project Specifications
- **Trivia Questions:** The quiz should have a minimum of _10 multiple-choice_ questions. The program should evaluate the user’s responses and provide overall feedback on their performance at the end of the quiz.
- **Main Program:** The main program should initialize the quiz, call the necessary functions, and handle the quiz’s overall flow.
- **User Interaction:** Ensure the quiz is interactive by taking user input and providing immediate feedback after each question.
- **Scoring:** Implement a scoring system that tracks the user’s correct answers and displays the final score at the end.
- **Error Handling:** Include basic error handling for user inputs (e.g., ensuring the user selects a valid option for multiple-choice questions).

#### Core Python Concepts to Implement
- **Variables:** Use variables to store user inputs, scores, and other relevant data.
- **Data Types:** Implement different data types, including `strings`, `integers`, `lists`, and `dictionaries`, to manage quiz questions, answers, and user data.
- **Dictionaries:** Use a `dictionary` to store each question and its corresponding possible answers.
  - Create a dictionary where the `keys` are the questions (stored as strings), and the `values` are lists containing possible answer choices. 
- **Functions:** Write at least two functions:
  - `ask_question(question, options, correct_answer)` displays the question and options, takes user input, checks if the answer is correct, and returns a boolean value indicating correctness.
  - `calculate_score(total_questions, correct_answers)` calculates and returns the user’s score as a percentage.
- **Loops:** Use loops to iterate through the questions stored in the list and handle repeated tasks (e.g., displaying questions, capturing responses).
- **Conditionals:** Implement conditionals to check if the user’s response is correct and update the score accordingly.

#### Bonus Challenges (Optional)
- **Randomized Questions:** Randomize the order of the questions each time the quiz is run.
- **Timed Quiz:** Implement a timer for each question, giving the user a limited amount of time to answer.
- **High Scores:** Add functionality to save and display the highest score achieved by any user.


</div> 


