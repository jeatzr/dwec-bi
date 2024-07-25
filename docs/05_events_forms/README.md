# **UNIT5 - Event Management and Form Validation**

## **1. Event Handling Models in JavaScript**

 falta aquí algo 

### **1.1 Assign an Event Handler**

In JavaScript, event handling allows you to respond to user actions or other events triggered in the browser. There are different models for handling events, each offering various ways to attach event listeners and manage event propagation.

1. **Traditional Event Model (`onclick`, `onmouseover`, etc.)**
      - **Description:** This model involves directly assigning event handler attributes to HTML elements.
      - **Usage:** Attach events inline within HTML tags or set them via JavaScript using element properties (`element.onclick = function() {...}`).
      - **Example:**
        ```html
        <button onclick="alert('Button clicked!')">Click me</button>
        ```

2. **DOM Level 2 Event Model (`addEventListener()` method)**
      - **Description:** Introduced in DOM Level 2, this model provides a more flexible approach to event handling.
      - **Usage:** Attach events using `addEventListener(event, handler, useCapture)`, where `event` is the event type (e.g., `'click'`), `handler` is the function to execute, and `useCapture` (optional) specifies event flow.
      - **Example:**
        ```javascript
        const button = document.querySelector('button');
        button.addEventListener('click', function() {
          alert('Button clicked using addEventListener!');
        });
        ```

3. **Event Delegation**
      - **Description:** Rather than attaching event listeners to individual elements, this technique involves attaching a single event listener to a parent element.
      - **Usage:** Utilize event bubbling by placing event listeners on parent elements and delegating handling based on the target element (`event.target`).
      - **Example:**
        ```html
        <ul id="list">
          <li>Item 1</li>
          <li>Item 2</li>
          <li>Item 3</li>
        </ul>

        <script>
          const list = document.getElementById('list');
          list.addEventListener('click', function(event) {
            if (event.target.tagName === 'LI') {
              console.log('Clicked on:', event.target.textContent);
            }
          });
        </script>
        ```

## **2. Types of Events in JavaScript**

JavaScript provides a wide variety of events that can be used to interact with web pages. These events can be classified into different categories based on their nature and the elements they are associated with.

#### Categories of Events
1. Mouse Events
2. Keyboard Events
3. Form Events
4. Document Events
5. Clipboard Events
6. Drag and Drop Events
7. Touch Events

### 2.1 **Mouse Events**
Mouse events are triggered by user actions with a mouse.

- **click**: Fired when the user clicks on an element.
- **dblclick**: Fired when the user double-clicks on an element.
- **mousedown**: Fired when the user presses a mouse button over an element.
- **mouseup**: Fired when the user releases a mouse button over an element.
- **mousemove**: Fired when the user moves the mouse pointer over an element.
- **mouseover**: Fired when the user moves the mouse pointer onto an element.
- **mouseout**: Fired when the user moves the mouse pointer out of an element.

### 2.2 **Keyboard Events**
Keyboard events are triggered by user actions with the keyboard.

- **keydown**: Fired when the user presses a key.
- **keyup**: Fired when the user releases a key.
- <strike>**keypress**</strike>: Fired when the user presses a key (deprecated, use `keydown` instead).

When a key is pressed and held down, it begins to "autorepeat": `keydown` fires repeatedly, and when the key is finally released, a single keyup event is triggered. Therefore, it's normal to have many `keydown` events and just one `keyup` event.

<div class="exercise-box">
    <h3><i class="fas fa-laptop-code"></i> Hands-On Exercise: Keyboard Event Handling</h3>
    <p>Create a simple HTML page with JavaScript that allows the user to control a character using the arrow keys.</p>
    <ol>
        <li><strong>HTML Structure:</strong> Create an HTML file (`index.html`) with a `div` element to represent the character.</li>
        <li><strong>CSS Styling:</strong> Style the character (`#character`) to make it visible and positioned on the screen.</li>
        <li><strong>JavaScript Functionality:</strong> Implement JavaScript code to handle `keydown` events for arrow keys and move the character accordingly.</li>
        <li><strong>Event Handling:</strong> Attach an event listener to the `document` object to capture arrow key presses and update the character's position.</li>
    </ol>
    <p><strong>Objective:</strong> Move the character smoothly on the screen using arrow keys.</p>
    <p><strong>Instructions:</strong></p>
    <ul>
        <li>Open `index.html` in a web browser.</li>
        <li>Use the arrow keys (`up`, `down`, `left`, `right`) to control the character's movement.</li>
        <li>Observe how the character updates its position in response to each arrow key press.</li>
    </ul>
    <p><strong>Explanation:</strong> This exercise demonstrates the basics of handling keyboard events in JavaScript to create interactive web applications.</p>
