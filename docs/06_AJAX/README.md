# **UNIT6 - AJAX**

## 1. **Introduction to AJAX**
What is AJAX? 

![ajax](img/00_ajax.png)

#### Definition

AJAX, which stands for Asynchronous JavaScript and XML, is a technique used to create dynamic and interactive web applications. It allows web pages to be updated asynchronously by exchanging small amounts of data with the server behind the scenes. This means that it is possible to update parts of a web page, without reloading the whole page.

### **1.1 The HTTP Request**

An AJAX request is essentially an asynchronous HTTP request. 

HTTP is a protocol for fetching resources such as HTML documents. It is the foundation of any data exchange on the Web and it is a client-server protocol, which means requests are initiated by the recipient, usually the Web browser. A complete document is typically constructed from resources such as text content, layout instructions, images, videos, scripts, and more.

![fetching a page](img/fetching-a-page.svg)

Source --> [mdn web docs_ ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)

Here are the basic components of an HTTP request:

#### HTTP Methods:

   - **GET:** Requests data from the server. It should only retrieve data and not change any server state.
   - **POST:** Submits data to be processed to a specified resource. It often causes a change in server state.
   - **PUT:** Updates a current resource with new data.
   - **PATCH:** Uptates part of a current resource with new data.
   - **DELETE:** Removes a specified resource.

#### Request URL

The URL specifies the **endpoint** to which the request is being sent. It is the address of the resource.

#### Headers

HTTP headers let the client and the server pass additional information with an HTTP request or response.

#### Body

The body of an HTTP request contains the data to be sent to the server (mostly used with **POST** and **PUT** requests).
The most common format to send data is plain text formated in JSON. 

Example of GET and POST request:

```http
  GET https://example.com/comments/1 HTTP/1.1

  ###

  GET https://example.com/topics/1 HTTP/1.1

  ###

  POST https://example.com/comments HTTP/1.1
  content-type: application/json
  {
      "name": "sample",
      "time": "Wed, 21 Oct 2015 18:27:50 GMT"
  }
```

#### **[HTTP Response Status Codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)**



### 1.2 **Understanding Asynchrony in JavaScript**

Asynchrony is a fundamental concept in JavaScript that allows programs to handle multiple tasks at once without blocking the main thread. It is crucial for improving performance, especially in web applications, where operations such as network requests, file reading, or timers are common.

![Async vs Sync](img/sync-vs-async.png)


Why Asynchrony is Important

1. **Improved Performance**: By handling tasks concurrently, the application remains responsive and can perform multiple operations efficiently.
2. **Better User Experience**: Users don't have to wait for long-running tasks to complete before interacting with the application.
3. **Non-blocking Operations**: Critical for network requests, file reading, and other I/O operations where waiting would otherwise halt the execution of subsequent code.

#### Common Asynchronous Patterns

1. **Callbacks**: Functions passed as arguments to other functions to be executed later. Can lead to "callback hell" when dealing with multiple nested callbacks.

2. **[Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)**:
   
      - Objects representing the eventual completion or failure of an asynchronous operation.
      - Provide methods like then and catch for handling success and error cases.

3. **[Async/Await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)**

      - Syntactic sugar built on top of Promises, providing a more readable and concise way to write asynchronous code.
      - Requires the use of the async keyword to define a function that uses await for asynchronous operations.

### 1.3 **Methods to Make Ajax Requests in JS**

#### [XMLHttpRequest Object](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest_API)
- **Description**: A classic method for making HTTP requests. Initially developed in 2006, it is still in use today. It originally had compatibility issues with Internet Explorer, which used a different name for this object.
- **Usage**: While it's older and considered more cumbersome, `XMLHttpRequest` is still functional and supported across all browsers.

#### [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
- **Description**: A more modern, powerful, flexible, and easier-to-use method for making HTTP requests.
- **Usage**: The Fetch API is now the preferred way to make HTTP requests due to its simplicity and built-in promise-based architecture.

