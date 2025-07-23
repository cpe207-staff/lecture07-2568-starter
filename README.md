# JavaScript/TypeScript DOM Tutorial

Find more information here

https://www.typescriptlang.org/docs/handbook/dom-manipulation.html

---

### Adding JavaScript to HTML

There are a few ways to add JavaScript to an HTML project.

#### 1. Adding `<script>` tag inside `body` section

We can insert `<script>...</script>` tag inside the `<body>...</body>` section of an HTML file.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <h1>Adding JavaScript to an HTML</h1>

    <script>
      // Write your JavaScript code here
      alert("This is an alert");
      console.log("Hello world");
      console.warn("This is a warning!");
      console.error("This is an error!!!");

      const fruits = ["apple", "papaya", "banana", "orange"];
      fruits.map((fruit) => {
        console.log(`I love ${fruit}`);
      });
    </script>
  </body>
</html>
```

#### 2. Adding `<script>` tag inside `head` section

Or put the `<script>` tag inside the `<head>...</head>` section.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <script>
      // Write your JavaScript code here
      alert("This is an alert");
      console.log("Hello world");
      console.warn("This is a warning!");
      console.error("This is an error!!!");

      const fruits = ["apple", "papaya", "banana", "orange"];
      fruits.map((fruit) => {
        console.log(`I love ${fruit}`);
      });
    </script>

    <title>Document</title>
  </head>
  <body>
    <h1>Adding JavaScript to an HTML</h1>
  </body>
</html>
```

#### 3. Refering to an external JavaScript file

In the `<script>` tag, we can specify to an external JavaScript file using the `src="script.js"` attribute.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <h1>Adding JavaScript to an HTML</h1>

    <script src="script.js"></script>
  </body>
</html>
```

Then we can put all the JavaScript code in the `script.js` file.

```javascript
// script.js file
alert("This is an alert");
console.log("Hello world");
console.warn("This is a warning!");
console.error("This is an error!!!");

const fruits = ["apple", "papaya", "banana", "orange"];
fruits.map((fruit) => {
  console.log(`I love ${fruit}`);
});
```

All methods give the same results.

---

### Create new HTML element

Create an `<p>...</p>` element.

```javascript
const p1 = document.createElement("p");
p1.innterText = "This paragraph is created by JavaScript DOM";

const p2 = document.createElement("p");
p2.innterText = "I am another paragraph created by JavaScript DOM";

document.body.appendChild(p1);
document.body.appendChild(p2);
```

We can use `for-loop` to create multiple elements.

```javascript
for (let i = 0; i < 6; i++) {
  const paragraph = document.createElement("p");
  paragraph.innerText = `I am paragraph ${i + 1}`;
  document.body.appendChild(paragraph);
}
```

### Create nested elements

An **ordered list**, `<ol>...</ol>`, and **unordered list**, `<ul>...</ul>`, can have multiple **list item**, `<li>...</li>`, as children.

We can create a list with multiple list items as well.

```javascript
const fruits = ["Apple", "Lemon", "Pineapple"];
const ul = document.createElement("ul");

for (let fruit of fruits) {
  const li = document.createElement("li");
  li.innerText = fruit;
  ul.appendChild(li);
}

document.body.appendChild(ul);
```

#### Example: Elapsed time

```javascript
let second = 0;

const p1 = document.createElement("p");
app.appendChild(p1);

setInterval(() => {
  second++;
  p1.innerText = `Time elapsed : ${second}`;
  if (second % 2 === 0) p1.style.color = "blue";
  else p1.style.color = "red";
}, 1000);
```

---

### Selecting HTML element

Many times we just want to use an existed element (without creating new elements).

#### `document.getElementById()`

Consider the code below

```javascript
let second = 0;

const p_timer = document.getElementById("timer");

setInterval(() => {
  second++;
  p_timer.innerText = `Time elapsed : ${second}`;
  if (second % 2 === 0) p1.style.color = "blue";
  else p1.style.color = "red";
}, 1000);
```

`.getElementById()` search the HTML DOM for an element with `id="timer"`. According to the HTML code below, it is a paragraph that displays elapse time.

```html
<body>
  <script src="script.js" defer></script>
  <h1>Adding JavaScript to an HTML</h1>

  <p id="timer">Time elapsed : 0</p>
</body>
```

Without `defer` attribute in the `<script>`, the `script.js` file will be executed as soon as possible. This could happen before the `<p id="timer">...</p>` element is rendered.

#### `document.querySelector()`

Another versatile method is `.querySelector()`. This method can be use for selecting an element by `element tag`,`id`, and `CSS class`.

- `.querySelector("div")` : select the first `<div>...</div>` element that is found.
- `.querySelector("#timer")` : select an element with `id="timer"`.
- `.querySelector(".btn-primary") : select the first element which use `btn-primary` CSS class.

