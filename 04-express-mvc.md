# Express MVC

| Term | Definition |
| ---- | ---------- |
| __MVC__ | Stands for Model-View-Controller, a software architectural pattern commonly used in web development. It separates an application into three interconnected components: the Model (handles data and logic), the View (responsible for rendering and displaying data), and the Controller (manages communication between the Model and View). |
| __Model__ | Represents the data and business logic of an application in the MVC pattern. It is responsible for managing data, performing validations, and defining relationships with other models. |
| __View__ | In the MVC pattern, the View component is responsible for rendering data and presenting it to the user. It receives data from the Model and generates the appropriate HTML, CSS, or other presentation formats. |
| __Controller__ | In the MVC pattern, the Controller component handles user interactions, receives input, and performs appropriate actions. It interacts with the Model to update or retrieve data and coordinates with the View to render the appropriate response. |
| __RESTful API__ | Stands for Representational State Transfer. It is an architectural style for designing networked applications that adhere to a set of principles, such as using HTTP methods (GET, POST, PUT, DELETE) for different operations and representing resources as URLs.|

---

## Models

```js
// bookmark.js
module.exports = [
  {
    name: "MDN",
    url: "https://developer.mozilla.org/en-US/",
    isFavorite: true,
    category: "educational",
  },
  {
    name: "Apartment Therapy",
    url: "https://www.apartmenttherapy.com",
    isFavorite: true,
    category: "inspirational",
  },
  {
    name: "DMV",
    url: "https://dmv.ny.gov",
    isFavorite: false,
    category: "adulting",
  },
];
```

<details>
<summary><strong>What is the purpose of exporting the array of bookmark objects from the <code>bookmark.js</code> module?</strong></summary>

The purpose of exporting the array of bookmark objects is to make it accessible to other parts of the application. It allows other modules or files to import and use the `bookmarksArray` data.
</details>

<details>
<summary><strong>How would you access the name of the second bookmark in the <code>bookmarksArray</code>?</strong></summary>

To access the name of the second bookmark in the `bookmarksArray`, you can use `bookmarksArray[1].name`. Array indices start at 0, so the second bookmark can be accessed using index 1.
</details>

<details>
<summary><strong>In the provided code snippet, what are the properties associated with each bookmark object?</strong></summary>

The properties associated with each bookmark object are `name`, `url`, `isFavorite`, and `category`. These properties store information such as the name of the bookmark, its URL, whether it is marked as a favorite, and its category.
</details>

<details>
<summary><strong>If you wanted to add a new bookmark to the <code>bookmarksArray</code>, what modifications would you make in the <code>bookmark.js</code> module?</strong></summary>

To add a new bookmark to the `bookmarksArray`, you would modify the `bookmark.js` module by inserting a new object representing the bookmark at the desired position within the array. For example, you can use the `push()` method to add it at the end: `bookmarksArray.push({ name: "New Bookmark", url: "https://example.com", isFavorite: false, category: "uncategorized" })`.
</details>

<details>
<summary><strong>Can the <code>bookmarksArray</code> contain elements other than objects? Explain your answer.</strong></summary>

Yes, the `bookmarksArray` can contain elements other than objects. JavaScript arrays can hold any type of value, including primitive data types (such as strings, numbers, booleans) and even other arrays or objects. However, in the provided code snippet, the intention is to store bookmark objects within the array.
</details>

<details>
<summary><strong>What does <code>module.exports</code> do? What happens if we forget to add it? What kind of error will we get?</strong></summary>

`module.exports` is a special object in Node.js that allows us to export values from a module. It specifies the objects or functions that should be accessible to other modules when they require or import the current module.

If we forget to add `module.exports` in a module, when we try to import that module in another file using `require()`, we will receive an `undefined` value. This is because the module didn't export anything explicitly, so there is no value to import.

The specific error message we would see when trying to import a module without `module.exports` varies depending on the environment or tool being used. However, a common error message is `TypeError: Cannot read property 'something' of undefined`, where `'something'` refers to the specific property or method we are trying to access from the imported module.
</details>

---

## Views

In Express MVC, views refer to the user interface components responsible for presenting data to the user and receiving user input. They play a crucial role in creating an engaging and interactive user experience.

In this course, React is utilized as the primary technology for handling views in an Express MVC application. To learn more about utilizing React with Express, refer to the [React with Express Guide](./07-express-with-react.md).

---

## Controllers

```js
// controllers/bookmarksController.js
// -----------------------------------
const express = require("express");
const bookmarks = express.Router();
const bookmarksArray = require("../models/bookmark.js");

bookmarks.get("/", (req, res) => {
  res.json(bookmarksArray);
});

module.exports = bookmarks;


// app.js
// -----------------------------------
const bookmarksController = require("./controllers/bookmarksController.js");
app.use("/bookmarks", bookmarksController);
```

<details>
<summary><strong>How is the <code>bookmarksController.js</code> module imported and used in the <code>app.js</code> file?</strong></summary>

The `bookmarksController.js` module is imported in the `app.js` file using the `require()` function and assigned to the `bookmarksController` variable. It is then incorporated into the Express application using the `.use()` method.

The `.use()` method is a middleware function provided by Express that allows us to mount the `bookmarksController` module on a specific base URL path ("/bookmarks" in this case). It acts as a routing middleware, handling requests that match the specified base URL.

When a request is made to a URL that starts with "/bookmarks", Express will invoke the `bookmarksController` middleware, which is responsible for handling the request and generating the appropriate response.

