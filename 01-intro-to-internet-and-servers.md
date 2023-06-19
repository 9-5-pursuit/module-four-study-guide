# Intro to the Internet and Servers

## Components of the Internet

| Term | Definition |
| ---- | ---------- |
| __Computer&nbsp;Networks__ | Networks that allow the connection of two or more computers to exchange and share data and resources. They can be set up by location, such as a company office, metropolitan area, or global network. |
| __Internet__ | A global computer network that uses the Internet protocol suite (TCP/IP). It encompasses public and private networks and enables communication between various networks worldwide. |
| __Web__ | The World Wide Web (WWW), a subset of the internet, accessible through web browsers like Chrome, Firefox, or Safari. Websites on the web often have URLs starting with "www." |

<details>
<summary><strong>What is the purpose of computer networks?</strong></summary>

Computer networks allow the connection of two or more computers to exchange and share data and resources. They facilitate communication and collaboration among users, enable the sharing of files and printers, and provide access to the internet.
</details>

<details>
<summary><strong>What is the internet and what protocol does it use?</strong></summary>

The internet is a global computer network that connects millions of computers and networks worldwide. It uses the Internet Protocol suite (TCP/IP) to enable communication and data transfer between different devices and networks.
</details>

<details>
<summary><strong>Differentiate between the internet and the World Wide Web (WWW).</strong></summary>

The internet is the vast network infrastructure that connects computers and networks globally, allowing them to communicate and exchange data. On the other hand, the World Wide Web (WWW) is a subset of the internet that consists of websites, web pages, and web content accessible through web browsers. The WWW is an application that utilizes the internet infrastructure to deliver information and multimedia resources.
</details>

---

## Components of a Request-Response Cycle

| Term | Definition |
| ---- | ---------- |
| __Client__ | Any device or software that connects to the internet and makes requests to servers. Clients can be web browsers, mobile apps, or other applications. They initiate requests to servers and receive responses. |
| __Server__ | A computer that receives requests from clients and responds to those requests. Servers are dedicated computers designed to handle requests, provide resources, and process data. They can be web servers, email servers, or other types of servers. |
| __Request-Response Cycle__ | The interaction between clients and servers, where clients send requests to servers, and servers respond with the requested data or perform requested actions. It forms the basis of communication in web applications. |

<details>
<summary><strong>Define a client and a server in the context of web applications.</strong></summary>

In the context of web applications, a client refers to any device or software (such as a web browser or mobile app) that connects to the internet and makes requests to servers. Clients initiate requests to servers to retrieve data or perform actions.

A server, on the other hand, is a computer that receives requests from clients and responds to those requests. Servers are dedicated computers designed to handle requests, provide resources, and process data. They store and serve web pages, process application logic, and interact with databases or other external systems.
</details>

<details>
<summary><strong>Describe the process of the request-response cycle.</strong></summary>

The request-response cycle is the interaction between clients and servers in a web application. The process typically involves the following steps:

1. The client sends a request to the server. The request includes information such as the desired resource (e.g., a specific web page) and any additional data or parameters.

2. The server receives the request and processes it. This may involve interpreting the requested resource, accessing databases or other resources, and performing any necessary calculations or operations.

3. The server generates a response based on the request. The response includes the requested data or performs the requested action. It may also include headers providing metadata about the response.

4. The server sends the response back to the client over the network.

5. The client receives the response and processes it. This may involve rendering web pages, displaying the requested data, or executing further actions based on the response.
</details>

<details>
<summary><strong>What is the role of servers in handling client requests?</strong></summary>

*__Summary:__*

Servers act as the central processing units in a web application, handling client requests, performing necessary computations, and returning the appropriate responses.*

*__Details:__*

Servers play a crucial role in handling client requests in a web application. When a client sends a request, the server receives it and performs various tasks, including:

- __Interpret the request__: The server examines the request to determine the desired resource or action.

- __Retrieve data__: The server may access databases, file systems, or other resources to gather the necessary data to fulfill the request.

- __Process logic__: The server may execute application logic or business rules to manipulate the data or perform required operations.

- __Generate a response__: Based on the request and processed data, the server constructs a response containing the requested information or performs the requested action.

- __Send the response__: The server sends the response back to the client over the network, ensuring that it is properly formatted and contains the necessary headers and content.
</details>

---

## Databases

| Term | Definition |
| ---- | ---------- |
| __Database__ | A computer program that stores electronic data in organized collections. It manages data and allows clients to access and interact with the data through servers. Examples include databases storing user information, product data, or other structured information. |

<details>
<summary><strong>What is a database and what is its purpose?</strong></summary>

A database is a computer program that stores electronic data in organized collections. Its purpose is to manage data effectively and provide a mechanism for clients (such as applications or users) to access, manipulate, and interact with that data. Databases provide a structured and efficient way to store and retrieve information, ensuring data integrity, security, and scalability.
</details>

<details>
<summary><strong>How does a server interact with a database?</strong></summary>

*__Summary__*

The server acts as an intermediary between the application or user and the database, enabling seamless communication and data retrieval or manipulation.

*__Details__*

