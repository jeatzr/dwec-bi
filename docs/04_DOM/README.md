# **UNIT4 - Manipulating the DOM**

## **1. Document Object Model (DOM)**

The DOM (Document Object Model) is a W3C standard that defines how to access documents such as HTML and XML. It is a W3C platform application programming interface (API) that allows scripts to access and dynamically update the content, structure, and style of a document.

- **Standard**: The DOM is a standard maintained by the World Wide Web Consortium (W3C) that provides a structured representation of a document.
- **API**: It serves as an interface for programming, enabling developers to manipulate the document's structure, style, and content through scripting languages like JavaScript.
- **Dynamic Updates**: With the DOM, scripts can dynamically modify the document's content, structure, and style, allowing for interactive and responsive web applications.

Here's a simple example of how you might use the DOM to dynamically change the content of an HTML element:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DOM Example</title>
</head>
<body>
    <h1 id="title">Hello, World!</h1>
    <button onclick="changeTitle()">Change Title</button>

    <script>
        function changeTitle() {
            // Access the DOM element with the id 'title'
            const titleElement = document.getElementById('title');
            // Change the content of the element
            titleElement.textContent = 'Hello, DOM!';
        }
    </script>
</body>
</html>
```

### **1.1 DOM History**

- **Early Web (1990s)**: The web started with simple static HTML pages. There was no standard way to manipulate the content or structure of these pages dynamically.

- **Netscape and IE Wars**: Netscape Navigator and Internet Explorer (IE) were the two dominant browsers. Each developed its own methods for manipulating HTML documents, leading to compatibility issues.

- **Introduction of JavaScript (1995)**: Brendan Eich created JavaScript for Netscape, allowing basic dynamic interactions. However, Netscape’s approach differed from IE’s. Netscape Navigator 2.0 was the fist browser to implement the denominated **DOM Level 0**. 

- **W3C Involvement (1998)**: The [World Wide Web Consortium (W3C)](https://www.w3.org) stepped in to standardize how documents should be accessed and manipulated, resulting in the creation of the Document Object Model **(DOM) Level 1**.

- **DOM Level 1 (1998)**: The first version of the DOM was released, providing a standardized way to manipulate document structure and content **across different browsers**.

- **DOM Level 2 (2000)**: Introduced more advanced features like **CSS support**, **events**, and XML document manipulation.

- **DOM Level 3 (2004)**: Further expanded the API to include more features for document manipulation and traversal.

- **HTML5 and Modern Web (2010s)**: HTML5 brought significant updates to the DOM, making it more robust and enabling more complex web applications. Modern browsers have largely adopted and implemented these standards consistently.

The development and standardization of the DOM have been crucial in creating the dynamic, interactive web we know today, providing a consistent way for scripts to interact with and modify web documents across different browsers.

[--> DOM Level 3 Standard by the W3C](https://www.w3.org/DOM/DOMTR)


## **2.The DOM Tree Structure**

A DOM tree is a tree structure whose nodes represent an HTML or XML document's contents. Each HTML or XML document has a DOM tree representation. For example, consider the following document:

```html
<html lang="en">
  <head>
    <title>My Title</title>
  </head>
  <body>
    <a href="http://alink.com">My Link</a>
    <h1>My Header</h1>
  </body>
