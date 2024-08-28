import argparse
import json
import os
from datetime import datetime

# File to store tasks
TASKS_FILE = 'tasks.json'

# Ensure the JSON file exists
if not os.path.exists(TASKS_FILE):
    with open(TASKS_FILE, 'w') as file:
        json.dump([], file)

def load_tasks():
    with open(TASKS_FILE, 'r') as file:
        return json.load(file)

def save_tasks(tasks):
    with open(TASKS_FILE, 'w') as file:
        json.dump(tasks, file, indent=4)

def add_task(description):
    tasks = load_tasks()
    task_id = len(tasks) + 1
    task = {
        "id": task_id,
        "description": description,
        "status": "todo",
        "createdAt": datetime.now().isoformat(),
        "updatedAt": datetime.now().isoformat()
    }
    tasks.append(task)
    save_tasks(tasks)
    print(f"Task added successfully (ID: {task_id})")

def update_task(task_id, description):
    tasks = load_tasks()
    for task in tasks:
        if task['id'] == task_id:
            task['description'] = description
            task['updatedAt'] = datetime.now().isoformat()
            save_tasks(tasks)
            print("Task updated successfully")
            return
    print("Task not found")

def delete_task(task_id):
    tasks = load_tasks()
    tasks = [task for task in tasks if task['id'] != task_id]
    save_tasks(tasks)
    print(f"Task {task_id} deleted successfully")

def mark_task(task_id, status):
    tasks = load_tasks()
    for task in tasks:
        if task['id'] == task_id:
            task['status'] = status
            task['updatedAt'] = datetime.now().isoformat()
            save_tasks(tasks)
            print(f"Task {task_id} marked as {status}")
            return
    print("Task not found")

def list_tasks(filter_status=None):
    tasks = load_tasks()
    if filter_status:
        tasks = [task for task in tasks if task['status'] == filter_status]
    for task in tasks:
        print(f"ID: {task['id']} | Description: {task['description']} | Status: {task['status']}")

def main():
    parser = argparse.ArgumentParser(description="Task Tracker CLI")

    parser.add_argument("action", type=str, help="Action to perform: add, update, delete, mark-in-progress, mark-done, list")
    parser.add_argument("args", nargs='*', help="Arguments for the action")

    args = parser.parse_args()
    action = args.action
    args = args.args

    if action == "add" and len(args) == 1:
        add_task(args[0])
    elif action == "update" and len(args) == 2:
        update_task(int(args[0]), args[1])
    elif action == "delete" and len(args) == 1:
        delete_task(int(args[0]))
    elif action == "mark-in-progress" and len(args) == 1:
        mark_task(int(args[0]), "in-progress")
    elif action == "mark-done" and len(args) == 1:
        mark_task(int(args[0]), "done")
    elif action == "list" and len(args) == 0:
        list_tasks()
    elif action == "list" and len(args) == 1:
        list_tasks(args[0])
    else:
        print("Invalid command or arguments")

if __name__ == "__main__":
    main()
