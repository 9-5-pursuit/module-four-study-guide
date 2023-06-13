# Intro to the Internet and Servers

## Components of the Internet

| Term | Definition |
| ---- | ---------- |
| __Computer&nbsp;Networks__ | Networks that allow the connection of two or more computers to exchange and share data and resources. They can be set up by location, such as a company office, metropolitan area, or global network. |
| __Internet__ | A global computer network that uses the Internet protocol suite (TCP/IP). It encompasses public and private networks and enables communication between various networks worldwide. |
| __Web__ | The World Wide Web (WWW), a subset of the internet, accessible through web browsers like Chrome, Firefox, or Safari. Websites on the web often have URLs starting with "www." |

<details>
    <summary>What is the purpose of computer networks?</summary>

    Computer networks allow the connection of two or more computers to exchange and share data and resources.
</details>

<details>
    <summary>What is the internet and what protocol does it use?</summary>

    The internet is a global computer network that uses the Internet protocol suite (TCP/IP).
</details>

<details>
    <summary>Differentiate between the internet and the World Wide Web (WWW).</summary>

    The internet is the overall global network, while the World Wide Web (WWW) is a subset of the internet that can be accessed through web browsers. Websites on the WWW often have URLs starting with "www."
</details>

---

## Components of a Request-Response Cycle

| Term | Definition |
| ---- | ---------- |
| __Client__ | Any device or software that connects to the internet and makes requests to servers. Clients can be web browsers, mobile apps, or other applications. They initiate requests to servers and receive responses. |
| __Server__ | A computer that receives requests from clients and responds to those requests. Servers are dedicated computers designed to handle requests, provide resources, and process data. They can be web servers, email servers, or other types of servers. |
| __Request-Response Cycle__ | The interaction between clients and servers, where clients send requests to servers, and servers respond with the requested data or perform requested actions. It forms the basis of communication in web applications. |

<details>
    <summary>Define a client and a server in the context of web applications.</summary>

    A client is any device or software that connects to the internet and makes requests to servers. A server is a computer that receives requests from clients and responds to those requests.
</details>

<details>
    <summary>Describe the process of the request-response cycle.</summary>

    The request-response cycle is the interaction between clients and servers. Clients send requests to servers, and servers respond with the requested data or perform requested actions.
</details>

<details>
    <summary>What is the role of servers in handling client requests?</summary>

    Servers receive client requests, process them, and provide the requested resources or perform the requested actions. They handle the logic and data management necessary to fulfill client requests.
</details>

<details>
    <summary>How many responses can you have per request?</summary>

    __A request can have only one response.__ However, the response can contain multiple resources or data.
</details>

---

## Databases

| Term | Definition |
| ---- | ---------- |
| __Database__ | A computer program that stores electronic data in organized collections. It manages data and allows clients to access and interact with the data through servers. Examples include databases storing user information, product data, or other structured information. |

<details>
    <summary>What is a database and what is its purpose?</summary>

    A database is a computer program that stores electronic data in organized collections. Its purpose is to manage data and allow clients to access and interact with the data through servers.
</details>

<details>
    <summary>How does a server interact with a database?</summary>

    The server contains the logic that manages how a client accesses and interacts with the data stored in the database. The server processes client requests, interacts with the database to retrieve or modify data, and responds to the client with the requested information.
</details>

<details>
    <summary>Give an example of a type of information stored in a database.</summary>

    Examples include user information (name, email, password), product data (name, description, price), or any other structured information that needs to be stored and accessed.
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
    <summary>What does HTTP stand for and what is its purpose?</summary>

    HTTP stands for HyperText Transfer Protocol. Its purpose is to facilitate communication between clients and servers over the internet by allowing the transfer of various data types.
</details>

<details>
    <summary>Explain the components of a URL.</summary>

    The components of a URL include the protocol, host/domain name, port, path, query string, and hash/fragment. These components provide the address and location of a resource on the internet.
</details>

<details>
    <summary>What is the difference between the header and body in an HTTP request or response?</summary>

    The header contains essential metadata about the request or response, such as the URL, request method, content type, and status code. The body, which is optional, contains the actual data or content being sent or received.
</details>

### URL Components

Let's break down the contents of a more complex URL:

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
    <summary>What is a protocol?</summary>

    In the context of the internet, protocols define how data is transmitted, received, and interpreted by different devices.

    Examples of protocols include HTTP (Hypertext Transfer Protocol), HTTPS (Hypertext Transfer Protocol Secure), SMTP (Simple Mail Transfer Protocol), and FTP (File Transfer Protocol).
</details>

<details>
    <summary>What is the purpose of the query-string in a URL?</summary>

    The query-string is used to pass additional parameters or data to the server through the URL. It allows clients to send specific information to the server, which can then process the request based on those parameters. The query-string consists of key-value pairs separated by ampersands (&).

    For example, in the URL https://example.com/search?q=apple&type=fruit, the query-string parameters are q=apple and type=fruit, which can be used by the server to perform a search for the query term "apple" within the category "fruit."
</details>

<details>
    <summary>How does the hash/fragment component in a URL contribute to the user experience of a web page?</summary>

    The hash/fragment component in a URL is used to identify a specific portion or location within a web page.

    When a user clicks on a link with a hash/fragment, the browser will automatically scroll to the corresponding section of the page. This feature is often used to navigate within long documents or web pages with multiple sections.

    It allows users to directly access and share specific content within a page, enhancing the overall user experience by providing quick and targeted access to relevant information.
</details>

---

## HTTP Protocol

| Term | Definition |
| ---- | ---------- |
| __Request&nbsp;Methods__ | The four primary ways to interact with data through HTTP: POST (create), GET (read), PUT/PATCH (update), and DELETE (destroy). These methods correspond to the CRUD operations (Create, Read, Update, Delete) commonly performed on data. |
| __HTTP Status Codes__ | Numerical codes included in the HTTP response that indicate the status of the request. Status codes in the range 100-399 confirm the request/response is OK. Codes in the 400s denote user errors, while codes in the 500s denote server errors. They provide information about the success or failure of the request and the reason for the failure. Common status codes include 200 (OK), 404 (Not Found), and 500 (Internal Server Error). |

<details>
    <summary>Name the four primary request methods in HTTP and their corresponding CRUD operations.</summary>

    The four primary request methods in HTTP are:

    - POST (create): Used to create new data or make a new user account.

    - GET (read): Used to retrieve data or see details of a user account.

    - PUT/PATCH (update): Used to update existing data or make changes to a user account.

    - DELETE (destroy): Used to delete data or delete a user account.
</details>

<details>
    <summary>How do HTTP status codes provide information about a request's outcome?</summary>

    HTTP status codes are numerical codes included in the response to indicate the status of the request. They provide information about the success or failure of the request and the reason for the failure. Different status code ranges convey different types of information, such as success, client errors, or server errors.
</details>

<details>
    <summary>Give examples of HTTP status codes for successful requests and common client/server errors.</summary>

    Examples of successful status codes include 200 (OK) for a successful request and 201 (Created) for a successful creation of a new resource.

    Examples of common client errors include 400 (Bad Request) for an invalid request or 404 (Not Found) for a resource that cannot be found.

    Examples of common server errors include 500 (Internal Server Error) for an unexpected server error and 503 (Service Unavailable) for a temporarily unavailable server.
</details>
---