</div>

Example HTML for the exercise:

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Simple Keyboard Event Exercise</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
    }
    #character {
      position: relative;
      width: 50px;
      height: 50px;
      background-color: blue;
      margin-top: 20px;
      transition: 0.2s ease-out;
    }
  </style>
</head>
<body>
  <h2>Move the Character with Arrow Keys</h2>
  <div id="character"></div>

  <script>
    // JavaScript code will go here
    const character = document.getElementById('character');
    let posX = 0;
    let posY = 0;
  </script>
</body>
</html>

```

### 2.3 **Form Events**
Form events are related to form elements.

- **submit**: Fired when a form is submitted.
- **reset**: Fired when a form is reset.
- **change**: Fired when the value of an element changes (for `<input>`, `<textarea>`, `<select>`).
- **focus**: Fired when an element gains focus.
- **blur**: Fired when an element loses focus.
- **input**: Fired when the user inputs text into an element.

### 2.4 **Document Events**
Document events are triggered by actions that affect the entire document.

- **DOMContentLoaded**: Fired when the initial HTML document has been completely loaded and parsed.
```js
document.addEventListener('DOMContentLoaded', (event) => {
            console.log('DOM is fully loaded and parsed');
});
```
- **DOMSubtreeModified**: Triggered when nodes are added or removed from the subtree of an element or document.
- **DOMNodeInserted**: Occurs when a new child node is added to a parent node.
- **DOMNodeRemoved**: Occurs when a node with a parent node is removed.

### 2.5 **Window Events**
- **load**: Fired when the whole page (window)and all dependent resources have finished loading.
```js
window.addEventListener('load', (event) => {
            console.log('Page is fully loaded');
        });
```

>The `load` event of `window` and the `DOMContentLoaded` event of `document`can be used for similar purposes, acting as a "main method" where we can ensure the code inside is executed once the page is loaded, with some nuances:
>
> - **DOMContentLoaded**: Fires once the DOM tree is fully constructed.
> - **load**: Fires once all the page's resources, including multimedia, are fully loaded.
> It's good practice to place the code we want to execute inside a handler function for one of these events. However, if the script is loaded at the end of the `body`, we can at least ensure that the entire DOM is loaded.

- **unload**: Fired when the whole page (window)or a child resource is being unloaded.
- **resize**: Fired when the document view (window) is resized.
- **scroll**: Fired when the document view (window) is scrolled.

### 2.6 **Drag and Drop Events**
Drag and drop events are used for dragging and dropping elements.

- **drag**: Fired when an element is being dragged.
- **dragstart**: Fired when the user starts dragging an element.
- **dragend**: Fired when the user finishes dragging an element.
- **dragenter**: Fired when a dragged element enters a valid drop target.
- **dragover**: Fired when an element is being dragged over a valid drop target.
- **dragleave**: Fired when a dragged element leaves a valid drop target.
- **drop**: Fired when a dragged element is dropped on a valid drop target.

## 3. **HTML Forms**

- A web form is used to send, process, and retrieve data that is sent and received between a client and a web server.
- Each form element stores a data type or triggers one of its functionalities.
- Forms have a defined architecture, within the context of the HTML language.

### 3.1 **Form Structure**

- Forms are defined using tags.
- The main tag is [**`<form> </form>`**](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form).
- To be functional, the `<form>` tag needs to initialize two attributes:
  - `action` – Contains the URL where the form data is redirected.
  - `method` – Indicates the method by which the form sends data. It can be POST or GET.

### 3.2 **Form Tags**

#### 1. **[`<input>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input)**

The `<input>` tag is a fundamental HTML element used within forms to collect user input. It is versatile and supports various types (`type` attribute), each tailored for specific data entry needs. Common input types include text fields, checkboxes, radio buttons, file upload controls, and more. The `<input>` tag does not have a closing tag and is self-contained with attributes that control its appearance, behavior, and interaction with the user.

