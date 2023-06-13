# npm & Express Response

| Term | Definition |
| ---- | ---------- |
| __Node__ | An open-source project that lets us run JavaScript in the Terminal. Previous to nodeJS, JavaScript could only be run in the browser. |
| __npm__ | Node Package Manager: an extensive library of 3rd party packages for Node. |
| __Express__ | A code framework hosted on npm and written in JavaScript for building web servers. |
| __Route__ | In Express, a route is like an event listener that listens for requests to a specific URL. It determines how the server should respond when a client makes a request to that URL. |
| __Request Object__ | The `request` object in Express represents the HTTP request sent by the client to the server. It contains information about the request, such as the URL, headers, query parameters, and request body. |
| __Response Object__ | The `response` object in Express represents the HTTP response sent by the server back to the client. It is used to send data, set response headers, and control the response behavior. |

## Editing `package.json`

When editing the `package.json` you must write proper JSON (JavaScript Object Notation). It is very similar to a JavaScript Object, but it is a bit more strict.

YOU MUST:

- use double quotes (never single quotes)
- use double quotes around object keys, numbers, and booleans.
- create and maintain valid JS objects, arrays, and strings.
- NOT have any trailing commas

## Intializing an Express Application

```js
const express = require('express');
const app = express();
```

- What is the role of `const express = require("express")` in the code?
- What does `const app = express()` do in the code?

## Creating a basic route

```js
app.get("/", (request, response) => {
  response.send("Hello World");
});
```

- What does `app.get("/", (request, response) => { ... })` define in the Express application?
- What is the purpose of `response.send("Hello World")`?
- What is the significance of using the root path `/` in `app.get("/", ...)`?
- How would you make a request for the `/universe` route instead?
- How can you modify the code to handle a POST request instead of a GET request?
- Can you explain the purpose of the request and response parameters in the callback function?

## Starting the server

```js
const PORT = 3000;
app.listen(PORT, () => {
  console.log(`Server listening on port ${PORT}`);
});
```

- What does `app.listen(PORT, () => {...})` do in the code?
- How can you access the Express application in a web browser after running this code?
- What would happen if you change the port number to a different value?
- How can you gracefully shut down the Express application when it's running?

## Putting it all together

```js
// app.js
const express = require("express");
const app = express();

app.get("/", (request, response) => {
  response.send("I love express!");
});

app.get("/universe", (request, response) => {
  response.send("Hello Universe!");
});

app.listen(3003, () => {
  console.log("I am listening for requests on port 3003!");
});
```

---

## Nodemon

| Term | Definition |
| ---- | ---------- |
| __Nodemon__ | A tool that monitors your Node.js application for file changes. It automatically restarts the server whenever it detects that a file has been modified and saved. This helps streamline the development workflow by eliminating the need to manually restart the server after every code change. |

- What is the purpose of nodemon in a Node.js application development workflow?
- How does nodemon help streamline the development process when working with Node.js applications?
- How can you install nodemon globally using npm?
- What happens when a file is modified and saved while nodemon is running?
- How can you start the server using nodemon after installing it globally?

---

## grep and kill nodemon

| Term | Definition |
| ---- | ---------- |
| `ps` | process status |
| `grep` | global regular expression print |

Suppose you don't cancel out of your server properly before putting your computer to sleep or try to run nodemon on the same port multiple times. In that case, you may have nodemon running amok in your background processes.

1. Find the Process

    `ps -A | grep nodemon` will get the "process status" (`ps`) of all processes (`-A`) and use a regular expression (`grep`) to specifically find the term `"nodemon"`

    ![](./images/ps-grep.png)
    *On the left, you will see the process number. In this case, it is `26625`.*

2. Kill the Process

    `kill 26625` => Be sure the number equals the number from the process you looked up before.

__*Get into good habits of gracefully exiting out of programs to avoid taking extra troubleshooting steps like the ones above.*__