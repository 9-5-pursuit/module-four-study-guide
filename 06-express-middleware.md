# Express Middleware

| Term | Definition |
| ---- | ---------- |
| __Middleware__ | Middleware refers to functions that process and modify requests and responses in an Express application. They allow you to add additional functionality or perform tasks like logging, authentication, or error handling. |
| __Middleware Function__ | A middleware function is a function that takes in a request and a response object, and optionally a "next" function. It can perform tasks such as modifying the request or response, or passing control to the next middleware function in the chain. |
| __Middleware Stack__ | The middleware stack refers to the collection of middleware functions that are executed in a sequential manner. The order of middleware execution is determined by the order in which they are declared. |
| __Global Middleware__ | Global middleware refers to middleware functions that are executed for every incoming request. They are registered using `app.use()` without specifying a route. |
| __Route-specific Middleware__ | Route-specific middleware refers to middleware functions that are executed only for specific routes. They are registered using `app.METHOD()` (e.g., `app.get()`, `app.post()`) with the desired route and middleware function. |
| __Error Handling Middleware__ | Error handling middleware refers to middleware functions that are responsible for handling errors that occur during the request-response cycle. They are a special type of middleware that takes four arguments: `err`, `req`, `res`, and `next`. |
| __Third-party Middleware__ | Third-party middleware refers to middleware functions or modules that are developed and maintained by external parties (not part of the Express core). They provide additional functionality that can be easily integrated into an Express application, such as authentication, session management, compression, and more. |

---

## Table of Contents

