# Ex03 To-Do List using JavaScript

## Date: 12/05/2026

## AIM
To create a To-do Application with all features using JavaScript.

## ALGORITHM

### STEP 1
Build the HTML structure (index.html).

### STEP 2
Style the App (style.css).

### STEP 3
Plan the features the To-Do App should have.

### STEP 4
Create a To-do application using Javascript.

### STEP 5
Add functionalities.

### STEP 6
Test the App.

### STEP 7
Open the HTML file in a browser to check layout and functionality.

### STEP 8
Fix styling issues and refine content placement.

### STEP 9
Deploy the website.

### STEP 10
Upload to GitHub Pages for free hosting.

## PROGRAM

### index.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Todo Application</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <div class="container">
        <h1>Simple Todo Application</h1>

        <div class="input-box">
            <input type="text" id="taskInput" placeholder="Enter your task">
            <button id="addBtn">Add</button>
        </div>

        <div class="filters">
            <button class="filter active" data-filter="all">All</button>
            <button class="filter" data-filter="completed">Completed</button>
            <button class="filter" data-filter="pending">Pending</button>
        </div>

        <ul id="taskList"></ul>

        <div class="bottom">
            <p id="taskCount">0 Tasks</p>
            <button id="clearBtn">Clear All</button>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>
```

### style.css

```
body {
    font-family: Arial, sans-serif;
    background: #f0f2f5;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
}

.container {
    width: 400px;
    background: white;
    padding: 25px;
    border-radius: 12px;
    box-shadow: 0px 4px 15px rgba(0,0,0,0.1);
}

h1 {
    text-align: center;
    color: #333;
    margin-bottom: 20px;
}

.input-box {
    display: flex;
    gap: 10px;
}

.input-box input {
    flex: 1;
    padding: 10px;
    border: 1px solid #bbb;
    border-radius: 5px;
    font-size: 15px;
}

.input-box button {
    background: #007bff;
    color: white;
    border: none;
    padding: 10px 18px;
    border-radius: 5px;
    cursor: pointer;
}

.input-box button:hover {
    background: #0056b3;
}

.filters {
    margin-top: 15px;
    text-align: center;
}

.filter {
    padding: 6px 12px;
    margin: 5px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    background: #ddd;
}

.filter.active {
    background: #007bff;
    color: white;
}

#taskList {
    list-style: none;
    padding: 0;
    margin-top: 20px;
}

#taskList li {
    background: #f9f9f9;
    padding: 10px;
    margin-bottom: 10px;
    border-radius: 6px;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.task-left {
    display: flex;
    align-items: center;
    gap: 10px;
}

.completed {
    text-decoration: line-through;
    color: gray;
}

.delete-btn {
    background: red;
    color: white;
    border: none;
    padding: 5px 10px;
    border-radius: 4px;
    cursor: pointer;
}

.delete-btn:hover {
    background: darkred;
}

.bottom {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 15px;
}

#clearBtn {
    background: #444;
    color: white;
    border: none;
    padding: 7px 12px;
    border-radius: 5px;
    cursor: pointer;
}

#clearBtn:hover {
    background: black;
}
```

### script.js

```
const taskInput = document.getElementById("taskInput");
const addBtn = document.getElementById("addBtn");
const taskList = document.getElementById("taskList");
const clearBtn = document.getElementById("clearBtn");
const taskCount = document.getElementById("taskCount");
const filterButtons = document.querySelectorAll(".filter");

let filter = "all";

addBtn.addEventListener("click", addTask);

taskInput.addEventListener("keypress", function(e) {
    if (e.key === "Enter") {
        addTask();
    }
});

clearBtn.addEventListener("click", function() {
    taskList.innerHTML = "";
    updateCount();
});

filterButtons.forEach(button => {
    button.addEventListener("click", function() {

        document.querySelector(".active").classList.remove("active");
        button.classList.add("active");

        filter = button.dataset.filter;
        filterTasks();
    });
});

function addTask() {

    let text = taskInput.value.trim();

    if (text === "") {
        alert("Please enter a task");
        return;
    }

    const li = document.createElement("li");

    li.innerHTML = `
        <div class="task-left">
            <input type="checkbox" class="check">
            <span>${text}</span>
        </div>
        <button class="delete-btn">Delete</button>
    `;

    taskList.appendChild(li);

    taskInput.value = "";

    const checkbox = li.querySelector(".check");
    const span = li.querySelector("span");
    const deleteBtn = li.querySelector(".delete-btn");

    checkbox.addEventListener("change", function() {

        if (checkbox.checked) {
            span.classList.add("completed");
        } else {
            span.classList.remove("completed");
        }

        filterTasks();
    });

    deleteBtn.addEventListener("click", function() {
        li.remove();
        updateCount();
    });

    updateCount();
    filterTasks();
}

function updateCount() {
    const total = taskList.children.length;
    taskCount.innerText = total + " Tasks";
}

function filterTasks() {

    const tasks = taskList.querySelectorAll("li");

    tasks.forEach(task => {

        const checked = task.querySelector(".check").checked;

        if (filter === "all") {
            task.style.display = "flex";
        }

        else if (filter === "completed") {

            if (checked) {
                task.style.display = "flex";
            } else {
                task.style.display = "none";
            }
        }

        else if (filter === "pending") {

            if (!checked) {
                task.style.display = "flex";
            } else {
                task.style.display = "none";
            }
        }
    });
}
```

## OUTPUT

### Empty Page

<img width="1919" height="1079" alt="ex3op1" src="https://github.com/user-attachments/assets/1c013e59-fd7f-49a8-9dc0-d729a3909c71" />

### Task Added

<img width="1919" height="1079" alt="ex3op2" src="https://github.com/user-attachments/assets/0a50541c-8e7d-40de-9cf4-c5170b1e5e59" />

### Total Tasks Status

<img width="1919" height="1079" alt="ex3op3" src="https://github.com/user-attachments/assets/cf8feb98-a613-4690-a1e7-4a7487dcce17" />

### Completed Task

<img width="1919" height="1079" alt="ex3op4" src="https://github.com/user-attachments/assets/b5b9d7ce-0098-4d28-b30c-64c1273ce830" />

### Pending Task

<img width="1919" height="1079" alt="ex3op5" src="https://github.com/user-attachments/assets/1be19c1c-6548-4c79-b919-5d8baa83e990" />

## RESULT
The program for creating To-do list using JavaScript is executed successfully.