The following code uses `.querySelector()` instead.

```javascript
let second = 0;

const p_timer = document.querySelector("#timer");

setInterval(() => {
  second++;
  p_timer.innerText = `Time elapsed : ${second}`;
  if (second % 2 === 0) p1.style.color = "blue";
  else p1.style.color = "red";
}, 1000);
```

---

### HTML events

There are many `HTML events` we can listen to.

https://www.w3schools.com/jsref/dom_obj_event.asp

When any of these event occurs, we can activate a `callback` function to do some tasks.

**Example: Click Counts**

#### Adding event callback in HTML file

```html
<body>
  <script src="script.js" defer></script>
  <h1>Listening to a Click event on a button</h1>

  <button onclick="clickCallBack()">Click Me!</button>
  <p id="counter">Clicked 0 time(s)</p>
</body>
```

```javascript
let clickCount = 0;

const p = document.querySelector("#counter");

const clickCallBack = () => {
  clickCount++;
  p.innerText = `Clicked ${clickCount} time(s)`;
  console.log(clickCount);
};
```

#### Adding event callback in JavaScript file

```html
<body>
  <script src="script.js" defer></script>
  <h1>Listening to a Click event on a button</h1>

  <button id="clickBtn">Click Me!</button>
  <p id="counter">Clicked 0 time(s)</p>
</body>
```

```javascript
let clickCount = 0;

const p = document.querySelector("#counter");
const btn_click = document.querySelector("#clickBtn");
// const btn_click = document.querySelector("button");

btn_click.onclick = () => {
  clickCount++;
  p.innerText = `Clicked ${clickCount} time(s)`;
  console.log(clickCount);
};
```

---

### Get data from `Input` Element

```html
<body>
  <script src="script.js" defer></script>
  <h1>Get data from input element</h1>

  <div>
    <input type="text" id="textInput" />
    <button id="clickBtn">Alert Me!</button>
  </div>
  <br />
  <div>
    Select background color:
    <input type="color" id="colorInput" value="#ffffff" />
  </div>
</body>
```

```javascript
const inputText = document.querySelector("#textInput");
const btn_click = document.querySelector("button");

btn_click.onclick = () => {
  alert(inputText.value);
};

const inputColor = document.querySelector("#colorInput");

inputColor.onchange = (event) => {
  const colorValue = inputColor.value;
  document.body.style.backgroundColor = colorValue;
};
```

---

### Simple Todo List

```html
<body>
  <script src="script.js" defer></script>
  <h1>Simple Todo List</h1>

  <div>
    <input type="text" id="todoInput" />
  </div>
  <div>
    <ul id="todoList"></ul>
  </div>
</body>
```

#### Step 1: Check key and code

```javascript
const inputText = document.querySelector("#todoInput");
const ul = document.querySelector("#todoList");

inputText.onkeyup = (event) => {
  console.log(`Key/Code: ${event.key}/${event.code}`);

  if (event.key !== "Enter") return;
  alert(inputText.value);
};
```

#### Step 2: Create `li` elements

```javascript
...

inputText.onkeyup = (event) => {
  if (event.key !== "Enter") return;

  // Create <li>...</li>
  const li = document.createElement("li");
  li.innerText = inputText.value;
  ul.appendChild(li);

  // reset input
  inputText.value = "";
};
```

#### Step 3: Add `delete` button

```javascript
...
inputText.onkeyup = (event) => {
  if (event.key !== "Enter") return;

  // Create <li>...</li>
  const li = document.createElement("li");

  // Create <span>..todo item.. </span>
  const todoText = document.createElement("span");
  todoText.innerText = inputText.value;

  // Create <button>X</button>
  const deleteBtn = document.createElement("button");
  deleteBtn.innerText = "x";
  deleteBtn.style.margin = "10px";
  deleteBtn.onclick = () => {
    // remove this <li>...</li> when click delete button
    ul.removeChild(li);
  };

  // Append <span> and <button> as children
  li.appendChild(todoText);
  li.appendChild(deleteBtn);

  // Append <li>...</li> as child to <ul>...</ul>
  ul.appendChild(li);

  // reset input
  inputText.value = "";
};
```

### Step 4: Add `Done` button