Servers interact with databases through a process known as database connectivity. The server communicates with the database management system (DBMS) to perform various operations, including:

1. __Establishing a connection__: The server establishes a connection to the database by providing the necessary credentials and connection parameters.

2. __Sending queries__: The server sends structured queries, such as SQL (Structured Query Language) statements, to the database. These queries can retrieve data, modify existing data, or perform other operations.

3. __Processing the queries__: The database management system receives the queries from the server and processes them. It analyzes the queries, accesses the appropriate data, and performs the requested operations.

4. __Returning results__: Once the database has processed the queries, it sends the results back to the server. This may include retrieved data, the outcome of data modification operations, or other relevant information.

5. __Handling transactions__: In many cases, servers manage transactions that involve multiple database operations. The server ensures the atomicity, consistency, isolation, and durability (ACID) properties of the transaction, coordinating with the database to maintain data integrity.


</details>

<details>
<summary><strong>Give an example of a type of information stored in a database.</strong></summary>

Databases can store various types of information depending on the application or system. Examples include:

- __User information__: Databases can store user details such as usernames, passwords, email addresses, and other profile data.

- __Product data__: E-commerce platforms often use databases to store information about products, including names, descriptions, prices, and inventory levels.

- __Financial records__: Banks and financial institutions utilize databases to store customer transaction data, account balances, and other financial records.

- __Social media posts__: Social networking platforms store user-generated content, such as posts, comments, photos, and videos, in databases.

- __Employee records__: Human resources departments maintain databases to store employee information, including personal details, employment history, and performance records.

These examples demonstrate how databases serve as repositories for structured and organized data, allowing efficient storage, retrieval, and management of information for various purposes.
</details>

---

## Requests and Responses

| Term | Definition |
| ---- | ---------- |
| __HTTP__ | HyperText Transfer Protocol, the protocol used for communication between clients and servers over the internet. It allows for the transfer of various data types, including HTML, JSON, images, etc. |
| __URL__ | Uniform Resource Locator, a string of text characters that identifies the address of a resource on the internet. URLs are used in requests and responses to locate and access resources. They consist of components such as the protocol, host/domain name, port, path, query string, and hash/fragment. |
| __Header__ | The metadata included in the HTTP request or response that provides essential information about the request or response. It includes details such as the URL, request method, content type, and status code. |
| __Body__ | The optional part of an HTTP request or response that contains data or content. For example, in a request, the body may include form data entered by a user, while in a response, it may contain HTML content to be rendered by a browser. |

<details>
<summary><strong>What does HTTP stand for and what is its purpose?</strong></summary>

HTTP stands for HyperText Transfer Protocol. Its purpose is to facilitate communication between clients and servers over the internet. It defines the rules and conventions for how clients (such as web browsers) and servers should exchange requests and responses. HTTP enables the transfer of various data types, including HTML, JSON, images, and more, allowing clients to retrieve and interact with resources hosted on servers.
</details>

<details>
<summary><strong>What is a URL and what purpose does it serve?</strong></summary>

A URL, or Uniform Resource Locator, is a string of text characters that identifies the address of a resource on the internet. It serves as a standardized format for specifying the location of a resource, such as a web page, image, video, or API endpoint. A URL consists of components such as the protocol (e.g., HTTP or HTTPS), host/domain name, port, path, query string, and hash/fragment. URLs are used in requests to locate and access specific resources on servers.
</details>

<details>
<summary><strong>What is the difference between the header and body in an HTTP request or response?</strong></summary>

In an HTTP request or response, the header and body are distinct parts.

- __Header__: The header is the metadata included in the HTTP request or response. It provides essential information about the request or response, such as the URL, request method, content type, and status code. Headers enable communication between the client and server by conveying instructions, details, and control information.

- __Body__: The body is the optional part of an HTTP request or response that contains the data or content being sent. In a request, the body may include form data entered by a user or JSON/XML payloads. In a response, the body contains the actual content being transferred, such as HTML markup, JSON data, or binary files like images or documents.

The header and body work together to facilitate effective communication between clients and servers. The header provides metadata and instructions, while the body carries the actual data being transmitted.
</details>

### URL Components

Let's break down the contents of a complex URL:

```
 https://www.example.org:3000/hello/world/index.html?name=foo&limit=20#footer
 \___/ \_______________/ \__/ \___________________/ \_______________/ \____/
protocol  host/domain    port         path            query-string  hash/fragment
```

The URL components are always in the same order.

| Element | About |
| ------- | ----- |
| __protocol__ | The application protocol in this example is HTTP or HTTPS (`S` stands for secure). Other familiar types of application protocols include SMTP/POP, and SSH. |
| __host/domain name__ | The server's name that provides the resource. |
| __port__ | A server can have multiple ports. Multiple ports allow users to access different applications on the same host. The port is usually pre-configured, so it typically does not need to be included in the URL to locate a resource. |
| __path__ | Web servers can organize resources into a system similar to files and folders in directories. |
| __query-string__ | The client can pass parameters to the server through the query-string. The query-string allows for additional request information to be passed through the URL. For example, if you go to an international website, it may have `lang=en`, which means respond with a web page in English. |
| __hash/fragment__ | The client can use a hash/fragment to identify some portion of the content in the response. If you click on an element in the table of contents on this page, the page will scroll down to that section and you will see a hash fragment in the URL corresponding to the section. If you send your friend the link with the hash fragment the page will load and automatically scroll down to the section. |

