# **UNIT8 - React: A Java Script framework**

## 1. **Modern JavaScript Features for React Development**

### 1.1 **JavaScript Modules**

- **What are Modules?**

  - Importing and exporting functions, objects, or values from one file to another.

- **Syntax**

  ```javascript
  // Exporting
  export const greet = () => {
    console.log("Hello!");
  };

  // Importing
  import { greet } from "./greetModule.js";
  greet();
  ```

### 1.2 **Destructuring Assignment**

- **What is Destructuring?**
  - A syntax to unpack values from arrays or properties from objects into distinct variables.
- **Examples**

  ```javascript
  // Array destructuring
  const [first, second] = [1, 2, 3];
  console.log(first, second); // Output: 1, 2

  // Object destructuring
  const user = { name: "Alice", age: 25 };
  const { name, age } = user;
  console.log(name, age); // Output: Alice, 25
  ```

### 3. **Spread and Rest Operators** (`...`)

- **Spread Operator**

  - Used to expand elements of an array or object.

  ```javascript
  const arr = [1, 2, 3];
  const newArr = [...arr, 4, 5];
  console.log(newArr); // Output: [1, 2, 3, 4, 5]

  const user = { name: "Alice", age: 25 };
  const updatedUser = { ...user, location: "NY" };
  console.log(updatedUser); // Output: { name: 'Alice', age: 25, location: 'NY' }
  ```

- **Rest Operator**

  - Used to collect arguments into an array or remaining properties into an object.

  ```javascript
  const sum = (...numbers) => numbers.reduce((total, num) => total + num, 0);
  console.log(sum(1, 2, 3)); // Output: 6

  const { name, ...rest } = { name: "Alice", age: 25, location: "NY" };
  console.log(rest); // Output: { age: 25, location: 'NY' }
  ```

### 1.4 **Arrow Functions**

- **What are Arrow Functions?**
  - A concise syntax for writing functions. They also handle `this` context differently than regular functions.
- **Syntax**
- ```javascript
  const add = (a, b) => a + b;
  console.log(add(2, 3)); // Output: 5
  ```

### 1.5 **Template Literals**

- **What are Template Literals?**
  - A syntax for creating strings with embedded expressions using backticks.
- **Examples**

  ```javascript
  const name = "Alice";
  console.log(`Hello, ${name}!`); // Output: Hello, Alice!
  ```

### 1.6 **Default Parameters**

- **What are Default Parameters?**
  - Setting default values for function parameters.
- **Examples**

  ```javascript
  const greet = (name = "Guest") => `Hello, ${name}!`;
  console.log(greet()); // Output: Hello, Guest!
  ```
