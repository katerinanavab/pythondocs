---
layout: project
title: "💻 PROJECT #1.1"
projectname: "Quiz App"
parent: "1️⃣ Python Bootcamp"
nav_order: 4
---

### Overview & Setup
In this project, students will demonstrate their understanding of Python programming basics, including variables, data types, functions, loops, conditionals, dictionaries, and lists, by creating an interactive quiz. The quiz should take input from the user, process that input, and provide appropriate feedback based on the user’s responses.

<div class="setup" markdown="block">

1. On [Replit](https://replit.com/~), click `+ Create Repl` on the sidebar to open a **NEW PROJECT**
2. In the pop-up menu, select `Python` as the **TEMPLATE**
3. Specify the **TITLE** following this pattern: `CS3_Unit1_Proj1_FirstNameLastInitial`

</div>

### Instructions & Requirements

<div class="task" markdown="block">

1. Project Overview
Project Description: Develop an interactive quiz in Python that tests the user’s knowledge on a topic of your choice (e.g., general knowledge, mathematics, history, etc.).
Project Scope: The quiz should have a minimum of 5 questions. Each question should be of a different type (e.g., multiple-choice, true/false, or short answer). The program should evaluate the user’s responses and provide feedback on their performance at the end of the quiz.
You are encouraged to be creative with the quiz topics and question types.
Testing your program thoroughly before submission is crucial to ensure it handles different inputs and scenarios effectively.
Collaboration with classmates is allowed, but each student must submit their unique quiz project.

3. Core Python Concepts to Implement
Variables: Use variables to store user inputs, scores, and other relevant data.
Data Types: Implement different data types, including strings, integers, lists, and dictionaries, to manage quiz questions, answers, and user data.
Lists: Use a list to store the questions of the quiz. Each element in the list should correspond to a different question.
Dictionaries: Use a dictionary to store each question and its corresponding possible answers. The keys in the dictionary should represent the questions, and the values should be lists or other suitable data structures representing the answer choices.
Functions: Write at least two functions:
A function to display each question and capture the user's response.
A function to calculate and display the final score based on the user’s responses.
Loops: Use loops to iterate through the questions stored in the list and handle repeated tasks (e.g., displaying questions, capturing responses).
Conditionals: Implement conditionals to check if the user’s response is correct and update the score accordingly.

4. Project Specifications
Question Types: Include at least three different types of questions (e.g., multiple-choice, true/false, short answer).
User Interaction: Ensure the quiz is interactive by taking user input and providing immediate feedback after each question.
Scoring: Implement a scoring system that tracks the user’s correct answers and displays the final score at the end.
Error Handling: Include basic error handling for user inputs (e.g., ensuring the user selects a valid option for multiple-choice questions).

5. Program Structure
Data Organization:
Questions List: Store your quiz questions in a list. Each item in the list should correspond to a unique question.
Questions and Answers Dictionary: Create a dictionary where the keys are the questions (stored as strings), and the values are lists containing possible answer choices. For short answer questions, the list might contain only one correct answer.
Main Program: The main program should initialize the quiz, call the necessary functions, and handle the quiz’s overall flow.
Functions:
ask_question(question, options, correct_answer): Displays the question and options, takes user input, checks if the answer is correct, and returns a boolean value indicating correctness.
calculate_score(total_questions, correct_answers): Calculates and returns the user’s score as a percentage.
Loop: Use a loop to iterate through the list of questions and capture user responses.
Conditional Logic: Use if-else statements to determine if the user's answer is correct and to adjust the score accordingly.

6. Bonus Challenges (Optional)
Randomized Questions: Randomize the order of the questions each time the quiz is run.
Timed Quiz: Implement a timer for each question, giving the user a limited amount of time to answer.
High Scores: Add functionality to save and display the highest score achieved by any user.


</div> 


