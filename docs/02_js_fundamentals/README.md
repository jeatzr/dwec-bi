# **UNIT2 - JS Fundamentals**


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

### **var**

The traditional way to declare a variable. Is is not recomended nowadays. 

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

### **let**

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

### **const**

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

### **Best Practices**

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

#### Additional Number Methods

JavaScript also provides several built-in methods for working with numbers by the Math object.

- `Math.abs()`: Absolute value
- `Math.ceil()`: Round up
- `Math.floor()`: Round down
- `Math.round()`: Round to nearest integer
- `Math.max()`: Maximum value
- `Math.min()`: Minimum value
- `Math.random()`: Random number between 0 and 1
- `Math.sqrt()`: Square root

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
```

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

### 4.4 Undefined and Null Types

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