</html>
```
It has a DOM tree that looks like that:

![DOM Tree](img/dom_tree.png)

Although the above tree is similar to the above document's DOM tree, it's not identical, as [the actual DOM tree preserves whitespace](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Whitespace).

When a web browser parses an HTML document, it builds a DOM tree and then uses it to display the document.

SOURCE: [mdn web docs_](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Using_the_Document_Object_Model)

#### Tree Structure Rules:

To organize the tree structure, there are a series of rules:

- In the tree of nodes, the top node (document) is called the **root**.
- **Each node**, except the root node, **has a parent**.
- A node can have **any number of children**.
- A **leaf** is a node with **no children**.
- Nodes that **share the same parent** are **siblings**.

### **2.1 The Node Interface**

A **Node** is an abstract interface representing a single node in the tree. These nodes can be a Document, an Element, a DocumentFragment, and more.

- **Document**: The root node of the HTML document.
- **DocumentType**: A node representing the DTD (Document Type Definition) of the page.
- **Element**: A node representing an HTML element.
- **Attr**: A node representing an attribute of an element.
- **Text**: A node that stores the text contained within an Element node.
- **Comment**: A node that stores a comment in the HTML document.

#### Node Interface

- To manipulate the information of nodes, JavaScript creates an object called `Node`.
- This object defines properties and methods for processing documents.
- It also defines a set of constants that identify the types of nodes. Those are the values that the `nodeType` property can have:

| **Constant**                       | **Description**                           | **Value** |
| ---------------------------------- | ----------------------------------------- | --------- |
| `Node.ELEMENT_NODE`                | Represents an element node.               | 1         |
| `Node.ATTRIBUTE_NODE`              | Represents an attribute node.             | 2         |
| `Node.TEXT_NODE`                   | Represents a text node.                   | 3         |
| `Node.CDATA_SECTION_NODE`          | Represents a CDATA section node.          | 4         |
| `Node.ENTITY_REFERENCE_NODE`       | Represents an entity reference node.      | 5         |
| `Node.ENTITY_NODE`                 | Represents an entity node.                | 6         |
| `Node.PROCESSING_INSTRUCTION_NODE` | Represents a processing instruction node. | 7         |
| `Node.COMMENT_NODE`                | Represents a comment node.                | 8         |
| `Node.DOCUMENT_NODE`               | Represents the document node.             | 9         |
| `Node.DOCUMENT_TYPE_NODE`          | Represents the document type node.        | 10        |
| `Node.DOCUMENT_FRAGMENT_NODE`      | Represents a document fragment node.      | 11        |
| `Node.NOTATION_NODE`               | Represents a notation node.               | 12        |

#### Node Properties and Methods

| **Property/Method**              | **Description**                                                                               |
| -------------------------------- | --------------------------------------------------------------------------------------------- |
| `nodeName`                       | Returns the name of the node.                                                                 |
| `nodeType`                       | Returns an integer code representing the type of the node.                                    |
| `nodeValue`                      | Sets or returns the value of the node. For element nodes, this is `null`.                     |
| `parentNode`                     | Returns the parent node of the specified node.                                                |
| `childNodes`                     | Returns a NodeList of child nodes for the specified node.                                     |
| `firstChild`                     | Returns the first child node of the specified node.                                           |
| `lastChild`                      | Returns the last child node of the specified node.                                            |
| `previousSibling`                | Returns the previous sibling node of the specified node.                                      |
| `nextSibling`                    | Returns the next sibling node of the specified node.                                          |
| `textContent`                    | Sets or returns the text content of the node and its descendants.                             |
| `appendChild(node)`              | Adds a new child node to the end of the list of children of a specified parent node.          |
| `removeChild(node)`              | Removes a child node from the DOM and returns the removed node.                               |
| `replaceChild(newNode, oldNode)` | Replaces a child node in the DOM and returns the replaced node.                               |
| `cloneNode(deep)`                | Returns a duplicate of the node, including all its attributes and children.                   |
| `hasChildNodes()`                | Returns a Boolean indicating whether the node has any child nodes.                            |
| `isEqualNode(node)`              | Returns a Boolean indicating whether two nodes are equal.                                     |
| `isSameNode(node)`               | Returns a Boolean indicating whether two nodes are the same node.                             |
| `normalize()`                    | Merges adjacent text nodes and removes empty text nodes in the subtree of the specified node. |

These properties and methods are fundamental for navigating and manipulating the structure and content of the DOM using the `Node` interface.


To know more [--> Node Interface @ mdn web docs_](https://developer.mozilla.org/en-US/docs/Web/API/Node)

## **3. The Element Class**

The `Element` class represents an element in the DOM hierarchy, inheriting from the `Node` interface.

In the context of the DOM (Document Object Model), an element refers to an individual HTML element within an HTML document. HTML elements are the building blocks of web pages and include tags such as `<div>`, `<p>`, `<a>`, `<img>`, and so on.

#### Some Element Properties and Methods

| **Property/Method**                    | **Description**                                                                                      |
| -------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| `attributes`                           | Returns a NamedNodeMap of the attributes of the element.                                             |
| `classList`                            | Returns a DOMTokenList containing the list of class attributes.                                      |
| `id`                                   | Sets or returns the ID of the element.                                                               |
| `className`                            | Sets or returns the class name(s) of the element.                                                    |
| `tagName`                              | Returns the tag name of the element in uppercase.                                                    |
| `innerHTML`                            | Gets or sets the HTML content (including child elements and text) of the element.                    |
| `outerHTML`                            | Gets or sets the HTML content (including the element itself) of the element.                         |
| `textContent`                          | Gets or sets the text content of the element and its descendants.                                    |
| `setAttribute(name, value)`            | Sets the value of an attribute on the specified element.                                             |
| `getAttribute(name)`                   | Returns the value of the attribute with the specified name on the element.                           |
| `removeAttribute(name)`                | Removes the specified attribute from the element.                                                    |
| `hasAttribute(name)`                   | Returns a Boolean indicating whether the element has the specified attribute or not.                 |
| `appendChild(node)`                    | Adds a new child node to the end of the list of children of a specified parent node.                 |
| `removeChild(node)`                    | Removes a child node from the DOM and returns the removed node.                                      |
| `querySelector(selector)`              | Returns the first element that matches a specified CSS selector within the element's subtree.        |
| `querySelectorAll(selector)`           | Returns a NodeList of all elements that match a specified CSS selector within the element's subtree. |
| `addEventListener(event, callback)`    | Adds an event listener to the element.                                                               |
| `removeEventListener(event, callback)` | Removes an event listener from the element.                                                          |

Read more: --> [Element Class @ mdn web docs](https://developer.mozilla.org/en-US/docs/Web/API/Element)

### **3.1 Moving to Relative Elements**

We can navigate through the DOM tree from a given node  to relative elements such parent, childen and siblings using these properties and mathods:

| **Method/Property**        | **Description**                                                                  |
| -------------------------- | -------------------------------------------------------------------------------- |
| `nextElementSibling()`     | Returns the element immediately following the specified element in the DOM tree. |
| `previousElementSibling()` | Returns the element immediately preceding the specified element in the DOM tree. |
| `parentElement()`          | Returns the parent element of the specified element in the DOM tree.             |
| `firstElementChild()`      | Returns the first child element of the specified element.                        |
| `lastElementChild()`       | Returns the last child element of the specified element.                         |
| `children`                 | Returns a live HTMLCollection of child elements of the specified element.        |
| `childElementCount`        | Returns the number of child elements of the specified element.                   |

### **3.2 Direct Access to Elements**

We can access in a more direct way to element nodes of the DOM with this methods:

#### Methods for Direct Access to Elements

- **`getElementById(id)`**: Retrieves an element by its ID attribute.
- **`getElementsByClassName(className)`**: Retrieves a collection of elements that have a specified class name.
- **`getElementsByTagName(tagName)`**: Retrieves a collection of elements with the specified tag name.
- **`querySelector(selector)`**: Returns the first element that matches a specified CSS selector.
- **`querySelectorAll(selector)`**: Returns a NodeList containing all elements that match a specified CSS selector.

#### Example in JavaScript

```javascript
// Example of direct access and manipulation
const paragraph1 = document.getElementById('paragraph1');
paragraph1.style.fontWeight = 'bold';