##### Attributes for Input:

**type**: Specifies the type of element being defined. This attribute determines the additional parameters. Possible values for the `type` attribute include:

- `text`: Text input field.
- `password`: Password input field, where characters are obscured (usually shown as asterisks).
- `checkbox`: Checkbox for multiple-choice selection.
- `radio`: Radio button for exclusive selection among two or more options.
- `submit`: Button to submit the form.
- `reset`: Button to reset or clear form fields.
- `button`: Generic button within the form.
- `file`: Button to browse and select files.
- `hidden`: Hidden field not visible to the user in the form.
- `image`: Image button within the form.

##### More HTML5 input types:

- `email`: Forces the user to enter a valid email address.
- `search`: Styled for search boxes, providing appropriate visual cues.
- `tel`: Allows input of a telephone number (on mobile devices, triggers a numeric keypad, but does not restrict input to numbers only).
- `url`: Enforces input restrictions to ensure the text conforms to URL format.
- `number`: Allows input of floating-point numbers only. Range restrictions can be applied.
- `range`: Creates a graphical slider for selecting a numeric range.
- `date/time inputs` (Note: not universally supported across all browsers):
      - `datetime-local`
      - `month`
      - `week`
      - `time`
- `color`: Provides a color selector control.

Check --> [https://developer.mozilla.org/en-US/docs/Learn/Forms/HTML5_input_types](https://developer.mozilla.org/en-US/docs/Learn/Forms/HTML5_input_types)

##### More Attributes for Input:

- **name**: Specifies the name used to pass the variable's value to the server.
- **value**: Indicates the initial value of the input in the form. It can be set initially and accessed to read or validate it. The data type depends on the input type.
- **size**: Specifies the size of the element in pixels. For text and password fields, it refers to the number of characters.
- **maxlength**: Specifies the maximum number of characters that can be entered in a text or password field.
- **checked**: Exclusive to checkbox and radio button elements. Indicates which option is selected.
- **disabled**: Disables the element, preventing its value from being submitted to the server.
- **readonly**: Makes the element's content uneditable.
- **src**: Specifies the path to an image used as a button within the form.
- **alt**: Provides alternative text for the image.
- **placeholder**: Text that appears as a hint in the input field before the user focuses on it.
- **autofocus**: Specifies that the element should automatically have focus when the page loads.

Check --> [https://developer.mozilla.org/en-US/docs/Learn/Forms/Basic_native_form_controls](https://developer.mozilla.org/en-US/docs/Learn/Forms/Basic_native_form_controls)

#### 2. [**`<label>`**](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/label): Associates a label with an `<input>`, `<select>`, `<textarea>`, or `<button>` element, providing user guidance. Use `for` attribute to match related control's `id`.

#### 3. [**`<select>`**](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select): Creates a drop-down list for selecting options. Uses nested `<option>` tags to define choices.

#### 4. [**`<textarea>`**](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea): Allows multi-line text input. Useful for longer responses like comments or messages.

#### 5. [**`<button>`**](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button): Creates a clickable button within a form. `type` attribute (`submit`, `reset`, or `button`) defines behavior.

#### 6. [**`<fieldset>` and `<legend>`**](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset): Groups related form controls (`<input>`, `<select>`, etc.) together. `<legend>` provides a title for the group.


### 3.3 **Styling Forms**

We can manually style forms using CSS to make them look better. Here are some key aspects to consider:

- Changing the style of buttons (different browsers display them differently).
- Using the fonts and colors of our website.
- Properly distributing form elements on the screen.
- Using CSS to distinguish erroneous fields during validation, e.g., by turning the border red or showing hidden error messages.

To add or remove CSS classes using JavaScript, we can use `element.classList.add("class")`.

We can also use libraries like Bootstrap where form elements are already defined.

#### 1. Manual Styling with CSS

##### Button Style

We can change the style of buttons to ensure they look consistent across browsers:

```css
button {
    background-color: #4CAF50; /* Green */
    border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    cursor: pointer;
    border-radius: 4px;
}

button:hover {
    background-color: #45a049;
}
```

##### Using Site Fonts and Colors

We can use specific fonts and colors from our website:

```css
body {
    font-family: 'Arial', sans-serif;
    background-color: #f2f2f2;
    color: #333;
}

input, select, textarea {
    font-family: inherit;
    font-size: 16px;
    padding: 10px;
    margin: 10px 0;
    box-sizing: border-box;
}

label {
    font-weight: bold;
}
```

##### Distributing Form Elements on the Screen

We can use a container to center the form and distribute its elements:

```css
.form-container {
    max-width: 500px;
    margin: auto;
    background: white;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

```

To organize forms and apply styles effectively, it is a good idea to group elements using `fieldset` or `div` with a class that helps in styling. For example, using a class like `form-group` can help you apply consistent styles to grouped elements.

```html
<div class="form-group">
    <label for="name">Name:</label>
    <input type="text" name="name" id="name" autofocus>
</div>
```

```js
.form-group {
  margin-bottom: 1em;
}

.form-group label {
    display: block;
    margin-bottom: 5px;
}

.form-group>input,
.form-group>textarea,
.form-group>select {
  display: block;
  width: 100%;
  padding: 10px;
  border-radius: 4px;
  border: 1px solid #ccc;
  font-family: inherit;
  font-size: 16px;
  box-sizing: border-box;
}

.form-group>input[type="checkbox"] {
  display: inline-block;
  width: auto;
}

```

#### 2. Erroneous Fields

We can highlight erroneous fields and display error messages:

```css
input.error, select.error, textarea.error {
    border-color: red;
}

.error-message {
    color: red;
    font-size: 12px;
    display: none;
}

.error-message.active {
    display: block;
}
```

We can use JavaScript to add or remove CSS classes:

```js
document.getElementById('myInput').classList.add('error');
document.getElementById('myErrorMessage').classList.add('active');
```

#### 3. Using Libraries like Bootstrap

Bootstrap provides predefined classes for forms:

```html
<form>
  <div class="mb-3">
    <label for="exampleInputEmail1" class="form-label">Email address</label>
    <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
    <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div>
  </div>
  <div class="mb-3">
    <label for="exampleInputPassword1" class="form-label">Password</label>
    <input type="password" class="form-control" id="exampleInputPassword1">
  </div>
  <div class="mb-3 form-check">
    <input type="checkbox" class="form-check-input" id="exampleCheck1">
    <label class="form-check-label" for="exampleCheck1">Check me out</label>
  </div>
  <button type="submit" class="btn btn-primary">Submit</button>
</form>
```

Check more information about [Bootstrap Forms](https://getbootstrap.com/docs/5.0/forms/overview/)

## 4. **Form Validation**

Form validation is crucial in ensuring that user inputs are correct and complete before submission. This can be achieved through various methods, including client-side validation with HTML5 attributes, JavaScript validation, and server-side validation.

<div class="important-box">
<h3><i class="fa-solid fa-circle-exclamation"></i></i>IMPORTANT</h3>
<p>Client-side validation improves the usability of a website but does not eliminate the need for server-side validation.</p>
</div>



### 4.1 **Vanilla JavaScript Validation**

Validation can be done in many ways, but it’s advisable to do it in an organized manner using functions that we can reuse later. We propose this solution:

##### Form to validate

```html
<form id="contactForm" class="needs-validation">
    <div class="form-group">
        <label for="name">Name</label>
        <input type="text" class="form-control" id="name" name="name">
        <div class="error-message">Name is required and must be at least 2 characters long.</div>
    </div>
    <div class="form-group">
        <label for="email">Email</label>
        <input type="email" class="form-control" id="email" name="email">
        <div class="error-message">Please provide a valid email address.</div>
    </div>
    <div class="form-group">
        <label for="password">Password</label>
        <input type="password" class="form-control" id="password" name="password">
        <div class="error-message">Password is required and must be at least 6 characters long.</div>
    </div>
    <button type="submit" class="btn btn-primary">Submit</button>
</form>
```


##### Main  Validation Function 
It's recommended that all the code be inside the window's load or DOMContentLoaded event. This ensures that the entire document is loaded before we start executing the code.

```js

// Is a good practice that all the code is inside 'DOMContentLoaded' or 'load'
document.addEventListener('DOMContentLoaded', function () {
  // Capture all elements 
  const form = document.getElementById('contactForm');
  const name = document.getElementById('name');
  const email = document.getElementById('email');
  const password = document.getElementById('password');

  // Create the event handler to the form 'submit'
  form.addEventListener('submit', function (event) {
    event.preventDefault(); // Prevents the form from submitting automatically
    event.stopPropagation(); // Prevents the event from bubbling up to parent elements

    // Calling the main validation function 
    if (validateForm()) {
      console.log("All fields are ok, we can proceed");
      form.submit();  // Forcing the submission
    } else {
      console.log("There is some not-valid field. The user should ckeck them.")
    }
  });

  // This function is in charge of validating all fields and 
  // return a boolean: true in case all fields are ok, false otherwise
  function validateForm() {
    // This flag is initialized as true. 
    // in case we find an error in a field this variable become false.
    var isValid = true;

    // Custom validation logic
    // Example custom validation just checking the logic 
    if (name.value.trim().length < 2) {
      markFieldAsNotValid(name)
      isValid = false;
    } else {
      markFieldAsValid(name)
    }

    // We can call custom field validation functions that validate certain fields
    // also we can check different conditions and show different error messages
    if (email.value === "") {
      markFieldAsNotValid(email, "Email is required")
      isValid = false;
    } else if (!isValidEmail(email.value)) {
      markFieldAsNotValid(email, "Please provide a valid email address.")
      isValid = false;
    } else {
      markFieldAsValid(email)
    }

    if (!isValidPassword(password.value)) {
      markFieldAsNotValid(password);
      isValid = false;
    } else {
      markFieldAsValid(password);
    }

    // after all field validations we return the isValid flag
    return isValid;
  }

  // definition of field validation functions and other auxiliary functions
  // ....

}
        
```

##### Custom field validation functions

When the validation is more complex, we can define functions that validate certain fields. 

```js

  function isValidEmail(email) {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return emailRegex.test(email);
  }

  function isValidPassword(passwd) {
    return (passwd.length >= 6)
  }

```

##### Auxiliary functions to manage error messages

We can create functions that manage the error messages. In this case we have created one to show the error and othe one to hide the error message. They work on the element that we pass to the function. The code navigates to the parent to add or remove the `is-not-valid-field` class.

```js
// This functions set a field as not-valid and adds the error-message
  function markFieldAsNotValid(element, message) {
    // If we have a custom message we show it. In other case we just show the error-message present in the HTML
    if (message) {
      element.parentNode.querySelector(".error-message").textContent = message;
    }
    // Adding the class that shows the error-message and adds the red border (css)
    element.parentNode.classList.add("is-not-valid-field");
  }

  // This function set a field as valid and hide the error field
  function markFieldAsValid(element, message = "Invalid field. You should check it.") {
    element.parentNode.classList.remove("is-not-valid-field");
  }
```

We need to remember the structure of a `form-group`element:

```html
<div class="form-group">
    <label for="name">Name</label>
    <input type="text" class="form-control" id="name" name="name">
    <div class="error-message">Name is required and must be at least 2 characters long.</div>
</div>
```

We need some CSS code to make visible the error message and the red border when the `is-not-valid-field` class is pressent in the `form-group` element.

```css
.form-group.is-not-valid-field input,
.form-group.is-not-valid-field select,
.form-group.is-not-valid-field textarea {
  border-color: red;
}

.error-message {
  color: red;
  font-size: 12px;
  display: none;
}

.is-not-valid-field .error-message {
  display: block;
}
```


<div class="exercise-box">
    <h3><i class="fas fa-laptop-code"></i> Hands-On Exercise</h3>
    <p>Add three new fields to the existing form:</p>
    <ul>
        <li>A confirm password field that must match the original password field.</li>
        <li>A birthdate field. Ensure the user is at least 18 years old.</li>
        <li>A checkbox to accept the conditions. The form should not submit unless this checkbox is checked.</li>
    </ul>
    <p>Implement the validation logic for these fields using vanilla JavaScript. Ensure that appropriate error messages are displayed for invalid inputs.</p>
    <p>Research different frameworks and select one that you would use to build a Single Page Application (SPA). State the reasons that convinced you.</p>
</div>

### 4.2 **Native validation with HTML5**

### 4.3 **Validation HTML5 with Bootstrap 5**

### 4.4 **Hybrid Validation**

### 4.5 **Validation using JS libraries**

## 5. **Regular Expressions (regex)**

