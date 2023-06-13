# Express Request

| Term | Definition |
| ---- | ---------- |
| __Environmental Variables__ | Variables that are part of the environment in which a program runs. They can be used to store configuration settings, API keys, and other sensitive information. |
| __.env__ | A file used to store environment variables, typically not tracked in version control. |
| __dotenv__ | A package that loads environment variables from a .env file into process.env. |
| __Separating Concerns__ | A design principle that states that code should be separated into distinct sections, each handling a specific task. |
| __Order of Routes__ | The sequence in which routes are defined, and how Express matches incoming requests to routes based on their order. |
| __Data modeling__ | A technique for defining business requirements for a database. |
| __Models__ | A folder or component that represents the data structure and logic of an application. |

---

## JavaScript Environments

```bash
# Create an .env file
touch .env

# Install dotenv
npm install dotenv
```

```js
// .env
PORT=3333
```

- What is the purpose of using an environment variable in a Node.js application?
- How can environment variables be defined and accessed in a Node.js application?
- Explain the role of the `.env` file in the context of environment variables. What information is typically stored in this file?
- Why is the `dotenv` package used in Node.js applications? What problem does it solve?
- How can the `dotenv` package be installed and utilized in a Node.js project?
- In the provided `.env` file, what is the significance of `PORT=3333`? How does it relate to configuring the server?
- Describe the process of accessing the value of an environment variable stored in the `.env` file within your code.
- Explain the benefits of using environment variables for configuration rather than hardcoding values directly in the code.
- What are the potential security implications of using environment variables? How does it help protect sensitive information?

---

## Separating Concerns

```js
// app.js
// --------------------------

// DEPENDENCIES
const express = require("express");

// CONFIGURATION
const app = express();

// ROUTES
app.get("/", (req, res) => {
  res.send("Welcome to Express Minerals App");
});

// EXPORT
module.exports = app;
```

```js
// server.js
// --------------------------

// DEPENDENCIES
const app = require("./app.js");

// CONFIGURATION
require("dotenv").config();
const PORT = process.env.PORT;

// LISTEN
app.listen(PORT, () => {
  console.log(`🪨 Listening on port ${PORT} 💎 `);
});
```

- Why is the express dependency necessary in the app.js file? What role does it play in building an Express application?
- How is the app object configured in the `app.js` file? What does it represent in the context of an Express application?
- Explain the purpose of the `route` defined as `app.get("/", ...)`. What response will be sent when this route is accessed?
- In the `app.js` file, what does the statement `module.exports = app` accomplish? How does it relate to the overall structure of an Express application?
- Describe the purpose of requiring the `app.js` file in the `server.js` file. How does it contribute to the organization of the application?
- What is the role of the `dotenv` package in the `server.js` file? How does it help with environment configuration?
- In the `server.js` file, what value does `process.env.PORT` retrieve? How is it used in the context of starting the server?
- Explain the significance of the `app.listen()` function in the `server.js` file. What does it do and how does it enable the server to handle incoming requests?
- What output will be printed to the console by the statement `console.log(🪨 Listening on port ${PORT} 💎 )` in the `server.js` file? Why is this message relevant?

---

## Data Modeling

```js
// models/rock.js
// --------------------------

module.exports = [
  "Crocoite",
  "Wulfenite",
  "Amber",
  "Malachite",
  "Azurite",
  "Amethyst",
];

```

- In the provided code snippet, what is the purpose of exporting an array of strings from the `rock.js` module?
- How can the exported array of rocks be accessed and used in other parts of the application?
- In the context of the application, what is the significance of having a separate module for defining and exporting the list of rocks?
- What advantages does separating the rock data into a separate module provide in terms of code organization and reusability?
- Suppose you want to add a new rock named "Jasper" to the existing array. How would you modify the `rock.js` module to include this new rock?
- In a different file of the application, what code would you use to import and use the array of rocks from the `rock.js` module?
- How would you modify the exported array in the `rock.js` module if you wanted to change the order of the rocks or remove some of them?
- Discuss the benefits of using modules and exports in Node.js applications and how they contribute to a modular and maintainable codebase.
- Can the exported array in the `rock.js` module contain elements other than strings? Explain your answer with an example.