<details>
<summary><strong>What is a protocol?</strong></summary>

A protocol is a set of rules and conventions that govern how data is transmitted and communicated between devices or systems. In the context of URLs, a protocol is an application protocol that determines how information is exchanged between clients and servers over the internet.

Common protocols include HTTP (Hypertext Transfer Protocol) and HTTPS (Hypertext Transfer Protocol Secure) for web communication, SMTP/POP for email, and SSH (Secure Shell) for secure remote access. Protocols define the format, syntax, and behavior of data transfers, enabling effective communication between different systems.
</details>

<details>
<summary><strong>What is the purpose of the query-string in a URL?</strong></summary>

The query-string in a URL allows clients to pass additional parameters or data to the server as part of a request. It is used to provide specific instructions or information related to the requested resource.

The query-string appears after the path component of the URL and is preceded by a question mark (?). It consists of key-value pairs, where each pair represents a parameter and its value, separated by an ampersand (&). The server can use these parameters to customize the response or perform specific operations.

For example, in a search query, the query-string may include parameters like `?q=keyword` to specify the search term.
</details>

<details>
<summary><strong>How does the hash/fragment component in a URL contribute to the user experience of a web page?</strong></summary>

The hash/fragment component in a URL is used to identify a specific portion or section of content within a web page. When a URL contains a hash/fragment, the web browser interprets it as an anchor within the page and scrolls the viewport to the corresponding section. This feature is often used to create internal page links or to highlight specific content on a page.

For example, when clicking on a table of contents on a long web page, the URL may update with a hash/fragment identifier that corresponds to the selected section. Sharing the URL with the hash/fragment allows others to directly access and view that specific content, enhancing the user experience by providing direct navigation to relevant information within a page.
</details>

---

## HTTP Protocol

| Term | Definition |
| ---- | ---------- |
| __Request&nbsp;Methods__ | The four primary ways to interact with data through HTTP: POST (create), GET (read), PUT/PATCH (update), and DELETE (destroy). These methods correspond to the CRUD operations (Create, Read, Update, Delete) commonly performed on data. |
| __HTTP Status Codes__ | Numerical codes included in the HTTP response that indicate the status of the request. Status codes in the range 100-399 confirm the request/response is OK. Codes in the 400s denote user errors, while codes in the 500s denote server errors. They provide information about the success or failure of the request and the reason for the failure. Common status codes include 200 (OK), 404 (Not Found), and 500 (Internal Server Error). |

<details>
<summary><strong>Name the four primary request methods in HTTP and their corresponding CRUD operations.</strong></summary>

The four primary request methods in HTTP are:

1. __POST__: Corresponds to the Create operation in CRUD. It is used to submit data to be processed and stored on the server. For example, creating a new user account or submitting a form.

2. __GET__: Corresponds to the Read operation in CRUD. It is used to retrieve data from the server. For example, fetching a web page, retrieving user information, or retrieving a list of products.

3. __PUT/PATCH__: Corresponds to the Update operation in CRUD. It is used to modify existing data on the server. PUT typically replaces the entire resource with the updated data, while PATCH modifies only specific parts of the resource. For example, updating a user's profile information or editing an article.

4. __DELETE__: Corresponds to the Delete operation in CRUD. It is used to remove data or resources from the server. For example, deleting a user account or removing a post.
</details>

<details>
<summary><strong>How do HTTP status codes provide information about a request's outcome?</strong></summary>

HTTP status codes are included in the response sent by the server to indicate the outcome of the request. They provide information about whether the request was successful, encountered an error, or requires further action. The status codes are three-digit numerical codes that categorize the response into different classes:

- __1xx__: Informational responses
- __2xx__: Successful responses
- __3xx__: Redirection responses
- __4xx__: Client error responses
- __5xx__: Server error responses

Each status code within these classes has a specific meaning. For example, a status code of 200 (OK) indicates that the request was successful, while a code of 404 (Not Found) means that the requested resource was not found on the server. By analyzing the status code received, developers can determine the outcome of their request and handle it accordingly in their application.
</details>

<details>
<summary><strong>Give examples of HTTP status codes for successful requests and common client/server errors.</strong></summary>

Examples of HTTP status codes include:

- __200 (OK)__: The request was successful, and the server has returned the requested resource.
- __201 (Created)__: The request was successful, and a new resource was created as a result.
- __204 (No Content)__: The request was successful, but there is no content to return.
- __400 (Bad Request)__: The server cannot process the request due to client error, such as malformed syntax or invalid parameters.
- __404 (Not Found)__: The requested resource could not be found on the server.
- __500 (Internal Server Error)__: The server encountered an error while processing the request.

These are just a few examples, and there are many more status codes available to indicate different outcomes of HTTP requests.
</details>

---