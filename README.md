import tkinter as tk
from tkinter import messagebox

# Questions, options, and answers data
quiz_data = [
    {"question": "What is the capital of France?", "options": ["Paris", "Berlin", "Rome", "Madrid"], "answer": "Paris"},
    {"question": "What is 5 + 7?", "options": ["10", "11", "12", "13"], "answer": "12"},
    {"question": "Which planet is known as the Red Planet?", "options": ["Earth", "Venus", "Mars", "Jupiter"], "answer": "Mars"},
    {"question": "Who wrote 'Romeo and Juliet'?", "options": ["Shakespeare", "Hemingway", "Tolstoy", "Orwell"], "answer": "Shakespeare"},
]

# Initialize main window
root = tk.Tk()
root.title("Quiz Game")
root.geometry("400x300")

# Quiz state variables
current_question = 0
score = 0

# Function to load question
def load_question():
    question_data = quiz_data[current_question]
    question_label.config(text=question_data["question"])
    for i, option in enumerate(question_data["options"]):
        radio_buttons[i].config(text=option, value=option)
    answer_var.set(None)

# Function to check answer and update score
def check_answer():
    global score, current_question
    selected_answer = answer_var.get()
    if selected_answer == quiz_data[current_question]["answer"]:
        score += 1
    current_question += 1
    if current_question < len(quiz_data):
        load_question()
    else:
        show_score()

# Function to display the score
def show_score():
    messagebox.showinfo("Quiz Complete", f"You scored: {score}/{len(quiz_data)}")
    root.quit()

# UI Components
question_label = tk.Label(root, text="", font=("Helvetica", 16))
question_label.pack(pady=20)

# Variable and radio buttons for answer options
answer_var = tk.StringVar()
radio_buttons = [tk.Radiobutton(root, variable=answer_var, font=("Helvetica", 14)) for _ in range(4)]
for rb in radio_buttons:
    rb.pack(anchor="w")

# Button to submit answer
next_button = tk.Button(root, text="Next", command=check_answer, font=("Helvetica", 12))
next_button.pack(pady=20)

# Load the first question
load_question()

# Run the application
root.mainloop()