## App Setup to Show All Rocks

```js
// app.js
// --------------------------

// DEPENDENCIES
const express = require("express");
const rocks = require("./models/rock.js");

// CONFIGURATION
const app = express();

// ROUTES
app.get("/", (req, res) => {
  res.send("Welcome to Express Minerals App");
});

app.get("/rocks", (req, res) => {
  res.send(rocks);
});

module.exports = app;
```

- In the provided code snippet, what is the purpose of the `express` module and why is it required?
- How is the `rock.js` module imported and used in the `app.js` file?
- What response will be sent when a GET request is made to the root route ("/") of the application?
- When a GET request is made to the "/rocks" route, what will be sent as the response?
- Explain how the `rocks` variable is populated with data and why it is available in the `app.js` file.
- Suppose you want to change the response sent for the root route ("/") to a different message. What modifications would you make in the `app.js` file?
- What happens if a request is made to a route that hasn't been defined in the provided code snippet?
- Discuss the role of routes in an Express application and how they handle different incoming requests.
- How would you modify the code to send an HTML response with a styled page instead of a plain text response?

## Showing each rock

```js
// ROUTES
app.get("/rocks/:index", (req, res) => {
  const { index } = req.params;
  res.send(rocks[index]);
});
```

- What type of HTTP request does the defined route (`/rocks/:index`) handle?
- What does the `:index` represent in the defined route?
- How is the `index` value extracted from the request parameters using `req.params`?
- What will be sent as the response when a request is made to the route `/rocks/2`?
- If the `index` value is not a valid index in the `rocks` array, what will be sent as the response?
- How would you modify the code to handle a different parameter name instead of `index` in the route?
- Explain how the code ensures that the response includes the correct rock based on the provided index.
- Can you provide an example of a valid request that would trigger this route and retrieve a specific rock from the `rocks` array?
- Discuss the significance of using route parameters in the context of dynamic data retrieval and manipulation.

## A Common Error

```js
// WRONG
// --------------------------
app.get("/rocks/oops/:index", (req, res) => {
  const { index } = req.params;
  res.send(rocks[index]);
  // error cannot send more than one response!
  res.send("this is the index: " + index);
});
```

```js
// RIGHT
// --------------------------
app.get("/rocks/:index", (req, res) => {
  const { index } = req.params;
  if (rocks[index]) {
    res.send(rocks[index]);
  } else {
    res.send("cannot find any rocks at this index: " + index);
  }
});
```

- What is the common error in the "WRONG" code snippet, and why does it occur?
- Explain why sending multiple responses in a single request is considered an error in Express.
- In the "RIGHT" code snippet, how does the code handle the case when the requested `index` is not valid?
- What will be sent as the response if the requested `index` exists in the `rocks` array in the "RIGHT" code snippet?
- Describe the significance of using conditional logic (`if` statement) in the "RIGHT" code snippet.
- How does the "RIGHT" code snippet provide a more robust error handling approach compared to the "WRONG" code snippet?
- Can you identify any potential improvements or alternative error handling strategies for the "RIGHT" code snippet?
- Explain why it's important to handle errors and provide meaningful responses in web applications.
- Discuss the benefits of using dynamic route parameters to retrieve and process data in web applications.
- Compare and contrast the error handling approaches in the "RIGHT" and "WRONG" code snippets, highlighting the advantages and disadvantages of each.

## Place routes in the correct order

```js
// WRONG
// --------------------------
app.get("/rocks/:index", (req, res) => {
  //:index can be anything, even awesome
  res.send(rocks[req.params.index]);
});

app.get("/rocks/awesome", (req, res) => {
  //this will never be reached
  res.send(`
 <h1>Rocks are awesome!</h1>
 <img src="https://tinyurl.com/2s7emynd" />
 `);
});
```

