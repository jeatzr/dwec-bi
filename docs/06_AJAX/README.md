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

### 5.1 **Fetch with Promises**

Fetch API uses [Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) to handle asynchronous operations. Here's a basic example of how to use Fetch with Promises:

```js
fetch('https://jsonplaceholder.typicode.com/posts/1')
  .then(response => response.json())
  .then(data => {
      document.getElementById('output').innerText = JSON.stringify(data);
  })
  .catch(error => console.error('Error:', error));
```

### 5.2 **Fetch with Async/Await**

The async/await syntax provides a cleaner and more readable way to handle asynchronous operations. 
It's important to note that `await` can only be used inside an `async` function. Here's how to use Fetch with async/await:

```js
async function fetchData() {
    try {
        const response = await fetch('https://jsonplaceholder.typicode.com/posts/1');
        const data = await response.json();
        console.log(data);
        document.getElementById('output').innerText = JSON.stringify(data,null,2);
    } catch (error) {
        console.error('Error:', error);
    }
}
```