const elementsByClass = document.getElementsByClassName('myClass');
for (let element of elementsByClass) {
    element.classList.add('highlight');
}

const elementsByTagName = document.getElementsByTagName('p');
for (let element of elementsByTagName) {
    element.style.color = 'blue';
}

const elementByQuery = document.querySelector('#parent > p:nth-child(2)');
elementByQuery.textContent = 'Modified second paragraph';

const elementsByQueryAll = document.querySelectorAll('.myClass');
elementsByQueryAll.forEach(element => {
    element.style.border = '1px solid red';
});

```

### **3.3 Accessing the attributes of an Element**

DOM allows direct access to all attributes of an element.
The `attributes` property provides access to the attributes of an element node.

DOM provides several methods that facilitate direct access to modifying, inserting, and deleting attributes of an element:

- **`getAttribute(attributeName)`**: This method is equivalent to `attributes.getNamedItem(attributeName)`.
- **`setAttribute(attributeName, attributeValue)`**: This method is equivalent to `attributes.getNamedItem(attributeName).value = attributeValue`.
- **`removeAttribute(attributeName)`**: This method is equivalent to `attributes.removeNamedItem(attributeName)`.

We can also access and modify the value of an attribute directly using dot notation followed by the attribute name:

```javascript
const value = element.value;
element.value = "new value";
element.checked = true;
```

### **3.4 The Style Attribute of an Element**

We can directly modify the CSS properties of an element by accessing its `style` attribute:
```javascript
element.style.color = "blue";
element.style.fontFamily = "Arial";
element.style.display = "block";
```

### **3.5 The Classlist Attribute**

The [`classList`](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList) attribute of an Element node allows us to manage the list of classes to which the HTML element belongs. While the attribute itself is read-only, it provides several methods for querying and modifying the classes:

- **`add( String [, String] )`**: Adds the specified classes. If these classes already exist in the element's class attribute, they are ignored.
- **`remove( String [, String] )`**: Removes the specified classes. Removing a class that does not exist does not throw an error.

    ```js
    // Select an element with id "myElement"
    const element = document.getElementById("myElement");

    // Add a class
    element.classList.add("active");

    // Remove a class
    element.classList.remove("inactive");

    ```

- **`item( Number )`**: Returns the class value by index in the collection.
- **`toggle( String [, force] )`**: When only one argument is present:
    - Toggles the class value; for example, if the class exists, it removes it and returns `false`; if not, it adds it and returns `true`.
    - When the second argument is present:
        - If the second argument evaluates to `true`, adds the specified class.
        - If the second argument evaluates to `false`, removes the specified class.
```js
// Select an element with class "toggleElement"
const element = document.querySelector(".toggleElement");

