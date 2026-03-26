from task_manager import *

def menu():
    while True:
        print("\nSMART STUDY PLANNER")
        print("1. Add Task")
        print("2. View Tasks")
        print("3. Complete Task")
        print("4. Delete Task")
        print("5. Exit")

        choice = input("Enter choice: ")

        if choice == "1":
            add_task()
        elif choice == "2":
            view_tasks()
        elif choice == "3":
            complete_task()
        elif choice == "4":
            delete_task()
        elif choice == "5":
            print("Goodbye!")
            break
        else:
            print("Invalid choice!")

menu()

from storage import load_tasks, save_tasks

def add_task():
    tasks = load_tasks()

    subject = input("Subject: ")
    task_name = input("Task: ")
    deadline = input("Deadline (YYYY-MM-DD): ")
    priority = input("Priority (High/Medium/Low): ")

    task = {
        "subject": subject,
        "task": task_name,
        "deadline": deadline,
        "priority": priority,
        "status": "Pending"
    }

    tasks.append(task)
    save_tasks(tasks)
    print("Task added successfully!")

def view_tasks():
    tasks = load_tasks()

    if not tasks:
        print("No tasks available.")
        return

    for i, task in enumerate(tasks, start=1):
        print(f"{i}. {task['subject']} - {task['task']} | "
              f"{task['deadline']} | {task['priority']} | {task['status']}")

def complete_task():
    tasks = load_tasks()
    view_tasks()

    index = int(input("Enter task number to complete: ")) - 1
    if 0 <= index < len(tasks):
        tasks[index]["status"] = "Completed"
        save_tasks(tasks)
        print("Task marked completed!")
    else:
        print("Invalid task number.")

def delete_task():
    tasks = load_tasks()
    view_tasks()

    index = int(input("Enter task number to delete: ")) - 1
    if 0 <= index < len(tasks):
        tasks.pop(index)
        save_tasks(tasks)
        print("Task deleted!")
    else:
        print("Invalid task number.")

        import json
import os

FILE_PATH = "../data/tasks.json"

def load_tasks():
    if not os.path.exists(FILE_PATH):
        return []

    with open(FILE_PATH, "r") as file:
        try:
            return json.load(file)
        except:
            return []

def save_tasks(tasks):
    with open(FILE_PATH, "w") as file:
        json.dump(tasks, file, indent=4)

        