- [Basic Middleware Creation and Usage](#basic-middleware-creation-and-usage)
- [Built-in Middleware](#built-in-middleware)
- [Route-specific Middleware](#route-specific-middleware)
- [Error Handling Middleware](#error-handling-middleware)
- [Third-party Middleware](#third-party-middleware)
- [Order of Middleware Execution](#order-of-middleware-execution)
- [Chaining Middleware](#chaining-middleware)

---

## Basic Middleware Creation and Usage

```js
const express = require('express');
const app = express();

// Custom middleware function
const logger = (req, res, next) => {
  console.log(`[${new Date().toISOString()}] ${req.method} ${req.url}`);
  next(); // Call next to pass control to the next middleware function
};

// Use the custom middleware
app.use(logger);

// Route handler
app.get('/', (req, res) => {
  res.send('Hello, world!');
});

// Start the server
app.listen(3000, () => {
  console.log('Server is listening on port 3000');
});
```

<details>
<summary><strong>How do you create a custom middleware function in Express?</strong></summary>

To create a custom middleware function in Express, you define a function that takes three arguments: `req`, `res`, and `next`. The `req` object represents the incoming request, the `res` object is the response that will be sent back to the client, and the `next` function is a callback that passes control to the next middleware function in the chain.

Example:
```js
const logger = (req, res, next) => {
    // Custom middleware logic here
    next(); // Call next to pass control to the next middleware function
};
```
</details>

<details>
<summary><strong>How do you use a custom middleware function in Express?</strong></summary>

To use a custom middleware function in Express, you use the `app.use()` method and pass the middleware function as an argument. This mounts the middleware function globally, meaning it will be executed for every incoming request.

Example:
```js
app.use(logger);
```
</details>

<details>
<summary><strong>What is the purpose of the <code>next</code> function in a middleware function?</strong></summary>

The `next` function in a middleware function is used to pass control to the next middleware function in the chain. By calling `next()`, you allow the application to proceed to the next middleware or route handler. If you don't call `next()`, the request will be left hanging and the client will not receive a response.

Example:
```js
const logger = (req, res, next) => {
    // Custom middleware logic here
    next(); // Call next to pass control to the next middleware function
};
```
</details>

---

## Built-in Middleware

```js
const express = require('express');
const app = express();

// Built-in middleware
app.use(express.json()); // Parse JSON bodies

// Route handler
app.post('/users', (req, res) => {
  console.log(req.body);
  res.send('User created');
});

// Start the server
app.listen(3000, () => {
  console.log('Server is listening on port 3000');
});
```

<details>
<summary><strong>What is built-in middleware?</strong></summary>

Built-in middleware refers to the middleware functions that are included with Express by default. They provide commonly used functionalities without the need for separate installations or additional setup.
</details>

<details>
<summary><strong>What is the purpose of the `express.json()` middleware?</strong></summary>

The `express.json()` middleware is a built-in middleware provided by Express. Its purpose is to parse JSON bodies in incoming requests. It examines the `Content-Type` header of the request and, if it is set to `application/json`, it parses the request body and makes it available on the `req.body` property.

Example:
```js
app.use(express.json());
```
</details>

---

## Route-specific Middleware

```js
const express = require('express');
const app = express();

// Global middleware
const globalMiddleware = (req, res, next) => {
  console.log('This is global middleware');
  next();
};

// Route-specific middleware
const routeMiddleware = (req, res, next) => {
  console.log('This is route-specific middleware');
  next();
};

// Global middleware
app.use(globalMiddleware);

// Route-specific middleware
app.get('/users', routeMiddleware, (req, res) => {
  res.send('Hello, world!');
});

// Start the server
app.listen(3000, () => {
  console.log('Server is listening on port 3000');
});
```

<details>
<summary><strong>What is the purpose of global middleware in Express?</strong></summary>

Global middleware in Express is used to handle requests globally, regardless of the specific route. It is registered using `app.use()` without specifying a route. Global middleware is executed for every incoming request and can be used for tasks such as logging, authentication, error handling, and more.
</details>

<details>
<summary><strong>How do you register global middleware in Express?</strong></summary>

To register global middleware in Express, you use the `app.use()` method without specifying a route. You pass the middleware function as an argument to `app.use()`.

Example:
```js
app.use(globalMiddleware);
```
</details>

<details>
<summary><strong>What is the purpose of route-specific middleware in Express?</strong></summary>

Route-specific middleware in Express is used to handle requests for specific routes only. It is registered using `app.METHOD()` (e.g., `app.get()`, `app.post()`) with the desired route and middleware function. Route-specific middleware is executed only for requests targeting the specified route and can be used for route-specific tasks or validations.
</details>

<details>
<summary><strong>How do you register route-specific middleware in Express?</strong></summary>

To register route-specific middleware in Express, you use the `app.METHOD()` method (e.g., `app.get()`, `app.post()`) with the desired route and middleware function. You pass the middleware function as an argument to the `app.METHOD()` method.

Example:
```js
app.get('/users', routeMiddleware, (req, res) => {
  // Route handler logic
});
```
</details>

---

## Error Handling Middleware

```js
const express = require('express');
const app = express();

// Custom middleware function
const errorHandler = (err, req, res, next) => {
  console.error(err);
  res.status(500).send('Something went wrong');
};

// Route handler
app.get('/users', (req, res) => {
  // Simulating an error
  throw new Error('Error occurred');
});

// Error handling middleware
app.use(errorHandler);

// Start the server
app.listen(3000, () => {
  console.log('Server is listening on port 3000');
});
```

<details>
<summary><strong>What is error handling middleware in Express?</strong></summary>

Error handling middleware in Express is responsible for handling errors that occur during the request-response cycle. It is a special type of middleware that takes four arguments: `err`, `req`, `res`, and `next`. It allows you to centralize error handling logic and provide consistent error responses to clients.
</details>

<details>
<summary><strong>How do you define error handling middleware in Express?</strong></summary>

To define error handling middleware in Express, you create a middleware function that takes four arguments: `err`, `req`, `res`, and `next`. The `err` parameter represents the error object, and `next` is a function to pass control to the next middleware. You can choose any name for the middleware function.

Example:
```js
const errorHandler = (err, req, res, next) => {
  // Error handling logic
};
```
</details>

<details>
<summary><strong>How do you register error handling middleware in Express?</strong></summary>

To register error handling middleware in Express, you use the `app.use()` method. Pass the error handling middleware function as an argument to `app.use()`.

Example:
```js
app.use(errorHandler);
```
</details>

<details>
<summary><strong>When does error handling middleware get executed in Express?</strong></summary>

Error handling middleware in Express gets executed when an error occurs during the request-response cycle. It is typically placed after all other middleware and route handlers in the middleware stack. When an error is encountered, Express will automatically skip regular middleware and pass control to the error handling middleware by calling `next(err)`, where `err` is the error object.
</details>

<details>
<summary><strong>What can you do in error handling middleware?</strong></summary>

In error handling middleware, you can perform various error handling tasks, such as logging the error, customizing the error response, redirecting to an error page, or sending an appropriate error status code and message to the client. You have access to the `err`, `req`, and `res` objects, allowing you to handle errors in a way that suits your application's needs.
</details>

---

## Third-party Middleware

In this example, we demonstrate the usage of the `helmet` middleware, which is a commonly used third-party middleware module for securing Express applications. The `helmet` middleware provides various security-related HTTP headers to enhance the security of the application.

```js
const express = require('express');
const helmet = require('helmet');
const app = express();

// Third-party middleware
app.use(helmet());

// Route handler
app.get('/', (req, res) => {
  res.send('Hello, world!');
});

// Start the server
app.listen(3000, () => {
  console.log('Server is listening on port 3000');
});
```

<details>
<summary><strong>What is third-party middleware in Express?</strong></summary>

Third-party middleware in Express refers to middleware functions or modules that are developed and maintained by external parties (not part of the Express core). These middleware modules provide additional functionality that can be easily integrated into an Express application, such as authentication, session management, compression, and more.
</details>

<details>
<summary><strong>How do you use third-party middleware in Express?</strong></summary>

To use third-party middleware in Express, you need to install the desired middleware module from the npm registry using a package manager like npm or yarn. Once installed, you can require the middleware module in your Express application and use it by invoking the corresponding function or attaching it using `app.use()`.

Example:
```js
const express = require('express');
const app = express();
const helmet = require('helmet');

app.use(helmet());
```
In this example, we install the `helmet` module, which provides security-related middleware for Express. We require the `helmet` module and use it as middleware by invoking `helmet()` and passing it to `app.use()`.
</details>

<details>
<summary><strong>What are some examples of commonly used third-party middleware in Express?</strong></summary>

There are numerous third-party middleware modules available for Express. Some examples of commonly used third-party middleware include:

- `body-parser`: Middleware for parsing request bodies, such as JSON, URL-encoded, or multipart data.
- `cors`: Middleware for handling Cross-Origin Resource Sharing (CORS) in Express.
- `cookie-parser`: Middleware for parsing and handling cookies in Express.
- `multer`: Middleware for handling file uploads in Express.
- `passport`: Authentication middleware for Express, providing various authentication strategies.
- `compression`: Middleware for compressing response bodies to reduce bandwidth usage.
- `morgan`: HTTP request logging middleware for Express.

These are just a few examples, and there are many more third-party middleware modules available to enhance and extend the functionality of your Express application.
</details>

<details>
<summary><strong>How do you install third-party middleware in an Express application?</strong></summary>

To install third-party middleware in an Express application, you use a package manager like npm or yarn. Open your terminal or command prompt, navigate to your project directory, and run the appropriate command to install the desired middleware module.

Example using npm:
```bash
npm install helmet
```

Example using yarn:
```bash
yarn add helmet
```

Replace `helmet` with the name of the specific middleware module you want to install.
</details>

---

## Order of Middleware Execution

In this example, we have global middleware and route-specific middleware declared in an Express application. The purpose is to showcase the order of middleware execution.

```js
const express = require('express');
const app = express();

// Global middleware 1
app.use((req, res, next) => {
  console.log('Global middleware 1');
  next();
});

// Route-specific middleware
app.get('/users', (req, res, next) => {
  console.log('Route-specific middleware');
  next();
});

// Global middleware 2
app.use((req, res, next) => {
  console.log('Global middleware 2');
  next();
});

// Route handler
app.get('/users', (req, res) => {
  res.send('Hello, world!');
});

// Start the server
app.listen(3000, () => {
  console.log('Server is listening on port 3000');
});
```

<details>
<summary><strong>What is the order of middleware execution in Express?</strong></summary>

The order of middleware execution in Express is based on their declaration order. The middleware functions are executed in a sequential manner, starting from the top-down. Global middleware, added using `app.use()`, is executed before route-specific middleware. Within each middleware type, the execution follows the order of their declaration.
</details>

<details>
<summary><strong>What happens if a middleware function does not call <code>next()</code>?</strong></summary>

If a middleware function does not call the `next()` function, the execution flow will be halted at that middleware function. Subsequent middleware functions or route handlers will not be executed, resulting in the request being left hanging without a response. It is important to call `next()` within middleware functions to ensure the execution continues to the next middleware or route handler.
</details>

<details>
<summary><strong>Based on the example provided, what will be the order of middleware execution?</strong></summary>

In the example given, the order of middleware execution will be as follows:

1. Global middleware 1: This middleware is declared using `app.use()` and will be executed first.
2. Route-specific middleware: The middleware added using `app.get('/users', ...)` will be executed next specifically for the `/users` route.
3. Global middleware 2: This middleware is declared using `app.use()` and will be executed after the route-specific middleware.
4. Route handler: Finally, the route handler for the `/users` route will be executed to send the response back to the client.

The execution order is determined by the order of the middleware declaration in the code.
</details>

---

## Chaining Middleware

In this example, we have three middleware functions (`middleware1`, `middleware2`, and `middleware3`) and a route handler for the `/users` route. The purpose is to demonstrate the concept of chaining middleware functions.

```js
const express = require('express');
const app = express();

// Middleware function 1
const middleware1 = (req, res, next) => {
  console.log('Middleware 1');
  next();
};

// Middleware function 2
const middleware2 = (req, res, next) => {
  console.log('Middleware 2');
  next();
};

// Middleware function 3
const middleware3 = (req, res, next) => {
  console.log('Middleware 3');
  next();
};

// Chaining middleware
app.get('/users', middleware1, middleware2, middleware3, (req, res) => {
  res.send('Hello, world!');
});

// Start the server
app.listen(3000, () => {
  console.log('Server is listening on port 3000');
});
```

<details>
<summary><strong>What is middleware chaining in Express?</strong></summary>

Middleware chaining in Express refers to the practice of passing multiple middleware functions as arguments to a route handler or using them with `app.use()`. The middleware functions are executed in the order they are passed, providing a sequential chain of operations before reaching the route handler. Each middleware function can perform specific tasks and either terminate the request-response cycle or pass control to the next middleware in the chain using the `next()` function.
</details>

<details>
<summary><strong>How do you chain middleware functions in Express?</strong></summary>

To chain middleware functions in Express, you can pass them as additional arguments to a route handler or use them with `app.use()`. The order in which you provide the middleware functions determines their execution order. For example:

```js
app.get('/users', middleware1, middleware2, middleware3, (req, res) => {
  // Route handler logic
});
```

In this example, `middleware1` will be executed first, followed by `middleware2`, `middleware3`, and finally the route handler logic.
</details>

<details>
<summary><strong>Can middleware functions terminate the request-response cycle?</strong></summary>

Yes, middleware functions have the ability to terminate the request-response cycle by sending a response or performing some action that ends the cycle. For example, middleware functions can send a response using `res.send()` or redirect the request using `res.redirect()`. When a middleware function terminates the cycle, subsequent middleware functions or route handlers will not be executed.
</details>