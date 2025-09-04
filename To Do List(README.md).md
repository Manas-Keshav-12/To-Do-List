# this is just a frontend for to do list it cannot save any task.

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>To-Do App</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f6f9;
      display: flex;
      justify-content: center;
      align-items: flex-start;
      min-height: 100vh;
      margin: 0;
      padding: 30px;
    }

    .todo-container {
      background: #fff;
      width: 400px;
      border-radius: 12px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.1);
      padding: 20px;
    }

    h1 {
      text-align: center;
      margin-bottom: 20px;
      color: #333;
    }

    .input-section {
      display: flex;
      gap: 10px;
      margin-bottom: 20px;
    }

    .input-section input {
      flex: 1;
      padding: 10px;
      border-radius: 8px;
      border: 1px solid #ccc;
      font-size: 16px;
    }

    .input-section button {
      padding: 10px 15px;
      border: none;
      background: #4CAF50;
      color: white;
      border-radius: 8px;
      cursor: pointer;
      transition: 0.3s;
    }

    .input-section button:hover {
      background: #45a049;
    }

    ul {
      list-style-type: none;
      padding: 0;
      margin: 0;
    }

    li {
      display: flex;
      align-items: center;
      padding: 10px;
      border-bottom: 1px solid #eee;
      font-size: 16px;
    }

    li:last-child {
      border-bottom: none;
    }

    li input[type="checkbox"] {
      margin-right: 10px;
      transform: scale(1.2);
      cursor: pointer;
    }
  </style>
</head>
<body>
  <div class="todo-container">
    <h1>My To-Do List</h1>

    <div class="input-section">
      <input type="text" id="taskInput" placeholder="Enter a new task">
      <button id="addTaskBtn">Add</button>
    </div>

    <ul id="taskList">
    </ul>
    <h2>Completed Tasks</h2>
    <ul id="completedList">
    </ul>
  </div>

  <script>

    let taskList = document.getElementById("taskList");
    let addButton = document.getElementById("addTaskBtn");
    let taskInput = document.getElementById("taskInput");  

    addButton.addEventListener("click", function() {

      taskText = taskInput.value.trim();

      if (taskText === "") {
        alert("PLease enter a task.");
      }
       
      else {

        let li = document.createElement("li");

        let checkbox = document.createElement("input");
        checkbox.type = "checkbox";

        let textNode = document.createTextNode("" + taskText);

        li.appendChild(checkbox);
        li.appendChild(textNode);

        taskList.appendChild(li);
        taskInput.value = "";

       checkbox.addEventListener("change", function() {
        if (checkbox.checked) {

             li.style.textDecoration = "line-through";
             li.style.color = "grey";


          let completedLi = li.cloneNode(true);
          completedLi.querySelector("input").disabled = true; 
          document.getElementById("completedList").appendChild(completedLi);
        } else {

            let completedList = document.getElementById("completedList");
            let completedItems = completedList.querySelectorAll("li");
            completedItems.forEach(item => {
            if (item.textContent.trim() === li.textContent.trim()) {
               completedList.removeChild(item);
            }
    });
    li.style.textDecoration = "none";
    li.style.color = "black";
  }
});
  }
    });

   localStorage.setItem("tasks", taskList.innerHTML);

    window.onload = function() {
  let saved = localStorage.getItem("tasks");
  if (saved) {
    taskList.innerHTML = saved;
  }
};
  </script>
</body>
</html>