// Toggle a class
element.classList.toggle("hidden");

// Toggle with force parameter (true/false)
element.classList.toggle("visible", true);  // Adds "visible" class
element.classList.toggle("visible", false); // Removes "visible" class
```
- **`contains( String )`**: Checks if the specified class exists in the element's class attribute.

    ```js
    // Select an element with id "myElement"
    const element = document.getElementById("myElement");

    // Check if a class exists
    if (element.classList.contains("active")) {
      console.log("Element is active");
    } else {
      console.log("Element is not active");
    }
    ```

- **`replace( oldClass, newClass )`**: Replaces an existing class with a new one.

    ```js
    // Select an element with id "myElement"
    const element = document.getElementById("myElement");

    // Check if a class exists
    if (element.classList.contains("active")) {
      console.log("Element is active");
    } else {
      console.log("Element is not active");
    }

    ```


## **4. Creating New Content**

When manipulating the Document Object Model (DOM) in JavaScript, there are various ways to create and add new content to a webpage. Initially, we may resort to a simpler method by directly modifying the `innerHTML` property of an element.

Example:
```javascript
// Select an element by its ID
const container = document.getElementById('container');

// Modify the innerHTML to add new content
container.innerHTML = '<h2>New Content</h2><p>This is dynamically added content.</p>';
// append a new paragraph
container.innerHTML += '<p>Adding new paragraph.</p>';
```

While `innerHTML` provides a straightforward approach, more sophisticated methods offer greater control and performance benefits. These methods involve creating and manipulating DOM nodes directly:

### **4.1 Methods to Create New Nodes**

In JavaScript, you can create various types of nodes using the following methods:

- `createElement(tagName)`: Creates a new element node with the specified tag name.
- `createTextNode(text)`: Creates a text node with the specified text content.
- `createAttribute(name)`: Creates an attribute node with the given name.
- `createCDATASection(text)`: Creates a CDATA section node with the specified text.
- `createComment(text)`: Creates a comment node with the specified text.
- `createDocumentFragment()`: Creates a document fragment node.

### **4.2 Append New Nodes to the DOM**

Once you've created nodes, you can append them to the DOM (Document Object Model) using methods like:

- `append()` method: accepts multiple parameters, each of which can be either a Node object or a DOMString (a plain text or HTML string). It appends each parameter as a child to the element.
- `appendChild(node)`: This method accepts only a single parameter, which must be a Node object. It appends the specified child node as the last child of the element.
- `insertBefore(newNode, referenceNode)`: Inserts a new node before a specified existing node in the DOM tree.

Example:

```javascript
// Create a new <div> element
const divElement = document.createElement('div');
divElement.textContent = 'Parent Element';

// Append multiple child nodes using append()
divElement.append(
  'Text Node',   // Appends a text node
  document.createElement('span'),  // Appends an empty <span> element
  '<strong>HTML</strong>'  // Appends an HTML string as a text node
);

// Select the div with the .main class
mainDiv = document.querySelector("div.main");

// Append the div element to the main div
mainDiv.appendChild(divElement);
```

These methods allow you to dynamically create and add elements, text, attributes, comments, and more to your web page using JavaScript.