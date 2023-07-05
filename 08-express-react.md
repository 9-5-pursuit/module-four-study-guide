# Express with React

## Table of Contents

- [Restful Routes](#restful-routes)
- [Project Structure](#project-structure)
- [Setting up the Backend](#setting-up-the-backend)
- [Setting up the Frontend](#setting-up-the-frontend)
- [Connecting the Frontend to the Backend](#connecting-the-frontend-to-the-backend)
    - [Setting Up Additional Routes](#setting-up-additional-routes)
    - [Fetching Data & Handling Requests](#fetching-data--handling-requests)
    - [Creating Data](#creating-data)
    - [Editing Data](#editing-data)

---

## Restful Routes

In the [Express Restful Routes](./07-express-restful-routes.md) guide, we covered five RESTful routes that map to CRUD operations.

The next four are ones that we will build in our front end:

|  #  | Action |         URL         | HTTP Verb |   CRUD   |              Description               |
| :-: | :----: | :-----------------: | :-------: | :------: | :------------------------------------: |
|  1  | Index  |     /bookmarks      |    GET    | **R**ead | Get a list (or index) of all bookmarks |
|  2  |  Show  |   /bookmarks/:id    |    GET    | **R**ead | Get an individual view (show one log)  |
|  3  |  New   |   /bookmarks/new    |    GET    | **R**ead |  Get a form to create a new bookmark   |
|  4  |  Edit  | /bookmarks/:id/edit |    GET    | **R**ead |    Get a form to update a bookmark     |

<details>
<summary><strong>Which two are new, and which ones have we built with ExpressJS?</strong></summary>

The two new routes are `New` and `Edit`. We've built the `Index` and `Show` routes with ExpressJS.
</details>

## Project Structure

Our project structure changes a little from what we're used to. Up to this point, we've always worked with one primary folder that housed all of our site information.

Now, we're going to have two folders: one for the backend and one for the frontend. The backend will be an ExpressJS server, and the frontend will be a ReactJS application.

```bash
name-of-project/
├── backend/
└── frontend/
```

## Setting up the Backend

### Example Folder Structure

```bash
backend/
├── controllers/
├── models/
├── .env
├── .gitignore
├── package.json
├── server.js
└── app.js
```

### Project Setup

```bash
# Make sure you're in your backend folder
cd ~/path/to/backend

# Initialize a new NodeJS project
npm init -y

# Install dependencies
npm i express dotenv morgan cors
```

### .env

```bash
# Establish a port for your server
PORT=3001
```

<details>
<summary><strong>What other types of information could we store in the <code>.env</code> file?</strong></summary>

The `.env` file is commonly used to store environment-specific configuration variables. It can include information such as database credentials, API keys, secret tokens, or any other sensitive or environment-specific values needed by the application. It allows you to separate configuration from code and keep sensitive information outside of version control.
</details>

### .gitignore

```bash
# Ignore any files or folders that you don't want to push to GitHub
node_modules
.env
```

### app.js

```js
// DEPENDENCIES
const express = require('express');
const morgan = require("morgan");
const cors = require('cors');

// CONTROLLERS
const exampleController = require('./controllers/example.controller');

// CONFIG
const app = express();

// MIDDLEWARE
app.use(morgan("dev")); // Log HTTP requests
app.use(express.json()); // Parse incoming JSON
app.use(cors()); // Enable Cross Origin Resource Sharing

// ROUTES
app.use('/example', exampleController);

app.get('/', (req, res) => {
    res.send('Hello World!');
});

// EXPORT
module.exports = app;
```

<details>
<summary><strong>What is the purpose of the <code>morgan</code> middleware?</strong></summary>

The `morgan` middleware is used for logging HTTP requests in Node.js applications. It provides information about each incoming request, such as the HTTP method, URL, response status code, response time, and more. By using the `"dev"` format with `morgan("dev")`, the logs are displayed in a concise and readable format in the console during development. It helps developers track and debug incoming requests to the server.
</details>

<details>
<summary><strong>What is the purpose of the <code>cors</code> middleware?</strong></summary>

The `cors` middleware stands for Cross-Origin Resource Sharing and is used to enable cross-origin requests in an Express.js application. It adds the necessary headers to allow requests from different origins (domains) to access resources on the server. Cross-origin requests are typically restricted due to security reasons, but by using the `cors` middleware, you can specify the allowed origins, methods, headers, and other configurations to control cross-origin access to your server. It helps in handling API requests from different domains or origins.
</details>

### server.js

```js
// DEPENDENCIES
const app = require('./app');

// CONFIGURATION
require('dotenv').config();
const PORT = process.env.PORT || 3001;

// LISTEN
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```

<details>
<summary><strong>What is the purpose of the <code>dotenv</code> package?</strong></summary>

The `dotenv` package is used to load environment variables from a `.env` file into the Node.js application's `process.env` object. It allows developers to store configuration values, such as database connection strings, API keys, or other sensitive information, in a separate file without hardcoding them into the codebase. The `dotenv` package reads the `.env` file and assigns the values to the `process.env` object, making them accessible throughout the application.
</details>

<details>
<summary><strong>What does the <code>|| 3001</code> do in the <code>PORT</code> variable?</strong></summary>

The `|| 3001` is a fallback value in case the `process.env.PORT` variable is not defined. The `PORT` variable is used to specify the port on which the server should listen for incoming requests. In this case, the code checks if `process.env.PORT` is defined. If it is not defined (or evaluates to a falsy value), the `||` operator allows the fallback value of `3001` to be used as the default port. This ensures that the server listens on port `3001` if no specific port is provided through the environment variables.
</details>

### models/example.model.js

```js
// This is an example model. You can use this as a template for your own models.
module.exports = [
    {
        id: 1,
        name: 'Example Item 1',
        description: 'This is a example item.',
        price: 1.99
    },
    {
        id: 2,
        name: 'Example Item 2',
        description: 'This is a example item.',
        price: 2.99
    },
    {
        id: 3,
        name: 'Example Item 3',
        description: 'This is a example item.',
        price: 3.99
    }
];
```

<details>
<summary><strong>What type of data is being exported from this file?</strong></summary>

The type of data being exported from the `models/example.model.js` file is an array of objects. Each object represents an example item and contains properties such as `id`, `name`, `description`, and `price`. The array serves as a sample dataset or template for working with example items in the application.
</details>

### controllers/example.controller.js

```js
// DEPENDENCIES
const express = require('express');
const router = express.Router();
let exampleModel = require('../models/example.model');

// GET
router.get('/:id', (req, res) => {
    // Controller logic to get a single item
});

router.get('/', (req, res) => {
    // Controller logic to get all items
});

// POST
router.post('/create', (req, res) => {
    // Controller logic to create a new item
});

// EDIT
router.put('/edit/:id', (req, res) => {
    // Controller logic to edit an item
});

// DELETE
router.delete('/delete/:id', (req, res) => {
    // Controller logic to delete an item
});

// EXPORT
module.exports = router;
```

<details>
<summary><strong>What is the purpose of the <code>express.Router()</code> function?</strong></summary>

The `express.Router()` function is used to create a modular, mountable set of routes for a specific path prefix. It allows us to define multiple routes in separate files and then combine them into a single router for the application.
</details>

<details>
<summary><strong>What does the <code>GET</code> route <code>/example/:id</code> do?</strong></summary>

The `GET` route `/example/:id` is used to get a single item from the collection of examples. It uses the `:id` parameter to specify the ID of the item to retrieve.
</details>

<details>
<summary><strong>What is the purpose of the <code>POST</code> route <code>/example/create</code>?</strong></summary>

The `POST` route `/example/create` is used to create a new item in the collection of examples. It handles the request to create a new item and executes the necessary controller logic to save the item to the database or perform any other required actions.
</details>

<details>
<summary><strong>What is the purpose of the <code>PUT</code> route <code>/example/edit/:id</code>?</strong></summary>

The `PUT` route `/example/edit/:id` is used to edit an existing item in the collection of examples. It handles the request to update an item with the specified `:id` parameter and executes the necessary controller logic to modify the item in the database or perform any other required actions.
</details>

<details>
<summary><strong>What does the <code>DELETE</code> route <code>/example/delete/:id</code> do?</strong></summary>

The `DELETE` route `/example/delete/:id` is used to delete an item from the collection of examples. It handles the request to delete the item with the specified `:id` parameter and executes the necessary controller logic to remove the item from the database or perform any other required actions.
</details>

---

## Setting up the Frontend

### Example Folder Structure

```bash
frontend/
├── public/
├── src/
│   ├── components/
│   └── App.js
├── .env
├── .gitignore
└── package.json
```

### Project Setup

```bash
# Make sure you're in your frontend folder
cd ~/path/to/frontend

# Use the boilerplate provided by the curriculum
git clone <boilerplate-repository-url> . # Don't forget the period at the end!
npm install

# OR

# Initialize a new ReactJS project
npx create-react-app . # Don't forget the period at the end!
npm i react-router-dom axios uuid
```

### .env

```bash
# Add any environment-specific configuration variables here
REACT_APP_API_URL=http://localhost:3001/api
```

### .gitignore

```bash
# Ignore any files or folders that you don't want to push to GitHub
node_modules
.env
```

### App.js

```jsx
// DEPENDENCIES
import React from 'react';
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';

// COMPONENTS
import Example from './components/Example/Example';

function App() {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<Example />} />
      </Routes>
    </Router>
  )
}

export default App
```

### components/Example/Example.js

```jsx
import React, { useState, useEffect } from 'react';

function Example() {
    const [exampleData, setExampleData] = useState([]);

    useEffect(() => {
        fetchData();
    }, []);

    async function fetchData() {
       // Fetch data from the backend and store in the "exampleData" state
    }

    return (
        <div className="App">
            {exampleData.map((item) => {
                return (
                    <div key={item.id}>
                        <h2>{item.name}</h2>
                        <p>{item.description}</p>
                        <p>{item.price}</p>
                    </div>
                );
            })}
        </div>
    );
}

export default Example;
```

<details>
<summary><strong>Based on how our data is used, what type of data is being stored in the <code>exampleData</code> state?</strong></summary>

Based on how the data is used, the `exampleData` state is storing an array of objects. Each object represents an example item and contains properties such as `id`, `name`, `description`, and `price`. The `exampleData` state is used to hold the fetched data from the backend.
</details>

<details>
<summary><strong>What is happening inside our <code>useEffect</code> hook?</strong></summary>

Inside the `useEffect` hook, the `fetchData` function is called when the component mounts (since the dependency array is empty). This function is responsible for fetching data from the backend and updating the `exampleData` state with the retrieved data. By making the `fetchData` function asynchronous, it allows for asynchronous API requests to be made and handles the data retrieval process.
</details>

---

## Connecting the Frontend to the Backend

Now that we have our backend and frontend set up, we need to connect them. We'll do this by making API calls from the frontend to the backend.

### Setting Up Additional Routes

First, let's create some new routes in the `App.js` file to account for creating and editing items. We make sure to import any new components that we need. In this case, we'll need the `CreateExample` and `EditExample` components.

```jsx
// App.js
import React from 'react';
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';

// COMPONENTS
import Example from './components/Example/Example';
import CreateExample from './components/CreateExample/CreateExample';
import EditExample from './components/EditExample/EditExample';

function App() {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<Example />} />
        <Route path="/create" element={<CreateExample />} />
        <Route path="/edit/:id" element={<EditExample />} />
      </Routes>
    </Router>
  )
}

export default App
```

<details>
<summary><strong>What backend considerations do we make when creating our routes?</strong></summary>

- We need to define corresponding routes in the backend server to handle the requests sent from the frontend. These routes should be configured to perform the necessary CRUD operations on the data.
- For example, we would need to create routes in the backend to handle requests for creating and editing example items. These routes would execute the appropriate controller logic to perform the necessary database operations.
</details>

<details>
<summary><strong>What frontend considerations do we make when creating our routes?</strong></summary>

- In the frontend, we need to define the corresponding routes using a library like `react-router-dom`.
- We create `<Route>` components and specify the path and the component that should be rendered when that path is matched.
- In the example provided, we have added routes for the `/create` and `/edit/:id` paths, which correspond to creating a new example item and editing an existing example item, respectively.
- By defining these routes, we ensure that the correct components are rendered when the user navigates to the corresponding URLs.
</details>


### Fetching Data & Handling Requests

Next, let's update our `Example` component to fetch data from the backend. We'll also update the interface and add some helper functions to handle editing and deleting items.

```jsx
// components/Example/Example.js
import React, { useState, useEffect } from 'react';
import axios from 'axios';

function Example() {
    const API_URL = process.env.REACT_APP_API_URL;
    const [exampleData, setExampleData] = useState([]);

    useEffect(() => {
        fetchData();
    }, []);

    async function fetchData() {
        // We reach out to our .env file to get the API URL
        // We use the "REACT_APP_" prefix to make sure that our variables are available in the frontend
        const response = await axios.get(`${API_URL}/example`);

        // We set the data from the response to our "exampleData" state
        setExampleData(response.data);
    }

    async function handleDeleteById(id) {
        try {
            await axios.delete(`${API_URL}/example/delete/${id}`);

            let filteredData = exampleData.filter((item) => item.id !== id);
            setExampleData(filteredData);
        } catch (e) {
            console.error(e);
        }
    }

    async function handleEdit(id) {
        navigate(`/edit/${id}`);
    }

    return (
        <div className="App">
            {exampleData.map((item) => {
                return (
                    <div key={item.id}>
                        <h2>{item.name}</h2>
                        <p>{item.description}</p>
                        <p>{item.price}</p>
                        <button onClick={() => handleEdit(item.id)}>Edit</button>
                        <button onClick={() => handleDeleteById(item.id)}>Delete</button>
                    </div>
                );
            })}
        </div>
    );
}
```

<details>
<summary><strong>What is the purpose of the <code>fetchData</code> function in the <code>Example</code> component?</strong></summary>

The `fetchData` function is responsible for fetching data from the backend API. It sends a GET request to the specified API URL (`${API_URL}/example`) and retrieves the response data. The retrieved data is then set to the `exampleData` state using the `setExampleData` function.
</details>

<details>
<summary><strong>How does the <code>handleDeleteById</code> function work?</strong></summary>

The `handleDeleteById` function is used to delete an item by its ID. When called, it sends a DELETE request to the backend API with the specified item ID (`${API_URL}/example/delete/${id}`). If the request is successful, it updates the `exampleData` state by removing the deleted item from the array using the `filter` method.
</details>

<details>
<summary><strong>What does the <code>handleEdit</code> function do?</strong></summary>


The `handleEdit` function is used to handle the editing of an item. It navigates the user to the edit page for a specific item by using the `navigate` function (which is not shown in the provided code snippet). It constructs the URL path for editing the item by appending the item ID to `/edit/` (e.g., `/edit/${id}`). This function is typically used as an event handler for an edit button click.
</details>

<details>
<summary><strong>How are the buttons for edit and delete functionality integrated into the rendered output?</strong></summary>

For each item in the `exampleData` array, the component renders a set of information (name, description, price) along with two buttons: "Edit" and "Delete". The buttons are created using the `<button>` element, and event handlers (`handleEdit` and `handleDeleteById`) are assigned to the `onClick` attribute of each button. The event handlers are called with the corresponding item ID as an argument to perform the necessary operations.
</details>

### Creating Data

Next, let's create a new component (`CreateExample`) to handle creating new items.

```jsx
// components/CreateExample/CreateExample.js
import React from 'react';
import { useNavigate } from 'react-router-dom';
import axios from 'axios';

function CreateExample() {
    const [exampleItem, setExampleItem] = React.useState({
        name: "",
        description: "",
        price: 0
    });
    const navigate = useNavigate();

    // These helper functions are used to update the state. We left out the details for brevity.
    function handleChange(e) { ... }
    function resetForm() { ... }

    async function handleSubmit(e) {
        e.preventDefault();

        try {
            // We pass our exampleItem state to the backend
            await axios.post(`${process.env.REACT_APP_API_URL}/example/create/`, { exampleItem });

            // We reset the form and navigate back to the home page once the item has been created
            resetForm();
            navigate("/");
        }
        catch (e) {
            console.error(e);
        }
    }

    // We've limited the form to only include the "name" field for simplicity
    return (
        <form onSubmit={handleSubmit}>
            <h2>Create Example Item</h2>
            <label>
                Name:
                <input
                    type="text"
                    value={exampleItem.name}
                    onChange={(e) => handleChange(e)}
                    required
                />
            </label>
            <button>Submit</button>
        </form>
    )
}

export default CreateTodo;
```

<details>
<summary><strong>What is the purpose of the <code>CreateExample</code> component?</strong></summary>

The `CreateExample` component is responsible for rendering a form to create new items. It provides a user interface for inputting the name of the item. When the form is submitted, it sends a POST request to the backend API to create the new item.
</details>

<details>
<summary><strong>How is the state managed for the form input fields?</strong></summary>

The state for the form input fields is managed using the `useState` hook. The `exampleItem` state is an object that contains properties for `name`, `description`, and `price`. In the provided code snippet, only the `name` field is included for simplicity. The `value` of the input field is set to `exampleItem.name`, and the `onChange` event is handled by the `handleChange` function, which updates the corresponding property in the `exampleItem` state.
</details>

<details>
<summary><strong>What happens when the form is submitted?</strong></summary>

When the form is submitted, the `handleSubmit` function is called. It prevents the default form submission behavior (`e.preventDefault()`) to handle the submission manually. Inside the function, a POST request is sent to the backend API (`${process.env.REACT_APP_API_URL}/example/create/`) with the `exampleItem` state as the request payload. If the request is successful, the form is reset using the `resetForm` function, and the user is navigated back to the home page (`navigate("/")`).
</details>

<details>
<summary><strong>How is the navigation back to the home page handled?</strong></summary>

The `useNavigate` hook from the `react-router-dom` library is used to handle navigation. It provides the `navigate` function, which can be used to programmatically navigate to a specific URL. In this case, after the item has been created successfully, the `navigate` function is called with `"/"` as the argument to navigate back to the home page.
</details>

### Editing Data

Finally, let's create a new component (`EditExample`) to handle editing existing items.

```jsx
// components/EditExample/EditExample.js
import React, { useEffect, useState } from 'react';
import { useParams, useNavigate } from 'react-router-dom';
import axios from 'axios';

function EditExample() {
    const API_URL = process.env.REACT_APP_API_URL;
    const { id } = useParams();
    const navigate = useNavigate();
    const [exampleItem, setExampleItem] = useState({
        name: "",
        description: "",
        price: 0
    });

    useEffect(() => {
        fetchDataById();
    }, []);

    // This helper function is used to update the state. We left out the details for brevity.
    function handleChange(e) { ... }

    // Fetch the requested data from the backend
    async function fetchDataById() {
        try {
            const response = await axios.get(`${API_URL}/example/${id}`);

            setExampleItem(response.data);
        } catch (e) {
            console.error(e);
        }
    }

    // Handle changes to the data
    async function handleSubmit(e) {
        e.preventDefault();

        try {
            let response = await axios.put(`${API_URL}/example/edit/${id}`, { exampleItem });
            const updatedItem = response.data;
            setExampleItem(updatedItem);
        } catch (e) {
            console.error(e);
        }
    }

    // We've limited the form to only include the "name" field for simplicity
    return (
        <form onSubmit={handleSubmit}>
            <h2>Edit Example Item</h2>
            <label>
                Name:
                <input
                    type="text"
                    value={exampleItem.name}
                    onChange={(e) => handleChange(e)}
                    required
                />
            </label>
            <button>Submit</button>
        </form>
    );
}

export default EditExample;
```

<details>
<summary><strong>What is the purpose of the <code>EditExample</code> component?</strong></summary>

The `EditExample` component is responsible for rendering a form to edit existing items. It retrieves the item data from the backend API based on the provided `id` parameter. The component allows the user to modify the `name` field of the item and submit the changes. The updated item data is sent to the backend API via a PUT request.
</details>

<details>
<summary><strong>How is the item data fetched from the backend API?</strong></summary>

The `useEffect` hook is used to fetch the item data from the backend API when the component mounts. It calls the `fetchDataById` function, which makes a GET request to the backend API (`${API_URL}/example/${id}`). The `id` parameter is obtained from the `useParams` hook. If the request is successful, the item data is stored in the `exampleItem` state using `setExampleItem`.
</details>

<details>
<summary><strong>How are the changes to the item data handled and submitted to the backend?</strong></summary>

When the form is submitted, the `handleSubmit` function is called. It prevents the default form submission behavior (`e.preventDefault()`) to handle the submission manually. Inside the function, a PUT request is sent to the backend API (`${API_URL}/example/edit/${id}`) with the updated `exampleItem` state as the request payload. If the request is successful, the response data containing the updated item is stored in the `exampleItem` state using `setExampleItem`.
</details>

<details>
<summary><strong>What's the difference between the input fields in the <code>CreateExample</code> and <code>EditExample</code> components?</strong></summary>

The input fields in the `CreateExample` component are empty by default, while the input fields in the `EditExample` component are pre-filled with the existing item data. This is because the `CreateExample` component is used to create new items, while the `EditExample` component is used to edit existing items.
</details>

---

## Additional Resources

- [Express React Skeleton](https://github.com/9-5-pursuit/express-react-skeleton)