#### Other Methods
- **[Axios](https://axios-http.com/docs/intro)**: A promise-based HTTP client for the browser and Node.js. It is popular for its ease of use and ability to handle requests and responses as JSON.
- **[jQuery](https://jquery.com/)**: A fast, small, and feature-rich JavaScript library. jQuery provides a simple [`$.ajax`](https://api.jquery.com/Jquery.ajax/) method for making Ajax requests, which simplifies the process. The jQuery library and its `$.ajax()` method had their moment of glory by facilitating things during the times of `XMLHttpRequest` and the old Microsoft IE.


## 2. **REST API**

A REST API (Representational State Transfer Application Programming Interface) is a set of rules and conventions for building and interacting with web services. REST APIs allow different systems to **communicate over HTTP** using the standard methods we have seen in the previous point, making it easier to integrate and interact with web applications and services.

#### Key Components
- **Endpoint:** A specific **URL** where the API can be accessed.
- **Method:** The type of request being made (e.g., GET, POST, PUT, DELETE, PATCH).
- **Request:** The data or action you want to send to the server. In the request are included the **headers** and the **body** if necessary. 
- **Response:** The data sent back from the server after processing the request.


![REST-API](img/rest-api.png)

### 2.1 **Backend Tools to construct REST API**

We can construct a REST API: With any server-side language:

  - PHP
  - Java
  - Rubi
  - Python
  - NODE.js 
  - ASP.NET

For constructing an API, you'll often use a server-side framework. Some popular options are:

- **Node.js with [Express](https://expressjs.com/) (JavaScript)**
- **[Django](https://docs.djangoproject.com/en/dev/internals/contributing/writing-code/javascript/) (Python)**
- **[FastAPI](https://fastapi.tiangolo.com/) (Python)**
- **[Ruby on Rails](https://rubyonrails.org/) (Ruby)**
- **[Spring Boot](https://stackabuse.com/build-a-spring-boot-rest-api-with-java-full-guide/) (Java)**


![js meme](img/js-meme.jpg)

But this is a Frontend subject, so we are going to use public REST API and toy REST API constructed with `json-server`.

### 2.2 **Public REST API**

Public REST APIs provide developers with access to a variety of services, data, and functionalities from different providers. Here is a list of some commonly used public REST APIs:

##### Social Media and Communication

1. **Twitter API**
      - **Description:** Allows developers to interact with Twitter data.
      - **Documentation:** [Twitter API Docs](https://developer.twitter.com/en/docs)

2. **Facebook Graph API**
      - **Description:** Provides access to Facebook's social graph data.
      - **Documentation:** [Facebook Graph API Docs](https://developers.facebook.com/docs/graph-api/)

3. **Slack API**
      - **Description:** Enables integration with Slack for messaging and collaboration.
      - **Documentation:** [Slack API Docs](https://api.slack.com/)

##### Maps and Geolocation

4. **Google Maps API**
      - **Description:** Offers a wide range of maps-related services, including geolocation, routing, and place information.
      - **Documentation:** [Google Maps API Docs](https://developers.google.com/maps/documentation)

5. **OpenWeatherMap API**
      - **Description:** Provides weather data, forecasts, and historical information.
      - **Documentation:** [OpenWeatherMap API Docs](https://openweathermap.org/api)

6. **Mapbox API**
      - **Description:** Offers customizable maps and geolocation services.
      - **Documentation:** [Mapbox API Docs](https://docs.mapbox.com/api/)

##### Finance and Cryptocurrency

7. **CoinGecko API**
      - **Description:** Provides data on cryptocurrencies, including prices, market capitalization, and trading volume.
      - **Documentation:** [CoinGecko API Docs](https://www.coingecko.com/en/api)

8. **Alpha Vantage API**
      - **Description:** Offers financial data, including stock prices, technical indicators, and forex data.
      - **Documentation:** [Alpha Vantage API Docs](https://www.alphavantage.co/documentation/)

##### Entertainment

9. **Spotify API**
      - **Description:** Allows access to Spotify's music catalog and user data.
      - **Documentation:** [Spotify API Docs](https://developer.spotify.com/documentation/web-api/)

10. **The Movie Database (TMDb) API**
    - **Description:** Provides information about movies, TV shows, and actors.
    - **Documentation:** [TMDb API Docs](https://developers.themoviedb.org/3)

11. **YouTube Data API**
    - **Description:** Allows access to YouTube content and user data.
    - **Documentation:** [YouTube Data API Docs](https://developers.google.com/youtube/v3)

##### Utility and Miscellaneous

12. **GitHub API**
    - **Description:** Provides access to GitHub repositories, issues, and user data.
    - **Documentation:** [GitHub API Docs](https://docs.github.com/en/rest)

13. **REST Countries API**
    - **Description:** Offers information about countries, including population, area, and capital cities.
    - **Documentation:** [REST Countries API Docs](https://restcountries.com/)

14. **NASA API**
    - **Description:** Provides access to a wide range of NASA data, including images, videos, and planetary information.
    - **Documentation:** [NASA API Docs](https://api.nasa.gov/)

15. **Random User API**
    - **Description:** Generates random user data, including names, addresses, and profile pictures.
    - **Documentation:** [Random User API Docs](https://randomuser.me/)

16. **Open Library API**
    - **Description:** Provides access to book data from the Open Library project.
    - **Documentation:** [Open Library API Docs](https://openlibrary.org/developers/api)

17. **PokeAPI**
    - **Description:** Offers data from the Pokémon universe, including Pokémon, abilities, and moves.
    - **Documentation:** [PokeAPI Docs](https://pokeapi.co/docs/)

> #### <i class="fa-solid fa-circle-check"></i> Check this!! 
> [Much more public REST API](https://github.com/public-apis/public-apis)


<div class="exercise-box">
  <h3><i class="fas fa-laptop-code"></i> Hands-On Exercise 1: Creating a .rest File for a public REST API</h3>
  <p>In this exercise, you will create a `.rest` file using the REST Client extension for Visual Studio Code. You will explore a free public REST API for Pokémon data. The file should contain at least 5 different endpoints.</p>
  <p>Follow these steps:</p>
  <ol>
    <li>Install the REST Client extension for Visual Studio Code if you haven't already.</li>
    <li>Choose a free access REST API.</li>
    <li>Create a new file named `your-chosen-api.rest` in your project directory.</li>
    <li>Add five different endpoints to your `your-chosen-api.rest` file:</li>
    <li>Test the endpoints.</li>
  </ol>
</div>



### 2.3 **JSON server**

[JSON Server](https://www.npmjs.com/package/json-server) is a powerful tool that allows developers to create a full fake REST API with minimal effort. It's especially useful for frontend developers who need a quick and easy way to simulate a backend server without setting up a full server environment. With JSON Server, you can quickly create a mock API, test your frontend code, and prototype applications without needing a real backend.

#### Key Features

- **Zero Coding Required:** Create a full API from a simple JSON file.
- **Extremely Fast Setup:** Get a mock API running in minutes.
- **RESTful Routes:** Automatically generates RESTful routes based on your data.
- **CRUD Operations:** Supports Create, Read, Update, and Delete operations.
- **Custom Routes:** Allows you to define custom routes and add middleware for more complex setups.
- **Static File Serving:** Can serve static files alongside the API, useful for serving your frontend application.

<div class="exercise-box">
  <h3><i class="fas fa-laptop-code"></i> Hands-On Exercise: Creating a Fake API with JSON Server</h3>
  <p>In this exercise, you will create a fake REST API using JSON Server. This will help you understand how to mock a backend for your frontend development. Follow the steps below to set up and run your fake API:</p>

  <h4>Steps to Create a Fake API</h4>

  <ol>
    <li>
      <strong>Install JSON Server:</strong>
      <p>First, ensure you have Node.js installed. Then, install JSON Server globally using npm.</p>
      <pre><code>npm install -g json-server</code></pre>
    </li>
    <li>
      <strong>Create a <code>db.json</code> File:</strong>
      <p>In your project directory, create a file named <code>db.json</code>. This file will contain your fake data. Below is an example structure for a simple API:</p>
      <pre><code>{
  "posts": [
    { "id": 1, "title": "Hello World", "author": "John Doe" },
    { "id": 2, "title": "Learning JSON Server", "author": "Jane Doe" }
  ],
  "comments": [
    { "id": 1, "postId": 1, "body": "Great post!" },
    { "id": 2, "postId": 2, "body": "Very informative." }
  ],
  "profile": { "name": "John Doe" }
}</code></pre>
    </li>
    <li>
      <strong>Start JSON Server:</strong>
      <p>Run the JSON Server with the <code>db.json</code> file you created.</p>
      <pre><code>npx json-server db.json</code></pre>
    </li>
    <li>
      <strong>Access Your Fake API:</strong>
      <p>Once JSON Server is running, you can access your fake API at <code>http://localhost:3000</code>. Here are some example endpoints based on the <code>db.json</code> file:</p>
      <ul>
        <li><code>GET /posts</code> - List all posts</li>
        <li><code>GET /posts/1</code> - Get a specific post by ID</li>
        <li><code>POST /posts</code> - Create a new post</li>
        <li><code>PUT /posts/1</code> - Update a post by ID</li>
        <li><code>DELETE /posts/1</code> - Delete a post by ID</li>
        <li><code>GET /comments</code> - List all comments</li>
        <li><code>GET /profile</code> - Get the profile</li>
      </ul>
    </li>
    <li>
      <strong>Make Requests to Your Fake API:</strong>
      <p>Use tools like Postman, cURL, or the REST Client extension in Visual Studio Code to make requests to your fake API endpoints and observe the responses.</p>
    </li>
  </ol>
  <p>Experiment with different data structures and endpoints to get a feel for how JSON Server works. This is a powerful tool for quickly setting up a mock backend to aid in frontend development.</p>
</div>


## 3. **Different Solutions to Check Your REST API**

When developing and testing REST APIs, it's essential to have tools that can help you make requests to your endpoints and inspect the responses. 

We can just paste the endpoint URL in the address bar of the browser when we have a simple GET request.

Try pasting this in your browser:

```
https://pokeapi.co/api/v2/pokemon/ditto
```

We can improve the JSON response shown in the browser with some plugin for Chrome as [JSON Viewer](https://chromewebstore.google.com/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh)

Also we can use the command [curl](https://linuxize.com/post/curl-rest-api/) to test and endpoint in the command line. 

But when we have more complicated request, also POST with more complex payloads and headers, we will prefer to use a more 

Here are three popular solutions:

### 3.1 **Postman**

#### Overview
Postman is a comprehensive API development environment that allows you to create, share, test, and document APIs. It has a user-friendly interface and offers a wide range of features.

#### Key Features
- **Collections:** Organize your API requests into collections for better management and collaboration.
- **Environment Variables:** Easily switch between different environments (e.g., development, staging, production) using variables.
- **Automated Testing:** Create test scripts using JavaScript to automate API testing.
- **Mock Servers:** Simulate API endpoints for testing purposes without needing the actual server.
- **Collaboration:** Share collections and workspaces with team members for better collaboration.

![Postman](img/postman.png)

#### Example Usage
1. Create a new request.
2. Set the HTTP method (GET, POST, PUT, DELETE, etc.).
3. Enter the API endpoint URL.
4. Add headers, query parameters, and request body if needed.
5. Click the "Send" button to make the request and inspect the response.

#### Download
[Download Postman](https://www.postman.com/downloads/)

### 3.2 **Thunder Client**

#### Overview
Thunder Client is a lightweight REST API client extension for Visual Studio Code (VSCode). It's designed to be simple and easy to use within the VSCode environment.

#### Key Features
- **Integrated with VSCode:** No need to switch between applications; use it directly within your code editor.
- **Environment Variables:** Manage environment variables to switch between different setups easily.
- **Collections:** Organize your requests into collections for better structure.
- **Quick Tests:** Basic testing capabilities to validate your API responses.
- **Lightweight:** Minimalist design with essential features for quick and efficient API testing.

#### Example Usage
1. Install the Thunder Client extension in VSCode.
2. Open the Thunder Client panel from the sidebar.
3. Create a new request and set the HTTP method.
4. Enter the API endpoint URL.
5. Add headers, query parameters, and request body if needed.
6. Click the "Send" button to make the request and view the response.

![thunder client](img/thunder-client.png)

#### Download
[Download Thunder Client](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client)

### 3.3 **REST Client**

#### Overview
REST Client is another VSCode extension that allows you to send HTTP requests and view the responses directly in your code editor. It's ideal for those who prefer a more code-centric approach.

#### Key Features
- **Request Files:** Write your requests in `.http` or `.rest` files for better organization and version control.
- **Environment Variables:** Use environment variables to manage different settings for your API requests.
- **Inline Documentation:** Document your requests inline with your code for better readability.
- **Support for Various HTTP Methods:** Easily send GET, POST, PUT, DELETE, and other types of HTTP requests.

#### Example Usage
  1. Install the REST Client extension in VSCode.
  2. Create a new `.http` or `.rest` file.
  3. Write your request, e.g.:

  ```http
  GET https://example.com/comments/1 HTTP/1.1

  ###

  GET https://example.com/topics/1 HTTP/1.1

  ###

  POST https://example.com/comments HTTP/1.1
  content-type: application/json
  {
      "name": "sample",
      "time": "Wed, 21 Oct 2015 18:27:50 GMT"
  }
  ```
  4. Click the "Send Request" link above the request to execute it and view the response in a split panel4ew3.

![REST client](img/rest-client.png)

#### Download
[Download REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)

## 4. **XMLHttpRequest**

We are not going to use this older way, but we can see this little example to understand it.

```js
// Create a new XMLHttpRequest object
var xhr = new XMLHttpRequest();

// Configure it: GET-request for the URL /users
xhr.open('GET', 'https://jsonplaceholder.typicode.com/users', true);

// Set up a function to handle the response
xhr.addEventListener("load", function () {
  if (xhr.status >= 200 && xhr.status < 300) {
    // Parse the JSON response
    var users = JSON.parse(xhr.responseText);

    // Log the response to the console
    console.log(users);

    // Display the response in the <pre> element
    document.getElementById('responseOutput').textContent = JSON.stringify(users, null, 2);
  } else {
    console.error('Request failed. Returned status of ' + xhr.status);
  }
});

// Handle network errors
xhr.addEventListener("error", function () {
  console.error('Request failed.');
})

// Send the request
xhr.send();
```

## 5. **Fetch API**

In modern web development, Fetch simplifies and enhances many aspects of AJAX connections. It is now compatible with most browsers, making it a preferred choice for handling asynchronous requests.

#### Key Methods to Handle Asynchrony with Fetch:
1. **Promises**
2. **async / await**
   
##### [--> Link to Fetch in msn](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)

### 5.1 **Fetch with Promises**

Fetch API uses [Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) to handle asynchronous operations. Here's a basic example of how to use Fetch with Promises:

```js
// This is a GET request with promises
fetch('https://jsonplaceholder.typicode.com/posts/1')
  .then(response => {
    // parse the json response
    response => response.json()
  })
  .then(data => {
      // Do something with data
      document.getElementById('output').innerText = JSON.stringify(data);
  })
  .catch(error => console.error('Error:', error));
```

### 5.2 **Fetch with Async/Await**

The [async/await](#52-fetch-with-asyncawait) syntax provides a cleaner and more readable way to handle asynchronous operations. 
It's important to note that `await` can only be used inside an `async` function. Here's how to use Fetch with async/await:

```js
// this is a GET request with async/await
async function fetchData() {
    try {
        const response = await fetch('https://jsonplaceholder.typicode.com/posts/1');
        // parse the json response
        const data = await response.json();
        // do something with data
        console.log(data);
        return data;
    } catch (error) {
        console.error('Error:', error);
    }
}
```

### 5.3 **Handling HTTP Responses**

The `Response` object in the Fetch API provides several methods to handle and format HTTP responses. Each of these methods returns a promise that resolves to different types of data.

- `response.json()`: Returns a promise resolved to a JSON object.
- `response.text()`: Returns a promise resolved to raw text.
- `response.formData()`: Returns a promise resolved to `formData`.
- `response.blob()`: Returns a promise resolved to a `Blob` (a file-like object of binary aw data).


#### `response.json()`

That's the one that we will be using most of the times, because JSON is the most common format that the API's out there serves us data.

- Returns a promise resolved to a JSON object.
- Useful for handling responses containing JSON data.
  
```javascript
fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

#### Connection Status Information

The `Response` object also provides information about the status of the connection:

#### `response.status`

- Returns the status code of the response.
- Typical values include:
    - `100-199`: Informational responses.
    - `200-299`: Successful responses.
          - `200`: OK.
    - `300-399`:Redirection messages
    - `400-499`: Client error response.
          - `404`: Not Found.
    - `500-599`: Server error responses.
          - `500`: Internal Server Error. 
    - [All HTTP Response Status Codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
```js
fetch('https://api.example.com/data')
    .then(response => {
        console.log(response.status); // e.g., 200, 404, 500
        return response.json();
    })
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

#### `response.ok`

- Returns a boolean indicating whether the response was successful (status in the range 200-299).

      ```js
      fetch('https://api.example.com/data')
          .then(response => {
              if (response.ok) {
                  return response.json();
              } else {
                  throw new Error('Network response was not ok');
              }
          })
          .then(data => console.log(data))
          .catch(error => console.error('Error:', error));
      ```

### 5.3 **GET, POST, PUT, PATCH, DELETE Requests**

As you could see, if you don't specify a method, the default method is GET. In the previous examples we have created GET requests. You can see we have not defined `method`, `body`or `headers`into fetch options.

When dealing with POST, PUT and PATCH requests, we need to include `method`, `body` and  `headers` as fetch options.

#### GET Requests:

- For GET requests, we typically do not need to include a Content-Type header. GET requests do not have a body, so there's no content type to specify.
- However we can send some data as params when the API endpoint allows it. 
- But maybe we could need to include some information in the header as `'Authorization'` in the cases is required.

Example:

```js
// GET simple request example
fetch('https://api.example.com/get-images?query=cats&limit=20')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));

// GET Authorization required
fetch('https://api.example.com/get-images?query=cats&limit=20', {
  headers: {
        'Authorization': 'Bearer your-api-key'
    },
})
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```


#### POST, PUT, PATCH Request:

For these types of requests that create or modify a resource, we do need to send a `body`. It  will be necessary to include:

- `Content-Type` header to specify the media type of content
      - Common values for the Content-Type header include `application/json`, `application/x-www-form-urlencoded`, `multipart/form-data`, etc.
- `method`:
      - `'POST'`
      - `'PUT'`
      - `'PATCH`
- `body`: Most of the times, when `Content-Type` is JSON we have to 'stringify' some data object:
      - `body: JSON.stringify(data)`

Examples:
```js
const BASE_URL = 'https://api.example.com';
const API_KEY = 'your-api-key';

// Function to handle POST requests
export async function postData(endpoint, body) {
    try {
        const response = await fetch(`${BASE_URL}${endpoint}`, {
            method: 'POST',
            headers: {
                'Authorization': `Bearer ${API_KEY}`,
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(body)
        });
        if (!response.ok) {
            throw new Error(`Error: ${response.statusText}`);
        }
        const data = await response.json();
        return data;
    } catch (error) {
        console.error('Post Data Error:', error);
        throw error;
    }
}

// Function to handle PUT requests
export async function putData(endpoint, body) {
    try {
        const response = await fetch(`${BASE_URL}${endpoint}`, {
            method: 'PUT',
            headers: {
                'Authorization': `Bearer ${API_KEY}`,
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(body)
        });
        if (!response.ok) {
            throw new Error(`Error: ${response.statusText}`);
        }
        const data = await response.json();
        return data;
    } catch (error) {
        console.error('Put Data Error:', error);
        throw error;
    }
}
```


#### DELETE Requests

  - The DELETE method is used to delete a resource identified by a URL. Like the GET method, the DELETE method typically doesn't need a body, and thus it usually doesn't require a `Content-Type` header. However, there are some scenarios where you might need to include a body with a DELETE request and also could be neccessary to include some information in the header as `'Authorization'`.

Example:
```js
// Simple delete function without options
export async function simpleDeleteData(endpoint) {
    try {
        const response = await fetch(`${BASE_URL}${endpoint}`, {
          method: 'DELETE'
        });
        if (!response.ok) {
            throw new Error(`Error: ${response.statusText}`);
        }
        const data = await response.json();
        return data;
    } catch (error) {
        console.error('Delete Data Error:', error);
        throw error;
    }
}

// mode advanced, with some options
export async function deleteData(endpoint, body = null) {
    try {
        const options = {
            method: 'DELETE',
            headers: {
                'Authorization': `Bearer ${API_KEY}`
            }
        };
        // asking for a body. In case there is body we stringify it 
        if (body) {
            options.headers['Content-Type'] = 'application/json';
            options.body = JSON.stringify(body);
        }
        const response = await fetch(`${BASE_URL}${endpoint}`, options);
        if (!response.ok) {
            throw new Error(`Error: ${response.statusText}`);
        }
        const data = await response.json();
        return data;
    } catch (error) {
        console.error('Delete Data Error:', error);
        throw error;
    }
}
```



### 5.4 **Encapsule fetch requests in reusable modules**

It is always a good practice to encapsule the `fetch` requests to our API in a separate js module that we can import in the main module. For that purpose we have to use [Ecma Script Modules](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules) (ESM)

1. Import the Main Script as a Module

      ```html
      <script src="your-main.js" type="module"></script>
      ```

2. Create the `your-api.js` Module

      Create a separate JavaScript file named `your-api.js` that will encapsulate all the logic for accessing the API. This module will contain constants, such as the base URL and API keys, and functions for making API requests.

      ```js
      // your-api.js

      const BASE_URL = 'https://api.example.com';
      const API_KEY = 'your-api-key';

      // Function to handle GET requests
      export async function fetchData(endpoint) {
          try {
              const response = await fetch(`${BASE_URL}${endpoint}`, {
                  headers: {
                      'Authorization': `Bearer ${API_KEY}`,
                      'Content-Type': 'application/json'
                  }
              });
              if (!response.ok) {
                  throw new Error(`Error: ${response.statusText}`);
              }
              const data = await response.json();
              return data;
          } catch (error) {
              console.error('Fetch Data Error:', error);
              throw error;
          }
      }

      // Function to handle POST requests
      export async function postData(endpoint, body) {
          try {
              const response = await fetch(`${BASE_URL}${endpoint}`, {
                  method: 'POST',
                  headers: {
                      'Authorization': `Bearer ${API_KEY}`,
                      'Content-Type': 'application/json'
                  },
                  body: JSON.stringify(body)
              });
              if (!response.ok) {
                  throw new Error(`Error: ${response.statusText}`);
              }
              const data = await response.json();
              return data;
          } catch (error) {
              console.error('Post Data Error:', error);
              throw error;
          }
      }

      // Other API-related functions can be added here

      ```

3. Import and Use the API Module in the Main Script
   
      In your main JavaScript file, `your-main.js`, import the functions from the `your-api.js` module and use them to make API requests.

      ```js
      // your-main.js
      import { fetchData, postData } from './your-api.js';

      async function main() {
          try {
              // Example of making a GET request
              const data = await fetchData('/some-endpoint');
              console.log('Fetched Data:', data);

              // Example of making a POST request
              const postDataBody = { key: 'value' };
              const postDataResponse = await postData('/some-endpoint', postDataBody);
              console.log('Posted Data:', postDataResponse);
          } catch (error) {
              console.error('Main Function Error:', error);
          }
      }

      // Run the main function
      main();

      ```

<div class="important-box">
<h3><i class="fa-solid fa-circle-exclamation"></i></i>IMPORTANT</h3>
<p>From now in advance it is MANDATORY to encapsule the fetch functions of each API that we are accessing in our project in a separate module.</p>
</div>