```js
// RIGHT
// --------------------------
app.get("/rocks/awesome", (req, res) => {
  res.send(`
 <h1>rocks are awesome!</h1>
 <img src="https://tinyurl.com/2s7emynd" />
 `);
});

app.get("/rocks/:index", (req, res) => {
  const { index } = req.params;
  if (rocks[index]) {
    res.send(rocks[index]);
  } else {
    res.send("cannot find anything at this index: " + index);
  }
});
```

- In the "WRONG" code snippet, explain why the `/rocks/awesome` route will never be reached.
- Describe the consequence of placing routes in the wrong order in an Express application.
- What is the purpose of the `/rocks/awesome` route in the "RIGHT" code snippet?
- How does the "RIGHT" code snippet ensure that the `/rocks/awesome` route is reachable and returns the expected response?
- In the "RIGHT" code snippet, what response will be sent if the requested `index` in the `/rocks/:index` route does not exist in the `rocks` array?
- Explain the significance of properly ordering routes in an Express application and its impact on the flow of request handling.
- Discuss the potential issues that can arise if routes are not organized in the correct order in a web application.
- Can you think of scenarios where the order of routes might be intentionally modified to achieve specific behavior in an Express application?
- How does the "RIGHT" code snippet demonstrate good coding practices and adherence to the principle of handling routes in the correct order?
- Reflect on the importance of route organization and order in terms of maintainability and scalability of an Express application.

## Multiple Parameters

```js
app.get("/hello/:firstName/:lastName", (req, res) => {
  console.log(req.params);
  const { firstName, lastName } = req.params;
  res.send(`hello ${firstName} ${req.params.lastName}`);
});
```

- Describe the purpose of the `/hello/:firstName/:lastName` route in the given code snippet.
- What are the placeholders `:firstName` and `:lastName` referred to in the route?
- How does the code extract the values of `:firstName` and `:lastName` from the URL?
- What is the purpose of the `console.log(req.params)` statement in the code snippet?
- How does the code construct and send the response message using the extracted `firstName` and `lastName` values?
- Discuss the potential use cases where multiple parameters in a route can be beneficial in an Express application.
- Can you think of alternative ways to achieve a similar result without using multiple parameters in the route?
- Explain the significance of parameter extraction and utilization in building dynamic routes and personalized responses.
- What happens if a request is made to the `/hello` route without providing values for `:firstName` and `:lastName`?
- Reflect on the advantages and challenges of handling routes with multiple parameters and the impact it has on the flexibility and functionality of an Express application.

## Query Strings

```js
// Basic Example
app.get("/calculator/:operator", (req, res) => {
  console.log("This is req.params", req.params);
  console.log("This is req.query", req.query);
  const sum = req.query.num1 + req.query.num2;
  res.send("sum is " + sum);
});
```

```js
// Code cleaned up
app.get("/calculator/:operator", (req, res) => {
  const { num1, num2 } = req.query;
  const sum = Number(num1) + Number(num2);
  res.send("sum is " + sum);
});
```

```js
// Even more logic
app.get("/calculator/:operator", (req, res) => {
  const { num1, num2 } = req.query;
  let sum = 0;
  if ((req.params.operator === "add")) {
    sum = Number(num1) + Number(num2);
  }
  res.send("sum is " + sum);
});
```

- What is the purpose of the `/calculator/:operator` route in the given code snippets?
- Explain the concept of query strings and their role in the Express application.
- How are query strings accessed and extracted from the URL in Express?
- What is the significance of the `console.log("This is req.query", req.query)` statement in the code snippet?
- In the cleaned-up version of the code, how does it ensure that the `num1` and `num2` values from the query string are treated as numbers?
- Describe the difference in behavior between the basic example and the cleaned-up version when handling the `num1` and `num2` values.
- In the third code snippet with additional logic, how does it determine whether to perform the addition operation based on the value of `req.params.operator`?
- What happens if the `req.params.operator` value is not "add" in the third code snippet?
- Discuss the benefits and potential limitations of using query strings for passing parameters in a URL.
- Can you think of alternative approaches or techniques to handle operations such as addition in an Express application without using query strings?

## Code Challenge

Figure out how to add the functionality of subtract, multiple, and divide to the calculator route. Put your __working__ solution in a code block below this paragraph.