```javascript
...
// Create <button>done</button>
  const doneBtn = document.createElement("button");
  doneBtn.innerText = "Done";
  doneBtn.onclick = () => {
    // strike "todo item"
    if (todoText.style.textDecoration !== "line-through")
      todoText.style.textDecoration = "line-through";
    else todoText.style.textDecoration = "";
  };

  // Append <span> and <button>s as children
  li.appendChild(todoText);
  li.appendChild(deleteBtn);
  li.appendChild(doneBtn);
...
```

### Step 5: Save todo items to an array

Now we create a `saveData()` function in the `script.js` file.

```javascript
const saveData = () => {
  const todoItems = [];

  for (const li of ul.children) {
    const todoItem = {};
    todoItem.title = li.children[0].innerText;
    todoItem.completed = li.children[0].style.textDecoration === "line-through";
    todoItems.push(todoItem);
  }

  console.log(todoItems);
};
```

We must save/update data when ...

1. Add a `new` todo item
2. `Delete` an existing item
3. Mark an item as `done`

Therefore we need to update the `inputText.onkeyup = (event) => {...}` as followed:

```javascript
...

inputText.onkeyup = (event) => {
  ...
  deleteBtn.onclick = () => {
    // remove this <li>...</li>
    ul.removeChild(li);

    // 2. Delete an existing todo item
    saveData();
  };
  ...
  doneBtn.onclick = () => {
    // strike "todo item"
    if (todoText.style.textDecoration !== "line-through")
      todoText.style.textDecoration = "line-through";
    else todoText.style.textDecoration = "";

    // 3. Mark todo item as done
    saveData();
  };
  ...

  // 1. Add a new todo item
  saveData();
};

```

### Step 6: Save data to `localStorage`

To save our `todoItems` array to web browser's `localStorage`. We need to modify the `saveData()` function as followed:

```javascript
const saveData = () => {
  const todoItems = [];

  for (const li of ul.children) {
    const todoItem = {};
    todoItem.title = li.children[0].innerText;
    todoItem.completed = li.children[0].style.textDecoration === "line-through";
    todoItems.push(todoItem);
  }

  const todoItems_string = JSON.string;
};
```

### Step 7: Load data from `localStorage` and render in HTML

We will create a `loadData()` function to load data from `localStorage` and add these `todoItems` data in the HTML.

```javascript
const loadData = () => {
  const todoItems_string = localStorage.getItem("todoItems");
  const todoItems = JSON.parse(todoItems_string);

  for (const todoItem of todoItems)
    renderTodoItem(todoItem.title, todoItem.completed);
};
```

We also need to create the `renderTodoItem()` function to render each `todoItem` in side the `<ul>...</ul>` element.

The `renderTodoItem()` is very similar to `todoText.onkeyup()` callback function.

```javascript
const renderTodoItem = (title, completed) => {
  // Create <li>...</li>
  const li = document.createElement("li");

  // Create <span>..todo item..</span>
  const todoText = document.createElement("span");
  // *** set the title of todoItem ***
  todoText.innerText = title;

  // Create <button>X</button>
  const deleteBtn = document.createElement("button");
  deleteBtn.innerText = "x";
  deleteBtn.style.margin = "10px";
  deleteBtn.onclick = () => {
    // remove this <li>...</li>
    ul.removeChild(li);

    // update save data
    saveData();
  };

  // Create <button>done</button>
  const doneBtn = document.createElement("button");
  doneBtn.innerText = "Done";
  doneBtn.onclick = () => {
    // *** check the completed status of todoItem ***
    if (completed === "true") todoText.style.textDecoration = "line-through";
    else todoText.style.textDecoration = "";

    // update save data
    saveData();
  };

  // Append <span> and <button> as children
  li.appendChild(todoText);
  li.appendChild(deleteBtn);
  li.appendChild(doneBtn);

  // ul is global variable, declared at the top of script.js
  ul.appendChild(li);
};
```

The final step is to call the `loadData();` function.

### Step 8: Code refactoring

Since the `renderTodoItem()` is very similar to the code inside `inputText.onkeyup`, we can refactor the latter fucntion as followed:

```javascript
inputText.onkeyup = (event) => {
  if (event.key !== "Enter") return;

  // render a todoItem in HTML
  renderTodoItem(inputText.value, false);

  // reset input
  inputText.value = "";

  // Save data
  saveData();
};
```

However the `delete` functionality is not working anymore. We need to go back to the `renderTodoItem()` and modify a bit.

```javascript
const renderTodoItem = (title, completed) => {
  ...

  doneBtn.onclick = () => {
    // strike "todo item"
    if (completed === "true" || todoText.style.textDecoration === "")
      todoText.style.textDecoration = "line-through";
    else todoText.style.textDecoration = "";

    // update save data
    saveData();
  };

  ...
};

```