By using the `.use()` method with the "/bookmarks" path and the `bookmarksController` module, we effectively delegate the handling of requests starting with "/bookmarks" to the `bookmarksController` module. This allows us to organize our code and separate concerns, keeping the route handling logic encapsulated in the `bookmarksController.js` file.
</details>

<details>
<summary><strong>What is the purpose of the <code>bookmarksArray</code> variable in the <code>bookmarksController.js</code> module?</strong></summary>

The `bookmarksArray` variable in the `bookmarksController.js` module is used to store an array of bookmark objects. It serves as the data source for the GET request to the "/bookmarks" route, where the array is sent as the response.
</details>

<details>
<summary><strong>If you wanted to add a new route to create a new bookmark, how would you modify the provided code in the <code>bookmarksController.js</code> module?</strong></summary>

To add a new route to create a new bookmark, you would need to define a new HTTP method handler on the `bookmarks` router. For example, to add a POST route, you can use the `.post()` method:

```js
bookmarks.post("/", (req, res) => {
  // Code to handle creating a new bookmark
});
```

You can then implement the logic to handle the creation of a new bookmark within the route handler function.
</details>

<details>
<summary><strong>How would you modify the code to change the base URL from "/bookmarks" to "/favorites"?</strong></summary>

To change the base URL from "/bookmarks" to "/favorites", you would modify the code in the `app.js` file where the `bookmarksController` module is incorporated into the Express application.

Currently, the `bookmarksController` middleware is mounted on the "/bookmarks" path using the `.use()` method:

```js
app.use("/bookmarks", bookmarksController);
```

To change it to "/favorites", you would update the code as follows:

```js
app.use("/favorites", bookmarksController);
```

This change will ensure that the `bookmarksController` middleware is now invoked for requests starting with "/favorites" instead of "/bookmarks". The routes defined in the `bookmarksController.js` module will now be accessible under the "/favorites" base URL.
</details>

---

## Error Handling

```js
// 404 PAGE - NO STATUS CODE
app.get("*", (req, res) => {
  res.json({ error: "Page not found" });
});

// 404 PAGE - WITH STATUS CODE
app.get("*", (req, res) => {
  res.status(404).json({ error: "Page not found" });
});
```

<details>
<summary><strong>What is the purpose of the first code snippet that handles the "404 PAGE - NO STATUS CODE"?</strong></summary>

The purpose of the first code snippet is to handle requests to routes that haven't been defined in the provided code snippets. When a request is made to a route that doesn't match any defined routes, the callback function `(req, res) => {...}` is executed. It sends a JSON response with an error message indicating that the page was not found.

```js
app.get("*", (req, res) => {
  res.json({ error: "Page not found" });
});
```

By using the `"*"` as the route pattern, this route acts as a catch-all for any undefined routes, ensuring that the error message is sent for any unrecognized URLs.

</details>

<details>
<summary><strong>How does the second code snippet differ from the first one in terms of the response sent for the "404 PAGE"?</strong></summary>

The second code snippet differs from the first one by including a status code in the response for the "404 PAGE". Instead of just sending a JSON response with an error message, it sets the HTTP status code to 404 using the `.status(404)` method before sending the JSON response.

```js
app.get("*", (req, res) => {
  res.status(404).json({ error: "Page not found" });
});
```

Setting the appropriate status code provides more specific information to the client's browser or API consumer about the nature of the error. In this case, it indicates that the requested page was not found (404 status code).

</details>

<details>
<summary><strong>What will be sent as the response when a request is made to a route that hasn't been defined in the provided code snippets?</strong></summary>

When a request is made to a route that hasn't been defined in the provided code snippets, the response will depend on which code snippet is being used:

- In the first code snippet, the response will be a JSON object with an error message: `{ error: "Page not found" }`. However, the response will not include an explicit HTTP status code.

- In the second code snippet, the response will be a JSON object with an error message: `{ error: "Page not found" }`, and the HTTP status code will be set to 404, indicating a "Page not found" error.

</details>

<details>
<summary><strong>If you wanted to customize the error message for the "404 PAGE" response, how would you modify the code in the second snippet?</strong></summary>

To customize the error message for the "404 PAGE" response in the second code snippet, you would modify the JSON object being sent in the response. Update the value of the `"error"` property to reflect the desired error message.

For example, to customize the error message to say "Custom message: Page not found", you can modify the code as follows:

```js
app.get("*", (req, res) => {
  res.status(404).json({ error: "Custom message: Page not found" });
});
```

By changing the value of the `"error"` property, you can customize the error message to suit your needs.

</details>

<details>
<summary><strong>Explain the significance of using the appropriate status code (404) when handling a "Page not found" error.</strong></summary>

Using the appropriate status code (404) when handling a "Page not found" error is significant for several reasons:

1. Clear indication: The 404 status code is a standard HTTP status code that signifies the requested resource (in this case, the page) could not be found. By setting this status code, the server clearly communicates to the client that the requested page is not available.

2. Browser behavior: When a browser receives a 404 status code, it knows that the requested page doesn't exist. The browser can handle this information appropriately by displaying an error page or taking alternative actions based on its configuration.

3. API consumers: When building APIs, using the 404 status code allows API consumers to distinguish between valid and invalid endpoints. It helps them understand that the requested resource is not available and provides a consistent approach for error handling.

Overall, using the appropriate status code, such as 404 for "Page not found" errors, improves the clarity and standardization of error responses, enabling better communication between the server and clients or API consumers.
</details>