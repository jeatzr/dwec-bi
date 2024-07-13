# **UNIT2 - JavaScript Fundamentals**


## **1. General Syntax of JavaScript**
#### ECMAScript Syntax
JavaScript, also known as ECMAScript, has a syntax similar to languages like C++ and Java.

#### Single-line Comments
Use `//` to write comments on a single line.

```javascript
// This is a single-line comment
```

#### Multi-line Comments
Use `/* ... */` to write comments that span multiple lines.
```javascript
/* This is 
a multiline
comment
*/
```

#### Semicolons
The semicolon (`;`) at the end of a line is optional but recommended to avoid potential issues during code execution.

```js
let x = 5;  // Semicolon is recommended
```

#### Reserved words
Do not use reserved keywords for variable names, as they have special meaning in the language.
```js
// Incorrect
let for = 10;  // 'for' is a reserved word

// Correct
let count = 10;
```

List of reserved words: [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#reserved_words](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#reserved_words)

#### Weak typing
JavaScript is a weakly typed language, meaning you do not need to declare data types explicitly.
```js
let variable = 10;   // No need to declare type, it's a number
variable = "text";   // Now it's a string
```

Lexical Grammar: [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar)


## **2. Console messages and browser alerts**

### **2.1 Debugging Console**

We can view the console in the browser by selecting the "Inspect" option.
We can interact with the system console object by invoking its methods.

```js
console.log('Hello World!');           // general message
console.info('This is an info message'); // info message
console.warn('Be careful!');            // warning message
console.error('Fatal error');           // error message
```
#### Debugger statement
The `debugger` statement can be used to pause the execution of a script for debugging purposes.

Using the `debugger` statement, you can pause the code execution at a specific point to inspect the current state of variables and the call stack.

```javascript
function add(a, b) {
    debugger;  // Execution will pause here if the developer tools are open
    return a + b;
}
add(2, 3);
```
When the code execution reaches the debugger statement, it will pause, allowing you to use the browser's developer tools to inspect the current state and debug your code effectively.



### **2.2 Alert, Prompt and Confirm**

These methods are used to show browser alerts, request data, and confirm actions with an OK/Cancel dialog.

#### alert()
The `alert()` method displays an alert dialog with a specified message and an OK button.

```javascript
alert("This is an alert message!");
```

#### prompt()
The `prompt()` method displays a dialog with a message prompting the user to input some text. It returns the text entered by the user, or `null` if the user pressed Cancel.

```js
let userInput = prompt("Please enter your name:");
console.log("User entered: " + userInput);
```

#### confirm()
The `confirm()` method displays a dialog with a specified message, along with an OK and a Cancel button. It returns `true` if the user pressed OK, and `false` otherwise.

```js
let userConfirmed = confirm("Do you really want to delete this item?");
if (userConfirmed) {
    console.log("User confirmed the action.");
} else {
    console.log("User canceled the action.");
}
```

#### Best Practices
We should try to avoid using these methods whenever possible. They interrupt the user experience and are generally considered bad practice for modern web development. We will use them only for now, as we do not yet know other forms of dynamic communication with the user.

## **3. Variable declaration**

We can declare variables in three ways:

#### **var**

The traditional way to declare a variable. It is not recomended nowadays. 

Variables declared with `var` inside a function are **function-scoped**, meaning they are accessible throughout the function in which they are declared, but not outside of it. 

`var`  will create **globally-scoped** variables when declared outside of a function or in the global scope.

```js
var globalVar = "I'm accessible from anywhere in the script";
function testVar() {
    var functionVar = "I'm accessible within this function only";
    console.log(globalVar);  // Outputs: I'm accessible from anywhere in the script
    console.log(functionVar);  // Outputs: I'm accessible within this function only
}
console.log(globalVar);  // Outputs: I'm accessible from anywhere in the script
// console.log(functionVar);  // Uncaught ReferenceError: functionVar is not defined
```

#### **let**

A variable that is only accessible within the block, statement, or expression where it is declared. `let` is **block-scoped**.

```js
function testLet() {
    let blockVar = "I'm accessible within this block only";
    if (true) {
        let innerBlockVar = "I'm accessible within this inner block only";
        console.log(blockVar);  // Outputs: I'm accessible within this block only
        console.log(innerBlockVar);  // Outputs: I'm accessible within this inner block only
    }
    console.log(blockVar);  // Outputs: I'm accessible within this block only
    // console.log(innerBlockVar);  // Uncaught ReferenceError: innerBlockVar is not defined
}
```

#### **const**

A constant that is only accessible within the block, statement, or expression where it is declared. Constants cannot be reassigned after their initial declaration. `const` is **block-scoped**.

```js
function testConst() {
    const constantVar = "I'm a constant within this block";
    if (true) {
        const innerConstantVar = "I'm a constant within this inner block";
        console.log(constantVar);  // Outputs: I'm a constant within this block
        console.log(innerConstantVar);  // Outputs: I'm a constant within this inner block
    }
    console.log(constantVar);  // Outputs: I'm a constant within this block
    // console.log(innerConstantVar);  // Uncaught ReferenceError: innerConstantVar is not defined
    // constantVar = "New value";  // Uncaught TypeError: Assignment to constant variable.
}
```

#### **Best Practices**

It is recommended to use `let` or `const` depending on whether the value of the variable should change or not.

- Use `let` for variables that will change.
- Use `const` for variables that should not change.

```js
let mutableVariable = "I can change";
mutableVariable = "I have changed";

const immutableVariable = "I cannot change";
// immutableVariable = "Trying to change";  // Uncaught TypeError: Assignment to constant variable.

```


## **4. Primitive Data Types**

JavaScript has several primitive data types:

- **Number:** Represents both integer and floating-point numbers.
  
- **String:** Represents a sequence of characters (text).

- **Boolean:** Represents a logical entity and can have two values: `true` or `false`.

- **Undefined:** Indicates that a variable has been declared but has not yet been assigned a value.
  
- **Null:** Represents the intentional absence of any object value. It is one of JavaScript's primitive values and is treated as falsy for boolean operations.


#### Note:
- **Undefined:** `undefined` means a variable has been declared but has not yet been assigned a value.
- **Null:** `null` is an assignment value. It can be assigned to a variable as a representation of no value.

These are the basic building blocks of data in JavaScript. Understanding and using them appropriately is crucial for effective programming in JavaScript.

### **4.1 Number Type**

In JavaScript, the `number` data type represents both integers and floating-point numbers.

#### Characteristics of Numbers

- **Positive or Negative Numbers:**

  ```javascript
  let positiveNumber = 4;
  let negativeNumber = -30;
  ```

- **Numbers with or without decimals**

```js
let integer = 34;
let floatingPoint = 34.4;
let zero = 0;
let negativeFloat = -9.45;
let largeNumber = 150000000;
```

#### Arithmetic Operations

You can perform various arithmetic operations on numbers:

- Addition `+`
- Subtraction `-`
- Multiplication `*`
- Division `/`
- Modulus `%`: Returns the remainder of a division.
- Exponentiation `**`: Raises the first operand to the power of the second operand.
- Increment `++`: Increases the value of a variable by 1.
- Decrement `--`: Decreases the value of a variable by 1.
  
```js
let sum = 4 + 5;  // 9
let difference = 10 - 3;  // 7
let product = 4 * 3;  // 12
let quotient = 12 / 4;  // 3

let power = 2 ** 3;  // 8

let counter = 0;
counter++;  // counter is now 1

let counter = 1;
counter--;  // counter is now 0
```

#### Comparison Operations

You can also compare numbers using various comparison operators:

-  Less than `<`
-  Greater than `>`
-  Less than or equal to `<=`
-  Greater than or equal to `>=`
-  Equal to `==`
-  Strict equal to `===`
-  Not equal to `!=`
-  Strict not equal to `!==`

```js
let isLessThan = 5 < 10;  // true
let isGreaterThan = 10 > 5;  // true
let isLessThanOrEqualTo = 5 <= 5;  // true
let isGreaterThanOrEqualTo = 10 >= 10;  // true
let isEqualTo = 5 == '5';  // true (type coercion)
let isStrictEqualTo = 5 === 5;  // true
let isStrictEqualToDifferentTypes = 5 === '5';  // false (no type coercion)
let isNotEqualTo = 5 != '5';  // false (type coercion)
let isStrictNotEqualTo = 5 !== '5';  // true (no type coercion)
```
[--> Equality comparisons and sameness](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)

#### Additional Number Methods in Math Object

JavaScript also provides several built-in methods for working with numbers by the [Math Object](#62-math-object).


<div class="exercise-box">
<h3><i class="fas fa-laptop-code"></i> Hands-On Exercise</h3>
<p>In JS there is not an operator to calculate the <strong>integer division</strong> operation. Can you implement a way to obtain this operation using the operations listed above
?</p>
<p>Examples:</p>
<ul>
  <li>10 // 3 = 3</li>
  <li>13 // -3 = -4</li>
</ul>
</div>

#### More about number

- `typeof`: Type of the variable
- `NaN`: Not-a-Number
- `isNaN()`: Check if value is NaN
- `.toString()`: Convert number to string
- `.toFixed()`: Format number to fixed decimal places

```js
// Type of the variable
let typeOfNumber = typeof 123;  // 'number'
let typeOfString = typeof '123';  // 'string'

// NaN (Not-a-Number)
let notANumber = NaN;
let isNanCheck1 = isNaN(123);  // false
let isNanCheck2 = isNaN(NaN);  // true
let isNanCheck3 = isNaN('Hello');  // true

// Convert number to string
let numberToString = (123).toString();  // '123'

// Format number to fixed decimal places
let fixedDecimal = (123.456).toFixed(2);  // '123.46'
```

### **4.2 String Type**

In JavaScript, the `string` data type is used to represent textual data.

#### Characteristics of Strings

- **Strings**: A sequence of characters enclosed in quotes.
  - Double quotes: `"Hello world"`
  - Single quotes: `'Hello world'`

#### Operations with Strings

- **Concatenation**: Combining multiple strings into one.
    - Example: `cadena = 'Hola' + ' mundo'` results in `'Hola mundo'`
- **Comparison Operations**: Comparing strings.
    - Equal to (`==`)
    - Strict equal to (`===`)
    - Not equal to (`!=`)
- **Other Useful Methods**: We can find them in the [String Object](#64-string-object)


```js
// Characteristics of Strings
let string1 = "Hello world";
let string2 = 'Hello world';

// Concatenation
let greeting = 'Hola' + ' mundo';  // 'Hola mundo'

// Comparison Operations
let isEqual = 'Hello' == 'Hello';  // true
let isStrictEqual = 'Hello' === 'Hello';  // true
let isStrictEqual2 = '123' === 132;  // false
let isNotEqual = 'Hello' != 'World';  // true

// Other useful methods
let stringLength = greeting.length;  // 10
let upperCase = greeting.toUpperCase();  // 'HOLA MUNDO'
let lowerCase = greeting.toLowerCase();  // 'hola mundo'
let includesWord = greeting.includes('mundo');  // true
let splitString = greeting.split(' ');  // ['Hola', 'mundo']
let substring = greeting.substring(1, 4);  // 'ola'  substring(start, end+1)
let charAt = greeting.charAt(1);  // 'o'
let indexOfChar = greeting.indexOf('m');  // 5
let replacedString = greeting.replace('mundo', 'everyone');  // 'Hola everyone'
let trimmedString = '   Hola mundo   '.trim();  // 'Hola mundo'
```

#### Template literals

Template literals, also known as template strings, are a feature in JavaScript that allows for easier string interpolation and multi-line strings. They are enclosed by backticks (`` ` ``) instead of single or double quotes.

```js
let text = `Hello, world!`;
```

#### Features of Template Literals

1. **String Interpolation**: Embed expressions within a string using the `${expression}` syntax.

```js
let firstName = "John";
let lastName = "Doe";
let age = 30;
let introduction = `My name is ${firstName} ${lastName} and I am ${age} years old.`;

let result = `2 + 2 is ${2 + 2}`;  // "2 + 2 is 4"
```

2. **Multi-line Strings**: Create strings that span multiple lines.

```js
let address = `1234 Elm Street
Springfield, IL
62704`;
```

<div class="exercise-box">
    <h3><i class="fas fa-laptop-code"></i> Hands-On Exercise: Working with Strings in JavaScript</h3>
    <p>Follow these steps to complete the exercise:</p>
    <ol>
        <li><strong>Concatenation and Template Literals</strong>:
            <ul>
                <li>Create two string variables, <code>firstName</code> and <code>lastName</code>.</li>
                <li>Concatenate them using both the <code>+</code> operator and template literals to form a full name.</li>
            </ul>
        </li>
        <li><strong>String Methods</strong>:
            <ul>
                <li>Use <code>.toUpperCase()</code> and <code>.toLowerCase()</code> methods to change the case of the full name.</li>
                <li>Extract a substring from the full name using both <code>substring()</code> and <code>slice()</code>.</li>
            </ul>
        </li>
        <li><strong>String Interpolation</strong>:
            <ul>
                <li>Create a multi-line string using template literals that includes the full name and an address.</li>
            </ul>
        </li>
        <li><strong>Splitting and Trimming Strings</strong>:
            <ul>
                <li>Create a string that includes a list of comma-separated items.</li>
                <li>Split the string into an array and trim any extra whitespace from each item.</li>
            </ul>
        </li>
        <li><strong>Checking and Converting</strong>:
            <ul>
                <li>Create a variable that includes a number as a string.</li>
                <li>Check if it is a number using <code>isNaN()</code> and convert it to a number.</li>
                <li>Use <code>.toString()</code> to convert a number back to a string.</li>
                <li>Use <code>.toFixed()</code> to format a number to two decimal places.</li>
            </ul>
        </li>
    </ol>
</div>

### **4.3 Boolean Type**

- It only accepts two values: `true` or `false`
- It is useful for checking the state of the application
- It is recommended that its name defines the positive state
    - Example: `userIsLogged`, `itemFound`, `errorFound` 

- `Boolean(value);` returns the boolean value of a condition or variable.

#### Boolean()

`Boolean(value);` returns the boolean value of a condition or variable.

#### True vs False 

| True         | False       |
| ------------ | ----------- |
| 1            | 0, -0       |
| `"Whatever"` | `""`        |
| 3.14         | NaN         |
| `100 > 5`    | null        |
| `1 < 100`    | undefined   |
| `'1' == 1`   | `'1' === 1` |

```js
// Example 1: Using Boolean() to get the boolean value
console.log(Boolean(1));           // true
console.log(Boolean(0));           // false
console.log(Boolean("Whatever"));  // true
console.log(Boolean(""));          // false

// Example 2: Using expressions
console.log(100 > 5);              // true
console.log(1 < 100);              // true
console.log('1' == 1);             // true
console.log('1' === 1);            // false

// Example 3: Checking for undefined and null
let a;
console.log(Boolean(a));           // false

let b = null;
console.log(Boolean(b));           // false

// Example 4: NaN check
let c = NaN;
console.log(Boolean(c));           // false
console.log(isNaN(c));             // true

// Example 5: Combining multiple checks
let value = "Hello";
if (value && typeof value === "string") {
    console.log("Value is a non-empty string"); // This will log
}

let number = 0;
if (!number) {
    console.log("Number is zero or false"); // This will log
}
```

### **4.4 Undefined and Null Types**

In JavaScript, `undefined` and `null` are two distinct types that represent absence of value or non-existence. They are often confused with each other but have different meanings and use cases.

#### Undefined
- **Type**: `undefined`
- **Description**: A variable that has been declared but has not yet been assigned a value has the value `undefined`.
- **Example**:
    ```javascript
    let a;
    console.log(a); // Output: undefined
    ```

#### Null
- **Type**: `object`
- **Description**: `null` is an assignment value that can be used to represent no value or no object. It's explicitly set by the programmer to indicate "no value".
- **Example**:
    ```javascript
    let b = null;
    console.log(b); // Output: null
    ```

#### Key Differences

- **Type**:
    - `undefined`: The type of `undefined` is `undefined`.
    - `null`: The type of `null` is `object` (this is a historical bug in JavaScript, but it remains for backward compatibility).

- **Default Value**:
    - `undefined` is the default value for uninitialized variables.
    - `null` is an explicit assignment to indicate an empty or non-existent value.

- **Usage**:
    - Use `undefined` to check if a variable has been declared but not yet assigned a value.
    - Use `null` to intentionally signify that a variable should be empty.

#### Examples

```javascript
// Undefined example
let x;
console.log(x); // Output: undefined

// Null example
let y = null;
console.log(y); // Output: null

// Checking types
console.log(typeof x); // Output: undefined
console.log(typeof y); // Output: object
```
## **5. Control Sentences**

### **5.1 Conditional Statements**

#### [if...else](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else) 

Conditional statements allow the execution of specific code blocks based on certain conditions. The most common conditional statements are `if`, `else if`, and `else`.

Examples of usage:

```js
let number = 10;

if (number > 0) {
    console.log("The number is positive.");
} else if (number < 0) {
    console.log("The number is negative.");
} else {
    console.log("The number is zero.");
}
```

#### [switch](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch)

A `switch` statement evaluates a variable or expression and matches its value to one of several possible cases. Each case corresponds to a specific code block that executes when a match is found. If no match is found, an optional `default` case can execute.

Examples of usage:

#### JavaScript

```javascript
let fruit = 'apple';

switch (fruit) {
    case 'apple':
        console.log("This is an apple.");
        break;
    case 'banana':
        console.log("This is a banana.");
        break;
    case 'orange':
        console.log("This is an orange.");
        break;
    default:
        console.log("Unknown fruit.");
}
```

#### [Conditional (ternary) operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_operator)


The conditional ternary operator is a concise way to perform conditional evaluations. It takes three operands: a condition, a result for true, and a result for false. The syntax is:

`condition ? expression_if_true : expression_if_false`

Examples of usage:

```javascript
let age = 18;
let canVote = (age >= 18) ? "Yes, you can vote." : "No, you cannot vote.";
console.log(canVote);
```

### **5.2 Loops or Iterations**

#### [for](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for) (traditional loop with a counter)
The `for` loop is a traditional loop that iterates with a counter. It is used to repeat a block of code a certain number of times.

Examples of usage:

```javascript
for (let i = 0; i < 5; i++) {
    console.log(i);
}

// Counting backwards in 5 units steps
for (let i = 50; i >= 0; i -= 5) {
    console.log(i);
}
```

#### [for..in](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in) (iterates over properties of an object)
The `for..in` loop iterates over the enumerable properties of an object. It is used to traverse object properties.

Examples of usage:
```js
let person = {name: 'John', age: 30, city: 'New York'};
for (let key in person) {
    console.log(key + ': ' + person[key]);
}
```
#### [for..of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of) (ES6) (iterates over a collection of objects)
The `for..of` loop, introduced in ES6, iterates over iterable objects such as arrays, strings, and other collections.

Examples of usage:

```js
let fruits = ['apple', 'banana', 'orange'];
for (let fruit of fruits) {
    console.log(fruit);
}
```

#### [forEach](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) (method to iterate over a collection of objects)

However, in JavaScript, **the most common way to iterate over arrays of objects** is using the `forEach` method. This method executes a provided function once for each array element, making it more convenient and readable for such tasks.

```js
const users = [
    { name: 'John', age: 30 },
    { name: 'Jane', age: 25 },
    { name: 'Jim', age: 35 }
];

users.forEach(user => {
    console.log(`${user.name} is ${user.age} years old.`);
});
```

#### while (traditional while loop)

The `while` loop repeats a block of code as long as a specified condition is true.

```js
let i = 0;
while (i > 0.5) {
    console.log(i);
    i = Math.rand();
}
console.log(`Found a rand number greater than 0.5: ${i}`);
```

## **6. Native JavaScript Objects** 

JavaScript provides several built-in objects that allow developers to work with different data types, perform common tasks, manipulate the DOM and handle errors. These objects are part of the JavaScript language and are available globally.

![Native Objects](img/native_objects.png)

JavaScript native objects can be categorized into two types based on their usage context and origin:

#### Browser-Independent Objects (Available also in Node.js)

These objects are part of the JavaScript language specification and can be used in both browser and server-side environments (like Node.js). They typically start with an uppercase letter:

- **Math**: Provides mathematical constants and functions.
- **Number**: Represents numerical values and provides methods for numeric operations.
- **Date**: Represents dates and times.
- **Array**: Represents a list-like collection of elements.

These objects are implemented as part of the JavaScript language itself and do not rely on the presence of a browser environment.

#### Browser-Dependent Objects (Client-Side Environment)

These objects are specific to the browser environment and are not available in server-side JavaScript (Node.js). They typically start with a lowercase letter:

- **window**: Represents the global browser window and acts as the global object in client-side JavaScript.
- **document**: Represents the HTML document loaded in the browser window.
- **navigator**: Provides information about the client's browser and operating system.
- **localStorage / sessionStorage**: Provides storage mechanisms within the browser for persisting data.

These objects interact directly with the browser's Document Object Model (DOM) and are essential for client-side scripting and web application development.

#### Usage Contexts

- **Node.js**: Browser-independent objects (e.g., Math, Number, Date) can be used in Node.js applications without any dependency on a browser environment.
- **Browser**: Browser-dependent objects (e.g., window, document, navigator) are specific to the client-side environment and require a web browser for execution.

We are going to explain the most useful for us for the scope of this course.

### **6.1 [Date Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)**

- The Date object in JavaScript is used for working with dates and times. 
- It allows you to create and manipulate dates, get and set various date components (like year, month, day, hour, minute, second), and perform operations such as formatting and arithmetic.
- Internally, the number of milliseconds since 00:00:00 UTC on January 1, 1970, is stored.
  
Constructor: 

```js
let currentDate = new Date();               // Current date and hour
let specificDate = new Date(1626176282855); // Example with number of millisecons
let customDate = new Date(2023, 5, 12, 14, 30, 0, 0); // June 12, 2023, 14:30:00

```

#### **getFullYear(), getMonth(), getDate(), getDay(), getHours(), getMinutes(), getSeconds(), getMilliseconds():** Retrieve various components of the date.

```js
let now = new Date();
let year = now.getFullYear();
let month = now.getMonth(); // 0-indexed (January is 0)
let day = now.getDate();
let hours = now.getHours();
let minutes = now.getMinutes();
let seconds = now.getSeconds();
```

#### **setFullYear(), setMonth(), setDate(), setHours(), setMinutes(), setSeconds(), setMilliseconds()**: Set various components of the date.

```js
day = new Date(2000, 0, 1); // January 1, 2000
birthday.setFullYear(2001); // Change year to 2001
```

#### **toDateString(), toISOString(), toLocaleDateString(), toLocaleTimeString()**: Convert date objects to different string representations.

```js
let today = new Date();
let dateString = today.toDateString(); // "Tue Jul 13 2024"
let isoString = today.toISOString(); // "2024-07-13T12:30:00.000Z"
let localeDateString = today.toLocaleDateString(); // Depends on locale
```

#### Working with dates

Here's an example that demonstrates creating a `Date` object, accessing its components, and formatting its output:

```js
let now = new Date();

let year = now.getFullYear();
let month = now.getMonth(); // 0-indexed (July is 6)
let day = now.getDate();
let hours = now.getHours();
let minutes = now.getMinutes();
let seconds = now.getSeconds();

console.log(`Current date and time: ${day}/${month + 1}/${year} ${hours}:${minutes}:${seconds}`);
```

Here's the example in JavaScript comparing two dates:

```js
// Create two dates
let date1 = new Date('2023-07-13');
let date2 = new Date('2023-07-14');

// Compare the dates
if (date1 < date2) {
    console.log(`${date1.toDateString()} is before ${date2.toDateString()}`);
} else if (date1 > date2) {
    console.log(`${date1.toDateString()} is after ${date2.toDateString()}`);
} else {
    console.log(`${date1.toDateString()} and ${date2.toDateString()} are equal`);
}
```

### **6.2 [Math Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math)**

The Math object in JavaScript provides mathematical constants and functions, allowing you to perform mathematical tasks without explicitly creating a Math object instance. It includes methods for rounding, trigonometry, logarithms, exponentiation, some constants as PI number, and more.

- `Math.abs()`: Absolute value
- `Math.ceil()`: Round up
- `Math.floor()`: Round down
- `Math.round()`: Round to nearest integer
- `Math.max()`: Maximum value
- `Math.min()`: Minimum value
- `Math.random()`: Random number between 0 and 1
- `Math.sqrt()`: Square root
- `Math.PI`: PI number

```js
let absoluteValue = Math.abs(-5);  // 5
let roundedUp = Math.ceil(4.2);  // 5
let roundedDown = Math.floor(4.8);  // 4
let rounded = Math.round(4.5);  // 5
let roundedDownExample = Math.round(4.4);  // 4
let max = Math.max(1, 2, 3);  // 3
let min = Math.min(1, 2, 3);  // 1
let random = Math.random();  // e.g., 0.543
let squareRoot = Math.sqrt(16);  // 4

// Also Math object contains some useful constants as PI or E number
let piNumber = Math.PI;  // 3.1415......
```

### [**6.4 String Object**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)

The String object is a wrapper around JavaScript's primitive string data type. It provides various methods and properties to work with strings effectively.

#### Creating String Objects
In JavaScript, you can create a string primitive directly or use the String object constructor to create a String object:

```javascript
// String primitive
let message = 'Hello, World!';

// Using String object constructor
let anotherMessage = new String('Hello, World!');
```

#### Useful Methods and properties

- `length`: Returns the length of the string.
- `charAt(index)`: Returns the character at the specified index.
- `concat(str1, str2, ...)`: Concatenates one or more strings to the end of the calling string and returns a new string.
- `toUpperCase()`: Converts all characters to uppercase.
- `toLowerCase()`: Converts all characters to lowercase.
- `indexOf(searchValue, startIndex)`: Returns the index of the first occurrence of `searchValue` in the string, starting the search at `startIndex`.
- `substring(startIndex, endIndex)`: Returns a new substring from `startIndex` to `endIndex` (excluding `endIndex`).
- `slice(startIndex, endIndex)`: Extracts a section of the string and returns it as a new string.
- `split(separator)`: Splits the string into an array of substrings based on a specified `separator`.

Examples of use:

Those methods already have been used in the [String Primitive Data Type](#42-string-type)

### **6.5 Browser Interaction Objects**

In addition to those presented earlier, there are other types of objects that allow manipulation of browser-specific features:

- **navigator**: Provides information about the client's browser and operating system.
- **screen**: Represents the properties of the user's screen.
- **window**: Represents the global browser window and acts as the global object in client-side JavaScript.
- **document**: Represents the HTML document loaded in the browser window.
- **history**: Provides the browser's session history (pages visited in the current tab/window).

#### [navigator](https://developer.mozilla.org/en-US/docs/Web/API/Navigator)

To identify the characteristics of the platform where a web application is running, you can use properties and methods provided by the `navigator` object in JavaScript:

1. **Type of Browser and Version**:
      - Use `navigator.userAgent` to obtain the User-Agent string, which includes information about the browser type and version.

2. **Operating System**:
      - Use `navigator.platform` to retrieve the platform on which the browser is executing (e.g., "Win32", "Linux x86_64", "MacIntel").

3. **Geolocation**:
      - Utilize the Geolocation API to request and obtain the device's current geographical location, provided the user grants permission.

   Example JavaScript code:
```javascript
// User Agent
let browserInfo = navigator.userAgent;
console.log(`User-Agent: ${browserInfo}`);

// Platform Info
let platformInfo = navigator.platform;
console.log(`Platform: ${platformInfo}`);

// Geolocation
if ('geolocation' in navigator) {
    navigator.geolocation.getCurrentPosition(position => {
      console.log('Latitude:', position.coords.latitude);
      console.log('Longitude:', position.coords.longitude);
    }, error => {
        console.error('Error getting geolocation:', error);
    });
} else {
    console.error('Geolocation is not supported by this browser.');
}
```

#### [screen](https://developer.mozilla.org/en-US/docs/Web/API/Window/screen) 


The `screen` object in JavaScript represents the user's screen and provides read-only properties to retrieve information about its characteristics.

#### Properties of the `screen` Object

- **`screen.width`**: Returns the width of the user's screen in pixels.
- **`screen.height`**: Returns the height of the user's screen in pixels.
- **`screen.availWidth`**: Returns the available width of the user's screen (excluding operating system taskbars, etc.) in pixels.
- **`screen.availHeight`**: Returns the available height of the user's screen (excluding operating system taskbars, etc.) in pixels.
- **`screen.colorDepth`**: Returns the bit depth of the color palette for displaying images on the user's screen.
- **`screen.pixelDepth`**: Returns the bit depth of the pixel buffer of the user's screen.

These properties allow web applications to adapt their content or behavior based on the user's screen dimensions and capabilities, enhancing the user experience.

Here's a simple example demonstrating how to access and use some of these properties in JavaScript:

```javascript
console.log(`Screen width: ${screen.width}px`);
console.log(`Screen height: ${screen.height}px`);
console.log(`Available screen width: ${screen.availWidth}px`);
console.log(`Available screen height: ${screen.availHeight}px`);
console.log(`Color depth: ${screen.colorDepth} bits`);
console.log(`Pixel depth: ${screen.pixelDepth} bits`);
```

#### [window](https://developer.mozilla.org/en-US/docs/Web/API/Window)

The `window` object is considered one of the most important objects in JavaScript for several reasons:

- **Window Management**: It allows for managing browser windows and provides methods to manipulate and interact with them.

- **Implicit Object**: The `window` object is implicit, meaning you don't need to explicitly reference it to access objects and properties nested within its hierarchy. For example, `window.document` directly refers to the `document` object without explicitly stating `window`.


#### [document](https://developer.mozilla.org/en-US/docs/Web/API/Document)
The `document` object in JavaScript represents the current web page loaded in the browser window. It provides access to the DOM (Document Object Model) of the page, allowing developers to manipulate its content, structure, and styles dynamically.

#### Key Features of the `document` Object:

- **DOM Manipulation**: Developers can access and modify elements within the web page using methods like `getElementById`, `querySelector`, and properties like `textContent`, `innerHTML`.

- **Event Handling**: Enables attaching event listeners to elements and responding to user interactions or other events on the page.

- **Dynamic Updates**: Allows scripts to dynamically update the content of the page based on user input, server responses, or other conditions.

##### Example of DOM Manipulation:

```javascript
// Accessing an element by its ID and changing its content
const headerElement = document.getElementById('header');
headerElement.textContent = 'Welcome to our Website!';
```

#### [history](https://developer.mozilla.org/en-US/docs/Web/API/History)

In JavaScript, the `history` object provides methods and properties to navigate through the user's browsing history. It allows storing references to visited web pages and facilitates navigation between them using a list-like structure.

##### Key Features of the `history` Object:

- **`history.length`**: Returns the number of entries in the browsing history stack.

- **`history.back()`**: Moves back one page in the session history. Equivalent to clicking the browser's back button.

- **`history.forward()`**: Moves forward one page in the session history. Equivalent to clicking the browser's forward button.

- **`history.go(n)`**: Loads a specific page from the session history, where `n` can be a positive or negative integer. Negative values move backwards, and positive values move forwards.

##### Example Usage:

```javascript
// Navigating back and forward in history
function goBack() {
    window.history.back();
}

function goForward() {
    window.history.forward();
}

// Accessing the length of the history stack
let historyLength = window.history.length;
console.log(`Number of pages in history: ${historyLength}`);
```

## **7. Functions**

A function in programming is a reusable block of code that performs a specific task. It can take inputs, process them, and return an output. Functions are fundamental building blocks in programming, allowing for modular, readable, and maintainable code.

#### Key Characteristics of Functions:

1. **Modularity**: Functions allow code to be divided into smaller, manageable pieces, each performing a specific task.
2. **Reusability**: Once defined, a function can be called multiple times within a program, reducing redundancy.
3. **Abstraction**: Functions enable the encapsulation of complex operations, hiding the details and exposing only necessary interfaces.
4. **Maintainability**: Functions make it easier to update and manage code. Changes made within a function do not affect other parts of the code that rely on it.

#### Basic Structure of a Function:

1. **Function Declaration**: Defines the function and specifies its name, parameters, and body.
2. **Function Call**: Executes the function by referencing its name and passing any required arguments. Optionally we can save the value that is returned by the function. 

#### Example in JavaScript:

Note that in Javascript we don't declare the type of the parameters and the return.

```javascript
// Function Declaration
function greet(name) {
    return `Hello, ${name}!`;
}

// Function Call
let message = greet('Alice');
console.log(message); // Output: Hello, Alice!
```

### **7.1 Global Functions in JavaScript**

Global functions in JavaScript are built-in functions that are part of the global object and can be called from anywhere in your code. They are available in both the browser and Node.js environments. Here are some of the most commonly used global functions:

1. **`parseInt(string, radix)`**
      - Parses a string and returns an integer of the specified radix (base).
      - Example:
     ```javascript
     let num = parseInt("10", 10); // 10
     ```

2. **`parseFloat(string)`**
      - Parses a string and returns a floating-point number.
      - Example:
        ```javascript
        let num = parseFloat("10.5"); // 10.5
        ```

3. **`isNaN(value)`**
      - Determines whether a value is NaN (Not-a-Number).
      - Example:
        ```javascript
        let result = isNaN("hello"); // true
        ```

4. **`isFinite(value)`**
      - Determines whether a value is a finite number.
      - Example:
        ```javascript
        let result = isFinite(10); // true
        let result2 = isFinite(Infinity); // false
        ```

5. **`eval(string)`**
      - Evaluates JavaScript code represented as a string.
      - Example:
        ```javascript
        let result = eval("2 + 2"); // 4
        ```

6. **`encodeURI(uri)`**
      - Encodes a Uniform Resource Identifier (URI) by escaping certain characters.
      - Example:
        ```javascript
        let uri = "https://www.example.com?name=John Doe";
        let encodedURI = encodeURI(uri); // "https://www.example.com?name=John%20Doe"
        ```

7. **`encodeURIComponent(uriComponent)`**
      - Encodes a URI component by escaping certain characters.
      - Example:
        ```javascript
        let uriComponent = "John Doe & Co";
        let encodedURIComponent = encodeURIComponent(uriComponent); // "John%20Doe%20%26%20Co"
        ```

8. **`decodeURI(encodedURI)`**
      - Decodes a Uniform Resource Identifier (URI) created by `encodeURI`.
      - Example:
        ```javascript
        let encodedURI = "https://www.example.com?name=John%20Doe";
        let decodedURI = decodeURI(encodedURI); // "https://www.example.com?name=John Doe"
        ```

9. **`decodeURIComponent(encodedURIComponent)`**
      - Decodes a URI component created by `encodeURIComponent`.
      - Example:
        ```javascript
        let encodedURIComponent = "John%20Doe%20%26%20Co";
        let decodedURIComponent = decodeURIComponent(encodedURIComponent); // "John Doe & Co"
        ```

10. **`setTimeout(function, delay)`**
      - Calls a function or evaluates an expression after a specified number of milliseconds.
      - Example:
          ```javascript
          setTimeout(function() {
              console.log("Hello after 2 seconds");
          }, 2000);
          ```

11. **`setInterval(function, delay)`**
      - Repeatedly calls a function or evaluates an expression at specified intervals (in milliseconds).
      - Example:
          ```javascript
          setInterval(function() {
              console.log("Hello every 2 seconds");
          }, 2000);
          ```

12. **`clearTimeout(timeoutID)`**
      - Clears a timer set with `setTimeout`.
      - Example:
          ```javascript
          let timeoutID = setTimeout(function() {
              console.log("This won't run");
          }, 2000);
          clearTimeout(timeoutID);
          ```

13. **`clearInterval(intervalID)`**
      - Clears a timer set with `setInterval`.
      - Example:
          ```javascript
          let intervalID = setInterval(function() {
              console.log("This won't run repeatedly");
          }, 2000);
          clearInterval(intervalID);
          ```

### **7.2 Declaring User Functions**

It is possible to create custom functions in JavaScript, different from the predefined functions provided by the language. There are two types of function declarations:

1. **Classical Function Declaration using the `function` Keyword**
2. **Function by Expression (Lambda)**
3. **Arrow Functions (introduced in ES6)**

#### Classical Function Declaration

The classical way to define a function in JavaScript is by using the `function` keyword. This method allows you to create named or anonymous functions.

Example:

```javascript
// Named function
function add(a, b) {
    return a + b;
}

// Function call
let result = add(2, 3);
console.log(result); // Output: 5
```

#### Function by Expression and Lambda function.

You can asign a function to a variable by a expression.

We can assing or pass as a parameter an anonymous function. We call this a Lambda function.


```js
// 1. Function by expression
const multiply = function multiplication(a, b) {
    return a * b;
};

// Calling the function
let result = multiply(5, 3);
console.log(result); // Output: 15

// 2. Lambda or anonymous function by expression
// this second options has more sense
const divide = function (a,b) {
    return a / b;
}

// We call exactly the same
let resultDiv = divide(15, 3);
console.log(resultDiv); // Output: 5

```

#### Arrow Functions (Lambda)

Arrow functions provide a more concise syntax to write functions in JavaScript. They are anonymous (also called Lambda) and are often used in place of function expressions.

```js
// Traditional Function
const f1 = function (a) {
  return a + 100;
}

// Breakdown of the Arrow Function

// 1. Remove the "function" keyword and place the arrow between the argument and the opening brace.
const f2 = (a) => {
  return a + 100;
}

// 2. Remove the braces of the body and the "return" keyword — the return is implicit.
const f3 = (a) => a + 100;

// 3. Omit the parentheses around the argument
const f4 = a => a + 100;
```
<div class="exercise-box">
    <h3><i class="fas fa-laptop-code"></i> Hands-On Exercise: Calculate Days Between Two Dates</h3>
    <p>Write a JavaScript function that calculates the number of days between two given dates.</p>
    <h4>Instructions:</h4>
    <ol>
        <li>Create a function <code>calculateDaysBetweenDates(date1, date2)</code> that takes two date strings as input.</li>
        <li>Parse the date strings into <code>Date</code> objects.</li>
        <li>Calculate the difference in milliseconds between the two dates.</li>
        <li>Convert the difference in milliseconds to days.</li>
        <li>Return the number of days between the two dates.</li>
    </ol>
    <h4>Example Usage:</h4>
    <pre><code>let date1 = "2024-07-01";
let date2 = "2024-07-13";
let daysBetween = calculateDaysBetweenDates(date1, date2);
console.log(`There are ${daysBetween} days between ${date1} and ${date2}.`); // Output: There are 12 days between 2024-07-01 and 2024-07-13.</code></pre>
    <h4>Hints:</h4>
    <ul>
        <li>Use <code>new Date(dateString)</code> to create <code>Date</code> objects from the date strings.</li>
        <li>Subtract the earlier date from the later date to get the difference in milliseconds.</li>
        <li>There are <code>1000 * 60 * 60 * 24</code> milliseconds in a day.</li>
    </ul>
</div>

### **7.3 Callback Functions**

At a high level, a callback is when a function B is passed as a parameter to another function A. This allows function A to invoke (or "call back") function B at a later time, typically in response to some event or condition.

#### Key Points:

- **Flexibility**: Callbacks provide a way to specify custom behavior that should be executed when an action is completed or an event occurs.
- **Asynchronous Operations**: They are commonly used in asynchronous programming to handle operations that take time to complete, such as fetching data from a server.
- **External Definition**: Callback functions are defined outside of the function that uses them, allowing for modular and reusable code.

##### Example Concept:

```javascript
// Function A takes function B as a callback parameter
function A(callback) {
    // Function A's logic
    console.log("Inside function A");
    
    // Invoke the callback function B
    callback();
}

// Function B (callback function)
function B() {
    console.log("Callback function B executed");
}

// Call function A and pass function B as a callback
A(B);
```
#### Ad-hoc callback functions

In JavaScript, ad-hoc callback functions are functions that are defined inline at the moment they are passed as arguments to another function. The `forEach` method is a good example where ad-hoc callbacks are frequently used to iterate over arrays.

##### Example Using `forEach`:

```javascript
// Array of numbers
const numbers = [1, 2, 3, 4, 5];

// Using forEach with an ad-hoc callback function
numbers.forEach(function(item) {
    console.log(item); // Show each number
});


// Using forEach with an ad-hoc callback arrow function
numbers.forEach( item => {
    console.log(item * 2); // Show each number multiplied by 2
});
```




